---
title: "Définition du port d'écoute TCP sur un serveur d'accès au client: Exchange 2013 Help"
TOCTitle: Définition du port d'écoute TCP sur un serveur d'accès au client
ms:assetid: 5f48f21a-d8d4-48b2-868f-9a3647693841
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673530(v=EXCHG.150)
ms:contentKeyID: 50555415
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Définition du port d'écoute TCP sur un serveur d'accès au client

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-09_

Vous pouvez configurer le port TCP qui est utilisé pour écouter les demandes SIP sur un serveur d'accès au client exécutant le service routeur des appels de messagerie unifiée Microsoft Exchange. Par défaut, quand vous installez un serveur d'accès au client, le numéro du port d'écoute TCP SIP est défini sur 5060 et le serveur d'accès au client démarre en mode TCP. Le port d'écoute TCP SIP ne peut pas être configuré à l'aide du Centre d'administration Exchange (CAE). Vous devez configurer le numéro du port d'écoute TCP SIP à l'aide de la cmdlet **Set-UMCallRouterSettings**.

Vous devez configurer le port d'écoute TCP sur 5061 si vos passerelles VoIP, les PBX IP ou les contrôleurs de frontière de session (SBC) sont configurés pour utiliser un port TCP différent de la norme SIP 5060.

Vous pouvez uniquement configurer les ports TCP et TLS du serveur d'accès au client. Vous ne pouvez pas configurer les ports d'un serveur de boîtes aux lettres Exchange 2013. Toutefois, vous pouvez utiliser la cmdlet **Set-UMService** pour configurer les ports d'écoute TCP et TLS pour des serveurs de messagerie unifiée Exchange 2010.

Pour d'autres tâches relatives aux serveurs de messagerie unifiée et d'accès au client, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Serveur d'accès au client (service routeur des appels de messagerie unifiée) » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Vérifiez que vous avez correctement installé les serveurs d'accès au client et de boîtes aux lettres.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour configurer le port d'écoute TCP sur un serveur d'accès au client

1.  Dans le Centre d'administration Exchange, accédez à **Serveurs** \> **Serveurs**.

2.  Dans l'affichage Liste, sélectionnez le serveur Exchange à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Exchange Server**, cliquez sur **Messagerie unifiée**.

4.  Sous **Paramètres de routeur d'appels de messagerie unifiée**, sous **Port d'écoute TCP**, entrez le numéro du port TCP, puis cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le port d'écoute TCP sur un serveur d'accès au client

Cet exemple définit le port d'écoute TCP d'un serveur d'accès au client intitulé `MyClientAccessServer` sur 5566.

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTCPListeningPort 5566

