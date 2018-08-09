---
title: 'L’héritage de la liste de contrôle d’accès (ACL) est bloqué'
TOCTitle: L’héritage de la liste de contrôle d’accès (ACL) est bloqué_InhBlockPublicFolderTree
ms:assetid: e3b89c8a-d6f8-4864-8bf0-35a78ce87cc4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.inhblockpublicfoldertree(v=EXCHG.150)
ms:contentKeyID: 50479410
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# L’héritage de la liste de contrôle d’accès (ACL) est bloqué\_InhBlockPublicFolderTree

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2015-03-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2007 ou d’Exchange Server 2010 ne peut pas continuer car les autorisations requises n’ont pas pu être propagées.

Le programme d’installation d’Exchange nécessite que l’héritage des autorisations soit activé sur les objets Exchange suivants :

  - Objet Organisation Exchange

  - Objet Groupe d’administration Exchange

  - Objet Conteneur de serveurs Exchange

  - Objet Liste d’adresses Exchange

  - Objet Dossier public Exchange

  - Objet Arborescence de dossiers publics Exchange

Si l’héritage des autorisations n’est pas activé sur ces objets, des problèmes de flux de messagerie et de montage des banques, ainsi que d’autres interruptions de service peuvent survenir.

Pour résoudre ce problème, assurez-vous que l’option « Permettre aux autorisations héritées du parent de se propager à cet objet et aux objets enfants » est activée pour l’objet, puis réexécutez le programme d’installation d’Exchange Server 2007 ou d’Exchange 2010.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Réactivation de l’héritage des autorisations pour un objet de configuration Exchange à l’aide du Gestionnaire système Exchange d’Exchange Server 2003</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Activez l’onglet <strong>Sécurité</strong> pour la zone des propriétés de l’objet du Gestionnaire système Exchange en définissant un paramètre de Registre</p>
<ol>
<li><p>Lancez un Éditeur du Registre (Regedt32.exe).</p></li>
<li><p>Localisez la clé suivante dans le Registre :</p>
<p><strong>HKEY_CURRENT_USER\Software\Microsoft\Exchange\EXAdmin</strong></p></li>
<li><p>Dans le menu <strong>Edition</strong>, cliquez sur <strong>Nouveau</strong>, puis ajoutez la valeur de Registre suivante :</p>
<p><strong>Nom de la valeur</strong> : ShowSecurityPage</p>
<p><strong>Type de données</strong> : REG_DWORD</p>
<p><strong>Base</strong> : Fichier binaire</p>
<p><strong>Valeur</strong> : 1</p></li>
<li><p>Quittez l’Éditeur du Registre.</p></li>
</ol>
> [!NOTE]
> Par défaut, l’onglet <strong>Sécurité</strong> n’est pas activé dans la zone des propriétés de l’objet de configuration.

</li>
<li><p>Ouvrez le Gestionnaire système Exchange, recherchez l’objet en question, cliquez avec le bouton droit sur l’objet, puis sélectionnez <strong>Propriétés</strong>.</p></li>
<li><p>Sélectionnez l’onglet <strong>Sécurité</strong>, puis cliquez sur <strong>Avancé</strong>.</p></li>
<li><p>Sélectionnez <strong>Permettre aux autorisations héritées du parent de se propager à cet objet et aux objets enfants</strong> pour réactiver l’héritage des autorisations.</p></li>
<li><p>Redémarrez Exchange Server.</p></li>
</ol></td>
</tr>
</tbody>
</table>


> [!Caution]  
> Si vous modifiez les attributs d’objets Active Directory de manière incorrecte lorsque vous utilisez ADSI Edit, l’outil LDP ou tout autre client LDAP version 3, cela risque de poser de graves problèmes. Ces problèmes peuvent nécessiter une réinstallation de Microsoft Windows Server™ 2003, d’Exchange Server 2003 ou des deux. Vous modifiez les attributs d’objets Active Directory à vos propres risques.



<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Réactivation de l’héritage des autorisations pour un objet de configuration Exchange à l’aide d’ADSIEdit d’Exchange Server 2007 ou d’Exchange Server 2010</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Installez ADSI Edit.</p></li>
<li><p>Lancez ADSI Edit. Cliquez sur <strong>Démarrer</strong>, puis <strong>Exécuter</strong>, entrez <strong>adsiedit.msc</strong> dans la zone de texte, puis cliquez sur OK.</p></li>
<li><p>Accédez à l’objet en question, cliquez avec le bouton droit sur l’objet, puis sélectionnez <strong>Propriétés</strong>.</p></li>
<li><p>Sélectionnez l’onglet <strong>Sécurité</strong>, puis cliquez sur <strong>Avancé</strong>.</p></li>
<li><p>Sélectionnez <strong>Permettre aux autorisations héritées du parent de se propager à cet objet et aux objets enfants</strong> pour réactiver l’héritage des autorisations.</p></li>
<li><p>Sélectionnez <strong>OK</strong> deux fois pour appliquer la modification.</p></li>
<li><p>Attendez que la réplication Active Directory propage les modifications ou forcez la réplication Active Directory en suivant les instructions de l’article de la Base de connaissances Microsoft, « Lancement de la réplication entre des partenaires de réplication directe dans Active Directory » (<a href="http://go.microsoft.com/fwlink/?linkid=3052&kbid=232072" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=232072</a>).</p></li>
</ol></td>
</tr>
</tbody>
</table>

