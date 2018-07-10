---
title: 'Certificats numériques et SSL: Exchange 2013 Help'
TOCTitle: Certificats numériques et SSL
ms:assetid: a9e2e08c-d46a-4135-a387-eb653212b676
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351044(v=EXCHG.150)
ms:contentKeyID: 51407218
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Certificats numériques et SSL

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-08-26_

Le protocole SSL (Secure Sockets Layer) permet de sécuriser les communications entre un client et un serveur. Pour Exchange Server 2013, le protocole SSL permet de sécuriser les communications entre le serveur et les clients. Les clients peuvent être des téléphones mobiles, des ordinateurs faisant partie du réseau d'une organisation et des ordinateurs extérieurs au réseau d'une organisation.

Par défaut, quand vous installez Exchange 2013, les communications clientes sont chiffrées à l'aide du protocole SSL si vous utilisez Outlook Web App, Exchange ActiveSync et Outlook Anywhere.

Le protocole SSL nécessite l'utilisation de certificats numériques. Cette rubrique présente les différents types de certificat numérique existants, ainsi que des informations sur la configuration d'Exchange 2013 pour utiliser ces certificats.

**Contenu de cette rubrique**

Vue d'ensemble des certificats numériques

Certificats numériques et utilisation de serveurs proxy

Recommandations concernant les certificats numériques

## Vue d'ensemble des certificats numériques

Les certificats numériques sont des fichiers électroniques fonctionnant comme les mots de passe en ligne permettant de vérifier l'identité d'un utilisateur ou d'un ordinateur. Ils sont utilisés pour créer le canal chiffré SSL utilisé pour les communications clientes. Un certificat est un relevé numérique émis par une autorité de certification (CA) qui authentifie l'identité du détenteur du certificat et permet aux parties de communiquer de manière sécurisée grâce au chiffrement.

Les certificats numériques effectuent les actions suivantes :

  - Ils attestent que leurs détenteurs (personnes, sites web ou ressources réseau telles que les routeurs) sont véritablement ceux qu'ils prétendent être.

  - Ils empêchent le vol ou la falsification des données échangées en ligne.

Ils peuvent être émis par une autorité de certification tierce approuvée ou une infrastructure à clé publique (PKI) Windows utilisant les services de certificats, ou ils peuvent être auto-signés. Chaque type de certificat présente des avantages et des inconvénients. Aucun type de certificat numérique ne peut être falsifié.

Les certificats sont émis à différentes fins, par exemple, l'authentification des utilisateurs web, l'authentification de serveurs web, le chiffrement S/MIME (Secure/Multipurpose Internet Mail Extensions), IPsec, TLS (Transport Layer Security) et la signature de code.

Un certificat contient une clé publique qu'il attache à l'identité de la personne, de l'ordinateur ou du service contenant la clé privée correspondante. Les clés publiques et privées permettent au client et au serveur de chiffrer les données avant de les transmettre. Pour les utilisateurs de Windows et les ordinateurs et services utilisant ce programme, l'approbation d'une autorité de certification est établie lorsqu'il existe une copie du certificat racine dans le magasin de certificats racines approuvés et lorsque le certificat contient un chemin d'accès de certification valide. Pour que le certificat soit valide, il ne doit pas avoir été révoqué ni être arrivé à expiration.

## Types de certificats

Il existe trois types principaux de certificats numériques : les certificats auto-signés, les certificats générés par l'infrastructure à clé publique Windows (PKI) et les certificats tiers.

## Certificats auto-signés

