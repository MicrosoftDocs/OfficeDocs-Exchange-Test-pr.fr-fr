---
title: 'Gestion de l’appr. des msg et résolution de problèmes: Exchange 2013 Help'
TOCTitle: Gestion de l’approbation des messages et résolution des problèmes
ms:assetid: 860df43f-a05b-4da3-83f1-68d3123a923d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298110(v=EXCHG.150)
ms:contentKeyID: 52062997
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion de l’approbation des messages et résolution des problèmes

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Vous pouvez recevoir l'erreur suivante lorsque vous essayez de supprimer une boîte à lettres d'arbitrage :


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Impossible de supprimer la boîte aux lettres d'arbitrage &lt;<em>boîte_aux_lettres</em>&gt;, car elle est utilisée pour le flux d'approbation des destinataires existants dont l'appartenance est sujette à des restrictions ou pour lesquels la modération est activée. Vous devriez désactiver les fonctionnalités d'approbation pour ces destinataires ou spécifier une autre boîte aux lettres d'arbitrage avant de supprimer cette boîte aux lettres d'arbitrage.</p></td>
</tr>
</tbody>
</table>


Une boîte aux lettres d'arbitrage peut être utilisée pour gérer le flux d'approbation des destinataires modérés et des approbations d'appartenance des groupes de distribution. À cette fin, vous utilisez PowerShell pour identifier tous les destinataires configurés pour utiliser la boîte aux lettres d'arbitrage. Après avoir identifié les destinataires, vous pouvez soit les configurer de sorte qu'ils utilisent une autre boîte aux lettres d'arbitrage, soit désactiver la modération en ce qui les concerne.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Arbitrage » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Étape 1 : utiliser l'environnement de ligne de commande Exchange Management Shell pour identifier tous les destinataires utilisant la boîte aux lettres d'arbitrage que vous tentez de supprimer

Exécutez les commandes suivantes :

    $AM = Get-Mailbox "<arbitration mailbox>" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

Par exemple, pour trouver tous les destinataires utilisant la boîte aux lettres d'arbitrage Arbitration Mailbox01, exécutez les commandes suivantes :

    $AM = Get-Mailbox "Arbitration Mailbox01" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

> [!NOTE]
> Vous spécifiez la boîte aux lettres d'arbitrage à l'aide du nom unique. Si vous connaissez le nom unique de la boîte aux lettres d'arbitrage, vous pouvez exécuter la commande unique : <code>Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq &lt;DN&gt;}</code>.


## Étape 2 : utiliser l'environnement de ligne de commande Exchange Management Shell pour spécifier une autre boîte aux lettres d'arbitrage ou désactiver la modération pour les destinataires

Pour empêcher les destinataires d'utiliser la boîte aux lettres d'arbitrage que vous tentez de supprimer, vous pouvez soit spécifier une autre boîte aux lettres d'arbitrage, soit désactiver la modération pour les destinataires.

Si vous décidez de spécifier une autre boîte aux lettres d'arbitrage pour les destinataires, exécutez la commande suivante :

    Set-<RecipientType> <Identity> -ArbitrationMailbox <different arbitration mailbox>

Par exemple, pour reconfigurer le groupe de distribution All Employees de sorte qu'il utilise la boîte aux lettres d'arbitrage Arbitration Mailbox02 pour l'approbation d'appartenance, exécutez la commande suivante :

    Set-DistributionGroup "All Employees" -ArbitrationMailbox "Arbitration Mailbox02"

Si vous choisissez de désactiver la modération pour les destinataires, exécutez la commande suivante :

    Set-<RecipientType> <Identity> -ModerationEanbled $false

Par exemple, pour désactiver la modération pour la boîte aux lettres Human Resources, exécutez la commande suivante :

    Set-Mailbox "Human Resources" -ModerationEanbled $false

## Comment savoir si cela a fonctionné ?

La procédure est réussie si vous parvenez à supprimer la boîte aux lettres d'arbitrage sans recevoir l'erreur indiquant que celle-ci est en cours d'utilisation.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

