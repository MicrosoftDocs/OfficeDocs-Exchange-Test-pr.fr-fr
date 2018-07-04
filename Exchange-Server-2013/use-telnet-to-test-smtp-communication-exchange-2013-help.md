---
title: 'Utilisation de Telnet pour tester la communication SMTP: Exchange 2013 Help'
TOCTitle: Utilisation de Telnet pour tester la communication SMTP
ms:assetid: 8a5f6715-baa4-48dd-8600-02c6b3d1aa9d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123686(v=EXCHG.150)
ms:contentKeyID: 52062977
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilisation de Telnet pour tester la communication SMTP

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Cette rubrique décrit comment utiliser Telnet pour tester la communication SMTP (Simple Mail Transfer Protocol) entre deux serveurs de messagerie. Par défaut, SMTP écoute sur le port 25. Si vous utilisez Telnet sur le port 25, vous pouvez entrer les commandes SMTP utilisées pour la connexion à un serveur SMTP et envoyer un message comme si votre session Telnet se trouvait sur un serveur de messagerie SMTP. Vous pouvez voir si chaque étape réussit ou échoue au cours du processus de connexion et de dépôt de message.

La liste suivante décrit les scénarios dans lesquels vous pouvez utiliser Telnet pour tester la communication SMTP à partir ou vers les serveurs de transport existant dans votre organisation Microsoft Exchange :

  - Connectez-vous au serveur Exchange avec accès via Internet de votre organisation à partir d'un hôte situé en dehors de votre réseau de périmètre et envoyez un message de test.

  - Connectez-vous à un serveur de messagerie distant à partir du serveur Exchange avec accès via Internet de votre organisation et envoyez un message de test.

La procédure de cette rubrique vous indique comment utiliser le client Telnet, qui est un composant inclus à Microsoft Windows. Les clients Telnet tiers nécessitent peut-être une syntaxe différente de celle du composant Windows Telnet.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 30 minutes

  - Les autorisations Exchange ne s'appliquent pas aux procédures de cette rubrique. Ces procédures sont exécutées dans le système d'exploitation du serveur Exchange ou sur un ordinateur client.

  - Les procédures décrites dans cette rubrique permettent généralement de se connecter de manière optimale vers et depuis un serveur avec accès via Internet qui autorise une connexion anonyme. La transmission des messages entre les serveurs Exchange internes est chiffrée et authentifiée. Pour utiliser Telnet afin de vous connecter au service de transport Hub sur un serveur de boîtes aux lettres, vous devez créer un connecteur de réception configuré pour permettre l'accès anonyme ou l'authentification de base pour recevoir des messages. Si le connecteur autorise l'authentification de base, vous devez disposer d'un utilitaire pour convertir les chaînes de texte utilisées pour le nom d'utilisateur et le mot de passe au format Base64. En cas d'utilisation de l'authentification de base, il est facile de discerner le nom d'utilisateur et le mot de passe. Aussi, nous vous déconseillons une authentification de base sans chiffrement.

  - Si vous vous connectez à un serveur de messagerie distant, envisagez d'exécuter les procédures décrites dans cette rubrique sur votre serveur Exchange avec accès via Internet. Cela vous aidera à éviter le rejet du message de test par les serveurs de messagerie distants qui sont configurés pour valider l'adresse IP source, le nom de domaine du DNS (domain name system) correspondant et l'adresse IP de la recherche inversée d'un hôte Internet essayant d'envoyer un message au serveur.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : installer le client Telnet dans Windows