Lors de l'installation d'Exchange 2013, un certificat auto-signé est automatiquement configuré sur les serveurs de boîtes aux lettres. Un certificat auto-signé est signé par l'application qui l'a créé. L'objet et le nom du certificat correspondent. L'émetteur et l'objet sont définis sur le certificat. Ce certificat auto-signé permet de chiffrer les communications entre le serveur d'accès au client et le serveur de boîtes aux lettres. Le serveur d'accès au client approuve automatiquement le certificat auto-signé sur le serveur de boîtes aux lettres de sorte qu'aucun certificat tiers n'est nécessaire sur le serveur de boîtes aux lettres. Lors de l'installation d'Exchange 2013, un certificat auto-signé est également créé sur le serveur d'accès au client. Ce certificat auto-signé autorise certains protocoles clients à utiliser le protocole SSL pour leurs communications. Exchange ActiveSync et Outlook Web App peuvent établir une connexion SSL à l’aide d’un certificat auto-signé. Outlook Anywhere ne fonctionne pas avec un certificat auto-signé sur le serveur d'accès au client. Les certificats auto-signés doivent être copiés manuellement dans le magasin de certificats racines approuvés sur l'ordinateur client ou l'appareil mobile. Quand un client se connecte à un serveur via une connexion SSL et que le serveur présente un certificat auto-signé, le client est invité à vérifier que le certificat a été émis par une autorité approuvée. Le client doit explicitement approuver l'autorité émettrice. Si le client approuve l'autorité émettrice, les communications SSL peuvent alors se poursuivre.

> [!NOTE]
> Par défaut, le certificat numérique installé sur le ou les serveurs de boîtes aux lettres est un certificat auto-signé. Il n’est pas nécessaire de remplacer un certificat auto-signé sur les serveurs de boîtes aux lettres de votre organisation par un certificat tiers approuvé. Le serveur d'accès au client approuve automatiquement le certificat auto-signé sur le serveur de boîtes aux lettres et aucune autre configuration n'est nécessaire pour les certificats sur le serveur de boîtes aux lettres.


Il arrive souvent que de petites organisations décident de ne pas utiliser un certificat tiers ou de ne pas installer leur propre infrastructure à clé publique (PKI) pour émettre leurs propres certificats. Elles peuvent être amenées à prendre cette décision, car ces solutions sont trop onéreuses ou parce que leurs administrateurs n'ont pas l'expérience ni la connaissance nécessaires pour créer leur propre hiérarchie de certificats, ou pour ces deux raisons. Si vous utilisez des certificats auto-signés, le coût est minimal et l'installation simple. Toutefois, la création d'une infrastructure pour la gestion du cycle de vie, le renouvellement, l'approbation et la révocation des certificats est beaucoup plus difficile avec des certificats auto-signés.

## Certificats d'infrastructure à clé publique Windows

Le deuxième type de certificat est le certificat généré par l'infrastructure à clé publique Windows (PKI). Une infrastructure à clé publique (PKI) est un système de certificats numériques, d'autorités de certification et d'autorités d'enregistrement qui permet de vérifier et d'authentifier la validité de chaque partie impliquée dans une transaction électronique à l'aide d'un chiffrement à clé publique. Lorsque vous implémentez une infrastructure à clé publique au sein d'une organisation qui utilise Active Directory, vous fournissez une infrastructure pour la gestion du cycle de vie, le renouvellement, la gestion de l'approbation et la révocation des certificats. Toutefois, le déploiement de serveurs et d'une infrastructure pour la création et la gestion de certificats générés par l'infrastructure à clé publique Windows a un coût.

Des services de certificats sont requis pour le déploiement d'une infrastructure à clé publique Windows. L'installation de ces services de certificats peut s'effectuer à l'aide de la fonctionnalité **Ajout/Suppression de programmes** du Panneau de configuration. Vous pouvez installer les services de certificats sur tous les serveurs du domaine.

Si vous obtenez des certificats d'une autorité de certification Windows appartenant à un domaine, vous pouvez utiliser l'autorité de certification pour demander ou signer des certificats à émettre pour vos propres serveurs ou ordinateurs sur votre réseau. Cela vous permet d'utiliser des certificats d'infrastructure à clé publique (PKI) semblables à des certificats d'un fournisseur tiers, mais plus économiques. Ces certificats PKI peuvent être déployés publiquement comme les autres types de certificat. Cependant, lorsqu'une autorité de certification PKI signe le certificat du demandeur en utilisant la clé privée, l'identité du demandeur est vérifiée. La clé publique de cette autorité de certification fait partie du certificat. Un serveur disposant de ce certificat dans le magasin de certificats racines approuvés peut utiliser cette clé publique pour déchiffrer le certificat du demandeur et authentifier celui-ci.

