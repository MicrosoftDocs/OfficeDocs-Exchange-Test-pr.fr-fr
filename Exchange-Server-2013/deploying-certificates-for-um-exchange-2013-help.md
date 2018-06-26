---
title: 'Déploiement de certificats pour la messagerie unifiée: Exchange 2013 Help'
TOCTitle: Déploiement de certificats pour la messagerie unifiée
ms:assetid: 95658f6f-eac2-4674-90e7-f2d3f25c5242
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee681661(v=EXCHG.150)
ms:contentKeyID: 52062983
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déploiement de certificats pour la messagerie unifiée

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-04-29_

L'authentification TLS (Transport Layer Security) mutuelle permet d'activer la messagerie unifiée pour chiffrer les données échangées entre vos serveurs Microsoft Exchange 2013 et des passerelles VoIP, PBX IP, contrôleurs de frontière de session (SBC) et Microsoft Lync Server. Les certificats lient l'identité du propriétaire de certificat à une paire de clés électroniques (publique et privée) utilisées pour chiffrer et signer numériquement les informations.

Si vous utilisez des plans de numérotation de type Sécurisé ou Sécurisé SIP dans votre organisation Exchange 2010, vous devez importer les certificats utilisés sur vos serveurs d'accès au client Exchange 2013 exécutant le service de routeur d'appels de messagerie unifiée Microsoft Exchange ainsi que sur les serveurs de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange. Pour les services de messagerie unifiée et de routeur d'appels de messagerie unifiée, vous pouvez utiliser l'un des certificats suivants :

  - Un certificat (Exchange) auto-signé

  - Un certificat d'infrastructure à clé publique (PKI) interne

  - Un certificat commercial tiers

Par défaut, quand vous installez une messagerie unifiée, un certificat auto-signé est créé et utilisé. Vous pouvez utiliser ce certificat auto-signé avec des passerelles VoIP, PBX IP et SBC, mais pas lorsque vous intégrez une messagerie unifiée avec Lync Server. Si vous déployez des certificats à utiliser avec Lync Server, vous devez utiliser l'Assistant Certificat Exchange ou la cmdlet **New-ExchangeCertificate** pour obtenir un certificat émis par une autorité de certification interne ou PKI (Infrastructure à clé publiques). Vous pouvez également acheter un certificat commercial ou tiers approuvé tant par la messagerie unifiée que par Lync Server.

## Déploiement de certificats pour les passerelles VoIP, PBX IP et SBC

Pour permettre à la messagerie unifiée de chiffrer les données échangées entre les passerelles VoIP, les PBX IP et les SBC, vous devez procéder comme suit :

  - Utilisez le certificat de messagerie unifiée auto-signé, créer une demande de certificat Exchange et obtenir un certificat PKI, ou acheter un certificat commercial tiers utilisable pour l'authentification TLS mutuelle entre la messagerie unifiée et les passerelles VoIP, PBX IP et SBC.

  - Importez le certificat à utiliser sur tous les serveurs d'accès au client et de boîtes aux lettres au sein de votre organisation.

  - Activez le certificat que les services de messagerie unifiée doivent utiliser.

  - Importez le certificat sur vos passerelles VoIP, PBX IP et SBC.

  - Configurez le plan de numérotation de messagerie unifiée en mode Sécurisé ou Sécurisé SIP.

  - Configurez le mode de démarrage de la messagerie unifiée sur les serveurs d'accès au client et de boîtes aux lettres au sein de votre organisation.

  - Créez les passerelles IP de messagerie unifiée avec un nom de domaine complet (FQDN).

  - Configurez le port d'écoute sur les passerelles IP de messagerie unifiée pour utiliser le port TLS 5061.

  - Redémarrez le service de routage d'appel de messagerie unifiée sur tous les serveurs d'accès au client, puis redémarrez le service de messagerie unifiée Microsoft Exchange sur tous les serveurs de boîtes aux lettres.

## Déploiement de certificats pour Lync Server

Pour chiffrer les données échangées entre la messagerie unifiée et Lync Server, vous devez procéder comme suit :

  - Créez un demande de certificat Exchange et obtenez un certificat PKI interne, ou achetez un certificat commercial tiers. Le certificat doit être approuvé tant par la messagerie unifiée que par Lync Server.

  - Importez le certificat à utiliser sur tous les serveurs d'accès au client et de boîtes aux lettres au sein de votre organisation.

  - Activez le certificat que les services de messagerie unifiée doivent utiliser.

  - Importez le certificat sur les ordinateurs exécutant Lync Server.

  - Configurez le plan de numérotation de messagerie unifiée URI SIP en mode Sécurisé ou Sécurisé SIP.

  - Configurez le mode de démarrage de la messagerie unifiée sur les serveurs d'accès au client et de boîtes aux lettres au sein de votre organisation.

  - Exécutez OcsUmUtil.exe à partir d'un ordinateur Lync Server.

  - Redémarrez le service de routage d'appel de messagerie unifiée sur tous les serveurs d'accès au client, puis redémarrez le service de messagerie unifiée Microsoft Exchange sur tous les serveurs de boîtes aux lettres au sein de votre organisation. Pour plus d'informations, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

  - Redémarrez le service frontal Lync Server sur tous les serveurs Lync faisant partie d'un pool frontal Enterprise Edition ou redémarrez les serveurs frontaux Standard Edition. Vous pouvez utiliser la cmdlet **Stop-CsWindowsService** pour arrêter les services Lync Server, et la cmdlet **Start-CsWindowsService** pour les démarrer.
    
    Les cmdlets **Start-CsWindowsService** et **Stop-CsWindowsService** sont similaires aux cmdlets Windows PowerShell génériques **Start-Service** et **Stop-Service**. Si vous le souhaitez, vous pouvez utiliser les cmdlets **Start-Service** et **Stop-Service** pour démarrer et arrêter un service Lync Server. Toutefois, les cmdlets **Start-CsWindowsService** et **Stop-CsWindowsService** incluent un paramètre *ComputerName* qui facilite l'arrêt et le démarrage d'un service Lync Server sur un ordinateur distant. Pour ce faire, incluez le paramètre *ComputerName* suivi du nom de domaine complet (FQDN) de l'ordinateur distant. Les cmdlets **Start-Service** et **Stop-Service** n'utilisent pas de paramètre comparable.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Pour intégrer pleinement la messagerie unifiée et Lync Server, vous devez également exécuter le script ExchUcUtil.ps1 sur un serveur d'accès au client ou un serveur de boîtes aux lettres au sein de votre organisation.</td>
    </tr>
    </tbody>
    </table>

