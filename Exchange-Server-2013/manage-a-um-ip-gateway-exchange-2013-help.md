---
title: "Gestion d'une passerelle IP de messagerie unifiée: Exchange 2013 Help"
TOCTitle: Gestion d'une passerelle IP de messagerie unifiée
ms:assetid: 387e540f-8c59-42d2-a423-99fcf97e00aa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997283(v=EXCHG.150)
ms:contentKeyID: 50477925
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMIPGatewayGeneralPropertyPageControl
ms.translationtype: HT
---

# Gestion d'une passerelle IP de messagerie unifiée

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-21_

Après avoir créé une passerelle IP de messagerie unifiée, vous pouvez afficher ou configurer divers paramètres. Par exemple, vous pouvez configurer l'adresse IP ou un nom de domaine complet, ainsi que les paramètres des appels sortants, et activer ou désactiver l'indicateur d'attente des messages.

Pour les autres tâches de gestion relatives aux passerelles IP de messagerie unifiée, consultez la rubrique [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).

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

## Utiliser le Centre d'administration Exchange (CAE) pour afficher ou configurer des propriétés de la passerelle IP de messagerie unifiée

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**. Dans l'affichage Liste, sélectionnez la passerelle IP de messagerie unifiée à gérer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  
    
    L'onglet **Passerelle IP de messagerie unifiée** permet d'afficher et de configurer les paramètres de la passerelle IP de messagerie unifiée. Vous pouvez également configurer les paramètres suivants :
    
      - **État**   Ce champ en affichage seul indique l'état de la passerelle IP de messagerie unifiée.
    
      - **Nom**   Cette zone de texte permet de spécifier un nom unique pour la passerelle IP de messagerie unifiée. Il s'agit du nom complet qui apparaît dans l'EAC. Si vous devez modifier le nom complet de la passerelle IP de messagerie unifiée après sa création, vous devez d'abord supprimer la passerelle IP de messagerie unifiée existante, puis en créer une autre avec le nom approprié. Le nom de passerelle IP de messagerie unifiée est obligatoire mais utilisé à des fins d'affichage uniquement. Dans la mesure où votre organisation peut utiliser plusieurs passerelles IP de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour ces passerelles. La longueur maximale d'un nom de passerelle IP de messagerie unifiée est de 64 caractères pouvant contenir des espaces.
    
      - **Adresse**   Vous pouvez configurer une passerelle IP de messagerie unifiée soit avec une adresse IP soit avec un nom de domaine complet. Utilisez cette boîte de dialogue pour spécifier l'adresse IP ou le nom de domaine complet configuré sur la passerelle VoIP, au standard privé (PBX) SIP, PBX IP ou SBC.
        
        Vous pouvez entrer des caractères alphabétiques et numériques dans cette zone. Les adresses IPv4, IPv6 et les adresses avec un nom de domaine complet sont prises en charge. Si vous utilisez un nom de domaine complet, vous devez également vous assurer que vous avez correctement configuré un enregistrement d'hôte DNS pour la passerelle VoIP afin de résoudre correctement le nom d'hôte en adresse IP. De même, si vous utilisez un nom de domaine complet à la place d'une adresse IP et si la configuration DNS de la passerelle IP de messagerie unifiée est modifiée, vous devez désactiver la passerelle IP de messagerie unifiée, puis l'activer pour garantir une mise à jour correcte des informations de configuration de cette passerelle IP de messagerie unifiée.
        
        Si vous souhaitez utiliser l'authentification TLS (Transport Layer Security) mutuelle entre une passerelle IP de messagerie unifiée et un plan de numérotation fonctionnant en mode Sécurisé SIP ou en mode Sécurisé, vous devez configurer la passerelle IP de messagerie unifiée avec un nom de domaine complet. Vous devez également la configurer pour écouter le port 5061 et vérifier que les passerelles IP ou les IP PBX ont également été configuré(e)s pour écouter les demandes TLS mutuelles sur le port 5061. Pour configurer une passerelle IP de messagerie unifiée, exécutez la commande suivante : `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
    
      - **Autoriser les appels sortants via cette passerelle IP de messagerie unifiée**   Activez cette case à cocher pour autoriser la passerelle IP de messagerie unifiée à accepter et traiter les appels sortants. Ce paramètre n'affecte pas les transferts d'appels ou les appels entrants en provenance d'une passerelle VoIP.
        
        Ce paramètre est activé par défaut lors de la création de la passerelle IP de messagerie unifiée. Si vous désactivez ce paramètre, les utilisateurs associés au plan de numérotation ne pourront pas passer d'appels sortants via la passerelle VoIP, le PBX IP ou le SBC défini dans le champ **Adresse**.
    
      - **Autoriser l'indicateur d'attente des messages**   Activez cette case à cocher pour autoriser l'envoi de notifications de messagerie vocale aux utilisateurs pour les appels pris par la passerelle IP de messagerie unifiée. Ce paramètre autorise la passerelle IP de messagerie unifiée à recevoir et envoyer des messages SIP NOTIFY pour les utilisateurs. Ce paramètre est activé par défaut et autorise l'envoi de notifications de message en attente aux utilisateurs.
        
        L'indicateur de message en attente peut être n'importe quel mécanisme indiquant l'existence d'un message nouveau ou non écouté. L'indication de l'arrivée d'un nouveau message vocal peut être trouvée dans la Boîte de réception d'applications clientes telles que Outlook et Outlook Web App. Cette indication peut être un SMS ou un message texte envoyé à un téléphone portable enregistré, ou un appel sortant émis à partir d'un serveur Exchange à un numéro préconfiguré ou encore l'illumination d'un voyant sur le téléphone fixe de l'utilisateur.

## Utiliser le shell pour configurer les propriétés de la passerelle IP de messagerie unifiée

Cet exemple modifie l'adresse IP d'une passerelle IP de messagerie unifiée nommée `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

Cet exemple empêche la passerelle IP de messagerie unifiée appelée `MyUMIPGateway` d'accepter les appels entrants et empêche les appels sortants.

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com -Status 2 -OutcallsAllowed $false

Cet exemple permet à la passerelle IP de messagerie unifiée de fonctionner comme simulateur de passerelle VoIP. Vous pouvez l'utiliser avec la cmdlet **Test-UMConnectivity**.

    Set-UMIPGateway -Identity MyUMIPGateway -Simulator $true

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il existe une période de latence avant que toutes les modifications que vous apportez à la configuration d'une passerelle IP de messagerie unifiée se répercutent sur tous les serveurs Exchange qui se trouvent dans le même plan de numérotation de messagerie unifiée que la passerelle IP de messagerie unifiée.</td>
</tr>
</tbody>
</table>


Cet exemple empêche la passerelle IP de messagerie unifiée nommée `MyUMIPGateway` d'accepter les appels entrants et empêche également les appels sortants, définit une adresse IPv6 et permet à la passerelle IP de messagerie unifiée d'utiliser les adresses IPv4 et IPv6.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## Utiliser le shell pour afficher les propriétés de la passerelle IP de messagerie unifiée

Cet exemple affiche une liste mise en forme de toutes les passerelles IP de messagerie unifiée dans la forêt Active Directory.

    Get-UMIPGateway |Format-List

Cet exemple de code affiche les propriétés d'une passerelle IP de messagerie unifiée nommée `MyUMIPGateway`.

    Get-UMIPGateway -Identity MyUMIPGateway

Cet exemple affiche toutes les passerelles IP de messagerie unifiée, y compris les simulateurs de passerelle VoIP dans la forêt Active Directory.

    Get-UMIPGateway -IncludeSimulator $true

