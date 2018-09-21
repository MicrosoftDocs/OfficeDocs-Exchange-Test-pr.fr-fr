---
title: 'Définir les limites de connexion pour POP3: Exchange 2013 Help'
TOCTitle: Définir les limites de connexion pour POP3
ms:assetid: 512d61c2-2a34-4813-92a9-875339d3388b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997988(v=EXCHG.150)
ms:contentKeyID: 50555392
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Définir les limites de connexion pour POP3

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-28_

Vous pouvez utiliser le Centre d’administration Exchange ou l’environnement de ligne de commande Exchange Management Shell pour gérer les limites de connexion POP3 de votre organisation.

Lorsque vous spécifiez des limites de connexion pour POP3, vous pouvez sélectionner des limites de connexion pour le serveur, une adresse IP ou un utilisateur spécifique.

Pour de plus amples informations sur POP3, consultez la rubrique [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Paramètres POP3 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utilisation de l’EMC pour définir les limites de connexion POP3 d’un serveur, d’une adresse IP ou d’un utilisateur

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Serveurs** **\>** **Serveurs**.

2.  Dans la liste des serveurs, sélectionnez le serveur d’accès au client, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page des propriétés du serveur, cliquez sur **POP3**.

4.  Faites défiler vers le bas, puis cliquez sur **Plus d’options**.

5.  Sous **Limites de connexion**, utilisez les paramètres suivants :
    
      - **Nombre maximal de connexions**   Indique le nombre total de connexions que le serveur spécifié acceptera. Celles-ci incluent les connexions authentifiées et non authentifiées. La valeur par défaut est 2 147 483 647. Les valeurs possibles sont comprises entre 1 et 2 147 483 647.
    
      - **Nombre maximal de connexions à partir d’une adresse IP**   Indique le nombre total de connexions que le serveur d’accès au client acceptera d’une adresse IP unique. La valeur par défaut est 2 147 483 647. Les valeurs possibles sont comprises entre 1 et 2 147 483 647.
    
      - **Nombre maximal de connexions d’un utilisateur unique**   Indique le nombre maximal de connexions que le serveur d’accès au client acceptera d’un utilisateur spécifique. La valeur par défaut est 16. Les valeurs possibles sont comprises entre 1 et 2 147 483 647.
    
      - **Taille de commande maximale (octets)**   Indique la taille maximale d’une commande unique. La valeur par défaut est 512. Les valeurs possibles sont comprises entre 40 et 1 024.

6.  Cliquez sur **Appliquer**, puis sur **OK** pour enregistrer les modifications.

Après avoir défini les limites de connexion, vous devez redémarrer les services POP3. Pour plus d’informations sur le redémarrage des services POP3, consultez la rubrique [Démarrage et arrêt des services POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Utilisation du Shell pour définir les limites de connexion POP3 d’un serveur, d’une adresse IP address ou d’un utilisateur

Cet exemple définit la limite de connexion pour un serveur.

```powershell
Set-PopSettings -Identity CAS01 -MaxConnections Value
```

Cet exemple définit la limite de connexion pour une adresse IP.

```powershell
Set-PopSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value
```

Cet exemple définit la limite de connexion pour un utilisateur.

    Set-PopSettings -MaxConnectionsPerUser Value 

Cet exemple montre comment définir la taille maximale d’une commande.

```powershell
Set-PopSettings -MaxCommandSize Value
```

Après avoir défini les limites de connexion, vous devez redémarrer les services POP3. Pour plus d’informations sur le redémarrage des services POP3, consultez la rubrique [Démarrage et arrêt des services POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Pour plus d’informations sur la syntaxe et les paramètres, voir [Set-PopSettings](https://technet.microsoft.com/fr-fr/library/aa997154\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien défini les limites de connexion, procédez de l’une des manières suivantes :

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Serveurs** **\>** **Serveurs**.

2.  Dans la liste des serveurs, sélectionnez le serveur d’accès au client, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page des propriétés du serveur, cliquez sur **POP3**.

4.  Faites défiler vers le bas, puis cliquez sur **Plus d’options**.

5.  Sous **Limites de connexion**, vérifiez que les paramètres de connexion sont corrects.

Ou

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
    ```powershell
Get-PopSettings | format-list
```

2.  Vérifiez que les paramètres de connexion sont corrects.

## Pour plus d'informations

Après avoir défini les limites de connexion POP3 d’un serveur, d’une adresse IP ou d’un utilisateur, vous pouvez également :

[Activation de POP3 dans Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[Définir les limites de délai d’expiration de connexion pour POP3](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

