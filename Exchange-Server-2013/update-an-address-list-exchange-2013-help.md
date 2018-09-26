---
title: "Mettre à jour une liste d'adresses: Exchange 2013 Help"
TOCTitle: Mettre à jour une liste d'adresses
ms:assetid: 163e7099-cf14-4bb0-a84c-1401e9db670e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996375(v=EXCHG.150)
ms:contentKeyID: 50477569
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.UpdateAddressListWizardForm.ScheduleWizardPage
ms.translationtype: HT
---

# Mettre à jour une liste d'adresses

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-14_

Les listes d’adresses sont un ensemble d’objets destinataire et autres objets Active Directory. Une liste d’adresses est applicable dès que la règle de filtrage de la liste d’adresses a été modifiée. Pour mettre à jour l’appartenance à la liste d’adresses afin d’inclure de nouveaux destinataires et supprimer ceux qui ne correspondent plus aux critères de filtrage, vous devez appliquer la liste d’adresses.

Pour connaître les autres tâches de gestion relatives aux listes d’adresses, consultez la rubrique [Procédures des listes d'adresses](address-list-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : L’exécution de ce processus risque de prendre du temps selon le nombre de destinataires figurant dans la liste d’adresses.

  - Certaines listes d’adresses contiennent des milliers ou des dizaines de milliers de destinataires selon la taille de l’organisation et les filtres ajoutés à la liste d’adresses. La mise à jour des listes d’adresses peut nécessiter de nombreuses ressources de l’ordinateur. Ainsi, vous souhaiterez sans doute mettre à jour la liste d’adresses pendant les heures creuses.

  - Si la liste d’adresses contient plus de 3 000 destinataires, nous vous conseillons d’utiliser l’environnement de ligne de commande Exchange Management Shell pour la mettre à jour.

Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour mettre à jour une liste d’adresses

1.  Accédez à **Organisation** \> **Listes d’adresses**.

2.  Dans l’affichage Liste, sélectionnez la liste d’adresses à mettre à jour.

3.  Dans le volet d’informations, cliquez sur **Mettre à jour**.

## Utiliser le Shell pour mettre à jour une liste d’adresses

Cet exemple met à jour la liste d’adresses intitulée État de Washington.

```powershell
Update-AddressList "Washington State"
```

Si plusieurs listes d’adresses portent le même nom, vous devez spécifier le chemin d’accès complet à la liste d’adresses que vous souhaitez mettre à jour. Par exemple, pour mettre à jour la liste d’adresses intitulée Ventes sous Amérique du Nord alors qu’il existe une liste d’adresses Ventes sous Europe, utilisez la commande suivante :

```powershell
Update-AddressList "North America\Sales"
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Update-AddressList](https://technet.microsoft.com/fr-fr/library/aa997982\(v=exchg.150\)).