Les étapes de déploiement d'un certificat généré par l'infrastructure à clé publique ressemblent à celles requises pour le déploiement d'un certificat auto-signé. Vous devez encore installer une copie du certificat racine approuvé à partir de l'infrastructure à clé publique (PKI) dans le magasin de certificats racines approuvés des ordinateurs ou appareils mobiles qui devront établir une connexion SSL à Microsoft Exchange.

Une infrastructure à clé publique Windows (PKI) permet à des organisations de publier leurs propres certificats. Les clients peuvent demander et recevoir des certificats d'une infrastructure à clé publique Windows (PKI) sur le réseau interne. L'infrastructure à clé publique Windows (PKI) peut renouveler ou révoquer des certificats.

## Certificats tiers approuvés

Les certificats tiers ou commerciaux sont des certificats générés par une autorité de certification commerciale ou tierce que vous pouvez acheter pour les utiliser sur les serveurs de votre réseau. Un problème lié aux certificats auto-signés et basés sur une infrastructure à clé publique (PKI) est que, comme ils ne sont pas automatiquement approuvés par l'ordinateur client ou l'appareil mobile, vous devez veiller à les importer dans le magasin de certificats racines approuvés sur les ordinateurs et les appareils clients. Les certificats tiers ou commerciaux ne posent pas ce problème. La plupart des certificats émis par une autorité de certification commerciale sont déjà approuvés, car le certificat réside déjà dans le magasin de certificats racines approuvés. Étant donné que l'émetteur est approuvé, le certificat l'est également. L'utilisation des certificats tiers simplifie énormément le déploiement.

Pour les organisations de grande taille ou les organisations devant déployer publiquement des certificats, l'utilisation d'un certificat tiers ou commercial est la meilleure solution, même si le certificat a un coût. Les certificats commerciaux peuvent ne pas être la meilleure solution pour les petites et moyennes organisations. Vous pouvez donc décider d'utiliser l'une des autres options de certificat disponibles.

Retour au début

## Choix d'un type de certificat

Lorsque vous sélectionnez le type de certificat à installer, vous devez tenir compte de plusieurs facteurs. Pour être valide, un certificat doit être signé. Il peut être auto-signé ou signé par une autorité de certification. Un certificat auto-signé a des restrictions. Par exemple, tous les appareils mobiles ne permettent pas à un utilisateur d'installer un certificat numérique dans le magasin de certificats racines approuvés. La possibilité d'installer des certificats sur un appareil mobile dépend du fabricant et de l'opérateur de ce dernier. Certains fabricants et opérateurs désactivent l'accès au magasin de certificats racines approuvés. Dans ce cas, il n'est pas possible d'installer un certificat auto-signé, ni un certificat émis par une autorité de certification d'infrastructure à clé publique Windows (PKI) sur l'appareil mobile.

## Certificats Exchange par défaut

Par défaut, Exchange installe un certificat auto-signé sur le serveur d'accès au client et sur le serveur de boîtes aux lettres afin de chiffrer toutes les communications réseau. Pour que toutes les communications réseau soient chiffrées, chaque serveur Exchange doit pouvoir utiliser un certificat X.509. Nous vous conseillons de remplacer ce certificat auto-signé sur le serveur d'accès au client par un certificat automatiquement approuvé par vos clients.

Lorsqu'un certificat est « auto-signé », cela signifie qu'il a été créé et signé uniquement par le serveur Exchange lui-même. Étant donné qu'il a été créé et signé par une autorité de certification en général approuvée, le certificat auto-signé par défaut ne sera approuvé par un aucun autre serveur que les serveurs Exchange se trouvant dans la même organisation. Le certificat par défaut est activé pour tous les services Exchange. Il comporte un autre nom d'objet (SAN) qui correspond au nom du serveur Exchange sur lequel il est installé. Il comporte également une liste de SAN qui indiquent le nom et le nom de domaine complet (FQDN) du serveur.

