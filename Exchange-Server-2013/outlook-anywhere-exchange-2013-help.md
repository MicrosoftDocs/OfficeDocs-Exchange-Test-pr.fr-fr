---
title: 'Outlook Anywhere: Exchange 2013 Help'
TOCTitle: Outlook Anywhere
ms:assetid: 9026d461-ec6a-4ef5-ba9d-de33030858f3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123741(v=EXCHG.150)
ms:contentKeyID: 50478702
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Anywhere

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Dans Microsoft Exchange Server 2013, la fonctionnalité Outlook Anywhere, anciennement appelée RPC sur HTTP, permet aux clients qui utilisent MicrosoftOutlook 2013, Outlook 2010 ou Outlook 2007 de se connecter à leurs serveurs Exchange à l'extérieur du réseau d'entreprise ou via Internet à l'aide du composant réseau RPC sur HTTP Windows. Cette rubrique décrit la fonctionnalité d'Outlook Anywhere et répertorie les avantages liés à son utilisation.

**Contenu de cette rubrique**

Outlook Anywhere et Exchange 2013

Avantages de l'utilisation d'Outlook Anywhere

Déploiement d'Outlook Anywhere

Gestion d'Outlook Anywhere

Coexistence Outlook Anywhere

Test de la connectivité d'Outlook Anywhere

## Outlook Anywhere et Exchange 2013

Le composant proxy RPC sur HTTP de Windows, que les clients d'Outlook Anywhere utilisent pour se connecter, renvoie les appels de procédures distantes (RPC) avec une couche HTTP. Cela permet au trafic de traverser les pare-feux du réseau sans requérir l'ouverture de ports RPC. Dans Exchange 2013, cette fonction est activée par défaut car Exchange 2013 n’autorise pas la connectivité RPC directe.

## Avantages de l'utilisation d'Outlook Anywhere

Outlook Anywhere offre les avantages suivants aux clients qui utilisent Outlook 2013, Outlook 2010 ou Outlook 2007 pour accéder à votre infrastructure de messagerie Exchange :

  - Les utilisateurs peuvent accéder à distance aux serveurs Exchange depuis Internet.

  - Vous pouvez utiliser les mêmes adresse URL et espace de noms que ceux utilisés pour Outlook Web App et Microsoft Exchange ActiveSync.

  - Vous pouvez utiliser le même certificat de serveur SSL (Secure Sockets Layer) que celui utilisé pour Outlook Web App et Exchange ActiveSync.

  - Les requêtes authentifiées en provenance d'Outlook ne peuvent pas accéder aux serveurs Exchange.

  - Vous n'avez pas besoin d'utiliser un réseau privé virtuel (VPN) pour accéder à des serveurs Exchange sur Internet.

  - Si vous utilisez déjà Outlook Web App avec SSL ou Exchange ActiveSync avec SSL, il n'est pas nécessaire d'ouvrir de ports supplémentaires depuis Internet.

  - Vous pouvez tester la connectivité de bout en bout du client pour les connexions d'Outlook Anywhere et TCP à l'aide de la cmdlet **Test-OutlookConnectivity**.

## Déploiement d'Outlook Anywhere

Dans Microsoft Exchange 2013, Outlook Anywhere est activé par défaut, car toute la connectivité Outlook s'effectue via Outlook Anywhere. La seule tâche consécutive au déploiement que vous devez effectuer pour utiliser correctement Outlook Anywhere consiste à installer un certificat SSL valide sur votre serveur d'accès au client. Les serveurs de boîtes aux lettres de votre organisation ne requièrent que le certificat SSL auto-signé par défaut.

## Gestion d'Outlook Anywhere

Vous pouvez gérer Outlook Anywhere à l'aide du centre d'administration Exchange ou de l'environnement de ligne de commande Exchange Management Shell.

## Coexistence Outlook Anywhere

Si vous envisagez d'installer Exchange 2013 dans un scénario de coexistence avec des versions précédentes d'Exchange Server, vous pouvez toujours avoir des clients Outlook 2003 dans votre organisation. Outlook 2003 n'est pas un client pris en charge pour Exchange 2013.