Par défaut, le client Telnet n’est pas installé dans la plupart des versions Client ou Serveur des systèmes d’exploitation Microsoft Windows. Pour l’installer, consultez la rubrique relative à son [installation](https://go.microsoft.com/fwlink/p/?linkid=179054).

## Étape 2 : utiliser Nslookup pour rechercher le nom de domaine complet ou l'adresse IP dans l'enregistrement MX du serveur SMTP distant

Pour vous connecter à un serveur SMTP de destination via Telnet sur le port 25, vous devez utiliser le nom de domaine complet (FQDN) ou l'adresse IP du serveur SMTP. Si le nom de domaine complet ou l'adresse IP est inconnu, la manière la plus simple d'obtenir ces informations est d'utiliser l'outil de ligne de commande Nslookup pour rechercher l'enregistrement MX du domaine de destination.

1.  À l'invite de commandes, tapez **nslookup**, puis appuyez sur Entrée. Cette commande ouvre une session Nslookup.

2.  Tapez **set type=mx**, puis appuyez sur Entrée.

3.  Tapez **set timeout=20**, puis appuyez sur Entrée. Par défaut, le délai d'expiration de la requête DNS récursive pour les serveurs DNS Windows est 15 secondes.

4.  Tapez le nom du domaine pour lequel vous voulez rechercher l'enregistrement MX. Par exemple, pour rechercher l'enregistrement MX du domaine fabrikam.com, tapez **fabrikam.com.**, puis appuyez sur Entrée.
    
    > [!NOTE]
    > Le point final ( <strong>.</strong> ) indique un nom de domaine complet. L'utilisation du point final empêche les suffixes DNS par défaut configurés sur votre réseau d'être ajoutés de façon involontaire au nom de domaine.
    
    Les données en sortie de la commande sont similaires à ce qui suit :
    
        fabrikam.com mx preference=10, mail exchanger = mail1.fabrikam.com
        fabrikam.com mx preference=20, mail exchanger = mail2.fabrikam.com
        mail1.fabrikam.com internet address = 192.168.1.10
        mail2 fabrikam.com internet address = 192.168.1.20
    
    Vous pouvez utiliser les noms d'hôte ou adresses IP associés aux enregistrements MX comme serveur SMTP de destination. Une valeur préférée inférieure indique un serveur SMTP préféré. Vous pouvez utiliser plusieurs enregistrements MX et des valeurs préférées différentes pour l'équilibrage de charge et la tolérance de panne.

5.  Quand vous êtes prêt à fermer la session Nslookup, tapez **exit**, puis appuyez sur Entrée.

> [!NOTE]
> Les restrictions de pare-feu et de proxy Internet imposées sur le réseau interne de votre organisation peuvent vous empêcher d'utiliser l'outil Nslookup pour interroger les serveurs DNS publics sur Internet.


## Étape 3 : utiliser Telnet sur le port 25 pour tester la communication SMTP

Dans cet exemple, les valeurs suivantes sont utilisées :

  - **Serveur SMTP de destination**   mail1.fabrikam.com

  - **Domaine source**   contoso.com

  - **Adresse de messagerie de l'expéditeur**   chris@contoso.com

  - **Adresse de messagerie du destinataire**   kate@fabrikam.com

  - **Objet du message**   Test depuis Contoso

  - **Corps du message**   Ceci est un message de test

> [!NOTE]
> <ul>
> <li><p>Les commandes du client Telnet ne tiennent pas compte de la casse. Les verbes de la commande SMTP sont écrits en majuscules par souci de clarté.</p></li>
> <li><p>Vous ne pouvez pas utiliser la touche Retour arrière après vous être connecté au serveur SMTP de destination dans la session Telnet. En cas d'erreur lors de la saisie d'une commande SMTP, vous devez appuyer sur ENTRÉE puis taper la commande à nouveau. Les commandes SMTP inconnues ou les erreurs de syntaxe entraînent l'affichage d'un message d'erreur similaire à ce qui suit :</p>
<pre><code>500 5.3.3 Unrecognized command</code></pre></li></ul>

1.  À l'invite de commandes, tapez **telnet**, puis appuyez sur Entrée. Cette commande ouvre la session Telnet.

2.  Tapez **set localecho**, puis appuyez sur Entrée. Cette commande facultative permet d'afficher les caractères à mesure que vous les tapez. Cette configuration peut être requise pour certains serveurs SMTP.

3.  Tapez **set logfile***\<nom\_fichier\>*. Cette commande facultative permet d'ouvrir la session Telnet sur le fichier journal spécifié. Si vous ne spécifiez qu'un nom de fichier, l'emplacement du fichier journal correspond au répertoire de travail actuel. Si vous spécifiez un chemin d'accès et un nom de fichier, le chemin d'accès doit être local sur l'ordinateur. Le chemin d'accès et le nom de fichier spécifiés doivent être entrés au format Microsoft DOS 8.3. Le chemin d'accès spécifié doit déjà exister. Si vous spécifiez un fichier journal inexistant, il sera créé pour vous.

4.  Tapez **open mail1.fabrikam.com 25**, puis appuyez sur Entrée.

5.  Tapez **EHLO contoso.com**, puis appuyez sur Entrée.

6.  Tapez **MAIL FROM:chris@contoso.com**, puis appuyez sur Entrée.

7.  Tapez **RCPT TO:kate@fabrikam.com NOTIFY=success,failure**, puis appuyez sur Entrée. La commande facultative NOTIFY définit les messages de notification d'état de remise particuliers que le serveur SMTP de destination doit fournir à l'expéditeur. Les messages de notification d'état de remise sont définis dans RFC 1891. Dans ce cas, vous exigez un message de notification d'état de remise indiquant le succès ou l'échec de la remise du message.

8.  Tapez **DATA**, puis appuyez sur Entrée. Vous recevez une réponse similaire à ce qui suit :
    
        354 Start mail input; end with <CLRF>.<CLRF>

9.  Tapez **Subject: Test depuis Contoso**, puis appuyez sur ENTRÉE.

10. Appuyez sur ENTRÉE. RFC 2822 requiert une ligne vide entre le champ d'en-tête `Subject:` et le corps du message.

11. Tapez **Ceci est un message de test**, puis appuyez sur ENTRÉE.

12. Appuyez sur Entrée, tapez un point ( **.** ), puis appuyez sur Entrée. Vous recevez une réponse similaire à ce qui suit :
    
        250 2.6.0 <GUID> Queued mail for delivery

13. Pour vous déconnecter du serveur SMTP de destination, tapez **QUIT**, puis appuyez sur Entrée. Vous recevez une réponse similaire à ce qui suit :
    
        221 2.0.0 Service closing transmission channel

14. Pour fermer la session Telnet, tapez **quit**, puis appuyez sur Entrée.

## Étape 4 : évaluer les résultats de la session Telnet

Cette section fournit des informations sur les réponses qui peuvent être générées pour les commandes utilisées dans l'exemple précédent :

  - Open mail1.fabrikam.com 25

  - EHLO contoso.com

  - MAIL FROM:chris@contoso.com

  - RCPT TO:kate@fabrikam.com NOTIFY=success,failure
    
    > [!NOTE]
    > Les codes de réponse SMTP à 3 chiffres définis dans RFC 2821 sont les mêmes pour tous les serveurs de messagerie SMTP. Ces descriptions peuvent légèrement varier pour certains serveurs de messagerie SMTP.


## Open mail1.fabrikam.com 25

**Réponse en cas de succès**   `220 mail1.fabrikam.com Microsoft ESMTP MAIL Service ready at <day-date-time>`

**Réponse en cas d'échec**   `Connecting to mail1.fabrikam.com...Could not open connection to the host, on port 25: Connect failed`

**Raisons possibles de l'échec**

  - Le service SMTP de destination est indisponible.

  - Il existe des restrictions sur le pare-feu de destination.

  - Il existe des restrictions sur le pare-feu source.

  - Un nom de domaine complet incorrect ou une adresse IP incorrecte ont été spécifiés pour le serveur SMTP de destination.

  - Un numéro de port incorrect a été spécifié.

## EHLO contoso.com

**Réponse en cas de succès**   `250 mail1.fabrikam.com Hello [<sourceIPaddress>]`

**Réponse en cas d'échec**   `501 5.5.4 Invalid domain name`

**Raisons possibles de l'échec**   Le nom de domaine comporte des caractères non valides. Il peut aussi y avoir des restrictions de connexion sur le serveur SMTP de destination.

> [!NOTE]
> EHLO est le verbe ESMTP (Extended Simple Message Transfer Protocol) défini dans RFC 2821. Les serveurs ESMTP peuvent annoncer leurs capacités lors de la connexion initiale. Ces capacités incluent la taille de message acceptée maximale, ainsi que leurs méthodes d'authentification prises en charge. HELO est l'ancien verbe SMTP défini dans RFC 821. La plupart des serveurs de messagerie SMTP prennent en charge ESMTP et EHLO.


## MAIL FROM:chris@contoso.com

**Réponse en cas de succès**   `250 2.1.0 Sender OK`

**Réponse en cas d'échec**   `550 5.1.7 Invalid address`

**Raisons possibles de l'échec**   L'adresse de messagerie de l'expéditeur comporte une erreur de syntaxe.

**Réponse en cas d'échec**   `530 5.7.1 Client was not authenticated`

**Raisons possibles de l'échec**   Le serveur de destination n'accepte pas les dépôts de message anonymes. Vous recevez cette erreur si vous tentez d'utiliser Telnet pour déposer un message directement sur un serveur de transport Hub.

## RCPT TO:kate@fabrikam.com NOTIFY=success,failure

**Réponse en cas de succès**   `250 2.1.5 Recipient OK`

**Réponse en cas d'échec**   `550 5.1.1 User unknown`

**Raisons possibles de l'échec**   Le destinataire spécifié n'existe pas dans l'organisation.

