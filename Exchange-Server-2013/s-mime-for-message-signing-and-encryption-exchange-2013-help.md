---
title: 'S/MIME pour la signature et le chiffrement des messages: Exchange 2013 Help'
TOCTitle: S/MIME pour la signature et le chiffrement des messages
ms:assetid: 887c710b-0ec6-4ff0-8065-5f05f74afef3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn626158(v=EXCHG.150)
ms:contentKeyID: 61212673
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# S/MIME pour la signature et le chiffrement des messages

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

S/MIME (Secure/Multipurpose Internet Mail Extensions) est une méthode (ou plutôt un protocole) largement acceptée, utilisée pour l’envoi de messages chiffrés et signés numériquement. S/MIME vous permet de chiffrer les e-mails et de les signer numériquement. Lorsque vous utilisez S/MIME dans un message électronique, les personnes qui reçoivent ce dernier savent que ce qu’elles voient dans leur boîte de réception est le message exact tel qu’il a été envoyé par l’expéditeur. Elles savent aussi que le message provient de l’expéditeur indiqué et pas de quelqu’un prétendant l’être. Pour ce faire, S/MIME fournit des services de sécurité de chiffrement tels que l’authentification, l’intégrité des messages et la non-répudiation de l’origine (à l’aide de signatures numériques). Le protocole permet également d’améliorer la confidentialité et la sécurité des données (à l’aide du chiffrement) de la messagerie électronique. Pour en savoir plus sur l’histoire et l’architecture du protocole S/MIME dans le cadre de la messagerie, consultez la rubrique [Présentation du protocole S/MIME](https://go.microsoft.com/fwlink/?linkid=393948).

En tant qu’administrateur, vous pouvez activer la sécurité basée sur S/MIME dans votre organisation si vous disposez de boîtes aux lettres dans Exchange 2013 SP1 ou Exchange Online, qui fait partie d’Office 365. Suivez les conseils des rubriques dont les liens sont fournis et utilisez l’environnement de ligne de commande Exchange Management Shell pour configurer S/MIME. Pour utiliser S/MIME dans des versions prises en charge d’Outlook ou d’ActiveSync, avec Exchange 2013 SP1 ou Exchange Online, les utilisateurs de votre organisation doivent disposer de certificats émis à des fins de signature et de chiffrement, et des données publiées sur votre service de domaine Active Directory sur site (AD DS). Votre service AD DS doit être situé sur des ordinateurs se trouvant dans un emplacement physique que vous contrôlez, et non dans un emplacement distant ou sur un service en nuage quelque part sur Internet. Pour plus d’informations sur le service AD DS, consultez la rubrique [Services de domaine Active Directory](https://go.microsoft.com/fwlink/?linkid=394064).

## Scénarios pris en charge et considérations techniques

Si votre organisation utilise Exchange 2013 SP1 ou Exchange Online, vous pouvez configurer S/MIME en vue de l’utilisation de l’un des points de fin suivants :

  - Outlook 2010

  - Outlook 2013

  - Outlook Web App

  - Exchange ActiveSync (EAS)

Les étapes à suivre pour configurer S/MIME avec chacun de ces points de fin sont légèrement différentes selon celui que vous choisissez. En règle générale, vous devez accomplir les tâches suivantes :

  - Installez une autorité de certification basée sur Windows et configurez une infrastructure à clé publique pour émettre des certificats S/MIME. Les certificats émis par des fournisseurs de certificats tiers sont aussi pris en charge. Pour plus d’informations, consultez la rubrique [Vue d’ensemble des services de certificats Active Directory](https://technet.microsoft.com/library/hh831740.aspx).

  - Publier le certificat utilisateur dans un compte AD DS local dans les attributs UserSMIMECertificate et/ou UserCertificate.

  - Pour les organisations Exchange Online, synchroniser les certificats utilisateur entre le service AD DS et Azure Active Directory en utilisant une version appropriée de DirSync. Ces certificats sont ensuite synchronisés entre Azure Active Directory et l’annuaire Exchange Online et utilisés lors du chiffrement d’un message envoyé à un destinataire.

  - Définir une collection de certificats virtuelle afin de valider S/MIME. Cette information est utilisée lorsqu’OWA valide la signature d’un e-mail et vérifie qu’il a été signé par un certificat approuvé.

  - Définir le point de fin Outlook ou EAS pour qu’il utilise S/MIME.

## Configuration de S/MIME avec Outlook Web App

La configuration de S/MIME pour Exchange 2013 SP1 ou Exchange Online avec Outlook Web App implique les étapes clés suivantes :

1.  [Configurer les paramètres S/MIME pour Outlook Web App](configure-s-mime-settings-for-outlook-web-app-exchange-2013-help.md)

2.  [Configuration d’une collection de certificats virtuelle pour la validation des certificats S/MIME](set-up-virtual-certificate-collection-to-validate-s-mime-exchange-2013-help.md)

3.  [Synchronisation des certificats utilisateur vers Office 365 pour S/MIME](https://technet.microsoft.com/fr-fr/library/dn626159\(v=exchg.150\)) Cette étape s’applique à Exchange Online uniquement.

## Technologies liées au chiffrement des messages

Comme la sécurité des messages devient de plus en plus importante, les administrateurs doivent comprendre les principes et les concepts de la messagerie sécurisée. Cet aspect est particulièrement important en raison de la diversité croissante des technologies liées à la protection, comme S/MIME, désormais disponibles. Pour plus d’informations sur S/MIME et son fonctionnement dans un contexte de messagerie électronique, consultez la rubrique [Présentation du protocole S/MIME](https://go.microsoft.com/fwlink/?linkid=393948). Diverses technologies de chiffrement fonctionnent ensemble pour assurer la protection des messages au repos et en transit. S/MIME peut utiliser simultanément les technologies suivantes, sans toutefois en dépendre :

  -  
    **Transport Layer Security (TLS)** chiffre le tunnel ou le routage entre les serveurs de messagerie pour empêcher la surveillance et l’écoute électroniques.

  -  
    **Secure Sockets Layer (SSL)** chiffre la connexion entre les clients de messagerie et les serveurs Office 365.

  -  
    **BitLocker** chiffre les données sur un disque dur dans un centre de données. Ainsi, si une personne obtient un accès non autorisé, elle ne peut pas lire les données.

## S/MIME comparé au chiffrement de messages Office 365

S/MIME requiert un certificat et une infrastructure de publication qui est souvent utilisée dans les situations entreprise-entreprise et entreprise-client. L’utilisateur contrôle les clés de chiffrement dans S/MIME et peut choisir de les utiliser ou non pour chaque message qu’il envoie. Les programmes de messagerie tels qu’Outlook recherchent un emplacement d’autorité de certification racine approuvée pour effectuer la signature numérique et la vérification de la signature. Le chiffrement de messages Office 365 est un service de chiffrement basé sur des stratégies qui peut être configuré par un administrateur, et non par un utilisateur individuel, pour chiffrer le courrier envoyé à l’intérieur ou à l’extérieur de l’organisation. Il s’agit d’un service en ligne s’appuyant sur Azure Rights Management (RMS) et ne reposant pas sur une infrastructure à clé publique. Le chiffrement de messages Office 365 fournit également des fonctionnalités supplémentaires, comme la possibilité de personnaliser le courrier avec la marque de l’organisation. Pour plus d’informations sur le chiffrement de messages Office 365, consultez la rubrique [Chiffrement dans Office 365](https://go.microsoft.com/fwlink/?linkid=392525).

## Plus d’informations

[Outlook Web App](outlook-web-app-exchange-2013-help.md)

[Courrier sécurisé (2000)](https://technet.microsoft.com/fr-fr/library/cc962043.aspx)

