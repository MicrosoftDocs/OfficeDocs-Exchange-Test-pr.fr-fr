---
title: 'Paramètres du périphérique Exchange ActiveSync avec des déploiements hybrides Exchange: Exchange 2013 Help'
TOCTitle: Paramètres du périphérique Exchange ActiveSync avec des déploiements hybrides Exchange
ms:assetid: 77f7cd72-2a8a-467e-9ffd-b93f5eeb2f69
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn931281(v=EXCHG.150)
ms:contentKeyID: 64965200
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Paramètres du périphérique Exchange ActiveSync avec des déploiements hybrides Exchange

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2016-01-27_

Les appareils Exchange ActiveSync sont maintenant reconfigurés automatiquement lorsqu’une boîte aux lettres est déplacée d’une organisation Exchange locale vers Office 365. Exchange ActiveSync détecte le nouvel emplacement de la boîte aux lettres dans Office 365 et met à jour sa configuration pour communiquer directement avec Office 365. L’appareil Exchange ActiveSync ne tentera pas de contacter le serveur Exchange local après avoir été correctement redirigé vers Office 365. À quelques exceptions près (plus de détails ci-dessous), l’utilisateur n’a plus besoin de configurer manuellement son appareil pour que la messagerie continue à fonctionner.

Si vous souhaitez déplacer une boîte aux lettres vers Office 365, consultez la rubrique [Déplacement de boîtes aux lettres entre des organisations locales et Exchange Online dans des déploiements hybrides](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md).

Pour plus d’informations sur les déploiements hybrides, consultez la rubrique [Déploiements hybrides Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

Pour utiliser la redirection automatique, vos serveurs locaux doivent exécuter les dernières versions d’Exchange 2010, Exchange 2013, Exchange 2016, ou des versions ultérieures. Vous devez également avoir utilisé le [Assistant de configuration hybride](hybrid-configuration-wizard-exchange-2013-help.md) pour configurer votre déploiement hybride. La fonctionnalité de redirection d’Exchange ActiveSync utilise l’URL cible Outlook sur le web qui est définie sur l’objet de relation d’organisation. Cet objet est configuré lors de l’exécution de l’assistant de configuration hybride.

Si votre organisation répond aux conditions décrites ci-dessus, les appareils mobiles doivent automatiquement être redirigés vers Office 365 lorsque la boîte aux lettres d’un utilisateur est déplacée, sans configuration supplémentaire. Pour une meilleure expérience, assurez-vous que les appareils mobiles de vos utilisateurs exécutent les versions les plus récentes de leurs systèmes d’exploitation et clients de messagerie. Certains appareils mobiles, tels que ceux exécutant le système d’exploitation Android, peuvent prendre plus de temps que prévu pour être redirigés. En outre, certains appareils peuvent interpréter de façon incorrecte les instructions de redirection d’Exchange ActiveSync 451 envoyées par Exchange. Pour ces appareils, les utilisateurs devront toujours reconfigurer ou recréer manuellement le compte de messagerie sur l’appareil. Si vous avez des questions relatives à la prise en charge de la redirection d’Exchange ActiveSync 451 par un appareil, contactez le fabricant de l’appareil.

La redirection automatique d’Exchange ActiveSync n’est pas prise en charge dans les scénarios suivants :

  - Déplacement des boîtes aux lettres d’Office 365 vers une organisation Exchange locale.

  - Déplacement de boîtes aux lettres entre des organisations Exchange locales.

  - Déplacement de boîtes aux lettres de serveurs Exchange 2007 vers Office 365.

