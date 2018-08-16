---
title: 'Liste de contrôle : nouvelle installation d’Exchange 2013: Exchange 2013 Help'
TOCTitle: 'Liste de contrôle : Effectuer une nouvelle installation d’Exchange 2013'
ms:assetid: f70d9dd3-7370-472e-b05e-1ea1671272b2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff805042(v=EXCHG.150)
ms:contentKeyID: 50479579
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Liste de contrôle : Effectuer une nouvelle installation d’Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Utilisez cette liste de vérification pour déployer Microsoft Exchange Server 2013. Avant de commencer avec cette liste de contrôle, assurez-vous d'avoir bien assimilé les concepts présentés dans :

  - [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Liste de vérification pour la sécurité du pré-déploiement](deployment-security-checklist-exchange-2013-help.md)

Cette liste est générique dans la mesure où elle fournit des instructions pour un scénario type.

> [!NOTE]
> L’Assistant Déploiement d’Exchange Server offre des conseils détaillés personnalisés sur le déploiement d’Exchange Server. Vous pouvez utiliser l’Assistant Déploiement pour déployer une nouvelle installation d’Exchange Server 2013, mettre à niveau une version antérieure vers Exchange 2013 ou configurer un déploiement hybride d’Exchange 2013 et d’Exchange Online. Pour en savoir plus, consultez la rubrique <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistant de déploiement Exchange Server</a>.


## Liste de contrôle d'une nouvelle installation Exchange 2013


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
<td><p>Rubrique</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. Lire les notes de publication.</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notes de publication relatives à Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. Vérifier la configuration système requise.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Configuration requise pour Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. Vérifier que les opérations préalables ont été effectuées.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. Configurer un espace de noms disjoint.</p>

> [!NOTE]  
> Cette étape est facultative. Elle n'est nécessaire que si votre organisation a recours à un espace de noms disjoint.

</td>
<td><p><a href="disjoint-namespace-scenarios-exchange-2013-help.md">Scénarios d’espace de noms disjoint</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>5. Installer le rôle serveur de boîtes aux lettres.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installer Exchange 2013 à l’aide de l’Assistant Installation</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>6. Installer le rôle serveur d'accès au client.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installer Exchange 2013 à l’aide de l’Assistant Installation</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Installer le rôle serveur de transport Edge.</p>

> [!NOTE]  
> Cette étape est facultative. Elle est nécessaire uniquement si vous souhaitez installer un serveur de transport Edge. Pour plus d’informations, voir <a href="edge-transport-servers-exchange-2013-help.md">Serveurs de transport Edge</a>.

</td>
<td><p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Installer le rôle de transport Edge d’Exchange 2013 à l’aide de l’Assistant Installation</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Créer un abonnement EdgeSync.</p>
<p>Cette étape est facultative. Elle est nécessaire uniquement si vous avez installé un serveur de transport Edge et que vous souhaitez configurer un abonnement EdgeSync entre votre serveur de transport Edge et un serveur de transport Hub. Pour plus d’informations, voir <a href="edge-subscriptions-exchange-2013-help.md">Abonnements Edge</a>.</p></td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configurer le flux de messagerie Internet via un serveur de transport Edge abonné</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Configurer le transport.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 1: Create a Send connector</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. Ajouter des domaines acceptés supplémentaires</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 2: Add additional accepted domains</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configurer des stratégies d'adresse de messagerie.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 3: Configure the default email address policy</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>12. Configurer les paramètres sur les répertoires virtuels, y compris le carnet d’adresses en mode hors connexion, les services web Exchange, le Centre d’administration Exchange (CAE), Outlook Web App et les répertoires virtuels Exchange ActiveSync.</p>

> [!NOTE]  
> Cette étape est nécessaire si vous voulez utiliser les services web Exchange, Outlook Anywhere ou le Carnet d'adresses en mode hors connexion. Elle peut également être nécessaire si vous devez modifier des paramètres par défaut du Centre d'administration Exchange (CAE), Outlook Web App ou Exchange ActiveSync.

</td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 4: Configure external URLs</a></p>
<p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 5: Configure internal URLs</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. Ajouter des certificats numériques sur le serveur d’accès au client.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 6: Configure an SSL certificate</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>14. Configurer la messagerie unifiée.</p>

> [!NOTE]  
> Cette étape est facultative. Elle n'est nécessaire que si vous voulez utiliser la messagerie unifiée dans votre organisation.

</td>
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Déploiement de la messagerie vocale et la messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configurer des paramètres supplémentaires de la messagerie unifiée et de Lync Server.</p>

> [!NOTE]  
> Cette étape est facultative. Elle n’est nécessaire que si vous avez configuré la messagerie unifiée dans votre organisation et que vous voulez l’intégrer à Lync Server.

</td>
<td><p><a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>16. Effectuer les tâches consécutives à l’installation.</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Tâches consécutives à l’installation d’Exchange 2013</a></p></td>
</tr>
</tbody>
</table>

