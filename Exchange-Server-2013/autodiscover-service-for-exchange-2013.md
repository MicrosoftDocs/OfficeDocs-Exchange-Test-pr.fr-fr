---
title: 'Service de découverte automatique: Exchange 2013 Help'
TOCTitle: Service de découverte automatique
ms:assetid: b03c0f21-cbc2-4be8-ad03-73a7dac16ffc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124251(v=EXCHG.150)
ms:contentKeyID: 50555476
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Service de découverte automatique

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Découvrez le service de découverte automatique d’Exchange pour Microsoft Exchange 2013. Vous découvrirez le rôle du service de découverte automatique d’Exchange, son mode de fonctionnement, ainsi que les options de déploiement disponibles.

MicrosoftExchange 2013 comprend un service nommé service de découverte automatique. Cette rubrique présente le service, elle explique son fonctionnement et comment il configure les clients Outlook. Elle présente également les options qui permettent de déployer le service de découverte automatique dans votre environnement de messagerie.

Le service de découverte automatique effectue ce qui suit :

  - Configure automatiquement des paramètres de profil utilisateur pour des clients qui exécutent MicrosoftOffice Outlook 2007, Outlook 2010 ou Outlook 2013, ainsi que des téléphones mobiles pris en charge. Les téléphones qui exécutent Windows Mobile 6.1 ou une version ultérieure sont pris en charge. Si votre téléphone n'est pas un téléphone mobile Windows, reportez-vous à la documentation de votre téléphone pour savoir s'il est pris en charge.

  - Fournit un accès aux fonctionnalités d’Exchange à des clients Outlook 2007, Outlook 2010 ou Outlook 2013 qui sont connectés à votre environnement de messagerie Exchange.

  - Utilise une adresse de messagerie et un mot de passe d’utilisateur pour fournir des paramètres de profil aux clients Outlook 2007, Outlook 2010 ou Outlook 2013 et des téléphones mobiles pris en charge. Si le client Outlook est connecté à un domaine, le compte de domaine de l’utilisateur est utilisé.

**Contenu de cette rubrique**

Présentation du service de découverte automatique

Fonctionnement du service de découverte automatique

Options de déploiement du service de découverte automatique

Configuration de la découverte automatique pour des déplacements inter-forêts

## Présentation du service de découverte automatique

Le service de découverte automatique facilite la configuration d’Outlook 2007, Outlook 2010 ou Outlook 2013 et de certains téléphones mobiles. Vous ne pouvez pas utiliser le service de découverte automatique avec des versions d’Outlook antérieures à Office Outlook 2007. Dans les versions antérieures de Microsoft Exchange (Exchange 2003 SP2 ou antérieure) et d'Outlook (Outlook 2003 ou antérieure), vous deviez configurer les profils des utilisateurs manuellement pour leur permettre d'accéder à Exchange. Une charge de travail supplémentaire était nécessaire pour gérer ces profils en cas de modifications de l'environnement de messagerie. Dans le cas contraire, les clients Outlook cessaient de fonctionner correctement.

Le service de découverte automatique permet à Outlook de trouver de nouveaux points de connexion constitués du GUID de boîte aux lettres de l’utilisateur + @ + la partie de domaine de l’adresse SMTP principale de l’utilisateur. Le service de découverte automatique renvoie les informations suivantes au client :

  - Nom complet de l'utilisateur

  - Paramètres de connexion séparés pour la connectivité interne et externe

  - Emplacement du serveur de boîtes aux lettres de l'utilisateur

  - URL de différentes fonctions Outlook qui régissent des fonctionnalités telles que les informations de disponibilité, la messagerie unifiée et le carnet d’adresses en mode hors connexion

  - Paramètres de serveur Outlook Anywhere

Lorsque les informations Exchange d'un utilisateur sont modifiées, Outlook reconfigure automatiquement le profil de l'utilisateur à l'aide du service de découverte automatique. Par exemple, si la boîte aux lettres d'un utilisateur est déplacée ou si le client ne peut pas se connecter à la boîte aux lettres de l'utilisateur ou aux fonctionnalités d'Exchange disponibles, Outlook contacte le service de découverte automatique et met automatiquement à jour le profil de l'utilisateur afin d'y inclure les informations requises pour se connecter à la boîte aux lettres de l'utilisateur et aux fonctionnalités d'Exchange.

Retour au début

## Fonctionnement du service de découverte automatique

Lorsque vous installez un serveur d’accès au client dans Exchange 2013, un répertoire virtuel par défaut intitulé Autodiscover est créé sous le site Web par défaut des Services Internet (IIS). Ce répertoire virtuel traite les demandes du service de découverte automatique émanant des clients Outlook 2007, Outlook 2010 et Outlook 2013 et des appareils mobiles pris en charge dans les circonstances suivantes :

  - Lorsqu’un compte d’utilisateur est configuré ou mis à jour

  - lorsqu'un client Outlook vérifie régulièrement si des modifications ont été apportées aux URL des services Web Exchange

  - lorsque des modifications de la connexion réseau sous-jacente se produisent dans votre environnement de messagerie Exchange

