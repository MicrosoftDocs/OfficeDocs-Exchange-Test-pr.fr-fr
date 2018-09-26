---
title: 'Déplacer la BAL système Exchange 2010 vers Exchange 2013: Exchange 2013 Help'
TOCTitle: Déplacer la boîte aux lettres système Exchange 2010 vers Exchange 2013
ms:assetid: a3b03c4e-0bc7-41a2-885c-e9cac37566c8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn249849(v=EXCHG.150)
ms:contentKeyID: 54915106
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déplacer la boîte aux lettres système Exchange 2010 vers Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Dans Exchange 2010, la boîte aux lettres système Microsoft Exchange est une boîte aux lettres d’arbitrage permettant de stocker les données à l’échelle de l’organisation, telles que les journaux d’audit de l’administrateur, les métadonnées des recherches de découverte électronique, ainsi que les données de messagerie unifiée, telles que les menus, les plans de numérotation et les messages d’accueil personnalisés. La boîte aux lettres système Microsoft Exchange est nommée **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}** ; le nom complet est **Microsoft Exchange**.

Lorsque vous mettez à niveau votre organisation Exchange 2010 existante vers Exchange 2013, vous devez déplacer la boîte aux lettres système Microsoft Exchange dans une base de données de boîtes aux lettres sur un serveur de boîtes aux lettres Exchange 2013. Vous devez déplacer cette boîte aux lettres une fois que vous avez installé et vérifié Exchange 2013. Si vous ne déplacez pas cette boîte aux lettres système vers Exchange 2013, les problèmes suivants se produiront en cas de coexistence d’Exchange 2010 et d’Exchange 2013 dans votre organisation Exchange :

  - Les tâches Exchange 2013 ne sont pas enregistrées dans le journal d’audit de l’administrateur. Lorsque vous exécutez la cmdlet **Search-AdminAuditLog** ou que vous essayez d’exporter le journal d’audit de l’administrateur dans le CAE, vous recevez un message d’erreur indiquant que vous ne pouvez pas créer de recherche dans le journal d’audit de l’administrateur, car la boîte aux lettres système, SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}, se trouve sur un serveur qui n’exécute pas Exchange 2013. Une erreur Microsoft Exchange avec l’ID d’événement 5000 est également enregistrée dans le journal des applications Windows chaque fois qu’une commande est exécutée.

  - Vous ne pouvez pas exécuter de recherche de découverte électronique à l’aide du CAE ou de l’environnement Shell dans Exchange 2013. Les recherches dans les boîtes aux lettres peuvent être créées et mises en file d’attente, mais elles ne peuvent pas être démarrées. Une erreur avec l’ID d’événement 6 est enregistrée dans le journal de gestion MsExchange, indiquant que la cmdlet **Start-MailboxSearch** a échoué. Vous pouvez toutefois effectuer des recherches dans les boîtes aux lettres à l’aide de l’environnement Shell et du Panneau de configuration Exchange (ECP) dans Exchange 2010.

Vous devez également déplacer la boîte aux lettres système Microsoft Exchange vers Exchange 2013 dans le cadre de la mise à niveau de la messagerie unifiée Exchange 2010 vers Exchange 2013.

Pour plus d’informations sur la mise à niveau vers Exchange 2013, consultez les rubriques suivantes :

  - [Mise à niveau d'Exchange 2010 vers Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)

  - [Mise à niveau de la messagerie unifiée d'Exchange 2010 vers celle d'Exchange 2013](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 20 minutes. Le temps réel peut varier en fonction de la taille de la boîte aux lettres système.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Autorisations de migration et de déplacement de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Exécutez la commande suivante dans Exchange 2013 pour obtenir l’identité et la version des serveurs Exchange et des bases de données de boîtes aux lettres qui contiennent les boîtes aux lettres système dans votre organisation.
    
    ```powershell
    Get-Mailbox -Arbitration | FL Name,DisplayName,ServerName,Database,AdminDisplayVersion
    ```
    
    La propriété **AdminDisplayVersion** indique la version d’Exchange que le serveur exécute. La valeur `Version 14.x` indique Exchange 2010 ; la valeur `Version 15.x` indique Exchange 2013.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour déplacer la boîte aux lettres système

1.  Dans le CAE, accédez à **Destinataires** \> **Migration**.

2.  Cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sur **Déplacer vers une base de données différente**.

3.  Dans la page **Déplacement vers une nouvelle boîte aux lettres locale**, cliquez sur **Sélectionner les utilisateurs que vous souhaitez déplacer**, puis sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans la page **Sélectionner une boîte aux lettres**, ajoutez la boîte aux lettres dont les propriétés sont les suivantes :
    
      - Le nom complet est **Microsoft Exchange**.
    
      - L’alias de l’adresse de messagerie de la boîte aux lettres est **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**.

5.  Cliquez sur **OK**, puis sur **Suivant**.

6.  Dans la page **Configuration du déplacement**, tapez le nom du lot de migration, puis cliquez sur **Parcourir** en regard de la zone **Base de données cible**.

7.  Dans la page **Sélectionner la base de données de boîtes aux lettres**, ajoutez la base de données de boîtes aux lettres vers laquelle déplacer la boîte aux lettres système. Vérifiez que la version de la base de données de boîtes aux lettres sélectionnée est 15. x, ce qui indique que la base de données se trouve sur un serveur Exchange 2013.

8.  Cliquez sur **OK**, puis sur **Suivant**.

9.  Dans la page **Démarrer le lot**, sélectionnez les options permettant de démarrer et d’exécuter automatiquement la demande de migration, puis cliquez sur **Nouveau**.

## Utiliser l’environnement Shell pour déplacer la boîte aux lettres système

Tout d’abord, exécutez la commande suivante dans Exchange 2013 pour obtenir les noms et les versions de toutes les bases de données de boîtes aux lettres de votre organisation.

```powershell
Get-MailboxDatabase -IncludePreExchange2013 | FL Name,Server,AdminDisplayVersion
```

Après avoir identifié le nom des bases de données de boîtes aux lettres dans votre organisation, exécutez la commande suivante dans Exchange 2013 pour déplacer la boîte aux lettres système Microsoft Exchange vers une base de données de boîtes aux lettres située sur un serveur Exchange 2013.

```powershell
Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | New-MoveRequest -TargetDatabase <name of Exchange 2013 database>
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez déplacé la boîte aux lettres système Microsoft Exchange vers une base de données de boîtes aux lettres située sur un serveur Exchange 2013, exécutez la commande suivante dans l’environnement Shell.

```powershell
Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | FL Database,ServerName,AdminDisplayVersion
```

Si la valeur de la propriété **AdminDisplayVersion** est **Version 15.x (Build xxx.x)**, cela confirme que la boîte aux lettres système réside sur une base de données de boîtes aux lettres située sur un serveur Exchange 2013.

Après avoir déplacé la boîte aux lettres système Microsoft Exchange vers Exchange 2013, vous pourrez également réaliser les tâches d’administration suivantes :

  - exécuter la cmdlet **Search-AdminAuditLog**;

  - exporter le journal d’audit de l’administrateur dans le CAE;

  - créer et lancer des recherches de découverte électronique à l’aide du CAE ou de l’environnement Shell dans Exchange 2013.

