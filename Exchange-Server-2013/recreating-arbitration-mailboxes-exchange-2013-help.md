---
title: 'Recreating arbitration mailboxes: Exchange 2013 Help'
TOCTitle: Recreating arbitration mailboxes
ms:assetid: bb6b8524-aaee-4be8-a04e-e61cd2ab3465
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt829264(v=EXCHG.150)
ms:contentKeyID: 74518127
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recreating arbitration mailboxes

 

_**Dernière rubrique modifiée :** 2018-01-17_

**Résumé** : À propos des boîtes aux lettres d’arbitrage dans Exchange 2013 et de la façon de les recréer.

Exchange 2013 est fourni avec cinq boîtes aux lettres système appelées *boîtes aux lettres d’arbitrage*. Les boîtes aux lettres d’arbitrage permettent de stocker plusieurs types de données système et de gérer des flux de travail d’approbation de messagerie. Le tableau ci-dessous répertorie chaque type de boîte aux lettres d’arbitrage et ses responsabilités.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de la boîte aux lettres d’arbitrage</th>
<th>Nom complet</th>
<th>Fonctionnalités persistantes</th>
<th>Fonction</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
<td><p>Boîte aux lettres Fédération Microsoft Exchange</p></td>
<td><p>{}</p></td>
<td><p>Cette boîte aux lettres stocke les données utilisées pour assurer la fédération entre les différentes organisations Exchange. Cela inclut les services RMS, les réponses et sondes de surveillance de flux de messagerie intersites, les notifications les archives en ligne, la gestion des enregistrements de messagerie, ainsi que les informations de disponibilité intersites.</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109}</p></td>
<td><p>Assistant Approbation Microsoft Exchange</p></td>
<td><p>{}</p></td>
<td><p>Cette boîte aux lettres est configurée pour l’infrastructure d’approbation Exchange, afin de gérer les demandes d’approbation de groupe automatique et de modération de destinataire.</p></td>
</tr>
<tr class="odd">
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
<td><p>Migration Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityManagement}</p></td>
<td><p>Stocke des données pour le service de migration Exchange à utiliser lors du déplacement de boîtes aux lettres par lots.</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMDataStorage}</p></td>
<td><p>Boîte aux lettres système de découverte.</p>
<p>Configurée pour la fonctionnalité de découverte électronique, qui est utilisée par des agents de conformité afin de localiser les messages qui correspondent aux critères de sélection spécifiés. Cette boîte aux lettres est également utilisée par la messagerie unifiée afin de stocker les fichiers de participation de la console de messagerie unifiée et d’autres informations.</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMGrammarReady, OrganizationCapabilityPstProvider, OrganizationCapabilityMessageTracking, OrganizationCapabilityMailRouting, OrganizationCapabilityClientExtensions, OrganizationCapabilityGMGen, OrganizationCapabilityOABGen, OrganizationCapabilityUMGrammar}</p></td>
<td><p>Il s’agit d’une boîte aux lettres d’organisation. Elle permet de créer des carnets d’adresses en mode hors connexion (OAB). Pour équilibrer la charge de la génération de carnet d’adresses en mode hors connexion dans votre organisation, y compris entre les sites géographiquement distincts, vous pouvez créer des boîtes aux lettres d’organisation supplémentaires.</p></td>
</tr>
</tbody>
</table>


Si vous devez recréer cette boîte aux lettres d’arbitrage, reportez-vous aux instructions ci-dessous.

## À savoir avant de commencer

  - Durée d’exécution estimée : 10 minutes par procédure.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Utilisation d’Environnement de ligne de commande Exchange Management Shell pour recréer une boîte aux lettres d’arbitrage

Utilisez les instructions suivantes pour recréer un certain type de boîte aux lettres d’arbitrage.

> [!NOTE]
> Toutes les étapes décrites dans les sections suivantes doivent être exécutées à partir du même répertoire où vous avez extrait le support d’installation Exchange.


## Recréation de la boîte aux lettres Fédération Microsoft Exchange

Pour recréer la boîte aux lettres d’arbitrage FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042, procédez comme suit :

1.  Si des boîtes aux lettres d’arbitrage sont manquantes, exécutez la commande suivante :
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

2.  Dans Environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
    ```powershell
Enable-Mailbox -Arbitration -Identity "FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042"
```

## Recréation de la boîte aux lettres Assistant Approbation Microsoft Exchange

Pour recréer la boîte aux lettres d’arbitrage SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109}, procédez comme suit :

1.  Si des boîtes aux lettres d’arbitrage sont manquantes, exécutez la commande suivante :
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

2.  Dans Environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
        Get-User | Where-Object {$_.Name -like "SystemMailbox{1f05a927-7709-4e35-9dbe-d0f608fb781a}"} | Enable-Mailbox -Arbitration

## Recréation de la boîte aux lettres Migration Microsoft Exchange

Pour recréer la boîte aux lettres d’arbitrage Migration.8f3e7716-2011-43e4-96b1-aba62d229136, procédez comme suit :

1.  Si des boîtes aux lettres d’arbitrage sont manquantes, exécutez la commande suivante :
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

2.  Dans Environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
    ```powershell
Enable-Mailbox -Arbitration -Identity "Migration.8f3e7716-2011-43e4-96b1-aba62d229136"
```

3.  Dans Environnement de ligne de commande Exchange Management Shell, définissez les fonctionnalités persistantes (msExchCapabilityIdentifiers) en exécutant la commande suivante :
    
    ```powershell
Set-Mailbox "Migration.8f3e7716-2011-43e4-96b1-aba62d229136" -Arbitration -Management:$True -Force
```

## Recréation de la boîte aux lettres système Découverte Microsoft Exchange

Pour recréer la boîte aux lettres d’arbitrage SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

## Recréation de la boîte aux lettres d’organisation Microsoft Exchange pour les carnets d’adresses en mode hors connexion

Pour recréer la boîte aux lettres d’arbitrage SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}, procédez comme suit :

1.  Si des boîtes aux lettres d’arbitrage sont manquantes, exécutez la commande suivante :
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

2.  Dans Environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
    ```powershell
Enable-Mailbox -Arbitration -Identity "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}"
```

3.  Dans Environnement de ligne de commande Exchange Management Shell, définissez les fonctionnalités persistantes (msExchCapabilityIdentifiers) en exécutant la commande suivante :
    
        Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration | Set-Mailbox -Arbitration -UMGrammar:$True -OABGen:$True -GMGen:$True -ClientExtensions:$True -MessageTracking:$True -PstProvider:$True -MaxSendSize 1GB -Force

Lorsque vous avez terminé, si vous exécutez la commande `$OABMBX = Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration (Get-ADUser $OABMBX.SamAccountName -Properties *).msExchCapabilityIdentifiers`, vous verrez que les éléments 46, 47 et 51 sont manquants. Exécutez la commande suivante pour rajouter toutes les fonctionnalités :

    Set-ADUser $OABMBX.SamAccountName -Add @{"msExchCapabilityIdentifiers"="40","42","43","44","47","51","52","46"}

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien recréé la boîte aux lettres d’arbitrage, utilisez la cmdlet **Get-Mailbox** avec le commutateur *Arbitration* pour récupérer les boîtes aux lettres système.

```powershell
Get-Mailbox -Arbitration | Format-Table Name, DisplayName
```

Affichez les résultats de la commande pour vérifier que la boîte aux lettres système appropriée a été recréée soit par nom, soit par nom d’affichage dans le tableau ci-dessus.

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

