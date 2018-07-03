---
title: 'Autoriser ou empêcher de répondeur automatique sur un serveur de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Autoriser ou empêcher de répondeur automatique sur un serveur de boîtes aux lettres
ms:assetid: 4b860c09-6669-4e3d-b3dc-17b8018b3860
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997908(v=EXCHG.150)
ms:contentKeyID: 50555393
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoriser ou empêcher de répondeur automatique sur un serveur de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-18_

Vous pouvez autoriser le service de messagerie unifiée de Microsoft Exchange sur un serveur de boîtes aux lettres pour répondre aux nouveaux appels ou l'empêcher de cette opération. Par défaut, un serveur de boîtes aux lettres est dans un état activé après son installation. Lorsque vous configurez le serveur de boîtes aux lettres d'accepter des messages vocaux entrants, télécopie, standard automatique et les appels Outlook Voice Access, vous utilisez l'applet de commande **Set-ServerComponentState** .

Configuration du Mode de Maintenance pour un serveur de boîtes aux lettres permet de prendre le serveur hors service. Pour un serveur de boîtes aux lettres, out-of-service signifie que le serveur ne sont pas héberger les bases de données actives, toutes les files d'attente de transport sont vides, et le serveur n'accepte pas les appels entrants d'accès au Client serveurs, VoIP passerelles, PBX IP, PBX compatible SIP ou de contrôleurs de frontière de session (SBC).

Dans Exchange 2007 et Exchange 2010, un paramètre d'état pouvait être utilisé pour contrôler l'état de fonctionnement d'un serveur de messagerie unifiée. Dans Exchange 2013, aucun paramètre d'état n'est disponible à cette fin sur la cmdlet **Set-UMService** pour un serveur de boîtes aux lettres.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il n'est pas nécessaire que les serveurs d'accès au Client et boîte aux lettres doit être ajouté à un plan de numérotation de messagerie unifiée avant qu'ils peuvent traiter les appels pour la messagerie unifiée, sauf lorsque vous êtes intégration de la messagerie unifiée et Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server. Par défaut, tous les accès au Client et boîte aux lettres de serveurs dans une organisation sont disponibles pour répondre aux appels entrants.</td>
</tr>
</tbody>
</table>


Pour d'autres tâches de gestion relatives aux serveurs de boîtes aux lettres, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Paramètres de configuration du serveur Exchange » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Vérifiez que le serveur de boîtes aux lettres est installé, soit sur le même ordinateur que le serveur d'accès au client, soit sur un ordinateur distinct.

  - Si vous placez un serveur de boîtes aux lettres en Mode Maintenance, vérifiez qu'il y a suffisamment de redondance de toutes les copies de base de données pour permettre au serveur de mise hors service.

  - Avant de passer à un serveur en mode Maintenance, vérifier l'intégrité du serveur et assurez-vous qu'il est prêt à passer en service.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver le répondeur automatique sur un serveur de boîtes aux lettres

Cet exemple autorise un serveur de boîtes aux lettres `UMMBXr-05x.contoso.com` à répondre à des appels vocaux, de télécopie, de standard automatique et Outlook Voice Access entrants à partir de passerelles VoIP, de PBX IP, de PBX compatibles SIP et de contrôleurs SBC, et à écrire les modifications dans le Registre du serveur UMMBX-05x.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

Cet exemple empêche un serveur de boîtes aux lettres `UMMBX-05x.contoso.com` de répondre à des appels vocaux, de télécopie, de standard automatique et Outlook Voice Access entrants à partir de passerelles VoIP, de PBX IP, de PBX compatibles SIP et de contrôleurs SBC, et d'écrire les modifications uniquement dans Active Directory.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