Par ailleurs, un objet Active Directory appelé point de connexion de service (SCP), est créé sur le serveur lorsque vous installez le serveur d’accès au client.

L’objet SCP contient la liste des URL du service de découverte automatique faisant autorité pour la forêt. La cmdlet **Set-ClientAccessServer** permet de mettre à jour l'objet SCP. Pour plus d'informations, voir [Set-ClientAccessServer](https://technet.microsoft.com/fr-fr/library/bb125157\(v=exchg.150\)).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Avant d'exécuter la cmdlet <strong>Set-ClientAccessServer</strong>, assurez-vous que le compte d'utilisateurs authentifiés sur le serveur d'accès au client dispose d'autorisations d'accès en lecture à l'objet SCP. Si les utilisateurs ne disposent pas des autorisations appropriées, ils ne pourront pas rechercher et lire des éléments dans l'objet SCP.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les objets SCP, consultez le site relatif à la [publication avec des points de connexion de service](https://go.microsoft.com/fwlink/p/?linkid=72744) .

Pour l’accès externe, ou l’utilisation de DNS, le client recherche le service de découverte automatique sur Internet à l’aide de l’adresse de domaine SMTP principale de l’adresse de messagerie de l’utilisateur.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous devez fournir un enregistrement de ressource de service d’hôte dans DNS pour que les clients Outlook détectent le service de découverte automatique en utilisant DNS. Pour plus d'informations, reportez-vous aux instructions relatives à la configuration de DNS dans votre documentation Windows et consultez également le <a href="https://go.microsoft.com/fwlink/p/?linkid=85214">Livre blanc: Service de découverte automatique d’Exchange 2007</a>.</td>
</tr>
</tbody>
</table>


Selon que vous avez configuré ou non le service de découverte automatique sur un site distinct, l'adresse URL du service de découverte automatique est soit https://\<*smtp-address-domain*\>/autodiscover/autodiscover.xml, soit https://autodiscover.\<*smtp-address-domain*\>/autodiscover/autodiscover.xml, où ://\<*smtp-address-domain*\> est l'adresse de domaine SMTP principale. Par exemple, si l’adresse de messagerie de l’utilisateur est tony@contoso.com, l’adresse de domaine SMTP principale est contoso.com. Lorsque le client se connecte à Active Directory, celui-ci recherche l’objet SCP créé au cours de l’installation. Dans les déploiements qui comprennent plusieurs serveurs d'accès au client, un objet SCP de découverte automatique est créé pour chaque serveur d'accès au client. L'objet SCP contient l'attribut *ServiceBindingInfo* qui dispose du nom de domaine complet (FQDN) du serveur d'accès au client sous la forme https://CAS01/autodiscover/autodiscover.xml, où CAS01 est le nom de domaine complet du serveur d'accès au client. A l'aide des informations d’identification de l'utilisateur, le client Outlook 2007, Outlook 2010 ou Outlook 2013 s’authentifie dans Active Directory et recherche les objets SCP de découverte automatique. Une fois que le client a obtenu et énuméré les instances du service de découverte automatique, il se connecte au premier serveur d'accès au client de la liste énumérée et obtient, sous forme de données XML, les informations de profil nécessaires pour se connecter à la boîte aux lettres de l'utilisateur et aux fonctionnalités d'Exchange disponibles.

Retour au début

## Options de déploiement du service de découverte automatique

Le service de découverte automatique doit être déployé et configuré correctement pour permettre aux clients Outlook 2007, Outlook 2010 et Outlook 2013 de se connecter automatiquement aux fonctionnalités d’Exchange, comme le carnet d’adresses en mode hors connexion, le service de disponibilité et la messagerie unifiée. Le déploiement du service de découverte automatique n’est qu’une étape du processus visant à vérifier que vos services Exchange, comme le service de disponibilité, sont accessibles par des clients Outlook 2007, Outlook 2010 ou Outlook 2013.

## Configuration de la découverte automatique pour des déplacements inter-forêts

Le service de découverte automatique peut fournir des informations de profil utilisateur aux clients Outlook qui se connectent à des boîtes aux lettres qui ont été déplacées d'une forêt Exchange à une autre. Pour cela, vous devez configurer un utilisateur à extension messagerie dans la forêt d’origine où la boîte aux lettres de l’utilisateur réside et dans la forêt cible à l’aide de la cmdlet **New-MailUser**. Dans la forêt source, vous devez utiliser le paramètre *ExternalEmailAddress* dans la cmdlet pour spécifier la nouvelle adresse de messagerie de la boîte aux lettres dans la forêt cible. Pour plus d’informations, consultez la rubrique [New-MailUser](https://technet.microsoft.com/fr-fr/library/aa996335\(v=exchg.150\)).

Lorsque vous configurez un utilisateur à extension messagerie, le service de découverte automatique dans la forêt d’origine redirige l’utilisateur qui s’authentifie sur la nouvelle adresse de messagerie dans la forêt cible. Le client Outlook qui se connecte est alors redirigé vers le serveur d'accès au client de la forêt cible où la boîte aux lettres a été déplacée.

Retour au début

