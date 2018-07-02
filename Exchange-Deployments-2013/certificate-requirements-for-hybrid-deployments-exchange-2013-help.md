---
title: 'Conditions requises pour les certificats dans le cadre de déploiements hybrides: Exchange 2013 Help'
TOCTitle: Conditions requises pour les certificats dans le cadre de déploiements hybrides
ms:assetid: 48d532cc-29f9-4009-9d2d-f19a9c13c320
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh563848(v=EXCHG.150)
ms:contentKeyID: 50479667
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conditions requises pour les certificats dans le cadre de déploiements hybrides

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2016-12-09_

Dans un déploiement hybride, les certificats numériques représentent une part importante de la sécurisation des communications entre l’organisation Exchange locale et Office 365. Les certificats permettent à chaque organisation Exchange d’approuver l’identité de l’autre. Les certificats permettent également d’assurer que chaque organisation Exchange communique vers la bonne source.

Dans un déploiement hybride, de nombreux services utilisent des certificats :

  - **Azure Active Directory Connect (Azure AD Connect) avec les services de fédération Active Directory (AD FS)**   Si vous décidez de déployer Azure AD Connect avec les services AD FS dans le cadre de votre déploiement hybride, un certificat émis par une autorité de certification tierce approuvée est utilisé pour établir une approbation entre les clients web et les serveurs proxy de fédération, pour signer et déchiffrer les jetons de sécurité.
    
    Pour plus d'informations, consultez la rubrique [Certificats](http://go.microsoft.com/fwlink/p/?linkid=205993).

  - **Exchange Federation**   Un certificat auto-signé est utilisé pour créer une connexion sécurisée entre les serveurs Exchange locaux et le système d'authentification Azure Active Directory.
    
    Pour plus d'informations, consultez la rubrique [Partage](https://technet.microsoft.com/fr-fr/library/dd638083\(v=exchg.150\)).

  - **Services Exchange**   Des certificats émis par une autorité de certification tierce approuvée permettent de sécuriser la communication SSL (Secure Sockets Layer) entre les clients et les serveurs Exchange. Les services qui utilisent des certificats comprennent Outlook sur le web, Exchange ActiveSync, Outlook Anywhere et le transport des messages sécurisé.

  - **Serveurs Exchange existants**   Vos serveurs Exchange existants peuvent utiliser des certificats pour sécuriser les communications Outlook sur le web, le transport des messages, etc. En fonction de votre utilisation des certificats sur vos serveurs Exchange, vous pouvez être amené à utiliser des certificats auto-signés ou des certificats émis par une autorité de certification tierce approuvée.

## Conditions requises pour l'utilisation d'un certificat dans le cadre d'un déploiement hybride

Dans le cadre de la configuration d’un déploiement hybride, vous devez utiliser et configurer des certificats que vous avez achetés auprès d’une autorité de certification tierce approuvée. Le certificat utilisé pour un transport de courrier sécurisé hybride doit être installé sur l’ensemble des boîtes aux lettres (Exchange 2016 et versions plus récentes) et des serveurs d’accès au client et de boîtes aux lettres (Exchange 2013 et versions antérieures) locaux.

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous configurez un déploiement hybride dans une organisation dont les serveurs Exchange sont déployés dans plusieurs forêts Active Directory, vous devez utiliser un certificat émis par une autorité de certification tierce distincte pour <em>chaque</em> forêt Active Directory.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque des serveurs de transport Edge Exchange sont déployés dans une organisation locale, ce certificat doit également être installé sur tous les serveurs de transport Edge. Chaque serveur de transport doit utiliser un certificat qui partage la même autorité de certification tierce émettrice et le même objet pour que le transport de courrier sécurisé hybride fonctionne correctement.</td>
</tr>
</tbody>
</table>


De nombreux services, tels que AD FS, Exchange Federation, les services et Exchange, requièrent des certificats. En fonction de la nature de votre organisation, vous pouvez choisir l'une des options suivantes :

  - Utiliser un certificat tiers employé par tous les services sur plusieurs serveurs.

  - Utiliser un certificat tiers pour chaque serveur fournissant des services.

Selon votre organisation et le service que vous mettez en œuvre, vous pouvez choisir d'utiliser un même certificat pour tous les services ou un certificat dédié à chaque service. Voici quelques éléments à prendre en compte pour chacune des options :

  - **Certificat tiers sur plusieurs serveurs**   Les certificats tiers utilisés par des services sur plusieurs serveurs peuvent constituer une solution légèrement moins onéreuse, mais risquent d'impliquer des opérations complexes de renouvellement et de remplacement. En effet, lorsqu'un certificat doit être remplacé, vous devez réaliser cette opération sur chaque serveur où il est installé.

  - **Certificat tiers pour chaque serveur**   L'utilisation d'un certificat dédié pour chaque serveur hébergeant des services vous permet de configurer le certificat spécifiquement pour les services qui s'y trouvent. Si vous devez remplacer le certificat ou le renouveler, vous devez seulement le remplacer sur le serveur où les services sont installés. Il n'y a aucune incidence sur les autres serveurs.

Nous vous recommandons d’utiliser un certificat tiers dédié pour un serveur AD FS en option, un autre certificat pour les services Exchange pour votre déploiement hybride et, le cas échéant, un autre certificat sur vos serveurs Exchange pour d’autres services ou fonctionnalités nécessaires. L’approbation de fédération locale configurée dans le cadre d’un partage fédéré dans un déploiement hybride utilise un certificat auto-signé par défaut. Sauf exigences spécifiques, il est inutile d’utiliser un certificat tiers avec l’approbation fédérée configurée dans le cadre d’un déploiement hybride.

Les services installés sur un seul serveur peuvent vous obliger à configurer plusieurs noms de domaines complets (FQDN) pour le serveur. Vous devez acheter un certificat permettant le nombre maximum requis de noms de domaines complets. Les certificats comprennent le nom de l’objet (également appelé nom principal), et un ou plusieurs autre(s) nom(s) d’objet. Le nom de l’objet correspond au nom de domaine complet pour lequel le certificat est émis, et doit utiliser le domaine SMTP principal partagé entre l’organisation locale et l’organisation Exchange Online. Les autres noms d’objet sont des noms de domaines complets supplémentaires pouvant être ajoutés à un certificat en plus du nom de l’objet. Si vous avez besoin d’un certificat pour prendre en charge cinq noms de domaines complets, achetez un certificat permettant d’ajouter cinq domaines : un nom d’objet et quatre autres noms d’objet.

Le tableau suivant indique le nombre minimum de noms de domaines complets suggérés devant être inclus sur des certificats configurés pour être utilisés dans un déploiement hybride.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Service</th>
<th>Nom de domaine complet suggéré</th>
<th>Champ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Domaine SMTP principal partagé</p></td>
<td><p>contoso.com</p></td>
<td><p>Nom de sujet</p></td>
</tr>
<tr class="even">
<td><p>Découverte automatique</p></td>
<td><p>Étiquette correspondant au nom de domaine complet de découverte automatique externe de votre serveur d'accès au client Exchange 2013, tel que autodiscover.contoso.com</p></td>
<td><p>Autre nom du sujet</p></td>
</tr>
<tr class="odd">
<td><p>Transport</p></td>
<td><p>Étiquette correspondant au nom de domaine complet externe de vos serveurs de transport Edge, tel que edge.contoso.com</p></td>
<td><p>Autre nom du sujet</p></td>
</tr>
</tbody>
</table>

