---
title: 'Création d’une boîte aux lettres de dossiers publics: Exchange 2013 Help'
TOCTitle: Création d’une boîte aux lettres de dossiers publics
ms:assetid: 64437ffd-231b-4c10-84df-232ccbe9538f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ552410(v=EXCHG.150)
ms:contentKeyID: 50478283
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Création d’une boîte aux lettres de dossiers publics

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2014-10-23_

Avant de pouvoir créer un dossier public, vous devez d'abord créer une boîte aux lettres de dossiers publics. Les boîtes aux lettres de dossiers publics contiennent des informations sur la hiérarchie et le contenu des dossiers publics. La première boîte aux lettres de dossiers publics que vous créez est la boîte aux lettres de hiérarchie principale et contient l'unique exemplaire de la hiérarchie dans lequel les opérations d'écriture sont autorisées. Toutes les autres boîtes aux lettres de dossiers publics que vous créez sont des boîtes aux lettres secondaires et contiennent une copie en lecture seule de la hiérarchie.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour plus d’informations sur les limites et les quotas de stockage pour les dossiers publics, consultez les rubriques suivantes :
<ul>
<li><p>Pour les dossiers publics dans Office 365, voir <a href="https://go.microsoft.com/fwlink/?linkid=391188">Limites d’Exchange Online</a>.</p></li>
<li><p>Pour les dossiers publics dans Exchange Server 2013 sur site, voir <a href="limits-for-public-folders-exchange-2013-help.md">Limites pour les dossiers publics</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Pour découvrir d'autres tâches de gestion associées aux dossiers publics dans Exchange 2013, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

Pour découvrir d'autres tâches de gestion associées aux dossiers publics dans Exchange Online, consultez la rubrique [Procédures de dossiers publics dans Office 365 et Exchange Online](https://technet.microsoft.com/fr-fr/library/jj966272\(v=exchg.150\)).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins de 5 minutes.

  - Des dossiers publics Exchange 2013 et des dossiers publics sur des serveurs Exchange hérités ne peuvent pas exister dans la même organisation. Si vous tentez de créer une boîte aux lettres de dossier public lorsque vous disposez encore de dossiers publics hérités, vous recevez l’erreur **Un déploiement de dossiers publics existant a été détecté. Pour migrer les données de dossiers publics existantes, créez une nouvelle boîte aux lettres de dossier public à l’aide du commutateur -HoldForMigration.**
    
    Pour pouvoir créer des dossiers publics dans Exchange 2013, vous devez migrer vos dossiers publics hérités vers Exchange 2013. Pour ce faire, suivez les étapes décrites dans [Migrer les dossiers publics vers Exchange 2013 à partir de versions antérieures](https://technet.microsoft.com/fr-fr/library/jj150486\(v=exchg.150\)). Ces étapes vous expliquent comment créer une boîte aux lettres de dossier public pouvant être utilisée pour stocker vos dossiers publics migrés.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Dossiers publics » dans la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour créer une boîte aux lettres de dossiers publics

1.  Accédez à **Dossiers publics**\>**Boîtes aux lettres de dossiers publics**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans **Boîte aux lettres de dossiers publics**, attribuez un nom à la boîte aux lettres de dossiers publics.

3.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une boîte aux lettres de dossiers publics

Cet exemple permet de créer la boîte aux lettres de dossiers publics principale.

    New-Mailbox -PublicFolder -Name MasterHierarchy

Cet exemple montre comment créer une boîte aux lettres de dossiers publics secondaire. La seule différence entre la création de la boîte aux lettres de hiérarchie principale et une boîte aux lettres de hiérarchie secondaire est que la boîte aux lettres principale est la première créée dans l'organisation. Vous pouvez créer d'autres boîtes aux lettres de dossiers publics à des fins d'équilibrage de la charge.

    New-Mailbox -PublicFolder -Name Istanbul 

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997663\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien converti la boîte aux lettres de dossiers publics principale, exécutez la commande suivante de l'environnement de ligne de commande Exchange Management Shell :

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997571\(v=exchg.150\)).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

