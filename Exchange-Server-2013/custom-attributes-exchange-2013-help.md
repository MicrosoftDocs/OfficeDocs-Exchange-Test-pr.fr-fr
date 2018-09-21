---
title: 'Attributs personnalisés: Exchange 2013 Help'
TOCTitle: Attributs personnalisés
ms:assetid: 2b043878-0b34-4563-a9c2-28a9efa7447e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423541(v=EXCHG.150)
ms:contentKeyID: 50477786
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Attributs personnalisés

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-17_

Microsoft Exchange Server 2013 comprend 15 attributs d’extension. Vous pouvez utiliser ces attributs pour ajouter des informations sur un destinataire, comme l’ID d’un employé, l’unité d’organisation, ou autre valeur personnalisée pour laquelle aucun attribut n’existe. Ces attributs personnalisés sont désignés dans Active Directory de **ms-Exch-Extension-Attribute1** à **ms-Exch-Extension-Attribute15**. Dans l’environnement de ligne de commande Exchange Management Shell, les paramètres correspondants sont *CustomAttribute1* à *CustomAttribute15*. Ces attributs ne sont pas utilisés par tous les composants Exchange. Ils peuvent servir au stockage de données Active Directory sans devoir étendre le schéma Active Directory.

Sur Exchange Server 2003 et les versions antérieures, si vous désirez stocker ces informations sur Active Directory, il vous faut créer un attribut en étendant le schéma Active Directory. Une extension de schéma nécessite une planification, la procuration d’identificateurs d’objet pour nouveaux attributs, et le test du processus d’extension dans un environnement de test avant de le mettre en œuvre dans un environnement de production. Dans Exchange 2013, les extensions de schémas ne peuvent être utilisées dans les filtres des destinataires eux-mêmes utilisés par des listes d’adresses, des stratégies d’adresse de messagerie, et des groupes de distribution dynamique.

**Contenu de cette rubrique**

Avantages des attributs personnalisés

Exemples d’attribut personnalisé

Exemple d’attribut personnalisé utilisant le paramètre ConditionalCustomAttributes

Exemple d’attribut personnalisé utilisant le paramètre ExtensionCustomAttributes

## Avantages des attributs personnalisés

Parmi les avantages de l’utilisation d’attributs personnalisés :

  - Vous évitez l’extension du schéma de Active Directory.

  - Les attributs sont créés par la configuration de Exchange.

  - Vous pouvez utiliser le Centre d’administration Exchange (CAE) ou l’environnement de ligne de commande Exchange Management Shell pour gérer les attributs. Il n’est pas nécessaire de créer des contrôles personnalisés ni d’écrire des scripts pour remplir et afficher ces attributs.

  - Les attributs sont des propriétés filtrables utilisables par le paramètre *Filter* avec des cmdlets de destinataires comme **Get-Mailbox**. Ils s’utilisent aussi dans le CAE et l’environnement de ligne de commande Exchange Management Shell pour créer des filtres pour les stratégies d’adresses de messagerie, les listes d’adresses, et les groupes de distribution dynamique.

## Attributs personnalisés à valeurs multiples

