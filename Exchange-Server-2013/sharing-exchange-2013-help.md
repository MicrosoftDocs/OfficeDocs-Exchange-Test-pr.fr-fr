---
title: 'Partage: Exchange 2013 Help'
TOCTitle: Partage
ms:assetid: 09e6732a-4e99-44d0-801d-9463fdc57a9b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638083(v=EXCHG.150)
ms:contentKeyID: 50477522
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Partage

 

_**Sapplique à :** Exchange Server 2013, Outlook 2013_

_**Dernière rubrique modifiée :** 2015-02-27_

Pour pouvoir collaborer avec des personnes de différentes organisations ou avec des amis et des membres de votre famille sur des projets ou planifier des événements sociaux ensemble, vous devrez peut-être coordonner vos calendriers. Avec Exchange 2013, les administrateurs peuvent configurer différents niveaux d’accès au calendrier pour permettre aux entreprises de collaborer avec d’autres entreprises et aux utilisateurs de partager leurs calendriers avec d’autres personnes. La configuration du partage de calendriers entre entreprises (B2B) passe par la création de *relations des organisations*. La configuration du partage de calendriers entre utilisateurs passe par l’application de *stratégies de partage*.

> [!NOTE]
> Cette fonctionnalité d’Exchange Server 2013 n’est pas entièrement compatible avec les systèmes Office 365 exécutés par 21Vianet en Chine et certaines limitations de fonctionnalités peuvent s’appliquer. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/?linkid=313640">En savoir plus sur Office 365 exécuté par 21Vianet</a>.


**Contenu de cette rubrique**

Scénarios de partage dans Exchange 2013

Limites du partage de disponibilité

Considérations de pare-feu pour le partage fédéré

Coexistence avec Exchange 2010

Coexistence avec Exchange 2007

Partage de documents

## Scénarios de partage dans Exchange 2013

Les scénarios de partage suivants sont pris en charge dans Exchange 2013 :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Objectif de partage</th>
<th>Paramètre à utiliser</th>
<th>Conditions requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Partage de calendriers avec une organisation Office 365</p></td>
<td><p>Relations des organisations</p></td>
<td><p>L’organisation Office 365 est prête pour la configuration. L’administrateur Exchange sur site doit configurer une relation d’authentification avec le nuage (également appelée « fédération ») et doit répondre à la configuration logicielle requise minimale. Pour en savoir plus sur la configuration de la fédération, consultez l’article <a href="federation-exchange-2013-help.md">Fédération</a>.</p></td>
</tr>
<tr class="even">
<td><p>Partage de calendriers avec une autre organisation Exchange sur site</p></td>
<td><p>Relations des organisations</p></td>
<td><p>Les deux organisations Exchange sur site doivent configurer la fédération et répondre à la configuration logicielle requise minimale</p></td>
</tr>
<tr class="odd">
<td><p>Partage du calendrier d’un utilisateur Exchange avec un utilisateur Internet</p></td>
<td><p>Stratégies de partage</p></td>
<td><p>Aucune, prêt pour la configuration</p></td>
</tr>
<tr class="even">
<td><p>Partage du calendrier d’un utilisateur Exchange avec un autre utilisateur Exchange sur site</p></td>
<td><p>Stratégies de partage</p></td>
<td><p>Les deux organisations Exchange sur site doivent configurer la fédération et répondre à la configuration logicielle requise minimale.</p></td>
</tr>
</tbody>
</table>


Le tableau suivant décrit les différences entre les relations d’organisation et les stratégies de partage.

### Relations d’organisation et stratégies de partage

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Relation organisationnelle</th>
<th>Stratégie de partage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nécessite une approbation de fédération pour votre organisation</p></td>
<td><p>Oui</p></td>
<td><p>Oui, lors du partage avec d’autres organisations à domaine fédéré. Non requis pour les stratégies de partage Internet.</p></td>
</tr>
<tr class="even">
<td><p>Recommande que le domaine externe soit fédéré</p></td>
<td><p>Oui</p></td>
<td><p>Oui, lors du partage avec d’autres organisations à domaine fédéré. Non requis pour les stratégies de partage Internet.</p></td>
</tr>
<tr class="odd">
<td><p>Autorise le partage des informations de disponibilité (y compris l’objet et l’emplacement) avec des organisations externes pour un grand nombre d’utilisateurs.</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Autorise le partage des dossiers de calendrier avec les informations de disponibilité</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Autorise le partage des dossiers de calendrier avec les informations de disponibilité, y compris l’objet et le corps</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Les utilisateurs doivent envoyer une invitation de partage aux destinataires externes</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Fournit une méthode d’accès</p></td>
<td><p>Votre serveur d’accès au client interne accède au serveur d’accès au client de l’organisation externe et extrait les informations de disponibilité pour l’utilisateur externe, lorsque cela est nécessaire.</p></td>
<td><p>Votre serveur d’accès au client accède au serveur d’accès au client de l’organisation externe et s’abonne au dossier de calendrier de l’utilisateur externe. Pour les stratégies de partage Internet, les utilisateurs externes accèdent à une URL restreinte ou publique sur le serveur d’accès au client.</p></td>
</tr>
<tr class="even">
<td><p>Peut être appliqué à tous les domaines externes</p></td>
<td><p>Non (une relation un-à-un entre deux organisations Exchange 2013)</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Permet aux utilisateurs d’échanger des types de données différents avec des destinataires externes</p></td>
<td><p>Non</p></td>
<td><p>Oui, en fonction de la stratégie de partage qui est appliquée</p></td>
</tr>
<tr class="even">
<td><p>Désactive le partage pour certains utilisateurs</p></td>
<td><p>Oui, en spécifiant un groupe de distribution de sécurité pour la relation organisationnelle</p></td>
<td><p>Oui, en désactivant la stratégie de partage appliquée</p></td>
</tr>
<tr class="odd">
<td><p>Nécessite que la boîte aux lettres réside sur un serveur de boîtes aux lettres Exchange 2013</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


