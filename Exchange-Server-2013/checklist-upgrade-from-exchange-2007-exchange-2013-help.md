---
title: "Liste de contrôle : mise à niveau à partir d'Exchange 2007: Exchange 2013 Help"
TOCTitle: "Liste de contrôle : mise à niveau à partir d'Exchange 2007"
ms:assetid: 53aaa370-4562-43e4-9b75-7a705400c5a5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff805032(v=EXCHG.150)
ms:contentKeyID: 51407188
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Liste de contrôle : mise à niveau à partir d'Exchange 2007

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Utilisez cette liste de contrôle pour effectuer une mise à niveau de Microsoft Exchange Server 2007 vers Exchange Server 2013. Avant de commencer avec cette liste de contrôle, assurez-vous d'avoir bien assimilé les concepts présentés dans :

  - [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Nouveautés d'Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md)

Cette liste de contrôle est générique dans la mesure où elle fournit des conseils pour un scénario de mise à niveau standard.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L’Assistant Déploiement d’Exchange Server offre des conseils détaillés personnalisés sur le déploiement d’Exchange Server. Vous pouvez utiliser l’Assistant Déploiement pour déployer une nouvelle installation d’Exchange Server 2013, mettre à niveau une version antérieure vers Exchange 2013 ou configurer un déploiement hybride d’Exchange 2013 et d’Exchange Online. Pour en savoir plus, consultez la rubrique <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistant de déploiement Exchange Server</a>.</td>
</tr>
</tbody>
</table>


## Aide-mémoire pour la mise à niveau d’Exchange 2007 vers Exchange 2013


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Actions</p></td>
<td><p>Tâche</p></td>
<td><p>Rubrique(s)</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. Lisez les notes de publication.</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notes de publication relatives à Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. Vérifiez la configuration requise.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Configuration requise pour Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. Vérifiez que les étapes préalables ont été effectuées.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">Liste de vérification pour la sécurité du pré-déploiement</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. Configurez un espace de noms disjoint.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette étape est facultative. Elle n'est nécessaire que si votre organisation exécute un espace de noms disjoint.</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">Configuration d’une liste de recherche de suffixe DNS pour un espace de noms disjoint</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. Sélectionnez un carnet d’adresses en mode hors connexion pour toutes les bases de données de boîtes aux lettres Exchange 2007.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/?linkid=320546">Procédure de configuration de destinataires pour les téléchargements de carnet d’adresses en mode hors connexion</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. Créez un nom d’hôte Exchange hérité.</p></td>
<td><p><a href="https://technet.microsoft.com/fr-fr/library/dn130105(v=exchg.150)">Créer un nom d'hôte Exchange hérité</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>7. Installez Exchange 2013.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installer Exchange 2013 à l’aide de l’Assistant Installation</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Installer le rôle de transport Edge d’Exchange 2013 à l’aide de l’Assistant Installation</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Vérifier une installation d’Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Créez une boîte aux lettres Exchange 2013.</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Création de boîtes aux lettres utilisateur</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Configurez des répertoires virtuels liés à Exchange.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette étape est essentielle si vous souhaitez utiliser les services web Exchange, Outlook Anywhere ou le carnet d'adresses en mode hors connexion. Elle peut également s’avérer nécessaire si vous souhaitez modifier l’un des paramètres par défaut pour le Panneau de configuration Exchange, Microsoft Office Outlook Web App ou Exchange ActiveSync.<br />
</td>
</tr>
</tbody>
</table>

<p></p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuration du serveur d’accès au client Exchange 2013</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>10. Configurez des certificats Exchange 2013.</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificats numériques et SSL</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configurez des certificats Exchange 2007.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/?linkid=320553">Gestion du protocole SSL pour un serveur d’accès au client</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>12. Configurez le serveur de transport Edge.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette étape est facultative. Elle n’est nécessaire que si votre organisation utilise un serveur de transport Edge.</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configurer le flux de messagerie Internet via un serveur de transport Edge abonné</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. Configurez la messagerie unifiée.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette étape est facultative. Elle n'est nécessaire que si vous souhaitez utiliser la messagerie unifiée dans votre organisation.</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Planification de la messagerie unifiée</a></p>
<p><a href="deploy-exchange-2013-um-exchange-2013-help.md">Déploiement de la messagerie unifiée Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. Activez et configurez Outlook Anywhere.</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook Anywhere</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configurez le point de connexion de service.</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuration du serveur d’accès au client Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16. Configurez les URL Exchange 2007.</p></td>
<td><p><a href="https://technet.microsoft.com/fr-fr/library/dn282262(v=exchg.150)">Configurer les URL Exchange 2007 externes</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. Configurez des enregistrements DNS.</p></td>
<td><p><a href="https://technet.microsoft.com/fr-fr/library/dn283988(v=exchg.150)">Configurer des enregistrements DNS pour une installation sur plusieurs serveurs Exchange 2007</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>18. Déplacez les boîtes aux lettres d’Exchange 2007 vers Exchange 2013.</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Déplacements de boîtes aux lettres dans Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>19. Déplacez des données de dossiers publics d’Exchange 2013 vers Exchange 2013.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette étape est facultative. Elle n’est nécessaire que si votre organisation utilise des dossiers publics.</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="public-folders-exchange-2013-help.md">Dossiers publics</a></p>
<p><a href="https://technet.microsoft.com/fr-fr/library/jj150486(v=exchg.150)">Migrer les dossiers publics vers Exchange 2013 à partir de versions antérieures</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>20. Effectuez les tâches consécutives à l'installation.</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Tâches consécutives à l’installation d’Exchange 2013</a></p></td>
</tr>
</tbody>
</table>

