---
title: 'Définir les infos d’identif. à utiliser avec l’outil de dépann. de MU Exchange'
TOCTitle: Définir les informations d’identification à utiliser avec l’outil de dépannage de la messagerie unifiée Exchange
ms:assetid: 542b7718-9345-40cc-bcb2-e307e70a1fa2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff630916(v=EXCHG.150)
ms:contentKeyID: 56269366
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir les informations d’identification à utiliser avec l’outil de dépannage de la messagerie unifiée Exchange

 

_**Sapplique à :** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

L’outil de dépannage de la messagerie unifiée de Microsoft Exchange 2010 est une cmdlet de l’environnement de ligne de commande Exchange Management Shell nommée **Test-ExchangeUMCallFlow**. Vous pouvez utiliser cette cmdlet pour diagnostiquer des erreurs de configuration inhérentes à des scénarios de répondeur automatique et pour tester si la messagerie vocale fonctionne correctement pour les déploiements de messagerie unifiée Microsoft Exchange Server 2010 Service Pack 1 (SP1) (ou ultérieur) locaux et entre différents locaux à la fois. Vous pouvez vous servir de cette cmdlet pour des déploiements avec Microsoft Office Lync Server 2010 (ou ultérieur) ou pour des déploiements de messagerie unifiée avec des passerelles VoIP, des PBX IP ou des contrôleurs de frontière de session.

Par défaut, lorsque vous exécutez l’outil de dépannage de la messagerie unifiée, celui-ci utilise les informations d’identification que vous avez saisies pour vous connecter à l’ordinateur. Les informations d’identification utilisées sont celles spécifiées pour l’appelant. Vous devez définir ou spécifier les informations d’identification à utiliser lorsque vous exécutez l’outil de dépannage de la messagerie unifiée en mode `SIPClient`. Toutefois, vous n’avez pas à définir les informations d’identification lorsque vous exécutez l’outil de dépannage de la messagerie unifiée en mode `Gateway`.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Serveur de messagerie unifiée » ou « Services de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Assurez-vous que votre organisation Exchange 2010 ou Exchange 2013 remplit les conditions suivantes :
    
      - Un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, voir [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).
    
      - Une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).
    
      - Une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, voir [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).
    
      - Un serveur de messagerie UNIFIÉE de Exchange 2010 a été ajouté pour le plan de numérotation de messagerie UNIFIÉE. Si vous utilisez Exchange 2013 avec Lync Server, ajoutez tous les accès Client et les serveurs de boîtes aux lettres pour les plans de numérotation URI SIP. Pour obtenir la procédure détaillée, voir [Ajouter un serveur de messagerie UNIFIÉE à un Plan de numérotation](https://go.microsoft.com/fwlink/p/?linkid=313051) ou [Ajouter des serveurs de boîtes aux lettres et accès au Client à un plan de numérotation URI SIP](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md).

  - Installez l’outil de dépannage de la messagerie unifiée. Pour obtenir la procédure détaillée, voir [Installer l’outil de dépannage de la messagerie unifiée Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).
    
    > [!NOTE]
    > Si vous utilisez l’outil Résolution des problèmes de messagerie UNIFIÉE en mode de <code>SIPClient</code> , il existe plusieurs autres Office Communications Server 2007 R2 ou Microsoft Lync Server des exigences et conditions préalables. Pour plus d’informations, consultez <a href="https://go.microsoft.com/fwlink/p/?linkid=311961">liste de vérification : déploiement Office Communications Server 2007 R2 et la messagerie unifiée Exchange 2010</a> ou <a href="checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md">Liste de contrôle : intégration de la messagerie unifiée d'Exchange 2013 à Lync Server</a>.


  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Définir les informations d’identification à utiliser avec l’outil de dépannage de la messagerie unifiée (MU)

1.  À partir du menu **Démarrer**, ouvrez l’**outil de dépannage de la messagerie unifiée Microsoft Exchange 2010**.

2.  À l’invite de la fenêtre **Outil de dépannage de la messagerie unifiée Microsoft Exchange 2010**, saisissez ce qui suit, puis appuyez sur la touche Entrée.
    
        $cred=Get-Credential

3.  Dans la fenêtre **Demande d’informations d’identification Windows PowerShell**, saisissez un nom d’utilisateur/de domaine et un mot de passe, puis cliquez sur **OK**.

4.  Dans la fenêtre de l’**outil de dépannage de la messagerie unifiée de Microsoft Exchange 2010**, indiquez les paramètres de cmdlet nécessaires pour tester le flux d’appels. Par exemple :
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

