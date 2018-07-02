---
title: 'Limites de banque gérée: Exchange 2013 Help'
TOCTitle: Limites de banque gérée
ms:assetid: bea9ec15-bfb5-4716-b14e-010e389c9f9e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt741981(v=EXCHG.150)
ms:contentKeyID: 73226009
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Limites de banque gérée

 

_**Dernière rubrique modifiée :**2016-09-15_

**Résumé** : À propos des limites de connexion de banque gérée et de leur configuration.

Dans MicrosoftExchange Server 2013, les limites d’utilisation et de connexion se trouvent dans la banque gérée Exchange pour empêcher une application unique ou un utilisateur unique d’utiliser toutes les connexions disponibles à la banque gérée. Si un utilisateur ou une application unique est autorisé(e) à se servir de toutes les connexions, d’autres utilisateurs ou applications ne pourront pas accéder à la banque gérée, ce qui pourrait entraîner un temps d’arrêt.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour les connexions établies par des comptes ayant des privilèges administrateur, les limites de session ont été augmentées à 64 000 au maximum.</td>
</tr>
</tbody>
</table>


## Terminologie

La connaissance des termes suivants vous permettra de comprendre les types de connexions référencées dans cette rubrique.

  - Sessions  
    Les sessions représentent les connexions utilisées par les applications client et services comme Microsoft Outlook pour se connecter à la banque gérée. Les services et les clients peuvent avoir plusieurs sessions à un moment donné. Les termes *connexions* et *sessions* peuvent être utilisés indifféremment.

<!-- end list -->

  - Threads  
    Les threads représentent des demandes s’exécutant simultanément vers la banque gérée. Par exemple, si un utilisateur ouvre un dossier dans Outlook, Outlook exécute une demande pour la banque gérée au nom de l’utilisateur. Cette exécution de la demande est un thread unique.
    
    Dans Exchange Server 2013, il n’existe plus de limites de thread en fonction du type de client. À la place, le nombre maximal de threads **par base de données de boîte aux lettres** est de 50 pour tous les clients. L’exception est le service de disponibilité, qui a une limite maximale de 16 par utilisateur.

Retour au début

## Limites de session

Le tableau ci-dessous répertorie les types de connexions client à la banque gérée et les limites en fonction de ces connexions. Si vous souhaitez modifier les limites de session, voir « Configurer les limites de session » immédiatement à la suite de ce tableau.

Les versions antérieures d’Exchange limitent le nombre de connexions à la banque gérée en fonction du nombre de connexions par serveur. Dans Exchange 2013, les limites de session dépendent des connexions par base de données de boîte aux lettres.

Les types de limites de connexion dans Exchange 2013 sont les suivants :

  - **Nombre maximal de sessions par serveur**   Spécifie le nombre maximal de sessions qu’un service Exchange peut ouvrir à un moment donné sur une base de données de boîte aux lettres.

  - **Nombre maximal de sessions utilisateur par serveur**   Spécifie le nombre maximal de sessions pour un protocole particulier d’un utilisateur unique.

La section suivante, « Configurer les limites de session », explique comment modifier ces limites.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de client</th>
<th></th>
<th>Nombre maximal de sessions par base de données de boîte aux lettres</th>
<th>Nombre de sessions utilisateur par défaut par base de données de boîte aux lettres</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrateur</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>Service de disponibilité</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Indexation de contenu</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td></td>
<td><p>Non applicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Services web Exchange</p></td>
<td></td>
<td><p>Non applicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>Gestion</p></td>
<td></td>
<td><p>Non applicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>MAPI sur le niveau intermédiaire (MoMT)</p></td>
<td></td>
<td><p>Non applicable</p></td>
<td><p>32</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants : Événements</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxAssistants : A dépassé le délai</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>RPC MSExchange (Appel de procédure distante)</p></td>
<td></td>
<td><p>Non applicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft OfficeOutlook Web App</p></td>
<td></td>
<td><p>Non applicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>POP3 et IMAP4</p></td>
<td></td>
<td><p>Non applicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Transport</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>Messagerie unifiée</p></td>
<td></td>
<td><p>Non applicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Autres</p></td>
<td></td>
<td><p>Non applicable</p></td>
<td><p>16</p></td>
</tr>
</tbody>
</table>


## Configurer des limites de session

Vous pouvez modifier les limites de session par défaut.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous souhaitez modifier les limites de session, vous devez les modifier sur tous les serveurs de boîtes aux lettres dans des groupes de disponibilité de base de données. Si vous n’effectuez pas les mêmes modifications sur tous les serveurs, les résultats seront incohérents. Pour augmenter la limite de session sur le serveur d’accès au client, la valeur <code>RCAMaxConcurrency</code> doit être augmentée conformément à la stratégie de limitation. Pour plus d’informations, voir <a href="https://technet.microsoft.com/fr-fr/library/dd298094(v=exchg.150)">Set-ThrottlingPolicy</a>.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Une modification incorrecte du Registre peut être à l’origine de problèmes graves qui vous obligeront peut-être à réinstaller votre système d’exploitation. Il se peut que les problèmes résultant d’une modification incorrecte du Registre soient impossibles à résoudre. Avant de modifier le Registre, sauvegardez les données importantes.</td>
</tr>
</tbody>
</table>


1.  Démarrez l'Éditeur du Registre (regedit).

2.  Naviguez jusqu’à la sous-clé de Registre suivante :
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**.

3.  Cliquez avec le bouton droit sur **ParametersSystem**, pointez sur **Nouveau**, puis cliquez sur **Valeur DWORD 32 bits**.
    
    La nouvelle valeur est créée dans le volet de résultats.

