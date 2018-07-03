---
title: 'Configuration du mode de démarrage sur un serveur de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Configuration du mode de démarrage sur un serveur de boîtes aux lettres
ms:assetid: 4457d6a0-52bd-4269-8cb5-d34d7fe9bfc3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423544(v=EXCHG.150)
ms:contentKeyID: 50555380
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du mode de démarrage sur un serveur de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-15_

Vous pouvez spécifier le mode de démarrage du service de messagerie unifiée Microsoft Exchange sur un serveur de boîtes aux lettres. Par défaut, le serveur de boîtes aux lettres démarre en mode TCP. Cependant, si vous utilisez TLS (Transport Layer Security) pour chiffrer le trafic VoIP (Voice over IP), vous devez configurer le serveur de boîtes aux lettres pour utiliser le mode TLS ou Double. nous vous recommandons de configurer les serveurs de boîtes aux lettres pour utiliser le mode de démarrage Double. En effet, tous les serveurs d'accès au client et de boîtes aux lettres peuvent répondre aux appels entrants pour tous les plans de numérotation de messagerie unifiée, qui peuvent comporter différents paramètres de sécurité (Non sécurisé, Sécurisé SIP ou Sécurisé). Si vous modifiez le mode de démarrage, vous devez redémarrer le service de messagerie unifiée Microsoft Exchange pour que la modification soit prise en compte.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Par défaut, les serveurs de boîtes aux lettres sont disponibles pour répondre aux appels entrants. Il n'est pas nécessaire d'ajouter un serveur de boîtes aux lettres à un plan de numérotation de messagerie unifiée pour traiter les appels de messagerie unifiée, sauf si vous intégrez la messagerie unifiée et Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server.</td>
</tr>
</tbody>
</table>


Pour d'autres tâches de gestion relatives aux serveurs de messagerie unifiée et de boîtes aux lettres, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Serveur de boîtes aux lettres (service de messagerie unifiée) » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Vérifiez que le serveur de boîtes aux lettres est installé, sur le même ordinateur que le serveur d'accès au client ou sur un ordinateur distinct.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour configurer le mode de démarrage sur un serveur de boîtes aux lettres

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Dans l'affichage Liste, sélectionnez le serveur Exchange à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Exchange Server**, cliquez sur **Messagerie unifiée**.

4.  Sous **Paramètres de service de messagerie unifiée** \> **Mode de démarrage de messagerie unifiée**, activez l'une des options suivantes dans la liste déroulante :
    
      - **TCP**   Activez cette option si vous n’utilisez pas mTLS et utilisez uniquement des plans de numérotation de type Non sécurisé.
    
      - **TLS**   Activez cette option si vous utilisez mTLS et si vous n'utilisez que des plans de numérotation de type Sécurisé SIP ou Sécurisé.
    
      - **DOUBLE**   Activez cette option si vous utilisez mTLS et si vous utilisez des plans de numérotation de type Non sécurisé, Sécurisé SIP ou Sécurisé.

5.  Après avoir sélectionné le mode de démarrage de messagerie unifiée, cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le mode de démarrage sur un serveur de boîtes aux lettres

Cet exemple définit le mode de démarrage d'un serveur de boîtes aux lettres nommé `MyUMServer1` sur Double.

    Set-UMService -Identity MyUMServer1 -UMStartUpMode Dual

Cet exemple définit le mode de démarrage d'un serveur de boîtes aux lettres nommé `MyUMServer1` sur TLS.

    Set-UMService -Identity MyUMServer1 -UMStartUpMode TLS