Retour au début

## Limites du partage de disponibilité

Les limites suivantes s’appliquent lors du partage d’informations de disponibilité entre des organisations Exchange :

1.  **Outlook Web Access 2003**   Lorsqu’un utilisateur d’une organisation Exchange 2003 utilise Outlook Web Access pour accéder à la disponibilité des utilisateurs d’une organisation Exchange 2013 distante, la requête échoue. Les connexions à Outlook Web Access à partir d’Exchange 2003 ne peuvent pas établir de connexions WebDAV (Web-based Distributed Authoring and Versioning) à un dossier système de disponibilité pour récupérer les informations de disponibilité d’utilisateurs distants. Étant donné qu’Exchange 2013 ne prend pas en charge les connexions WebDAV, le serveur Exchange 2003 ne peut pas se connecter à Externe (FYDIBOHF25SPDLT) sur le serveur CAS Exchange 2013 pour traiter des requêtes Outlook Web Access. Les clients Outlook ne sont pas affectés par ce problème, car ils utilisent MAPI au lieu de WebDAV lorsqu’ils se connectent à Externe (FYDIBOHF25SPDLT).

2.  **Latence du réseau étendu (WAN)**   Dans les organisations Exchange 2003, les réplicas de tous les dossiers de disponibilité doivent résider sur des serveurs de boîte aux lettres Exchange 2010 SP2 ou de version supérieure. Dans les environnements où des bases de données de dossiers publics Exchange 2003 figurent sur plusieurs sites physiques, des problèmes de latence excessive et de performance peuvent survenir si des requêtes de disponibilité internes doivent traverser des liens WAN pour accéder à des bases de données de dossiers publics Exchange 2010 ne se trouvant pas sur le même site physique.

3.  **Période d’informations de disponibilité**   Les requêtes d’informations de disponibilité adressées à une organisation Exchange 2007 par une organisation Exchange 2013 peuvent échouer en raison d’une incohérence de la période des informations de disponibilité requises. Par défaut, Exchange 2007 accepte des requêtes de disponibilité pour 42 jours d’informations de disponibilité et Exchange 2013 peut demander 62 jours d’informations de disponibilité. Si la demande dépasse la limite par défaut de 42 imposée par Exchange 2007, la requête échouera.
    
    Suivez la procédure ci-dessous pour configurer vos serveurs CAS Exchange 2007 afin qu’ils acceptent des requêtes d’informations de disponibilité pour de plus longues périodes :
    
    1.  Sur tous vos serveurs CAS Exchange 2007, ouvrez le fichier suivant avec un éditeur de texte, par exemple le Bloc-notes : \<Chemin d’installation Exchange\>\\V14\\ClientAccess\\ExchWeb\\EWS\\web.config
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Avant d’apporter des modifications au fichier web.config, créez une copie du fichier et placez-la en lieu sûr.</td>
        </tr>
        </tbody>
        </table>
    
    2.  Recherchez la section **appSettings** dans le fichier web.config.
    
    3.  Ajoutez une nouvelle clé « \<add key="maximumQueryIntervalDays" value="62" /\> » et enregistrez le fichier web.config.
        
        > [!NOTE]
        > La valeur de maximumQueryIntervalDays n’est pas présente par défaut. Lorsque cette valeur n’est pas spécifiée, Exchange 2007 utilise l’intervalle par défaut de 42 jours.
    
    4.  Arrêtez et redémarrez Microsoft Internet Information Services (IIS) sur tous les serveurs CAS Exchange 2007.

4.  **Organisations Exchange avec des utilisateurs locaux et en nuage**   Si vous configurez le partage de calendriers avec une autre organisation Exchange configurée dans un déploiement hybride avec Microsoft Office 365, les recherches de disponibilité pour les utilisateurs d’Office 365 ou pour les utilisateurs distants ayant été transférés vers le nuage échoueront. Étant donné que la relation organisationnelle pour votre organisation Exchange est établie avec l’organisation Exchange distante locale et pas avec l’organisation Exchange Online utilisant Office 365, la requête de disponibilité ne peut pas s’adresser aux utilisateurs d’Office 365. Exchange 2013 ne prend pas en charge la fonctionnalité de redirection via proxy de ces requêtes de disponibilité vers le service Office 365 en passant par l’organisation locale.

