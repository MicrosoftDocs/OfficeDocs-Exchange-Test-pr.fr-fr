---
title: 'Rechercher les modif. des groupes de rôles ou les journaux d’audit de l’admin.'
TOCTitle: Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur
ms:assetid: c7188d53-e672-492b-b57d-cd711379ddb3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff459262(v=EXCHG.150)
ms:contentKeyID: 50553896
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-12-02_

Vous pouvez effectuer des recherches dans les journaux d’audit de l’administrateur pour savoir qui a apporté des changements de configuration à l’organisation, aux serveurs et aux destinataires. Ceci peut s’avérer utile lorsque vous tentez d’identifier la cause d’un comportement inattendu, de confondre un administrateur malveillant ou bien de vous assurer que les exigences en matière de conformité sont respectées. Pour plus d’informations sur l’enregistrement dans des journaux d’audit de l’administrateur, consultez la rubrique [Connexion au service d’audit administrateur](administrator-audit-logging-exchange-2013-help.md).

Pour effectuer des recherches dans le journal d’audit d’une boîte aux lettres, consultez la rubrique [Enregistrement d’audit dans les boîtes aux lettres](mailbox-audit-logging-exchange-2013-help.md).

> [!TIP]
> Dans Exchange Online, vous pouvez utiliser le CAE pour afficher les entrées du journal d’audit de l’administrateur. Pour plus d’informations, consultez la rubrique <a href="view-the-administrator-audit-log-exchange-2013-help.md">Consulter le journal d’audit de l’administrateur</a>.


## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : moins de 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Enregistrement d’audit d’administrateur en affichage seul » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - La journalisation d’audit de l’administrateur est activée par défaut. Pour vérifier qu’elle a été activée, exécutez la commande suivante :
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    La valeur `True` indique que la journalisation d’audit de l’administrateur est activée. La valeur `False` indique qu’elle est désactivée. Si vous devez activer la journalisation d’audit de l’administrateur pour une organisation Exchange locale, exécutez la commande suivante :
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $true
    
    > [!NOTE]
    > La cmdlet <strong>Set-AdminAuditLogConfig</strong> n'est pas disponible dans Exchange Online.
    
    Pour plus d’informations, consultez la rubrique [Gestion de la journalisation d’audit de l’administrateur](manage-administrator-audit-logging-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour lancer le rapport des modifications des groupes de rôles de gestion

Pour connaître les changements qui ont été apportés aux groupes de rôles de gestion de votre organisation en matière d’appartenance à ces groupes, utilisez le rapport de groupe de rôles d’administrateur du Centre d’administration Exchange (EAC). Dans ce rapport, vous pouvez afficher la liste des groupes de rôles qui ont été modifiés dans une plage de dates précise. Vous pouvez aussi sélectionner les groupes de rôles spécifiques dont vous souhaitez afficher les changements.

1.  Dans le Centre d’administration Exchange (EAC), sélectionnez **Gestion de la conformité** \> **Audit**, puis cliquez sur **Exécuter un rapport de groupe de rôles d’administrateur**.

2.  Sélectionnez une plage de dates à l’aide des champs **Date de début** et **Date de fin**.

3.  Cliquez sur **Sélectionner les groupes de rôles**, puis sélectionnez les groupes de rôles pour lesquels vous souhaitez afficher les modifications ou laissez ce champ vide pour rechercher les modifications apportées à tous les groupes de rôles.

4.  Cliquez sur **Rechercher**.

Si vous trouvez des modifications selon les critères que vous avez spécifiés, la liste des modifications s’affiche dans le volet des résultats. Lorsque vous cliquez sur un groupe de rôles, les modifications de ce dernier s’affichent dans le volet d’informations.

## Utiliser le Centre d’administration Exchange (EAC) pour exporter le journal d’audit de l’administrateur

Pour créer un fichier XML qui contient des modifications apportées à votre organisation, utilisez le rapport « Exporter le journal d’audit de l’administrateur » du Centre d’administration Exchange (EAC). Dans ce rapport, vous pouvez spécifier une plage de dates pour rechercher des entrées du journal d’audit contenant des modifications apportées par des utilisateurs que vous avez spécifiés. Le fichier XML est alors transmis à un destinataire sous la forme d’une pièce jointe à un message électronique. La taille maximale du fichier XML est de 10 mégaoctets (Mo).

> [!NOTE]
> Outlook Web App ne vous permet pas d’ouvrir des pièces jointes au format XML par défaut. Vous pouvez soit configurer Exchange de façon à autoriser l’affichage des pièces jointes au format XML à l’aide d’Outlook Web App, soit utiliser un autre client de messagerie électronique, tel que Microsoft Outlook, de façon à afficher la pièce jointe. Pour plus d’informations sur la configuration d’Outlook Web App afin de permettre l’affichage d’une pièce jointe au format XML, consultez la rubrique <a href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Affichage ou configuration des répertoires virtuels d’Outlook Web App</a>.


1.  Dans le Centre d’administration Exchange (EAC), sélectionnez **Gestion de la conformité** \> **Audit**, puis cliquez sur **Exporter le journal d’audit de l’administrateur**.

2.  Sélectionnez une plage de dates à l’aide des champs **Date de début** et **Date de fin**.

3.  Dans le champ **Envoyer le rapport d’audit à**, cliquez sur **Sélectionner des utilisateurs**, puis sélectionnez le destinataire auquel vous voulez envoyer le rapport.

4.  Cliquez sur **Exporter**.

Si des entrées du journal sont retrouvées selon les critères que vous avez spécifiés, un fichier XML est créé et envoyé sous forme de pièce jointe à un message électronique au destinataire que vous avez précisé.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour rechercher des entrées du journal d’audit

Vous pouvez faire appel à l’environnement de ligne de commande Exchange Management Shell pour rechercher des entrées du journal d’audit qui correspondent aux critères définis. Pour obtenir une liste des critères de recherche, consultez la rubrique [Connexion au service d’audit administrateur](administrator-audit-logging-exchange-2013-help.md). Cette procédure utilise la cmdlet **Search-AdminAuditLog** et affiche les résultats dans l’environnement de ligne de commande Exchange Management Shell. Vous pouvez utiliser cette cmdlet si vous devez renvoyer un ensemble de résultats au-delà des limites définies dans la cmdlet **New-AdminAuditLogSearch** ou dans les rapports d’audit du Centre d’administration Exchange.

Pour envoyer à un destinataire les résultats de la recherche dans le journal d’audit sous forme de pièce jointe, consultez la section Utiliser l’environnement de ligne de commande Exchange Management Shell pour rechercher des entrées du journal d’audit et envoyer les résultats à un destinataire plus loin dans cette rubrique.

Pour effectuer une recherche dans le journal d’audit d’après les critères que vous avez définis, utilisez la syntaxe suivante.

    Search-AdminAuditLog - Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False >

> [!NOTE]
> Par défaut, la cmdlet <strong>Search-AdminAuditLog</strong> renvoie un maximum de 1 000 entrées du journal. Utilisez le paramètre <em>ResultSize</em> pour spécifier un seuil maximal de 250 000 entrées. ou bien la valeur <code>Unlimited</code> pour renvoyer toutes les entrées.


Cet exemple effectue une recherche portant sur toutes les entrées du journal d’audit avec les critères suivants :

  - **Date de début**   04/08/2012

  - **Date de fin**   10/03/2012

  - **ID d’utilisateur**   davids, chrisd, kima

  - **Cmdlets** **Set-Mailbox**

  - **Paramètres** *ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

<!-- end list -->

    Search-AdminAuditLog -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima

Cet exemple recherche les modifications apportées à une boîte aux lettres spécifique. Ceci est utile si vous effectuez des opérations de dépannage ou devez fournir des informations à des fins d’investigation. Les critères suivants sont définis :

  - **Date de début**   01/05/2012

  - **Date de fin**   10/03/2012

  - **ID d’objet**   contoso.com/Users/DavidS

<!-- end list -->

    Search-AdminAuditLog -StartDate 05/01/2012 -EndDate 10/03/2012 -ObjectID contoso.com/Users/DavidS

Si vos recherches renvoient un nombre important d’entrées du journal, nous vous recommandons de suivre la procédure décrite à la section Utiliser l’environnement de ligne de commande Exchange Management Shell pour rechercher des entrées du journal d’audit et envoyer les résultats à un destinataire plus loin dans cette rubrique. La procédure décrite dans cette section a pour objet d’envoyer aux destinataires que vous spécifiez un fichier XML sous forme de pièce jointe à un message électronique, ce qui vous permet d’extraire plus aisément les données qui vous intéressent.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Search-AdminAuditLog](https://technet.microsoft.com/fr-fr/library/ff459250\(v=exchg.150\)).

## Afficher le détail des entrées du journal d’audit

La cmdlet **Search-AdminAuditLog** renvoie les champs décrits dans la section « Contenu des journaux d’audit » de la rubrique [Connexion au service d’audit administrateur](administrator-audit-logging-exchange-2013-help.md). Parmi les champs renvoyés par la cmdlet, deux champs (**CmdletParameters** et **ModifiedProperties**) comportent des données supplémentaires qu’il est impossible de visualiser par défaut.

Pour afficher le contenu des champs **CmdletParameters** et **ModifiedProperties**, suivez la procédure ci-après. Ou bien exécutez la procédure décrite à la section Utiliser l’environnement de ligne de commande Exchange Management Shell pour rechercher des entrées du journal d’audit et envoyer les résultats à un destinataire plus loin dans cette rubrique pour créer un fichier XML.

Cette procédure exploite les concepts suivants :

  - [Tableaux](https://technet.microsoft.com/fr-fr/library/aa998267\(v=exchg.150\))

  - [Variables définies par l’utilisateur](https://technet.microsoft.com/fr-fr/library/bb123690\(v=exchg.150\))

<!-- end list -->

1.  Déterminez les critères sur lesquels doivent porter vos recherches, exécutez la cmdlet **Search-AdminAuditLog** et stockez les résultats dans une variable au moyen de la commande suivante.
    
        $Results = Search-AdminAuditLog <search criteria>

2.  Chaque entrée du journal d’audit est stockée sous la forme d’un élément de tableau dans la variable `$Results`. Vous pouvez sélectionner un élément de tableau en précisant son index. Les index des éléments de tableau commencent à zéro (0) pour le premier élément du tableau. Par exemple, pour extraire le cinquième élément de tableau dont l’index est 4, utilisez la commande suivante.
    
        $Results[4]

3.  La commande précédente renvoie l’entrée du journal stockée dans l’élément de tableau 4. Pour afficher le contenu des champs **CmdletParameters** et **ModifiedProperties** pour cette entrée du journal, utilisez les commandes suivantes.
    
        $Results[4].CmdletParameters
        $Results[4].ModifiedProperties

4.  Pour afficher le contenu des champs **CmdletParameters** ou **ModifiedParameters** dans une autre entrée du journal, modifiez l’index de l’élément de tableau.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour rechercher des entrées du journal d’audit et envoyer les résultats à un destinataire

Vous pouvez faire appel à l’environnement de ligne de commande Exchange Management Shell pour rechercher des entrées du journal d’audit qui correspondent aux critères définis, puis transmettre ces résultats à un destinataire de votre choix sous forme de fichier XML en pièce jointe. Les résultats sont envoyés au destinataire dans un délai de 15 minutes. Pour obtenir une liste des critères de recherche, consultez la rubrique [Connexion au service d’audit administrateur](administrator-audit-logging-exchange-2013-help.md).

> [!NOTE]
> Outlook Web App ne vous permet pas d’ouvrir des pièces jointes au format XML par défaut. Vous pouvez soit configurer Exchange de façon à autoriser l’affichage des pièces jointes au format XML à l’aide d’Outlook Web App, soit utiliser un autre client de messagerie électronique, tel que Microsoft Outlook, de façon à afficher la pièce jointe. Pour plus d’informations sur la configuration d’Outlook Web App afin de permettre l’affichage d’une pièce jointe au format XML, consultez la rubrique <a href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Affichage ou configuration des répertoires virtuels d’Outlook Web App</a>.


Pour effectuer une recherche dans le journal d’audit d’après les critères que vous avez définis, utilisez la syntaxe suivante.

    New-AdminAuditLogSearch -Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False > -StatusMailRecipients <recipient 1, recipient 2, ...> -Name <string to include in subject>

Cet exemple effectue une recherche portant sur toutes les entrées du journal d’audit avec les critères suivants :

  - **Date de début**   04/08/2012

  - **Date de fin**   10/03/2012

  - **ID d’utilisateur**   davids, chrisd, kima

  - **CmdletsSet-Mailbox**

  - **Paramètres***ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

La commande envoie les résultats à l’adresse SMTP davids@contoso.com avec le texte « Mailbox limit changes » (changements restrictifs de la boîte aux lettres) inclus dans la ligne d’objet du message.

    New-AdminAuditLogSearch -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima -StatusMailRecipients davids@contoso.com -Name "Mailbox limit changes"

> [!NOTE]
> Le rapport créé par la cmdlet <strong>New-AdminAuditLogSearch</strong> peut avoir une taille de 10 Mo au maximum. Si la recherche que vous effectuez émet un rapport d’une taille supérieure à 10 Mo, modifiez les critères de votre recherche. Vous pouvez notamment réduire la taille de la plage de dates et exécuter plusieurs rapports en attribuant à chacun une portion de la plage de dates d’origine.


Pour plus d’informations sur le format du fichier XML, consultez la rubrique [Structure du journal d’audit de l’administrateur](administrator-audit-log-structure-exchange-2013-help.md).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-AdminAuditLogSearch](https://technet.microsoft.com/fr-fr/library/ff459243\(v=exchg.150\)).

