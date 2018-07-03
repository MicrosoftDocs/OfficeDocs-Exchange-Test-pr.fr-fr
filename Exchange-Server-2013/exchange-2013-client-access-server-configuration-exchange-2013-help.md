---
title: 'Configuration du serveur d’accès au client Exchange 2013: Exchange 2013 Help'
TOCTitle: Configuration du serveur d’accès au client Exchange 2013
ms:assetid: 01432ae4-2a00-44a4-a4dd-4eb8d7e6cfae
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh529912(v=EXCHG.150)
ms:contentKeyID: 50477418
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du serveur d’accès au client Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-07-25_

Après avoir installé le serveur d’accès au client Exchange 2013, vous pouvez exécuter diverses tâches de configuration. Bien que le serveur d’accès au client dans Exchange 2013 ne gère pas le traitement des protocoles clients, plusieurs paramètres doivent lui être appliqués, notamment les paramètres de répertoire virtuel et de certificat.

## Configuration des certificats de serveur

Dans Exchange 2013, vous pouvez utiliser l'Assistant Certificat pour demander un certificat numérique à une autorité de certification. Lorsque vous l’aurez obtenu, vous devrez l’installer sur le serveur d’accès au client.

Il est inutile d’installer les certificats numériques sur les serveurs de boîtes aux lettres de votre organisation. En effet, un certificat auto-signé est installé par défaut sur les serveurs de boîtes aux lettres. Il n’a pas besoin d’être remplacé. Les serveurs d'accès au client de votre organisation approuvent implicitement le certificat auto-signé sur les serveurs de boîtes aux lettres. Pour plus d'informations, consultez la rubrique [Interface utilisateur de la gestion de certificats Exchange 2013](exchange-2013-certificate-management-ui-exchange-2013-help.md).

## Configuration des répertoires virtuels

Vous pouvez configurer plusieurs paramètres dans les répertoires virtuels pour le carnet d'adresses en mode hors connexion, les services web Exchange, Exchange ActiveSync, Outlook Web App et le Centre d'administration Exchange. Pour plus d'informations sur la gestion des répertoires virtuels, consultez la rubrique [Gestion des répertoires virtuels](virtual-directory-management-exchange-2013-help.md). Vous pouvez configurer les répertoires virtuels à l'aide des commandes suivantes.

  - Exchange 2013 fournit deux ensembles de paramètres de connectivité HTTP pour la configuration Outlook Anywhere afin que les administrateurs puissent configurer un point de terminaison interne et un point de terminaison externe.
    
    Pour configurer Outlook Anywhere avec une URL unique pour la connectivité, vous devez indiquer le nom d'hôte, si SSL est requis et un package d'authentification à l'aide de la commande suivante dans Exchange Management Shell :
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    
    Vous pouvez également indiquer un point de terminaison accessible en externe en utilisant la commande suivante dans Exchange Management Shell :
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -ExternalHostname "externalServer.company.com" -ExternalClientAuthenticationMethod Basic -ExternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    
    > [!TIP]
    > Bien qu'Exchange 2013 prenne en charge Negotiate pour l'authentification HTTP Outlook Anywhere, vous ne devez l'utiliser que lorsque tous les serveurs de l'environnement exécutent Exchange 2013.


  - Pour configurer Exchange ActiveSync, exécutez la commande suivante.
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2013>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl "https://mail.contoso.com/Microsoft-Server-ActiveSync"

  - Pour configurer le répertoire virtuel des services web Exchange, exécutez la commande suivante.
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalUrl https://mail.contoso.com/EWS/Exchange.asmx

  - Pour configurer le carnet d'adresses en mode hors connexion, exécutez la commande suivante.
    
        Set-OABVirtualDirectory -Identity "<CAS2013>\OAB (Default Web Site)" -ExternalUrl "https://mail.contoso.com/OAB"

  - Pour configurer le point de connexion de service, exécutez la commande suivante.
    
        Set-ClientAccessServer -Identity <CAS2013> -AutoDiscoverServiceInternalURI https://autodiscover.contoso.com/AutoDiscover/AutoDiscover.xml

## Mettre à niveau à partir d'un accès client Exchange 2007 et 2010

Cette section vous aide à configurer l'accès externe aux protocoles sur le serveur d'accès au client Exchange 2013. Exécutez les commandes Exchange Management Shell dans la section Répertoires virtuels de configuration ci-dessus, ainsi que les commandes suivantes.

Vous devrez exécuter les commandes suivantes pour configurer les répertoires virtuels pour Exchange 2013.

1.  Pour configurer une URL externe pour Outlook Web App, exécutez la commande suivante dans Exchange Management Shell.
    
        Set-OwaVirtualDirectory "<CAS2013>\OWA (Default Web Site)" -ExternalUrl https://mail.contoso.com/OWA
    
    À l'invite de commande, exécutez les commandes suivantes une fois que vous avez défini le répertoire virtuel Outlook Web App.
    
        Net stop IISAdmin /y
    
        Net start W3SVC

2.  Pour configurer l'accès externe au CAE, exécutez la commande suivante dans Exchange Management Shell.
    
        Set-EcpVirtualDirectory "<CAS2013>\ECP (Default Web Site)" -ExternalUrl https://mail.contoso.com/ECP -InternalURL https://mail.contoso.com/ECP 

3.  Pour configurer le service de disponibilité, exécutez la commande suivante dans Exchange Management Shell.
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalURL https://mail.contoso.com/EWS/Exchange.asmx

Pour vérifier que l’URL externe a été correctement configurée pour Exchange ActiveSync ou Outlook Web App, vous pouvez utiliser l’analyseur de connectivité à distance, un outil web gratuit fourni par Microsoft. Vous trouverez l’analyseur de connectivité à distance [ici](http://go.microsoft.com/fwlink/?linkid=154308).

Pour vérifier que l'authentification a été correctement configurée pour Exchange ActiveSync ou Outlook Web App, vous pouvez aussi utiliser ExRCA.

Pour vérifier qu'un accès direct au fichier a été correctement configuré pour Outlook Web App, connectez-vous en tant qu'utilisateur à Outlook Web App, à l'aide de l'option d'ordinateur public, puis essayez d'accéder à un fichier joint à un message électronique et de l'enregistrer.

## Configurer des protocoles sur les serveurs d'accès au client Exchange 2007

Vous devrez exécuter les commandes suivantes pour configurer les répertoires virtuels pour Exchange 2007.

  - Pour configurer l'URL externe sur le répertoire virtuel Exchange ActiveSync, exécutez la commande suivante dans Exchange Management Shell.
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2007>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl https://mail.contoso.com/Microsoft-Server-ActiveSync

  - Pour configurer l’URL externe sur le répertoire virtuel Outlook Web App, exécutez la commande suivante dans Exchange Management Shell.
    
        Set-OwaVirtualDirectory -Identity "<CAS2007>\owa (Default Web Site)" -ExternalUrl https://legacy.contoso.com/owa

