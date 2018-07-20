---
title: "Liste de contrôle : mise à niveau à partir d'Exchange 2010: Exchange 2013 Help"
TOCTitle: "Liste de contrôle : mise à niveau à partir d'Exchange 2010"
ms:assetid: 06c1045a-5fcf-4e24-a901-1a979302fb8d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee332309(v=EXCHG.150)
ms:contentKeyID: 51407152
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Liste de contrôle : mise à niveau à partir d'Exchange 2010

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Utilisez cette liste de contrôle pour effectuer une mise à niveau de Microsoft Exchange 2010 vers Exchange 2013. Avant de commencer avec cette liste de contrôle, assurez-vous d'avoir bien assimilé les concepts présentés dans :

  - [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Nouveautés d'Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md)

Cette liste de contrôle est générique dans la mesure où elle fournit des conseils pour un scénario de mise à niveau standard.

> [!NOTE]
> L’Assistant Déploiement d’Exchange Server offre des conseils détaillés personnalisés sur le déploiement d’Exchange Server. Vous pouvez utiliser l’Assistant Déploiement pour déployer une nouvelle installation d’Exchange Server 2013, mettre à niveau une version antérieure vers Exchange 2013 ou configurer un déploiement hybride d’Exchange 2013 et d’Exchange Online. Pour en savoir plus, consultez la rubrique <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistant de déploiement Exchange Server</a>.


## Aide-mémoire pour la mise à niveau d'Exchange 2010 vers Exchange 2013


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
<td><p>1. Lisez les notes de mises à jour</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notes de publication relatives à Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>2. Vérifiez la configuration requise</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Configuration requise pour Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>3. Vérifiez que les étapes préalables ont été effectuées.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">Liste de vérification pour la sécurité du pré-déploiement</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>4. Configurez un espace de noms disjoint.</p>

> [!NOTE]  
> Cette étape est facultative. Elle n'est nécessaire que si votre organisation exécute un espace de noms disjoint.

</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">Configuration d’une liste de recherche de suffixe DNS pour un espace de noms disjoint</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. Sélectionnez un carnet d’adresses en mode hors connexion pour toutes les bases de données de boîtes aux lettres Exchange 2010.</p></td>
<td><p><a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Set mailbox database properties</a> dans <a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Gestion des bases de données de boîtes aux lettres dans Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. Installez Exchange 2013.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installer Exchange 2013 à l’aide de l’Assistant Installation</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Installer le rôle de transport Edge d’Exchange 2013 à l’aide de l’Assistant Installation</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Vérifier une installation d’Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Créez une boîte aux lettres Exchange 2013.</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Création de boîtes aux lettres utilisateur</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Configurez des répertoires virtuels liés à Exchange.</p>

> [!NOTE]
> Cette étape est essentielle si vous souhaitez utiliser les services web Exchange, Outlook Anywhere ou le carnet d'adresses en mode hors connexion. Elle peut également s’avérer nécessaire si vous souhaitez modifier l’un des paramètres par défaut pour le Panneau de configuration Exchange, Microsoft Office Outlook Web App ou Exchange ActiveSync.

</td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuration du serveur d’accès au client Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Ajoutez des certificats numériques sur le serveur d’accès au client.</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificats numériques et SSL</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. Déplacez la boîte aux lettres d’arbitrage.</p></td>
<td><p><a href="move-the-exchange-2010-system-mailbox-to-exchange-2013-exchange-2013-help.md">Déplacer la boîte aux lettres système Exchange 2010 vers Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configurez la messagerie unifiée.</p>

> [!NOTE]  
> Cette étape est facultative. Elle n'est nécessaire que si vous souhaitez utiliser la messagerie unifiée dans votre organisation.

</td>
<td><p><a href="upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md">Mise à niveau de la messagerie unifiée d'Exchange 2010 vers celle d'Exchange 2013</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>12. Configurez le serveur de transport Edge</p>

> [!NOTE]  
> Cette étape est facultative. Elle n’est nécessaire que si votre organisation utilise un serveur de transport Edge.

</td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configurer le flux de messagerie Internet via un serveur de transport Edge abonné</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>13. Activez et configurez Outlook Anywhere.</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook Anywhere</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. Configurez le point de connexion de service.</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuration du serveur d’accès au client Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configurez des enregistrements DNS.</p></td>
<td><p><a href="https://technet.microsoft.com/fr-fr/library/dn307232(v=exchg.150)">Configurer des enregistrements DNS pour une installation à plusieurs serveurs Exchange 2010</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16. Déplacez les boîtes aux lettres d’Exchange 2010 vers Exchange 2013.</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Déplacements de boîtes aux lettres dans Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. Déplacez des données de dossiers publics d’Exchange 2013 vers Exchange 2013.</p></td>
<td><p><a href="public-folders-exchange-2013-help.md">Dossiers publics</a></p>
<p><a href="https://technet.microsoft.com/fr-fr/library/jj150486(v=exchg.150)">Migrer les dossiers publics vers Exchange 2013 à partir de versions antérieures</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>18. Effectuez les tâches consécutives à l'installation.</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Tâches consécutives à l’installation d’Exchange 2013</a></p></td>
</tr>
</tbody>
</table>