Bien que les autres serveurs Exchange de votre organisation Exchange approuvent ce certificat automatiquement, les clients tels que les navigateurs web, les clients Outlook, les téléphones mobiles et les clients de messagerie, ainsi que les serveurs de messagerie externes ne l'approuveront pas automatiquement. Par conséquent, envisagez de remplacer ce certificat par un certificat tiers approuvé sur vos serveurs d'accès au client Exchange. Si vous disposez déjà d'une infrastructure à clé publique (PKI) et si tous vos clients approuvent cette entité, vous pouvez également utiliser les certificats que vous émettez vous-même.

## Conditions requises pour l'utilisation de certificats par service

Les certificats servent à plusieurs choses dans Exchange. La plupart des utilisateurs ont également recours à des certificats sur plusieurs serveurs Exchange. En règle générale, moins vous utilisez de certificats, plus il est facile de les gérer.

## Services Internet (IIS)

Tous les services Exchange suivants utilisent le même certificat sur un serveur d'accès au client Exchange donné :

  - Outlook Web App

  - Centre d'administration Exchange (CAE)

  - Services web Exchange

  - Exchange ActiveSync

  - Outlook Anywhere

  - Découverte automatique

  - Distribution de carnets d'adresses Outlook

Étant donné qu'un seul certificat peut être associé à un site web et que tous ces services sont offerts sous un seul site web par défaut, tous les noms que les clients de ces services utilisent doivent figurer dans le certificat (ou apparaître en tant que noms génériques dans le certificat).

## POP/IMAP

Les certificats utilisés pour POP ou IMAP peuvent être spécifiés séparément à partir du certificat utilisé pour IIS. Cependant, pour simplifier l'administration, nous vous recommandons d'inclure le nom du service POP ou IMAP dans le certificat IIS et d'utiliser un seul certificat pour tous ces services.

## SMTP

Vous pouvez utiliser un certificat distinct pour chaque connecteur de réception que vous configurez. Le certificat doit inclure le nom que les clients SMTP (ou des serveurs SMTP) utilisent pour accéder à ce connecteur. Pour simplifier la gestion des certificats, ajoutez tous les noms dont vous devez prendre en charge le trafic TLS dans un seul certificat.

## Certificats numériques et utilisation de serveurs proxy

L'utilisation de serveurs proxy est la méthode permettant à un serveur d'envoyer les connexions clientes à un autre serveur. Dans le cas d’Exchange 2013, cela se produit lorsque le serveur d’accès au client envoie une demande cliente entrante par proxy au serveur de boîtes aux lettres contenant la copie active de la boîte aux lettres du client.

Lorsque des serveurs d'accès au client transfèrent des demandes, SSL est utilisé pour le chiffrement et non pour l'authentification. Le certificat auto-signé sur le serveur de boîtes aux lettres chiffre le trafic entre le serveur d'accès au client et le serveur de boîtes aux lettres.

## Serveurs proxy inverses et certificats

De nombreux déploiements d'Exchange utilisent des serveurs proxy inverses pour publier des services Exchange sur Internet. Les proxys inverses peuvent être configurés pour mettre fin au chiffrement SSL, examiner le trafic en détail qui transite sur ces serveurs, puis ouvrir un nouveau canal de chiffrement SSL entre les serveurs proxy inverses et les serveurs Exchange qui se trouvent derrière. C'est ce qu'on appelle un pontage SSL. Une autre manière de configurer les serveurs de proxy inverses est de permettre aux connexions SSL d'accéder directement aux serveurs Exchange derrière les serveurs proxy inverses. Dans un modèle de déploiement comme dans l'autre, les clients sur Internet se connectent au serveur proxy inverse à l'aide d'un nom d'hôte permettant l'accès à Exchange, par exemple mail.contoso.com. Puis, le serveur proxy inverse se connecte à Exchange à l'aide d'un autre nom d'hôte, par exemple le nom d'ordinateur du serveur d'accès au client Exchange. Vous n'avez pas besoin d'inclure le nom d'ordinateur du serveur d'accès au client Exchange sur votre certificat, car la plupart des serveurs proxy inverses sont capables de vérifier que le nom d'hôte d'origine utilisé par le client correspond au nom d'hôte interne du serveur d'accès au client Exchange.

## SSL et DNS réparti

