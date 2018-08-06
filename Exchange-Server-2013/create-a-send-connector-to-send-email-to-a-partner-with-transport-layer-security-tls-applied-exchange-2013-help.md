---
title: 'Créer un connecteur d’envoi de courrier électronique à un partenaire avec TLS | Microsoft Docs'
TOCTitle: Créer un connecteur d’envoi pour envoyer un courriel à un partenaire, avec le protocole TLS (TLS)
ms:assetid: ff2abefc-dd3e-4431-b947-df942fbf82d9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657514(v=EXCHG.150)
ms:contentKeyID: 50479653
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer un connecteur d’envoi pour envoyer un courrier électronique à un partenaire, avec le protocole TLS (TLS)

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-15_

Si vous voulez être certain d’établir des communications sûres et chiffrées avec un partenaire, vous pouvez créer un connecteur d’envoi configuré pour forcer l’application de TLS (Transport Layer Security) aux messages envoyés à un domaine partenaire. TLS permet une communication sécurisée sur Internet.

Intéressé par des scénarios où cette procédure est utilisée ? Consultez les rubriques suivantes :

  - [Configuration du flux de messagerie et de l’accès au client](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Connecteurs d’envoi » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Voir [Déployer une nouvelle installation d’Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si vous commencez votre installation. À l’issue de l’installation, vous pouvez utiliser les étapes de cette rubrique pour créer votre connecteur d’envoi.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser le Centre d’administration Exchange (CAE) pour créer un connecteur d’envoi afin d’envoyer un courrier électronique à un partenaire en appliquant TLS

Pour créer un connecteur d’envoi dans ce scénario, ouvrez une session dans le Centre d’administration Exchange (CAE) et procédez comme suit :

1.  Dans le Centre d’administration Exchange, accédez à **Flux de messagerie** \> **Connecteurs d’envoi**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans l’Assistant **Nouveau connecteur d’envoi**, indiquez un nom pour le connecteur d’envoi et sélectionnez **Partenaire** comme **Type**. Lorsque vous sélectionnez **Partenaire**, le connecteur est configuré pour permettre les connexions uniquement avec des serveurs qui effectuent l’authentification avec des certificats TLS. Cliquez sur **Suivant**.

3.  Vérifiez si **Enregistrement MX associé au domaine du destinataire** est sélectionné, ce qui spécifie que ce connecteur utilise le système DNS (Domain Name System) pour acheminer les messages. Cliquez sur **Suivant**.

4.  Sous **Espace d’adressage**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Ajouter un domaine**, vérifiez que SMTP apparaît dans la liste **Type**. Pour **Nom de domaine complet (FQDN)**, entrez le nom de votre domaine partenaire. Cliquez sur **Enregistrer**.

5.  Pour **Serveur source**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Sélectionner un serveur**, sélectionnez un serveur de boîtes aux lettres qui sera utilisé pour envoyer des messages à l’Internet via le serveur d’accès au client puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Après avoir sélectionné le serveur, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Cliquez sur **OK**.

6.  Cliquez sur **Terminer**.

Une fois créé, le connecteur d’envoi apparaît dans la liste des connecteurs d’envoi.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement créé un connecteur d’envoi pour envoyer un courrier électronique à un partenaire en appliquant TLS, envoyez un message provenant d’un utilisateur dans votre organisation à un destinataire de l’organisation partenaire. Si le destinataire reçoit le message, le connecteur a été créé sans problème.

## Pour plus d'informations

[Créer un connecteur d’envoi pour les messages électroniques envoyés vers Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Créer un connecteur d’envoi pour router le courrier sortant via un hôte actif](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

