---
title: 'Créer une stratégie de rétention: Exchange 2013 Help'
TOCTitle: Créer une stratégie de rétention
ms:assetid: d8806c98-fea5-492f-906d-f514e25361b2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150573(v=EXCHG.150)
ms:contentKeyID: 50479300
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une stratégie de rétention

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Dans Exchange Online et Exchange Server 2013, vous pouvez utiliser des stratégies de rétention pour gérer le cycle de vie de la messagerie. Les stratégies de rétention sont appliquées en créant des balises de rétention, en les ajoutant à une stratégie de rétention et en appliquant la stratégie aux utilisateurs de la boîte aux lettres.

Cette [vidéo](https://go.microsoft.com/fwlink/?linkid=825854) décrit comment créer une stratégie de rétention et l’appliquer à une boîte aux lettres dans Exchange Online.

Pour connaître les tâches de gestion supplémentaires relatives aux stratégies de rétention, consultez la rubrique [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 30 minutes.

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Les boîtes aux lettres auxquelles vous appliquez des stratégies de rétention doivent résider sur des serveurs Exchange Server 2010 ou versions ultérieures.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Comment procéder ?

## Étape 1 : Création d’une balise de rétention

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Gestion des enregistrements de messagerie » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

**Utilisation du Centre d’administration Exchange pour créer une balise de rétention**

1.  Accédez à **Gestion de la conformité** \> **Balises de rétention**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter")

2.  Sélectionnez l'une des options suivantes :
    
      - **Appliqué automatiquement à l’intégralité de la boîte aux lettres (par défaut)**   Sélectionnez cette option pour créer une balise de stratégie par défaut (DPT). Les balises de stratégie par défaut (DPT) permettent de créer une stratégie de suppression par défaut et une stratégie d’archivage par défaut qui s’appliquent à tous les éléments de la boîte aux lettres.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Vous ne pouvez pas utiliser le Centre d’administration Exchange (EAC) pour créer une balise de stratégie par défaut (DPT) afin de supprimer des éléments de messagerie vocale. Pour plus d’informations sur la création d’une balise de stratégie par défaut (DPT) pour supprimer des éléments de messagerie vocale, voir l’exemple de l’environnement de ligne de commande Exchange Management Shell ci-dessous.</td>
        </tr>
        </tbody>
        </table>
    
      - **Appliqué automatiquement à un dossier spécifique**   Sélectionnez cette option pour créer une balise de stratégie de rétention (RPT) pour un dossier par défaut, comme **Boîte de réception** ou **Éléments supprimés**.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Vous ne pouvez créer des balises de stratégie de rétention qu’avec les actions <strong>Supprimer et autoriser la récupération</strong> ou <strong>Supprimer définitivement</strong>.</td>
        </tr>
        </tbody>
        </table>
    
      - **Appliqué par les utilisateurs aux éléments et aux dossiers (personnels)**   Sélectionnez cette option pour créer des balises personnelles. Ces balises permettent à des utilisateurs de Outlook et de Outlook Web App d’appliquer des paramètres d’archivage et de suppression à un message ou à des dossiers qui diffèrent de ceux appliqués au dossier parent ou à la boîte aux lettres complète.

3.  Le titre et les options de la page **Nouvelle balise de rétention** varient selon le type de balise que vous avez sélectionné. Renseignez les champs suivants :
    
      - **Nom**   Entrez un nom pour la balise de rétention. Le nom de la balise est utilisé à des fins d’affichage et n’a aucun impact sur le dossier ou l’élément auquel une balise est appliquée. Rappelez-vous que les balises personnelles que vous configurez pour les utilisateurs sont disponibles dans Outlook et Outlook Web App.
    
      - **Appliquer cette balise au dossier par défaut suivant**   Cette option n’est accessible que si vous avez sélectionné **Appliqué automatiquement à un dossier spécifique**.
    
      - **Action de rétention**   Sélectionnez l’une des actions suivantes à effectuer après que l’élément ait atteint sa période de rétention :
        
          - **Supprimer et autoriser la récupération**   Sélectionnez cette action pour supprimer des éléments, tout en autorisant les utilisateurs à les récupérer via l’option **Récupération des éléments supprimés** dans Outlook or Outlook Web App. Les éléments sont conservés tant que la période de rétention des éléments supprimés configurée pour la base de données de boîtes aux lettres ou pour l’utilisateur de la boîte aux lettres n’est pas atteinte.
        
          - **Supprimer définitivement** Sélectionnez cette option pour supprimer définitivement l’élément de la base de données de boîtes aux lettres.
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>Les boîtes aux lettres ou les éléments soumis à un blocage sur place et une suspension pour litige doivent être conservés et renvoyés dans les recherches de découverte électronique sur place (In-Place eDiscovery). Pour en savoir plus, consultez la rubrique <a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Conservation inaltérable et conservation pour litige</a>.</td>
            </tr>
            </tbody>
            </table>
        
          - **Déplacer vers l’archive**   Cette action n’est accessible que si vous créez une balise de stratégie par défaut ou une balise personnelle. Sélectionnez cette action pour déplacer des éléments vers l’archivage local de l’utilisateur.
    
      - **Période de rétention** Sélectionnez l’une des options suivantes :
        
          - **Jamais**   Sélectionnez cette option pour spécifier que des éléments ne doivent jamais être supprimés ni déplacés vers l’archivage.
        
          - **Lorsque l’élément atteint l’âge suivant (en jours)**   Sélectionnez cette option et spécifiez le nombre de jours pour conserver des éléments avant qu’ils ne soient déplacés ou supprimés. L’âge de rétention de tous les éléments pris en charge, à l’exception de Calendrier et de Tâches, est calculé à partir de la date de réception ou de création d’un élément. L’âge de rétention pour des éléments Calendrier et Tâches est calculé à partir de la date de fin.
    
      - **Commentaire**   Utilisez ce champ facultatif pour entrer des notes administratives ou des commentaires. Le champ n’est pas visible par les utilisateurs.

**Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une balise de rétention**

La cmdlet **New-RetentionPolicyTag** permet de créer une balise de rétention. Différentes options disponibles dans la cmdlet vous permettent de créer différents types de balises de rétention. Utilisez le paramètre *Type* pour créer une balise de stratégie par défaut (`All`), une balise de stratégie de rétention (spécifiez un type de dossier par défaut, comme `Inbox`) ou une balise personnelle (`Personal`).

Cet exemple illustre la création d’une balise de stratégie par défaut pour supprimer tous les messages de la boîte aux lettres après 7 ans (2 556 jours).

    New-RetentionPolicyTag -Name "DPT-Corp-Delete" -Type All -AgeLimitForRetention 2556 -RetentionAction DeleteAndAllowRecovery

Cet exemple illustre la création d’une balise de stratégie par défaut visant à déplacer tous les messages vers l’archivage local dans 2 ans (730 jours).

    New-RetentionPolicyTag -Name "DPT-Corp-Move" -Type All -AgeLimitForRetention 730 -RetentionAction MoveToArchive

Cet exemple illustre la création d’une balise de stratégie par défaut visant à supprimer les messages vocaux après 20 jours.

    New-RetentionPolicyTag -Name "DPT-Corp-Voicemail" -Type All -MessageClass Voicemail -AgeLimitForRetention 20 -RetentionAction DeleteAndAllowRecovery

Cet exemple illustre la création d’une balise de stratégie de rétention visant à supprimer définitivement les messages du dossier Courrier indésirable après 30 jours.

    New-RetentionPolicyTag -Name "RPT-Corp-JunkMail" -Type JunkEmail -AgeLimitForRetention 30 -RetentionAction PermanentlyDelete

Cet exemple illustre la création d’une balise personnelle visant à ne jamais supprimer un message.

    New-RetentionPolicyTag -Name "Never Delete" -Type Personal -RetentionAction DeleteAndAllowRecovery -RetentionEnabled $false

## Étape 2 : Création d’une stratégie de rétention

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Gestion des enregistrements de messagerie » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

**Utilisation du Centre d’administration Exchange pour créer une stratégie de rétention**

1.  Accédez à **Gestion de la conformité** \> **Stratégies de rétention**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter")

2.  Dans **Nouvelle stratégie de rétention**, renseignez les champs suivants :
    
      - **Nom**   Attribuez un nom à la stratégie de rétention.
    
      - **Balises de rétention**   Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour sélectionner les balises que vous souhaitez ajouter à cette stratégie de rétention.
        
        Une stratégie de rétention peut contenir les balises suivantes :
        
          - Une balise de stratégie par défaut avec l’action **Déplacer vers l’archive**
        
          - Une seule balise de stratégie par défaut avec l’action **Supprimer et autoriser la récupération** ou **Supprimer définitivement**
        
          - Une seule balise de stratégie par défaut pour des messages vocaux avec les actions **Supprimer et autoriser la récupération** ou **Supprimer définitivement**
        
          - Une balise de stratégie de rétention par dossier par défaut, telle que **Boîte de réception** pour supprimer des éléments
        
          - N’importe quel nombre de balises personnelles
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>Bien que vous puissiez ajouter n’importe quel nombre de balises personnelles à une stratégie de rétention, le fait de disposer d’un grand nombre de balises personnelles avec différents paramètres de rétention peut dérouter les utilisateurs. Nous recommandons de ne pas associer plus de 10 balises personnelles à une stratégie de rétention.</td>
            </tr>
            </tbody>
            </table>
        
        Vous pouvez créer une stratégie de rétention sans lui ajouter de balises de rétention, sauf que des éléments de la boîte aux lettres à laquelle la stratégie s’applique ne seront pas déplacés ni supprimés. Vous pouvez également ajouter et supprimer des balises de rétention d’une stratégie de rétention après sa création.

**Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une stratégie de rétention**

Cet exemple illustre la création d’une stratégie de rétention RetentionPolicy-Corp et l’utilisation du paramètre *RetentionPolicyTagLinks* pour associer cinq balises à la stratégie.

    New-RetentionPolicy "RetentionPolicy-Corp"  -RetentionPolicyTagLinks "DPT-Corp-Delete","DPT-Corp-Move","DPT-Corp-Voicemail","RPT-Corp-JunkMail","Never Delete"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-RetentionPolicy](https://technet.microsoft.com/fr-fr/library/dd297970\(v=exchg.150\)).

## Étape 3 : Application d’une stratégie de rétention aux utilisateurs de boîtes aux lettres

Après avoir créé une stratégie de rétention, vous devez l’appliquer aux utilisateurs de la boîte aux lettres. Vous pouvez appliquer différentes stratégies de rétention à différents groupes d’utilisateurs. Pour plus d'informations, consultez la rubrique [Appliquer une stratégie de rétention aux boîtes aux lettres](apply-a-retention-policy-to-mailboxes-exchange-2013-help.md).

## Comment savoir si cette tâche a fonctionné ?

Une fois que vous avez créé des balises de rétention, ajoutez-les à une stratégie de rétention et appliquez la stratégie à un utilisateur de boîte aux lettres. Lors du prochain traitement de la boîte aux lettres par l’assistant de boîte aux lettres MRM, les messages seront déplacés ou supprimés, en fonction des paramètres que vous avez configurés dans la balise de rétention.

Pour vérifier que vous avez appliqué la stratégie de rétention, procédez comme suit :

1.  Exécutez la commande de l’environnement de ligne de commande Exchange Management Shell pour exécuter manuellement l’assistant MRM sur une boîte aux lettres unique.
    
        Start-ManagedFolderAssistant -Identity <mailbox identity>

2.  Connectez-vous à la boîte aux lettres via Outlook ou Outlook Web App et vérifiez que les messages sont supprimés ou déplacés vers une archive conformément à la configuration de la stratégie.

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

