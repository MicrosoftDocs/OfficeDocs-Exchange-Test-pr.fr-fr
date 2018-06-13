---
title: 'Configuration requise pour un déploiement hybride: Exchange 2013 Help'
TOCTitle: Configuration requise pour un déploiement hybride
ms:assetid: e7454db0-fed4-4662-8890-9501126b1ba2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh534377(v=EXCHG.150)
ms:contentKeyID: 50479679
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration requise pour un déploiement hybride

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2017-07-25_

**Résumé** : Préparation de votre environnement Exchange pour pouvoir configurer un déploiement hybride.

Avant de créer et de configurer un déploiement hybride à l’aide de l’Assistant Configuration hybride, vous devez vous assurer que votre organisation Exchange locale remplit certaines conditions préalables. Dans le cas contraire, vous ne pourrez ni exécuter la procédure de l’Assistant Configuration hybride, ni configurer un déploiement hybride entre votre organisation Exchange locale et Exchange Online.

## Conditions préalables à un déploiement hybride

Les conditions préalables suivantes doivent être réunies pour la configuration d'un déploiement hybride :

  - **Organisation Exchange locale**   Des déploiements hybrides peuvent être configurés pour des organisations Exchange 2007 locales ou de version ultérieure.
    
    La version d’Exchange que vous avez installée dans votre organisation locale détermine la version de déploiement hybride que vous pouvez installer. Vous devez généralement configurer la version de déploiement hybride la plus récente prise en charge par votre organisation. Par exemple, si votre organisation locale exécute Exchange 2007, vous devez configurer un déploiement hybride Exchange 2013. Consultez le tableau suivant pour obtenir une liste complète de la compatibilité du déploiement hybride Exchange Server et Office 365 pour entreprises.
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Environnement local</th>
    <th>Déploiement hybride d’Exchange 2016</th>
    <th>déploiement hybride d’Exchange 2013</th>
    <th>déploiement hybride d'Exchange 2010</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Exchange 2016</p></td>
    <td><p>Pris en charge</p></td>
    <td><p>Non pris en charge</p></td>
    <td><p>Non pris en charge</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2013</p></td>
    <td><p>Pris en charge</p></td>
    <td><p>Pris en charge</p></td>
    <td><p>Non pris en charge</p></td>
    </tr>
    <tr class="odd">
    <td><p>Exchange 2010</p></td>
    <td><p>Pris en charge</p></td>
    <td><p>Pris en charge</p></td>
    <td><p>Pris en charge</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2007</p></td>
    <td><p>Non pris en charge</p></td>
    <td><p>Pris en charge</p></td>
    <td><p>Pris en charge</p></td>
    </tr>
    </tbody>
    </table>


  - **Versions Exchange locales** Les déploiements hybrides nécessitent la dernière mise à jour cumulative ou le dernier correctif cumulatif disponible pour la version d’Exchange que vous avez installée dans votre organisation locale. Si vous ne pouvez pas installer la dernière mise à jour cumulative ou le dernier correctif cumulatif, la version antérieure la plus récente est également prise en charge. Les mises à jour cumulatives ou les correctifs cumulatifs antérieurs ne sont pas pris en charge.
    
    Par exemple, supposons que vous avez installé la mise à jour cumulative 8 d’Exchange 2013 dans votre organisation locale et que la dernière version disponible d’Exchange 2013 est la mise à jour cumulative 10. Pour rester dans une configuration hybride prise en charge, vous devez mettre à niveau vos serveurs Exchange 2013 vers la mise à jour cumulative 9 au minimum. Toutefois, nous vous recommandons fortement de les mettre à niveau vers la mise à jour cumulative 10.
    
    Les mises à jour cumulatives et les correctifs cumulatifs sont publiés chaque trimestre. Par conséquent, le fait de doter vos serveurs de la dernière mise à jour cumulative ou du dernier correctif cumulatif vous offre davantage de flexibilité si vous avez régulièrement besoin de davantage de temps pour effectuer des mises à niveau.

  - **Rôles serveur local** Les rôles serveur que vous devez installer dans votre organisation locale dépendent de la version d’Exchange que vous avez installée.
    
      - **Exchange 2010** Au moins un serveur sur lequel les rôles de serveur de boîte aux lettres, de transport Hub et d’accès au client sont installés. Alors qu’il est possible d’installer les rôles de boîte aux lettres, de transport Hub et d’accès au client sur des serveurs séparés, nous vous recommandons vivement d’installer tous les rôles sur chaque serveur pour accroître la fiabilité et améliorer les performances.
    
      - **Exchange 2013** Au moins un serveur sur lequel les rôles de serveur de boîte aux lettres et d’accès au client sont installés. Alors qu’il est possible d’installer les rôles de boîte aux lettres et d’accès au client sur des serveurs séparés, nous vous recommandons vivement d’installer ces deux rôles sur chaque serveur pour accroître la fiabilité et améliorer les performances.
    
      - **Exchange 2016 et versions ultérieures** Au moins un serveur sur lequel le rôle serveur de boîte aux lettres est installé.
    
    Les déploiements hybrides prennent également en charge les serveurs Exchange exécutant le rôle serveur de transport Edge. Les serveurs de transport Edge doivent aussi être mis à jour vers la dernière mise à jour cumulative ou le dernier correctif cumulatif disponible pour la version d’Exchange que vous avez installée. Nous vous recommandons vivement de déployer les serveurs de transport Edge dans un réseau de périmètre. Les serveurs de boîte aux lettres et d’accès au client ne peuvent pas être déployés dans un réseau de périmètre.

  - **Office 365**   Les déploiements hybrides sont pris en charge dans tous les plans Office 365 prenant en charge Synchronisation Azure Active Directory. Tous les plans Office 365 Entreprise, Secteur Public, Éducation et Moyenne Entreprise prennent en charge les déploiements hybrides. Les plans Office 365 Business et Famille ne prennent pas en charge les déploiements hybrides.
    
    Pour plus d’informations, consultez la page relative à l’[inscription à Office 365](https://go.microsoft.com/fwlink/p/?linkid=203981).

  - **Domaines personnalisés**   Enregistrez n'importe quel domaine personnalisé que vous souhaitez utiliser dans votre déploiement hybride avec Office 365. Cela est possible à l'aide du Portail d'administration Office 365 ou bien en configurant les services de fédération (AD FS) Active Directory dans votre organisation locale.
    
    Pour plus d’informations, consultez la rubrique [Ajouter un domaine et des utilisateurs à Office 365](https://go.microsoft.com/fwlink/p/?linkid=229238).

  - **Synchronisation Active Directory**   Déployez l’outil Azure Active Directory Connect pour activer la synchronisation Active Directory avec votre organisation locale.
    
    Pour en savoir plus, voir [Options d’authentification de l’utilisateur via Azure AD Connect](http://go.microsoft.com/fwlink/p/?linkid=723514)

  - **Enregistrements de découverte automatique DNS**   Configurez les enregistrements publics de découverte automatique DNS pour vos domaines SMTP existants afin qu'ils désignent un serveur d'accès au client Exchange 2013 local.

  - **Organisation Office 365 dans le Centre d’administration Exchange (CAE)**   Le nœud de l’organisation Office 365 est intégré par défaut au CAE local, mais vous devez connecter le CAE à votre organisation Office 365 à l’aide de vos informations d’identification d’administrateur Office 365 avant de pouvoir utiliser l’assistant de configuration hybride. Ceci vous permettra de gérer à la fois l’organisation locale et l’organisation Exchange Online depuis une console de gestion unique.
    
    Pour plus d'informations, consultez la rubrique [Gestion hybride dans les déploiements hybrides Exchange](hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md).

  - 
    
    **Certificats**   Installez et affectez des services Exchange à un certificat numérique valide acquis auprès d’une autorité de certification publique approuvée. Même s’il est possible de les utiliser pour l’approbation de fédération locale avec le service Microsoft Federation Gateway, les certificats auto-signés ne peuvent pas servir dans le cadre de services Exchange lors d’un déploiement hybride. L’instance IIS (Internet Information Services) sur les serveurs Exchange configurés dans le déploiement hybride doit disposer d’un certificat numérique valide acquis auprès d’une autorité de certification approuvée. De plus, l’URL externe d’EWS et le point de terminaison du service de découverte automatique spécifié sur votre serveur DNS public doivent être enregistrés dans l’autre nom d’objet du certificat. Le certificat installé sur les serveurs Exchange utilisés pour le transport de messagerie dans le déploiement hybride doit être identique (à savoir, émis par la même autorité de certification approuvée et avec le même objet).
    
    Pour plus d'informations, consultez la rubrique [Conditions requises pour les certificats dans le cadre de déploiements hybrides](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md).

  - **EdgeSync**   Si vous avez déployé des serveurs de transport Edge dans votre organisation locale et que vous souhaitez configurer les serveurs de transport Edge pour le transport de messagerie sécurisée hybride, vous devez configurer EdgeSync avant d’utiliser l’assistant de configuration hybride. Vous devez également exécuter EdgeSync chaque fois que vous appliquez une nouvelle mise à jour cumulative ou un correctif cumulatif à un serveur de transport Edge.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Bien qu'EdgeSync soit une condition préalable aux déploiements avec des serveurs de transport Edge, d'autres paramètres de configuration de transport manuel seront requis lors de la configuration de serveurs de transport Edge pour le transport de messagerie sécurisée hybride.</td>
    </tr>
    </tbody>
    </table>
    
    Pour plus d'informations, consultez la rubrique [Serveurs de transport Edge avec déploiements hybrides](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md).

  - **Boîtes aux lettres de messagerie unifiée** Si vous avez des boîtes aux lettres de messagerie unifiée et que vous souhaitez les déplacer vers Office 365, vous devez disposer des éléments suivants en plus d’un déploiement Exchange hybride. Ces conditions sont requises **avant** de déplacer des boîtes aux lettres de messagerie unifiée vers Office 365.
    
      - Lync Server 2010, Lync Server 2013 ou Skype Entreprise Server 2015 ou version ultérieure intégré à votre système de téléphonie local **ou**
    
      - Skype Entreprise Online intégré à votre système de téléphonie local **ou**
    
      - Une solution PBX ou IP-PBX locale classique.
    
      - Stratégies de boîte aux lettres de messagerie unifiée créées dans Exchange Online qui reflètent les noms des stratégies de boîte aux lettres de messagerie unifiée dans votre organisation locale.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Vous pouvez mapper plusieurs stratégies de boîte aux lettres de messagerie unifiée locale avec une stratégie de boîte aux lettres de messagerie unifiée dans Exchange Online. Si vous souhaitez effectuer cette action, vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour mapper manuellement chaque stratégie de boîte aux lettres de messagerie unifiée locale sur une stratégie Exchange Online.</td>
        </tr>
        </tbody>
        </table>
    
    Pour plus d’informations, consultez [Intégration des systèmes téléphoniques à la messagerie unifiée](https://technet.microsoft.com/fr-fr/library/jj673558\(v=exchg.150\)), [Gestionnaire de téléphonie pour Exchange 2013](https://technet.microsoft.com/fr-fr/library/ee364753\(v=exchg.150\)) et [Configuration de la messagerie vocale PBX cloud - Aide pour l’administrateur](https://go.microsoft.com/fwlink/p/?linkid=826207).

## Ports, points de terminaison et protocoles de déploiement hybride

Pour fonctionner correctement, les composants et les fonctionnalités de déploiement hybride requièrent qu’Office 365 puisse accéder à certains ports, points de terminaison de connexion et protocoles entrants. Avant de configurer votre déploiement hybride, vérifiez que votre réseau local et votre configuration de sécurité prennent en charge les fonctionnalités et les composants du tableau ci-dessous. En plus d’autoriser les protocoles entrants spécifiques, les ports et les points de terminaison, les ordinateurs de votre réseau doivent également pouvoir accéder aux adresses IP, aux ports et aux URL répertoriés dans [URL et plages d’adresses IP Office 365](https://go.microsoft.com/fwlink/?linkid=823100).


<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocole de transport</th>
<th>Protocole du niveau supérieur</th>
<th>Fonctionnalité/composant</th>
<th>Point de terminaison local</th>
<th>Chemin local</th>
<th>Fournisseur d’authentification</th>
<th>Méthode d’autorisation</th>
<th>Authentification préalable prise en charge ?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP 25 (SMTP)</p></td>
<td><p>SMTP/TLS</p></td>
<td><p>Flux de messagerie entre Office 365 et l’installation locale</p></td>
<td><p>Boîte aux lettres Exchange 2016/Edge</p>
<p>Serveur CAS/EDGE Exchange 2013</p>
<p>Serveur HUB/EDGE Exchange 2010</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>Basée sur les certificats</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>Découverte automatique</p></td>
<td><p>Découverte automatique</p></td>
<td><p>Boîte aux lettres Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Système d’authentification Azure AD</p></td>
<td><p>Authentification WS-Security</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Disponibilité, infos-courrier, suivi des messages</p></td>
<td><p>Boîte aux lettres Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p></td>
<td><p>Système d’authentification Azure AD</p></td>
<td><p>Authentification WS-Security</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Recherche dans plusieurs boîtes aux lettres</p></td>
<td><p>Boîte aux lettres Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Serveur d’authentification</p></td>
<td><p>Authentification WS-Security</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Migrations de boîtes aux lettres</p></td>
<td><p>Boîte aux lettres Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/mrsproxy.svc</p></td>
<td><p>NTLM</p></td>
<td><p>Basique</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>Découverte automatique</p>
<p>EWS</p></td>
<td><p>OAuth</p></td>
<td><p>Boîte aux lettres Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Serveur d’authentification</p></td>
<td><p>Authentification WS-Security</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>N/A</p></td>
<td><p>AD FS (inclus avec Windows)</p></td>
<td><p>Windows 2008/2012 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Système d’authentification Azure AD</p></td>
<td><p>Varie en fonction de la configuration</p></td>
<td><p>2 facteurs</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>N/A</p></td>
<td><p>Azure Active Directory Connect avec AD FS</p></td>
<td><p>Windows 2012 R2 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Système d’authentification Azure AD</p></td>
<td><p>Varie en fonction de la configuration</p></td>
<td><p>2 facteurs</p></td>
</tr>
</tbody>
</table>


## Outils et services recommandés

Outre les conditions préalables décrites plus haut, d’autres outils et services peuvent être utiles lorsque vous configurez des déploiements hybrides à l’aide de l’assistant Configuration hybride :

  - **Assistant Déploiement d’Exchange Server**   L’Assistant Déploiement d’Exchange Server est un outil web gratuit qui vous aide à déployer Exchange dans votre organisation locale, à configurer un déploiement hybride entre votre organisation locale et Office 365 ou à effectuer une migration complète vers Office 365. L’outil vous pose une brève série de questions, puis, en fonction de vos réponses, crée une liste personnalisée contenant des instructions pour déployer ou configurer Exchange Server. L’Assistant Déploiement vous donne exactement les informations dont vous avez besoin pour configurer votre déploiement hybride.
    
    Découvrez l’[Assistant de déploiement Exchange Server](https://technet.microsoft.com/exdeploy2013).
    
     

  - **Outil Analyseur de connectivité à distance**   L’outil Analyseur de connectivité à distance de Microsoft vérifie la connectivité externe de votre organisation Exchange locale et s’assure que vous êtes prêt à configurer votre déploiement hybride. Nous vous recommandons vivement de vérifier votre organisation locale à l'aide de l'outil Analyseur de connectivité à distance avant de configurer votre déploiement hybride via l'Assistant Configuration hybride.
    
    Pour plus d’informations, consultez la rubrique [Analyseur de connectivité à distance Microsoft](http://go.microsoft.com/fwlink/p/?linkid=167905)
    
     

  - **Authentification unique**   L’authentification unique permet aux utilisateurs d’accéder à la fois aux organisations locales et Exchange Online à l’aide d’un nom d’utilisateur et d’un mot de passe uniques. Elle offre aux utilisateurs une expérience d’authentification familière et permet aux administrateurs de contrôler facilement les stratégies de compte pour les boîtes aux lettres de l’organisation Exchange Online à l’aide des outils de gestion Active Directory locaux.
    
    Vous disposez de deux options lors du déploiement de l’authentification unique : la synchronisation de mot de passe et les services ADFS (Active Directory Federation Services). Les deux options sont fournies par Azure Active Directory Connect. La synchronisation de mot de passe permet à pratiquement n’importe quelle organisation, indépendamment de sa taille, d’implémenter facilement l’authentification unique. Pour cette raison, et parce que l’expérience utilisateur dans un déploiement hybride est largement meilleure avec l’authentification unique activée, nous vous recommandons vivement de l’implémenter. Pour les très grandes organisations, telles que celles comportant plusieurs forêts Active Directory devant rejoindre le déploiement hybride, ADFS (Active Directory Federation Services) est requis.
    
    Pour plus d’informations, voir : [Authentification unique avec les déploiements hybrides](single-sign-on-with-hybrid-deployments-exchange-2013-help.md).