Dans Exchange 2010 Service Pack 2 (SP2), cinq attributs personnalisés à valeurs multiples ont été ajoutés à Exchange pour vous permettre de stocker des informations supplémentaires sur les destinataires de messagerie si les attributs personnalisés traditionnels ne répondent plus à vos besoins. Les paramètres *ExtensionCustomAttribute1* à *ExtensionCustomAttribute5* peuvent contenir jusqu’à 1 300 valeurs chacun. Vous pouvez indiquer plusieurs valeurs sous la forme d’une liste délimitée par des virgules. Les cmdlets suivantes prennent en charge ces nouveaux paramètres :

  - [Set-DistributionGroup](https://technet.microsoft.com/fr-fr/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/fr-fr/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/fr-fr/library/aa995950\(v=exchg.150\))

  - [Set-MailPublicFolder](https://technet.microsoft.com/fr-fr/library/bb123707\(v=exchg.150\))

  - [Set-RemoteMailbox](https://technet.microsoft.com/fr-fr/library/ff607302\(v=exchg.150\))

Pour plus d’informations sur les propriétés à valeurs multiples, consultez la rubrique [Modification de propriétés à valeurs multiples](modifying-multivalued-properties-exchange-2013-help.md).

## Exemples d’attribut personnalisé

Dans de nombreux déploiements Exchange, créer une stratégie d’adresses de messagerie pour tous les destinataires d’une unité d’organisation est un scénario courant. L’unité d’organisation est une propriété filtrable pouvant être utilisée dans le paramètre *RecipientFilter* d’une stratégie d’adresses de messagerie ou d’une liste d’adresses.

> [!NOTE]
> Les groupes de distribution dynamique disposent d’un paramètre supplémentaire que vous pouvez utiliser pour les restreindre aux destinataires d’une unité d’organisation particulière ou conteneur.


Si les destinataires de cette unité d’organisation ne partagent aucune propriété commune par laquelle vous pouvez la filtrer, comme un département ou un emplacement, vous pouvez renseigner l’un des attributs personnalisés avec une valeur commune, comme illustré dans l’exemple.

```powershell
Get-Mailbox -OrganizationalUnit Sales | Set-Mailbox CustomAttribute1 "SalesOU"
```

Maintenant, vous pouvez créer une stratégie d’adresse de messagerie pour tous les destinataires ayant la propriété *CustomAttribute1* égale à SalesOU, comme illustré dans l’exemple.

    New-EmailAddressPolicy -Name "Sales" -RecipientFilter { CustomAttribute1 -eq "SalesOU"} -EnabledEmailAddressTemplates "SMTP:%s%2g@sales.contoso.com"

## Exemple d’attribut personnalisé utilisant le paramètre ConditionalCustomAttributes

Quand on crée des groupes de distribution dynamique, des stratégies d’adresses de messagerie, ou des listes d’adresses, le paramètre *RecipeintFilter* n’est pas nécessaire pour spécifier des attributs personnalisés. Vous pouvez utiliser les paramètres *ConditionalCustomAttribute1* à *ConditionalCustomAttribute15* à la place.

Cet exemple crée un groupe de distribution dynamique basé sur les destinataires dont *CustomAttribute1* est défini sur SalesOU.

    New-DynamicDistributionGroup -Name "Sales Users and Contacts" -IncludedRecipients "MailboxUsers,MailContacts" -ConditionalCustomAttribute1 "SalesOU"

> [!NOTE]
> Vous devez utiliser le paramètre <em>IncludedRecipients</em> si vous utilisez un paramètre <em>Conditional</em>. En outre, vous ne pouvez pas utiliser de paramètres <em>Conditional</em> si vous utilisez le paramètre <em>RecipientFilter</em>. Si vous désirez des filtres supplémentaires pour créer votre groupe de distribution dynamique, des stratégies d’adresses de messagerie, ou des listes d’adresses, utilisez le paramètre <em>RecipientFilter</em>.


## Exemple d’attribut personnalisé utilisant le paramètre ExtensionCustomAttributes

Dans cet exemple, le paramètre *ExtensionCustomAttribute1* de la boîte aux lettres de Kweku sera mis à jour pour refléter son inscription aux formations suivantes : MATH307, ECON202 et ENGL300.

```powershell
Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 MATH307,ECON202,ENGL300
```

Ensuite, un groupe de distribution dynamique pour tous les étudiants inscrits à MATH307 est créé à l’aide du paramètre *RecipientFilter* où *ExtensionCustomAttribute1* est égal à MATH307. Lorsque vous utilisez les paramètres *ExtentionCustomAttributes*, vous pouvez utiliser l’opérateur `-eq` au lieu de l’opérateur `-like`.

    New-DynamicDistributionGroup -Name Students_MATH307 -RecipientFilter {ExtensionCustomAttribute1 -eq "MATH307"}

Dans cet exemple, les valeurs *ExtensionCustomAttribute1* de Kweku sont mises à jour pour refléter son ajout de la formation ENGL210 et son retrait de la formation ECON202.

```powershell
Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 @{Add="ENGL210"; Remove="ECON202"}
```

