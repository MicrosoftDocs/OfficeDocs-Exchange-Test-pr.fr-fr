---
title: 'Créer la navigation de menu: Exchange 2013 Help'
TOCTitle: Créer la navigation de menu
ms:assetid: 3cfc9a01-0a61-4d15-9561-621568dc30d9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997471(v=EXCHG.150)
ms:contentKeyID: 50477964
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantKeyMappingControl
ms.translationtype: MT
---

# Créer la navigation de menu

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Vous pouvez utiliser la page **nouvelle entrée de navigation de menu** pour créer un seul ou plusieurs mappages de touches pour les entreprises ou les heures creuses du menu principal vous invite à fournir les standards automatiques. Vous pouvez définir l'action qui sera effectuée lors d'une touche du clavier du téléphone est activée, par exemple, transférez l'appel vers un numéro de poste ou un autre standard automatique.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser le CAE pour configurer les menus de navigation standard automatique de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel vous souhaitez créer la navigation de menu. Dans la barre d'outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de **Standard automatique de messagerie unifiée**, cliquez sur **Menu de navigation**, sélectionnez **Activer la navigation de menu heures ouvrées** ou **Activer la navigation de menu en dehors des heures**, puis cliquez sur **Add**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans la page **nouvelle entrée de navigation de menu**, configurez les options suivantes :
    
      - **Invite**   Cette zone permet de saisir le nom du nouveau menu de navigation. Le nom du menu de navigation est uniquement utilisé à des fins d’affichage. Ce champ est obligatoire.
        
        Comme vous pouvez spécifier plusieurs nouveaux menus de navigation, nous vous recommandons d’utiliser des noms significatifs pour vos mappages de touches. La longueur maximale de ce nom est de 64 caractères et il peut contenir des espaces. Toutefois, il ne peut pas contenir les caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Lorsque cette touche est enfoncée**   Utilisez cette liste pour activer le mappage de touches. Le mappage de touches est le numéro de la touche qu’un appelant doit enfoncer pour que le standard automatique effectue une opération spécifique, telle que le transfert d’un appelant vers un autre standard automatique ou un opérateur. Par défaut, aucune entrée n’est définie.
        
        Utilisez la liste déroulante pour sélectionner la clé numérique (de 1 à 9) que l'appelant doit appuyer. Zéro (0) est réservé à l'opérateur de standard automatique.
        
        L’option **Délai d’attente** de la liste déroulante permet d’activer les appelants à transférer vers un numéro de poste ou un autre standard automatique s’ils n’enfoncent pas une touche du clavier du téléphone. Par exemple, « Veuillez patienter, un agent va bientôt vous répondre. » Le paramètre par défaut est 5 secondes. Si vous activez cette option, un mappage de touches vide est créé.
    
      - **Lire le fichier audio suivant**    Utilisez cette option pour sélectionner un fichier audio précédemment enregistré pour les appelants. Cliquez sur **Modifier**, puis cliquez sur **Parcourir** pour localiser le fichier audio.
    
      - **Effectuer cette action supplémentaire**   Sélectionnez l’une des actions suivantes pour définir l’action que vous souhaitez que le standard automatique effectue pour le compte de l’appelant:
        
          - **Aucun**    Si vous ne souhaitez du standard automatique pour transférer l'appel à une extension ou à un autre standard automatique ou laisser un message pour un utilisateur, utilisez cette option.
        
          - **Transférer vers cette extension**   Activez cette option pour activer le transfert des appels vers une extension. Si vous activez cette option, utilisez cette zone pour saisir le numéro de l'extension vers lequel l'appel sera transféré. Ce champ ne peut contenir que des caractères numériques. Il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Transférer vers ce standard automatique de messagerie unifiée**   Activez cette option pour transférer l'appel vers un standard automatique. Cliquez sur **Parcourir** pour localiser le standard automatique que vous voulez utiliser. Avant d'activer cette option, vous devez créer et configurer le standard automatique. Cette option est utilisée lorsque vous créez une structure parent/enfant de standards automatiques de messagerie unifiée.
        
          - **Laisser un message vocal pour cet utilisateur**   Activez cette option pour permettre à un appelant de laisser un message vocal à un utilisateur qui appartient au même plan de numérotation que le standard automatique de messagerie unifiée que vous configurez. Lorsqu'un appelant choisit cette option dans un menu de standard automatique, il est invité à laisser un message vocal à l'utilisateur qui a été sélectionné. Cliquez sur **Parcourir** pour accéder à l'utilisateur à extension messagerie unifiée.
        
          - **Annoncer l’adresse de l’entreprise**   Sélectionnez cette option pour permettre à un appelant de choisir une option de menu de standard automatique pour écouter l’adresse de l’entreprise qui a été configurée sur le standard automatique de messagerie unifiée. Pour que ce service fonctionne correctement, vous devez d’abord saisir l’adresse de l’entreprise dans la zone **Adresse de l’entreprise** de la page **Général** dudit standard.
        
          - **Annoncer les heures d’ouverture**   Sélectionnez cette option pour permettre à un appelant de choisir une option de menu de standard automatique pour écouter les heures d’ouverture de l’entreprise qui a été configurée sur le standard automatique de messagerie unifiée. Pour que ce service fonctionne correctement, vous devez d’abord configurer les heures d’ouverture dans la page **Heures d’ouverture** du standard automatique de messagerie unifiée.

5.  Cliquez sur **OK** pour créer le nouveau menu de navigation.

6.  Dans la page **Standard automatique de messagerie unifiée**, cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser le Shell pour configurer les mappages clés standard automatique de messagerie unifiée

Cet exemple active les mappages de touches heures ouvrées afin que :

  - Lorsque les appelants appuyez sur 1, ils seront transférés vers un autre standard automatique de messagerie unifiée nommé `SalesAutoAttendant`.

  - Lorsqu'il clique sur 2, ils seront transférés vers le numéro de poste 12345 pour la prise en charge.

  - Lorsqu'il clique sur 3, ils seront envoyés à un autre standard automatique qui lira un fichier audio.

<!-- end list -->

    Set-UMAutoAttendant -id MyAutoAttendant -BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

Cet exemple montre comment définit les mappages de clés définis dans un fichier de valeurs séparées par des virgules (.csv). Vous devez d'abord créer le fichier .csv avec les en-têtes suivants et la correction : \< key \>, \< description \>, \[\< extension \>\], \[\< nom autoattendant \>\], \[\< promptfilenamepath \>\], \[\< asrphrase1 ; asrphrase2 \>\], \[\< leavevoicemailfor \>\], \[\< transfertomailbox \>\]. Les valeurs entre crochets sont facultatifs. Après avoir créé le fichier .csv, importez le fichier .csv à l'aide de l'applet de commande **Import-csv** .

    $o = Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    Set-UMAutoAttendant MyAutoAttendant -BusinessHoursKeyMapping $o

Cet exemple exporte les mappages de clés à partir d'un standard automatique de messagerie unifiée existant vers un fichier .csv, puis importe les mappages de touches mêmes dans un autre standard automatique de messagerie unifiée. Vous pourriez également exporter les mappages de touches vers un fichier .csv, modifier ou modifier les mappages de clés dans le fichier .csv et puis d'importer les mappages de touches dans un autre standard automatique de messagerie unifiée.

    $aa = Get-UMAutoAttendant -id MyAutoAttendant
    $aa1 = Get-UMAutoAttendant -id MyAutoAttendant2
    $aa.BusinessHoursKeyMapping | Export-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    $aa1.BusinessHoursKeyMapping = (Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv")