Avant de déplacer votre espace de noms vers Exchange 2013, vous devez vous assurer que tous les clients Outlook ont été mis à niveau vers la version minimum prise en charge. Outlook 2007 ou version ultérieure est requis pour une connexion Outlook Anywhere à Exchange 2013, même si la boîte aux lettres cible se trouve toujours sur Exchange 2007 ou Exchange 2010.

Si vous utilisez actuellement Outlook Anywhere dans vos environnements Exchange 2007 ou 2010, pour permettre à votre serveur d’accès au client Exchange 2013 de rediriger les connexions vers vos serveurs Exchange 2007/2010, vous devez activer et configurer Outlook Anywhere sur toutes les serveurs d’accès au client Exchange 2007/2010 dans votre organisation. Toutefois, si vous n’utilisez pas Outlook Anywhere dans votre environnement Exchange 2007/2010 et que vous ne souhaitez pas l’utiliser, vous n’avez pas besoin d’activer Outlook Anywhere dans l’ancien environnement. Pour plus d’informations sur l’activation d’Outlook Anywhere sur des serveurs d’accès au client exécutant Exchange Server 2007, consultez la rubrique [Procédure d’activation d’Outlook Anywhere](https://go.microsoft.com/fwlink/p/?linkid=510497). Pour plus d’informations sur l’activation d’Outlook Anywhere sur des serveurs d’accès au client exécutant Exchange Server 2010, consultez la rubrique [Activer Outlook Anywhere](https://go.microsoft.com/fwlink/p/?linkid=510502).

Veillez à choisir NTLM pour l’authentification IIS lorsque vous activez Outlook Anywhere sur le serveur d’accès au client.

Enfin, configurez le nom d’hôte externe Outlook Anywhere pour qu’il pointe vers le nom d’hôte Outlook Anywhere Exchange 2013. Pour plus d’informations sur Exchange Server 2007, consultez la rubrique [Procédure de configuration d’un nom d’hôte externe pour Outlook Anywhere](https://go.microsoft.com/fwlink/p/?linkid=510530). Pour plus d’informations sur Exchange Server 2010, consultez la rubrique [Configurer un nom d’hôte externe pour Outlook Anywhere](https://go.microsoft.com/fwlink/p/?linkid=510531).

## Test de la connectivité d'Outlook Anywhere

Pour tester la connectivité d'Outlook de bout en bout pour un client, effectuez l'une des opérations suivantes :

  - Exécutez la cmdlet **Test-OutlookConnectivity**. Cette dernière teste les connexions d'Outlook Anywhere (RPC sur HTTP). Si le test de la cmdlet échoue, la sortie note l'étape qui a échoué. Pour plus d'informations sur la syntaxe et les paramètres, consultez la rubrique [Test-OutlookConnectivity](https://technet.microsoft.com/fr-fr/library/dd638082\(v=exchg.150\)).

  - Exécutez le test de connectivité d'Outlook Anywhere à l'aide de l'analyseur de connectivité à distance d'Exchange (ExRCA). Après l'exécution de ce test, vous recevez un récapitulatif détaillé indiquant où le test a échoué et les mesures à prendre pour résoudre les problèmes. Pour plus d'informations, consultez la rubrique [Analyseur de connectivité à distance Exchange](exchange-remote-connectivity-analyzer-exchange-2013-help.md).

Les deux tests tentent de se connecter via Outlook Anywhere après avoir obtenu les paramètres du serveur de la part du service de découverte automatique. La vérification de bout en bout inclut les éléments suivants :

  - Test de connectivité de découverte automatique

  - Validation de DNS

  - Validation des certificats (déterminer si le nom du certificat correspond au site web, si le certificat a expiré et s'il est approuvé)

  - Vérification de la configuration adéquate du pare-feu (ExRCA vérifie la configuration générale du pare-feu. La cmdlet teste la configuration du pare-feu Windows.)

  - Vérification de la connectivité des clients via une connexion à la boîte aux lettres de l'utilisateur

