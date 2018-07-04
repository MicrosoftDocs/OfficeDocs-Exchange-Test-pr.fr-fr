---
title: "Création d'une stratégie d'adresse de messagerie: Exchange 2013 Help"
TOCTitle: Création d'une stratégie d'adresse de messagerie
ms:assetid: eb2bf42e-2058-4e17-85d5-97546433b40a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125137(v=EXCHG.150)
ms:contentKeyID: 50479453
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: HT
---

# Création d'une stratégie d'adresse de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-12-10_

Pour qu'un destinataire puisse recevoir ou envoyer des messages électroniques, il doit avoir une adresse de messagerie. Les stratégies d’adresse de messagerie génèrent des adresses de messagerie principale et secondaire pour vos destinataires (incluant les utilisateurs, les contacts et les groupes), de façon à ce qu’ils puissent recevoir et envoyer des messages.

Lors de la création d’une stratégie d’adresse de messagerie, les types d’adresse de messagerie suivants peuvent être utilisés :

  - **Adresse de messagerie SMTP prédéfinie**. Les adresses de messagerie SMTP *prédéfinies* sont des types d’adresse de messagerie fréquemment utilisés qui vous sont fournis.

  - **Adresse de messagerie SMTP personnalisée**. Si vous ne voulez pas utiliser l’une des adresses de messagerie SMTP prédéfinies, vous pouvez spécifier une adresse de messagerie SMTP personnalisée.
    
    Lors de la création d’une adresse de messagerie SMTP personnalisée, vous pouvez utiliser les variables indiquées dans le tableau suivant pour spécifier d’autres valeurs pour la partie locale de l’adresse de messagerie.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Variable</th>
    <th>Valeur</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>Prénom</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>Initiale intermédiaire</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>Nom</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>Nom d’affichage</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Alias Exchange</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>Utilise les <em>x</em> premières lettres du nom. Par exemple, si <em>x</em> = 2, les deux premières lettres du nom sont utilisées.</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>Utilise les <em>x</em> premières lettres du prénom. Par exemple, si <em>x</em> = 2, les deux premières lettres du prénom sont utilisées.</p></td>
    </tr>
    </tbody>
    </table>


  - **Adresse de messagerie non SMTP**. Les types d’adresses de messagerie non SMTP suivants sont pris en charge :
    
      - EX (nom complet du préfixe d’adresse proxy DN héritée)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - Adresse proxy de messagerie unifiée Exchange (adresse proxy EUM)
    
    > [!NOTE]
    > Dans Exchange, toutes les adresses de messagerie non SMTP sont considérées comme des adresses personnalisées. Exchange ne fournit aucune boîte de dialogue ou page de propriétés unique pour les types d’adresses de messagerie X.400, GroupWise ou Lotus Notes. Si vous ajoutez une adresse de messagerie personnalisée non SMTP, vous devez disposer des fichiers bibliothèque de liens dynamiques correspondants. Si vous ne fournissez pas les fichiers DLL appropriés, vous ne pourrez pas créer de stratégie d’adresse de messagerie personnalisée. L’erreur suivante sera enregistrée dans l’Observateur d’événements : « L’objet de description de l’adresse de messagerie dans l’annuaire Microsoft Exchange pour le type d’adresse &quot; SADF &quot; sur les ordinateurs &quot; i386 &quot; est manquant. »


Pour des instructions détaillées sur la création d’une stratégie d’adresse de messagerie, voir les rubriques suivantes :

[Création d'une stratégie d'adresse de messagerie](create-an-email-address-policy-exchange-2013-help.md)

[Créer une stratégie d'adresses de messagerie en utilisant des filtres de destinataires](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

## Que devez-vous savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies d’adresses de messagerie électronique » dans la rubrique [Adresses de messagerie et carnets d’adresses](email-addresses-and-address-books-exchange-2013-help.md).

  - Avant de pouvoir utiliser un domaine d'adresse SMTP dans une stratégie d'adresse de messagerie, vous devez configurer un domaine accepté. Pour plus d'informations, voir [Domaines acceptés](accepted-domains-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!WARNING]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le CAE pour créer une stratégie d'adresse de messagerie

1.  Accédez à **Flux de messagerie** \> **Stratégies d'adresse de messagerie**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans **Stratégie d'adresse de messagerie**, complétez les champs suivants :
    
      - **Nom de la stratégie**
    
      - **Format de l’adresse de messagerie**
    
      - **Spécifiez les types de destinataire auxquels s'appliquera cette adresse de messagerie**

3.  Cliquez sur **Ajouter une règle** pour restreindre davantage les destinataires auxquels cette stratégie s'appliquera. Cela crée l’instruction booléenne **And**.
    
    > [!CAUTION]
    > Si vous appliquez un trop grand nombre de règles, la stratégie d’adresse de messagerie peut être restreinte au point de ne plus contenir d’utilisateurs.


4.  Cliquez sur **Afficher un aperçu des destinataires auxquels la stratégie s'applique** pour visualiser les destinataires auxquels cette stratégie doit s'appliquer.

5.  Cliquez sur **Enregistrer** pour enregistrer vos modifications et créer la stratégie.

6.  Un avertissement apparaît pour vous indiquer que la stratégie d’adresse de messagerie s’appliquera uniquement lorsque vous l’aurez mise à jour. Après sa création, sélectionnez-la puis, dans le volet des détails, cliquez sur **Appliquer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une stratégie d'adresse de messagerie

Cet exemple crée une stratégie d'adresse de messagerie incluant les utilisateurs de boîte aux lettres des bureaux du Sud-Est qui auront des adresses de messagerie comprenant leur nom associé aux deux premières lettres de leur prénom.

    New-EmailAddressPolicy -Name "southeast offices" -IncludedRecipients MailboxUsers -ConditionalStateorProvince "Georgia","Alabama","Louisiana" -EnabledEmailAddressTemplates "SMTP:%s%2g@southeast.contoso.com"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-EmailAddressPolicy](https://technet.microsoft.com/fr-fr/library/aa996800\(v=exchg.150\)).

