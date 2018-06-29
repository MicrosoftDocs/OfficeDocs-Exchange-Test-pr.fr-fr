---
title: 'Créer un connecteur d’envoi pour router le courrier sortant via un hôte actif: Exchange 2013 Help'
TOCTitle: Créer un connecteur d’envoi pour router le courrier sortant via un hôte actif
ms:assetid: 4a9ef08e-bd62-4c6b-8790-d24fb0f8f24b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673059(v=EXCHG.150)
ms:contentKeyID: 50478105
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer un connecteur d’envoi pour router le courrier sortant via un hôte actif

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2013-02-07_

Dans certaines situations, vous pouvez avoir besoin d'acheminer un message électronique via un hôte actif tiers, tel que lors d'une instance dans laquelle vous avez un Network Appliance pour lequel vous voulez exécuter des vérifications de stratégie sur des messages sortant.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L'hôte actif tiers doit utiliser SMTP pour le transport. Dans le cas contraire, vous devez utiliser un connecteur étranger ou un connecteur d'agent de remise.</td>
</tr>
</tbody>
</table>


Intéressé par des scénarios où cette procédure est utilisée ? Consultez les rubriques suivantes :

  - [Configuration du flux de messagerie et de l’accès au client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Connecteurs d’envoi » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Voir [Déployer une nouvelle installation d’Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si vous commencez votre installation. À l’issue de l’installation, vous pouvez utiliser les étapes de cette rubrique pour créer votre connecteur d’envoi.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Utilisez le centre d'administration Exchange pour créer un connecteur d'envoi afin d'acheminer les messages électroniques via un hôte actif

1.  Dans le Centre d’administration Exchange, accédez à **Flux de messagerie** \> **Connecteurs d’envoi**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans l'assistant **Nouveau connecteur d'envoi**, spécifiez un nom pour le connecteur d'envoi, puis sélectionnez **Personnaliser** pour le **Type**. Cette sélection est généralement effectuée pour acheminer des messages vers des ordinateurs qui n'exécutent pas Exchange Server 2013. Cliquez sur **Suivant**.

3.  Sélectionnez **Acheminer tous les messages via les hôtes actifs**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Ajouter un hôte actif**, spécifiez l'adresse IP, telle que 192.168.100.1, ou le nom de domaine complet, tel que contoso.com. Cliquez sur **Enregistrer**.
    
    Pour l'**authentification des hôtes actifs**, sélectionnez le type d'authentification requis par l'hôte actif. Si vous sélectionnez **Authentification de base**, vous devez entrer un nom d'utilisateur et un mot de passe.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous sélectionnez l'authentification de base, nous vous recommandons d'utiliser une connexion chiffrée car le nom d'utilisateur et le mot de passe sont envoyés dans un texte en clair.</td>
    </tr>
    </tbody>
    </table>


4.  Sous **Espace d’adressage**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Ajouter un domaine**, vérifiez que SMTP apparaît dans la liste **Type**. Pour **Nom de domaine complet**, entrez \* pour spécifier que ce connecteur d'envoi s'applique aux messages envoyés dans n'importe quel domaine. Cliquez sur **Enregistrer**.

5.  Pour **Serveur source**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Sélectionner un serveur**, sélectionnez un serveur de boîtes aux lettres qui sera utilisé pour envoyer des messages à l’Internet via le serveur d’accès au client puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Après avoir sélectionné le serveur, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Cliquez sur **OK**.

6.  Cliquez sur **Terminer**.

Une fois créé, le connecteur d’envoi apparaît dans la liste des connecteurs d’envoi.

## Comment savoir si cela a fonctionné ?

Pour vérifier la création correcte d'un connecteur d'envoi pour acheminer le message électronique sortant via un hôte actif, envoyez un message depuis un utilisateur de votre organisation (vous pouvez utiliser Outlook Web App) vers le domaine spécifié pour l'**Espace d'adressage**. Si le destinataire reçoit le message, vous avez correctement configuré le connecteur d'envoi.

## Pour plus d'informations

[Créer un connecteur d’envoi pour les messages électroniques envoyés vers Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Connecteurs d'envoi](send-connectors-exchange-2013-help.md)