4.  Reparamétrez la clé sur l’une des valeurs suivantes, puis appuyez sur Entrée :
    
      - **Maximum Allowed Sessions Per User**   Cette limite spécifie le nombre maximal de sessions admissibles par utilisateur.
    
      - **Maximum Allowed Service Sessions Per User**   Cette limite spécifie le nombre maximal de sessions admissibles par utilisateur.
    
      - **Maximum Allowed Sessions Per SCT**   Cette limite spécifie le nombre maximal de sessions Exchange admissibles par service. La valeur par défaut est 10 000.

5.  Cliquez avec le bouton droit de la souris sur la clé nouvellement créée, puis cliquez sur **Modifier**.

6.  Dans la zone **Données de lavaleur**, tapez le nombre d’objets auxquels vous souhaitez limiter cette entrée, puis cliquez sur **OK**. Utilisez le tableau précédent pour afficher les paramètres par défaut.

Retour au début

## Limites d’éléments ouverts

Les limites d’éléments ouverts sont des limites placées sur le nombre d’éléments qui peuvent être ouverts par une seule boîte aux lettres dans une session unique. Toutefois, un utilisateur peut avoir plusieurs sessions ouvertes simultanément. Par exemple, si un utilisateur dispose de deux sessions ouvertes, l’utilisateur peut ouvrir 1 000 dossiers.

Si vous souhaitez modifier ces limites de session, voir « Configurer les limites d’éléments ouverts » immédiatement à la suite de ce tableau.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Type d’élément</th>
<th>Type d’objet du Registre</th>
<th>Nombre maximal d’éléments ouverts par session</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Affichage de la liste de contrôle d’accès</p></td>
<td><p>objtACLView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Pièce jointe</p></td>
<td><p>objtAttachment</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Affichage de la pièce jointe</p></td>
<td><p>objtAttachmentView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>CStream</p></td>
<td><p>objtCStream</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>Dossier</p></td>
<td><p>objtFolder</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Affichage des dossiers</p></td>
<td><p>objtFolderView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Flux de destination FX</p></td>
<td><p>objtFXDstStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Flux source FX</p></td>
<td><p>objtFXSrcStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Message</p></td>
<td><p>objtMessage</p></td>
<td><p>250</p></td>
</tr>
<tr class="even">
<td><p>Affichage des messages</p></td>
<td><p>objtMessageView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Notification</p></td>
<td><p>objtNotify</p></td>
<td><p>500,000</p></td>
</tr>
<tr class="even">
<td><p>Affichage de la règle</p></td>
<td><p>objtRulesView</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>Flux</p></td>
<td><p>objtStream</p></td>
<td><p>250</p></td>
</tr>
</tbody>
</table>


## Configurer les limites d’éléments ouverts

Vous pouvez limiter le nombre maximal de ressources qu’un client MAPI peut utiliser simultanément.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous souhaitez modifier les limites d’éléments ouverts, vous devez les modifier sur tous les serveurs de boîtes aux lettres dans des groupes de disponibilité de base de données et des tableaux d’accès au client. Si vous n’effectuez pas les mêmes modifications sur tous les serveurs, les résultats seront incohérents.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Une modification incorrecte du Registre peut être à l’origine de problèmes graves qui vous obligeront peut-être à réinstaller votre système d’exploitation. Il se peut que les problèmes résultant d’une modification incorrecte du Registre soient impossibles à résoudre. Avant de modifier le Registre, sauvegardez les données importantes.</td>
</tr>
</tbody>
</table>


1.  Démarrez l'Éditeur du Registre (regedit).

2.  Naviguez jusqu’à la sous-clé de Registre suivante :
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**

3.  Cliquez avec le bouton droit sur **ParametersSystem**, pointez sur **Nouveau**, puis cliquez sur **Clé**.
    
    Une nouvelle clé est créée dans l’arborescence de la console.

4.  Renommez la clé **MaxObjsPerMapiSession**, puis appuyez sur Entrée.

5.  Cliquez avec le bouton droit sur **MaxObjsPerMapiSession**, pointez sur **Nouveau**, puis cliquez sur **Valeur DWORD 32 bits**.
    
    La nouvelle valeur est créée dans le volet de résultats.

6.  Renommez la clé *\<Object\_type\>*, où *\<Object\_type\>* correspond au nom du type d’objet de Registre que vous êtes en train de modifier. Par exemple, pour modifier le nombre de messages qui peuvent être ouverts, utilisez *objtMessage*. Appuyez sur Entrée.

7.  Cliquez avec le bouton droit de la souris sur la clé nouvellement créée, puis cliquez sur **Modifier**.

8.  Dans le champ **Données de la valeur**, tapez le nombre d’objets pour lesquels vous souhaitez limiter cette entrée, puis cliquez sur **OK**. Par exemple, tapez **350** pour augmenter la valeur de l’objet.

9.  Redémarrez le service de banque d’informations de Microsoft Exchange.

Retour au début

## Limites de taille des éléments

Les limites de taille des éléments sont les limites placées sur les éléments dans une boîte aux lettres de chaque utilisateur. Elles sont configurables à l’aide des paramètres *MaxSendSize* et *MaxReceiveSize* sur l’applet de commande [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type d’élément</th>
<th>Limite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Message (enregistré)</p></td>
<td><p>Taille maximale de SendLimit et ReceiveLimit</p></td>
</tr>
<tr class="even">
<td><p>Message (envoyé)</p></td>
<td><p>Taille maximale de SendLimit</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>


Retour au début

