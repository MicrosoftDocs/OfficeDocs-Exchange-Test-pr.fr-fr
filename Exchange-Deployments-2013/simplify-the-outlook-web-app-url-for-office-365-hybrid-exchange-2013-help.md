---
title: 'Simplifier l’URL d’Outlook Web App pour une configuration hybride d’Office 365: Exchange 2013 Help'
TOCTitle: Simplifier l’URL d’Outlook Web App pour une configuration hybride d’Office 365
ms:assetid: 19449aee-3796-4298-90c6-c7579b8d2f7a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt791749(v=EXCHG.150)
ms:contentKeyID: 74259163
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Simplifier l’URL d’Outlook Web App pour une configuration hybride d’Office 365

 

_<strong>Dernière rubrique modifiée :</strong>2016-11-11_

Découvrez comment configurer une URL pour Outlook sur le web (Outlook Web App) pour les utilisateurs de boîte aux lettres cloud dans un environnement hybride.

Un souci majeur pour les organisations qui passent à Office 365 à partir d’un environnement Exchange local est l’expérience utilisateur. Les utilisateurs ont besoin d’un accès continu à leurs boîtes aux lettres, quel que soit l’endroit où le moment où elles sont migrées. À cet égard, la coexistence Outlook sur le web (anciennement nommée Outlook Web App) est importante.

Imaginons le cas de figure suivant : une entreprise utilise un déploiement hybride pour déplacer certaines de ses boîtes aux lettres d’un environnement Exchange local vers Office 365. Jusqu’au vendredi précédant la migration, les utilisateurs accédaient à leurs boîtes aux lettres locales à l’aide de l’URL https://mail.contoso.com/owa. Le lundi suivant la migration, ces mêmes utilisateurs obtiennent une erreur lorsqu’ils essaient d’accéder à leur boîte aux lettres via cette URL.

Pour autoriser les utilisateurs concernés à se connecter à leurs boîtes aux lettres à l’aide d’Outlook sur le web, vous avez deux possibilités :

  - **Indiquer la nouvelle URL aux utilisateurs (par exemple, https://outlook.com/owa/contoso.com)**   Les inconvénients de cette solution sont les suivants :
    
      - L’URL est complexe.
    
      - L’expérience utilisateur est fractionnée.

  - **Configurer le paramètre TargetOWAUrl sur la relation organisationnelle**   Les inconvénients de cette solution sont les suivants :
    
      - Le point de terminaison des boîtes aux lettres cloud est externe (ce n’est pas le domaine attendu par les utilisateurs).
    
      - Le point de terminaison requiert que le domaine apparaisse dans l’URL (pour faire la distinction entre l’offre Office 365 professionnelle et l’offre outlook.com grand public).
    
      - À cause du point de terminaison, les utilisateurs reçoivent des avertissements de certificats non correspondant.

Pour éviter ces problèmes aux utilisateurs ayant des boîtes aux lettres cloud, procédez comme suit :

1.  **Créez un enregistrement CNAME dans le DNS (par exemple, cloudowa.contoso.com) qui pointe vers mail.office365.com**
    
      - Veillez à bien créer l’enregistrement CNAME dans vos DNS (public) interne et externe, car les utilisateurs peuvent se connecter à partir de connexions Internet internes ou externes.
    
      - Dans notre exemple, le domaine contoso.com est utilisé dans la demande (la partie cloudowa est supprimée). Cela signifie que vous n’avez pas besoin de spécifier le domaine dans l’URL.

2.  **Configurez la redirection Outlook sur le web dans la relation organisationnelle locale**   Pour ce faire, utilisez la syntaxe suivante dans l’Environnement de ligne de commande Exchange Management Shell de l’instance locale d’Exchange :
    
        Set-OrganizationRelationship -TargetOWAUrl http://<CNAME value>/owa
    
    Par exemple, si l’enregistrement CNAME que vous avez créé à l’étape 1 est cloudowa.contoso.com, exécutez la commande suivante :
    
        Set-OrganizationRelationship -TargetOWAUrl http://cloudowa.contoso.com/owa
    
    **Remarques :**
    
      - Utilisez le protocole http, et pas https.
    
      - La valeur /owa mise à la fin est requise dans la relation organisationnelle, mais les utilisateurs n’ont pas besoin de l’entrer dans l’URL.

## Demandes d’authentification multiples

Les utilisateurs peuvent voir plusieurs demandes d’authentification en fonction des facteurs suivants :

  - L’emplacement à partir duquel ils se connectent (connexions Internet internes ou externes).

  - Si leur ordinateur est joint au domaine.

  - Si vous utilisez la fédération des identités dans votre environnement hybride.

Les invites d’authentification que les utilisateurs doivent normalement recevoir sont indiquées dans le tableau suivant.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Méthode d’authentification</th>
<th>Ordinateur client</th>
<th>Invites d’authentification reçues</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Fédération des identités</p></td>
<td><p>Connexion Internet interne</p></td>
<td><p>Une seule invite</p></td>
</tr>
<tr class="even">
<td><p>Fédération des identités</p></td>
<td><p>Connexion Internet externe</p></td>
<td><p>Invite double</p></td>
</tr>
<tr class="odd">
<td><p>Sans fédération des identités</p></td>
<td><p>Joint à un domaine (interne ou externe)</p></td>
<td><p>Invite double</p></td>
</tr>
<tr class="even">
<td><p>Avec ou sans fédération des identités</p></td>
<td><p>Non joint à un domaine (interne ou externe)</p></td>
<td><p>Invite double</p></td>
</tr>
</tbody>
</table>


**Remarque** : la fédération des identités requiert que le point de terminaison AD FS soit configuré dans la zone intranet d’Internet Explorer, comme décrit dans la rubrique [https://go.microsoft.com/fwlink/p/?linkid=834460](https://go.microsoft.com/fwlink/p/?linkid=83446), et qu’AD FS soit configuré conformément aux indications générales relatives à Office 365.

