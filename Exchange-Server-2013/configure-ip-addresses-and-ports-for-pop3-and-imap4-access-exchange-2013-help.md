---
title: 'Configurer les ports et les adresses IP pour les accès POP3 et IMAP4: Exchange 2013 Help'
TOCTitle: Configurer les ports et les adresses IP pour les accès POP3 et IMAP4
ms:assetid: 8292747b-6626-4d7f-ba73-1e17f5d99fa4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123530(v=EXCHG.150)
ms:contentKeyID: 50555433
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer les ports et les adresses IP pour les accès POP3 et IMAP4

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-28_

Le Centre d’administration Exchange et l’environnement de ligne de commande Exchange Management Shell vous permettent de configurer des services POP3 et IMAP4 Microsoft Exchange pour utiliser des adresses IP et des ports qui diffèrent des paramètres par défaut.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Entrez les adresses IP et les plages d'adresses IP au format IPv4 (Internet Protocol Version 4) ou IPv6 (Internet Protocol Version 6), ou aux deux formats. Une installation par défaut de Windows Server 2008 prend en charge les protocoles IPv4 et IPv6.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur POP3 et IMAP4, voir [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrées « Paramètres POP3 » et « Paramètres IMAP4 » de la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

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

## Configurer des adresses IP et des ports pour POP3

## Utiliser le Centre d’administration Exchange (EAC) pour configurer des adresses IP et des ports pour POP3

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Serveurs** **\>** **Serveurs**.

2.  Dans la liste des serveurs, sélectionnez un serveur d’accès au client, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés du serveur, cliquez sur **POP3**.

4.  Sous **Connexions TLS ou non chiffrées**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

5.  Sur la page **Ajouter une adresse IP**, sous **Adresse IP**, sélectionnez l’une des options suivantes :
    
      - **Toutes les adresses IPv4 disponibles**   Utilisation de toutes les adresses IP IPv4 pour un serveur.
    
      - **Toutes les adresses IPv6 disponibles**   Utilisation de toutes les adresses IP IPv6 pour un serveur.
    
      - **Spécifiez une adresse IP**   Utilisation d’une adresse IP spécifique.

6.  Sous **Port**, entrez un numéro de port ou acceptez le port par défaut.

7.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

Après avoir défini les paramètres de l’adresse IP et du port pour POP3, vous devez redémarrer le service POP3 pour que les paramètres prennent effet. Pour plus d’informations sur le redémarrage du service POP3, voir [Démarrage et arrêt des services POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer des adresses IP et des ports pour POP3

Cet exemple définit le port et l'adresse IP à utiliser pour communiquer avec Exchange via le service POP3 avec chiffrement SSL (Secure Sockets Layer).

    Set-PopSettings -SSLBindings: IPaddress:Port

Cet exemple définit le port et l'adresse IP à utiliser pour communiquer avec Exchange via le service POP3 sans chiffrement ou chiffrement TLS (Transport Layer Security).

    Set-PopSettings -UnencryptedOrTLSBindings IPaddress:Port

Après avoir défini les paramètres de l’adresse IP et du port pour POP3, vous devez redémarrer le service POP3 pour que les paramètres prennent effet. Pour plus d’informations sur le redémarrage du service POP3, voir [Démarrage et arrêt des services POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Pour plus d'informations sur la syntaxe et les paramètres, voir [Set-PopSettings](https://technet.microsoft.com/fr-fr/library/aa997154\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Procédez comme suit pour vérifier que les paramètres de l’adresse IP POP3 et du port ont été modifiés sur un serveur.

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-PopSettings | format-list

2.  Vérifiez que les paramètres *UnencryptedOrTLSBindings* et *SSLBindings* sont corrects.

## Configurer des adresses IP et des ports pour IMAP4

## Utiliser le Centre d’administration Exchange (EAC) pour configurer des adresses IP et des ports pour IMAP4

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Serveurs** **\>** **Serveurs**.

2.  Dans la liste des serveurs, sélectionnez un serveur d’accès au client, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés du serveur, cliquez sur **IMAP4**.

4.  Pour définir des paramètres de connexions TLS ou non chiffrées, sous **Connexions TLS ou non chiffrées**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour modifier des paramètres de connexions SSL (Secure Sockets Layer), sous **Connexions SSL (Secure Sockets Layer)**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

5.  Sur la page **Ajouter une adresse IP**, sous **Adresse IP**, sélectionnez l’une des options suivantes :
    
      - **Toutes les adresses IPv4 disponibles**   Utilisation de toutes les adresses IP IPv4 pour un serveur.
    
      - **Toutes les adresses IPv6 disponibles**   Utilisation de toutes les adresses IP IPv6 pour un serveur.
    
      - **Spécifiez une adresse IP**   Utilisation d’une adresse IP spécifique.

6.  Sous **Port**, entrez un numéro de port ou acceptez le port par défaut.

7.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

Après avoir défini les paramètres de l’adresse IP et du port pour IMAP4, vous devez redémarrer les services IMAP4 pour que les paramètres prennent effet. Pour plus d’informations sur le redémarrage des services IMAP4, voir [Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer des adresses IP et des ports pour IMAP4

Cet exemple définit le port et l'adresse IP à utiliser pour communiquer avec Exchange via le service IMAP4.

    Set-ImapSettings -SSLBindings: IPaddress:Port

Cet exemple définit le port et l'adresse IP à utiliser pour communiquer avec Exchange via le service IMAP4 sans chiffrement ou chiffrement TLS (Transport Layer Security).

    Set-ImapSettings -UnencryptedOrTLSBindings IPaddress:Port 

Après avoir défini les paramètres de l’adresse IP et du port pour IMAP4, vous devez redémarrer le service IMAP4 pour que les paramètres prennent effet. Pour plus d’informations sur le redémarrage du service IMAP4, voir [Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Pour plus d'informations sur la syntaxe et les paramètres, voir [Set-ImapSettings](https://technet.microsoft.com/fr-fr/library/aa998252\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Procédez comme suit pour vérifier que les paramètres de l’adresse IP IMAP4 et du port ont été modifiés sur un serveur.

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-ImapSettings | format-list

2.  Vérifiez que les paramètres *UnencryptedOrTLSBindings* et *SSLBindings* sont corrects.

## Pour plus d'informations

Une fois que vous avez configuré les adresses IP et les ports pour l'accès POP3 et IMAP4, vous pouvez également :

[Activation d’IMAP4 dans Exchange 2016](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Activation de POP3 dans Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md)

