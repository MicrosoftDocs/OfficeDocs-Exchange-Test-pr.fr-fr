---
title: 'Définir les limites de connexion pour IMAP4: Exchange 2013 Help'
TOCTitle: Définir les limites de connexion pour IMAP4
ms:assetid: 8e3aa366-e77c-4c70-b78d-ddbb178cb521
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123712(v=EXCHG.150)
ms:contentKeyID: 50555445
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Définir les limites de connexion pour IMAP4

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-11-28_

Le Centre d’administration Exchange (EAC) ou l’environnement de ligne de commande Exchange Management shell vous permet de gérer des limites de connexion IMAP4 pour votre organisation.

Lorsque vous spécifiez des limites de connexion pour IMAP4, vous pouvez les sélectionner pour le serveur, une adresse IP ou un utilisateur spécifique.

Pour plus d’informations sur IMAP4, voir [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Paramètres IMAP4 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

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

## Utiliser le Centre d’administration Exchange (EAC) pour définir les limites de connexion IMAP4 pour un serveur, une adresse IP ou un utilisateur

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Serveurs** **\>** **Serveurs**.

2.  Dans la liste des serveurs, sélectionnez un serveur d’accès au client, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés du serveur, cliquez sur **IMAP4**.

4.  Faites défiler, puis cliquez sur **Autres options**.

5.  Sous **Limites de connexion**, utilisez les paramètres suivants :
    
      - **Nombre maximal de connexions**   Indique le nombre total de connexions que le serveur spécifié accepte. Celles-ci incluent les connexions authentifiées et non authentifiées. La valeur par défaut est 2 147 483 647. Les valeurs possibles sont comprises entre 1 et 2 147 483 647.
    
      - **Connections maximales d’une adresse IP unique**   Indique le nombre total de connexions que le serveur doit accepter à partir d’une adresse IP unique. La valeur par défaut est 2 147 483 647. Les valeurs possibles sont comprises entre 1 et 2 147 483 647.
    
      - **Nombre maximal de connexions d’un utilisateur unique**   Indique le nombre maximum de connexions que le serveur doit accepter d’un utilisateur particulier. La valeur par défaut est 16. Les valeurs possibles sont comprises entre 1 et 2 147 483 647.
    
      - **Taille maximale d’une commande (octets)**   Indique la taille maximale d’une commande unique. La valeur par défaut est 10 240. Les valeurs possibles sont comprises entre 1 024 et 16 384.

6.  Cliquez sur **Appliquer**, puis sur **OK** pour enregistrer les modifications.

Après avoir défini les limites de connexion, vous devez redémarrer les services IMAP4. Pour plus d’informations sur le redémarrage des services IMAP4, voir [Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour définir les limites de connexion IMAP4 d’un serveur, d’une adresse IP ou d’un utilisateur

Cet exemple définit la limite de connexion pour un serveur.

    Set-ImapSettings -Identity CAS01 -MaxConnections Value

Cet exemple définit la limite de connexion pour une adresse IP.

    Set-ImapSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value

Cet exemple définit la limite de connexion pour un utilisateur.

    Set-ImapSettings -MaxConnectionsPerUser Value

Dans cet exemple, nous définissons la taille de commande maximale.

    Set-ImapSettings -MaxCommandSize Value

Après avoir défini les limites de connexion, vous devez redémarrer les services IMAP4. Pour plus d’informations sur le redémarrage des services IMAP4, voir [Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Pour plus d’informations sur la syntaxe et les paramètres, voir [Set-ImapSettings](https://technet.microsoft.com/fr-fr/library/aa998252\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que les limites de connexion ont été correctement définie, procédez comme suit :

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Serveurs** **\>** **Serveurs**.

2.  Dans la liste des serveurs, sélectionnez un serveur d’accès au client, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés du serveur, cliquez sur **IMAP4**.

4.  Faites défiler, puis cliquez sur **Autres options**.

5.  Sous **Limites de connexion**, vérifiez que les paramètres de connexion sont correctes.

Ou

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-ImapSettings | format-list

2.  Vérifiez que les paramètres de connexion sont correctes.

## Pour plus d'informations

Après avoir défini les limites de connexion IMAP4 d’un serveur, d’une adresse IP ou d’un utilisateur, vous pouvez également :

[Activation d’IMAP4 dans Exchange 2016](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Définir les limites de délai d’expiration de connexion pour IMAP4](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

