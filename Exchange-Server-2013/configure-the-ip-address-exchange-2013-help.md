---
title: 'Configurer l’adresse IP: Exchange 2013 Help'
TOCTitle: Configurer l’adresse IP
ms:assetid: 100541c1-2297-4c46-9602-b304736541a8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb266940(v=EXCHG.150)
ms:contentKeyID: 50477572
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer l’adresse IP

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-11_

Avant de créer une passerelle IP de messagerie unifiée, vous devez définir l’adresse IP ou le nom de domaine complet sur la passerelle voix sur IP, le PBX IP ou le contrôleur de frontière de session (SBC) que vous utilisez. Ensuite, lorsque vous créez la passerelle IP de messagerie unifiée, vous définissez l’adresse IP ou le nom de domaine complet. Vous pouvez modifier ultérieurement l’adresse IP ou le nom de domaine complet.

Vous pouvez configurer l’adresse IP ou le nom de domaine complet via le Centre d’administration Exchange ou le Shell. Dans le CAE, le champ **Adresse** de la page **Passerelle IP de messagerie unifiée** peut reconnaître une adresse IP IPv4, une adresse IPv6 ou un nom de domaine complet. Vous pouvez également utiliser le paramètre *Address* de la cdmlet **Set-UMIPGateway** dans le Shell pour définir une adresse IP IPv4, une adresse IPv6 ou un nom de domaine complet. Si vous créez une passerelle IP de messagerie unifiée à l’aide d’un nom de domaine complet, vous devez créer les enregistrements HOST A appropriés dans votre zone de recherche directe DNS. Si la configuration DNS de la passerelle IP de messagerie est modifiée, vous devez désactiver, puis activer la passerelle IP de messagerie unifiée pour assurer la bonne mise à jour de sa configuration.

Pour les autres tâches de gestion relatives aux passerelles IP de messagerie unifiée, voir [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour configurer l’adresse IP sur une passerelle IP de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, sélectionnez la passerelle IP de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sur la page **Passerelle IP de messagerie unifiée**, dans le champ **Adresse**, saisissez l’adresse IP de la passerelle VoIP, du PBX IP ou du contrôleur de frontière de session (SBC).

3.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

> [!NOTE]
> Si vous utilisez un nom de domaine complet, et non une adresse IP, pour la passerelle IP de messagerie unifiée, vérifiez que les enregistrements DNS corrects ont été créés.


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer l’adresse IP sur une passerelle IP de messagerie unifiée

Cet exemple configure une passerelle IP de messagerie unifiée nommée `MyUMIPGateway` avec l’adresse IP 10.10.10.1.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

Cet exemple configure une passerelle IP de messagerie unifiée nommée `MyUMIPGateway` avec l’adresse 10.10.10.10, et écoute les requêtes SIP sur le port TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.10 -Port 5061

Cet exemple empêche la passerelle IP de messagerie unifiée nommée `MyUMIPGateway` d’accepter les appels entrants et sortants, définit une adresse IPv6 et permet à la passerelle IP de messagerie unifiée d’utiliser les adresses IPv4 et IPv6.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

