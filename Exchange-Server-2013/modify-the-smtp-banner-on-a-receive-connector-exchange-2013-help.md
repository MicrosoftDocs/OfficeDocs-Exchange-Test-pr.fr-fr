---
title: 'Modifier la bannière SMTP sur un connecteur de réception: Exchange 2013 Help'
TOCTitle: Modifier la bannière SMTP sur un connecteur de réception
ms:assetid: d667704e-fd69-4aca-9c35-eef7006944b2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124740(v=EXCHG.150)
ms:contentKeyID: 52063022
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifier la bannière SMTP sur un connecteur de réception

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

La *bannière SMTP* est la réponse de la connexion SMTP qu'un serveur de messagerie SMTP distant reçoit une fois connecté à un connecteur de réception configuré sur un ordinateur exécutant Microsoft Exchange Server 2013.

Voici la réponse par défaut reçue par un serveur de messagerie SMTP distant une fois connecté au connecteur de réception :

    220 <Servername> Microsoft ESMTP MAIL service ready at <RegionalDay-Date-24HourTimeFormat> <RegionalTimeZoneOffset>

Quand vous spécifiez une valeur personnalisée pour la bannière SMTP sur un connecteur de réception, un serveur de messagerie SMTP distant qui se connecte à ce connecteur de réception SMTP reçoit la réponse suivante.

    220 <Banner Text>

Vous pouvez modifier la bannière SMTP des connecteurs de réception SMTP accédant à Internet afin que le nom du serveur et le logiciel de serveur de messagerie ne soient pas divulgués par la bannière SMTP.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Connecteurs de réception » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - La chaîne du texte de remplacement de la bannière SMTP doit toujours commencer par `220`. Tel que défini par RFC 2821, le code de réponse SMTP de service prêt par défaut est 220.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier la bannière SMTP sur un connecteur de réception

Exécutez la commande suivante :

    Set-ReceiveConnector <ConnectorIdentity> -Banner "220 <Banner Text>"

Cet exemple modifie la bannière SMTP sur le serveur de connexion existant From the Internet pour que la bannière SMTP affiche `220 Contoso Corporation`.

    Set-ReceiveConnector "From the Internet" -Banner "220 Contoso Corporation"

Cet exemple supprime la bannière SMTP personnalisée sur le connecteur de réception From the Internet, qui renvoie la bannière SMTP à la valeur par défaut.

    Set-ReceiveConnector "From the Internet" -Banner $null

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié la bannière SMTP sur un connecteur de réception, procédez comme suit :

1.  Ouvrez un client Telnet sur un ordinateur qui peut accéder au connecteur de réception, et exécutez la commande suivante :
    
        open <Connector FQDN or IP address> <Port>

2.  Vérifiez que la réponse du connecteur de réception contient la bannière SMTP que vous avez configurée.

Notez que cette procédure ne fonctionne que sur des connecteurs de réception qui autorisent l'authentification de base ou anonyme. Pour plus d'informations, consultez la rubrique [Utilisation de Telnet pour tester la communication SMTP](use-telnet-to-test-smtp-communication-exchange-2013-help.md).