La technologie Split DNS vous permet de configurer différentes adresses IP pour le même nom d'hôte, selon la provenance de la demande DNS d'origine. Cette technologie est également appelée split-horizon DNS, split-view DNS ou split-brain DNS. DNS réparti peut vous aider à réduire le nombre de noms d'hôtes que vous devez gérer pour Exchange en permettant à vos clients de se connecter à Exchange avec le même nom d'hôte, qu'ils se connectent à partir d'Internet ou d'un intranet. DNS réparti permet aux demandes provenant d'un intranet de recevoir une adresse IP différente de celle des demandes qui proviennent d'Internet.

DNS réparti est en général inutile dans le cas d'un petit déploiement Exchange, car les utilisateurs peuvent accéder au même point de terminaison DNS, que ce soit à partir d'un intranet ou d'Internet. Toutefois, pour de plus grands déploiements, cette configuration produira une charge trop élevée sur votre serveur proxy Internet sortant et votre serveur proxy inverse. Dans ce cas, configurez le DNS réparti pour que, par exemple, les utilisateurs externes accèdent à mail.contoso.com et que les utilisateurs internes accèdent à internal.contoso.com. En utilisant le DNS réparti pour cette configuration, les utilisateurs n'auront pas besoin de se rappeler d'utiliser des noms d'hôtes différents selon leur emplacement.

## Remote Windows PowerShell

Remote Windows PowerShell utilise l'authentification Kerberos et le chiffrement Kerberos, à partir du Centre d'administration Exchange et l'environnement de ligne de commande Exchange Management Shell Exchange. Par conséquent, vous n'avez pas besoin de configurer vos certificats SSL à des fins d'utilisation avec Remote Windows PowerShell.

Retour au début

## Recommandations concernant les certificats numériques

Bien que la configuration des certificats numériques de votre organisation varie selon ses besoins, des recommandations sont incluses pour vous aider à choisir la configuration de certificat numérique qui vous convient.

## Recommandation : utiliser un certificat tiers approuvé

Pour éviter que les clients reçoivent des messages d'erreur relatifs à des certificats non approuvés, le certificat qui est utilisé par votre serveur Exchange doit être émis par quelqu'un en qui les clients ont confiance. Bien que la plupart des clients puissent être configurés pour approuver n'importe quel certificat ou émetteur de certificat, il est plus simple d'utiliser un certificat tiers approuvé sur votre serveur Exchange. Cela est dû au fait que la plupart des clients approuvent déjà leurs certificats racines. Il existe plusieurs émetteurs de certificats tiers qui offrent des certificats configurés spécialement pour Exchange. Vous pouvez utiliser le CAE pour générer des demandes de certificats qui fonctionnent avec la plupart des émetteurs de certificats.

## Sélection d'une autorité de certification

Une autorité de certification est une société qui émet des certificats et en garantit la validité. Les logiciels clients (par exemple, les navigateurs tels que Microsoft Internet Explorer ou les systèmes d'exploitation tels que Windows ou Mac OS) comportent une liste d'autorités de certification qu'ils approuvent. Cette liste peut en général être configurée pour ajouter et supprimer des autorités de certification, mais cette opération est souvent fastidieuse. Conformez-vous aux critères suivants lorsque vous envisagez d'acheter des certificats d'une autorité de certification :

  - Vérifiez que l'autorité de certification est approuvée par les logiciels clients (systèmes d'exploitation, navigateurs et téléphones mobiles) qui se connecteront à vos serveurs Exchange.

  - Choisissez une autorité de certification qui indique qu'elle prend en charge les « certificats de communications unifiées » pour utilisation avec les serveurs Exchange.

  - Assurez-vous que l’autorité de certification prend en charge les types de certificat que vous allez utiliser. À cet égard, il peut être judicieux d'utiliser des certificats SAN (Subject Alternative Name, Autre nom de l'objet). Toutes les autorités de certification ne prennent pas en charge les certificats SAN et d'autres autorités de certification ne prennent pas en charge autant de noms d'hôte que vous le souhaiteriez.

  - Assurez-vous que la licence que vous achetez pour les certificats vous permet de placer le certificat sur tous les serveurs que vous avez l'intention d'utiliser. Certaines autorités de certification permettent uniquement de placer un certificat sur un seul serveur.

  - Comparez les prix des certificats d'une autorité de certification à une autre.