Pour plus d’informations sur la configuration du partage de disponibilité entre déploiements Exchange courants, consultez la rubrique [Configuration du partage fédéré entre des organisations Exchange](configuring-federated-sharing-between-exchange-organizations-exchange-2013-help.md).

## Considérations de pare-feu pour le partage fédéré

Les fonctions de partage fédéré exigent que les serveurs d’accès au client dans votre organisation aient un accès sortant à Internet à l’aide d’HTTPS. Vous devez autoriser un accès HTTPS sortant (port 443 pour TCP) à tous les serveurs de boîtes aux lettres Exchange 2013 de l’organisation.

Pour qu’une organisation externe ait accès aux informations de disponibilité de votre organisation, vous devez publier au moins un serveur d’accès au client sur Internet. Un accès HTTPS entrant depuis Internet vers le serveur d’accès au client est nécessaire. Les serveurs d’accès au client dans les sites Active Directory n’ayant pas de serveur d’accès au client publié sur Internet peuvent utiliser les serveurs d’accès au client dans d’autres sites Active Directory accessibles depuis Internet. Les serveurs d’accès au client qui ne sont pas publiés sur Internet doivent avoir l’URL externe du répertoire virtuel des services Web définie avec l’URL accessible aux organisations externes.

Retour au début

## Coexistence avec Exchange 2010

Dans les organisations comprenant des serveurs Exchange 2010 et Exchange 2013, les utilisateurs qui possèdent une boîte aux lettres sur un serveur de boîtes aux lettres Exchange 2010 peuvent utiliser des relations organisationnelles pour échanger leurs informations de disponibilité avec les destinataires d’organisations à domaine fédéré Exchange 2013 externes. Les serveurs de boîtes aux lettres et d’accès au client Exchange 2010 doivent exécuter SP2 ou une version supérieure, et vous devez disposer d’au moins un serveur d’accès au client Exchange 2013 dans l’organisation Exchange 2010.

## Coexistence avec Exchange 2007

Dans les organisations comprenant des serveurs Exchange 2013 et Exchange 2007, les utilisateurs qui possèdent une boîte aux lettres sur un serveur de boîtes aux lettres Exchange 2007 peuvent utiliser des relations organisationnelles pour échanger leurs informations de disponibilité avec les destinataires d’organisations à domaine fédéré externes. Le serveur de boîtes aux lettres doit exécuter Exchange 2007 SP2 ou une version supérieure. Par ailleurs, vous devez disposer d’au moins un serveur d’accès au client Exchange 2013 dans l’organisation Exchange. Vous pouvez utiliser les relations organisationnelles en introduisant un seul serveur d’accès au client Exchange 2013 dans l’organisation, offrant ainsi une solution plus robuste que les solutions qui synchronisent les informations de disponibilité et requièrent une synchronisation de la liste d’adresses globale.

Lors de l’utilisation d’Outlook 2010 ou d’Outlook Web App pour planifier une réunion sur un serveur Exchange 2007, un utilisateur dont la boîte aux lettres réside sur un serveur Exchange 2007 peut consulter les informations de disponibilité d’un utilisateur de l’organisation externe. Les informations de disponibilité des boîtes aux lettres Exchange 2007 sont accessibles aux destinataires de l’organisation externe.

Les stratégies de partage sont attribuées aux utilisateurs de boîtes aux lettres Exchange 2013. Pour utiliser les stratégies de partage, une boîte aux lettres doit être située sur un serveur de boîtes aux lettres Exchange 2013. Seuls les clients Outlook 2010 et Outlook Web App peuvent être utilisés pour générer ou répondre à des invitations de partage.

Retour au début

## Partage de documents

Le tableau suivant contient des liens vers des rubriques qui vous aideront à découvrir et à gérer le partage dans Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rubrique</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="federation-exchange-2013-help.md">Fédération</a></p></td>
<td><p>Apprenez-en davantage sur l’infrastructure d’approbation sous-jacente qui prend en charge le partage ; un moyen facile pour les utilisateurs de partager des informations de calendrier avec des destinataires externes.</p></td>
</tr>
<tr class="even">
<td><p><a href="organization-relationships-exchange-2013-help.md">Relations des organisations</a></p></td>
<td><p>Apprenez-en davantage sur les relations un-à-un entre les organisations Exchange qui permettent le partage des disponibilités de calendrier.</p></td>
</tr>
<tr class="odd">
<td><p><a href="sharing-policies-exchange-2013-help.md">Stratégies de partage</a></p></td>
<td><p>Apprenez-en davantage sur les stratégies de personne à personne qui activent le partage.</p>
<p></p></td>
</tr>
</tbody>
</table>