## Recommandation : utiliser des certificats SAN

Selon la manière dont vous configurez les noms de services dans votre déploiement Exchange, votre serveur Exchange peut nécessiter un certificat pouvant représenter plusieurs noms de domaine. Bien qu'un certificat avec caractères génériques tel que le certificat \*.contoso.com puisse résoudre ce problème, de nombreux clients considèrent que le fait d'utiliser un certificat pour n'importe quel sous-domaine présente un risque pour la sécurité de leurs systèmes. Une autre méthode plus sûre consiste à répertorier chacun des domaines requis en tant que SAN dans le certificat. Par défaut, cette approche est utilisée lorsque des demandes de certificat sont générées par Exchange.

## Recommandation : utiliser l'Assistant Certificat Exchange pour demander des certificats

De nombreux services dans Exchange utilisent des certificats. Une erreur courante lors d'une demande de certificats consiste à ne pas inclure les noms corrects des services. L'Assistant Certificat du Centre d'administration Exchange vous aide à inclure la liste correcte des noms de services dans la demande de certificat. L'Assistant vous permet de spécifier les services avec lesquels le certificat sera utilisé et, selon les services sélectionnés, il inclut les noms qui doivent figurer dans le certificat pour que celui-ci puisse être utilisé avec ces services. Exécutez l'Assistant Certificat lorsque vous avez déployé vos serveurs Exchange 2013 et déterminé les noms d'hôtes à utiliser pour les différents services du déploiement. Vous n'aurez normalement à exécuter l'Assistant qu'une fois pour chaque site Active Directory où vous déployez Exchange.

Pour éviter d'oublier un nom d'hôte dans la liste des SAN du certificat que vous achetez, vous pouvez utiliser une autorité de certification qui offre gratuitement une période d'essai pendant laquelle vous pouvez retourner un certificat et redemander le même certificat avec des noms d'hôte supplémentaires.

## Recommandation : utiliser le moins de noms d'hôtes possible

En plus d'utiliser le moins de certificats possible, vous pouvez faire de même avec les noms d'hôte. Cette approche peut vous permettre de réaliser des économies. De nombreux fournisseurs de certificats facturent les noms d'hôte que vous ajoutez à votre certificat.

La meilleure manière de réduire le nombre d'hôtes dont vous devez disposer et, par conséquent, faciliter la gestion de votre certificat, est de ne pas inclure les noms d'hôte des serveurs dans les SAN du certificat.

Les noms d'hôte que vous devez inclure dans vos certificats Exchange sont les noms d'hôte utilisés par les applications clientes pour se connecter à Exchange. Voici une liste des noms d'hôte qui sont en général requis pour une société nommée Contoso :

  - **Mail.contoso.com**   Ce nom d'hôte couvre la plupart des connexions vers Exchange, y compris depuis MicrosoftOutlook, Outlook Web App, Outlook Anywhere, le carnet d'adresses en mode hors connexion, les services web Exchange, POP3, IMAP4, SMTP, le Panneau de configuration Exchange et ActiveSync.

  - **Autodiscover.contoso.com**   Ce nom d'hôte est utilisé par les clients qui prennent en charge la découverte automatique, y compris Microsoft Office Outlook 2007 et versions ultérieures, Exchange ActiveSync et les services web Exchange.

  - **Legacy.contoso.com**   Ce nom d’hôte est requis dans un scénario de coexistence avec Exchange 2007 et Exchange 2013. Si vous devez prendre en charge des clients avec des boîtes aux lettres sur d’Exchange 2007 et Exchange 2013, configurez un nom d’hôte hérité pour éviter que les utilisateurs aient à utiliser une seconde URL au cours du processus de mise à niveau.

## Présentation des certificats avec caractères génériques

Un certificat avec caractères génériques est conçu pour prendre en charge un domaine et plusieurs sous-domaines. Si vous configurez par exemple un certificat avec caractères génériques pour \*.contoso.com, celui -ci fonctionne pour mail.contoso.com, web.contoso.com et autodiscover.contoso.com.

Retour au début

