---
title: "Gérer l'agrégation de listes fiables: Exchange 2013 Help"
TOCTitle: Gérer l'agrégation de listes fiables
ms:assetid: 5ac17168-f411-4cb7-ae98-ebefb865b210
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998280(v=EXCHG.150)
ms:contentKeyID: 50478263
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer l'agrégation de listes fiables

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

L’*agrégation de listes fiables* fait référence à la fonction de blocage du courrier indésirable partagée depuis Microsoft Outlook vers Microsoft Exchange Server 2013. Cette fonction permet de collecter des données dans les listes des destinataires approuvés, des expéditeurs approuvés, des expéditeurs bloqués et dans les données de contacts configurées par les utilisateurs d’Outlook, tout en rendant ces données accessibles aux agents de blocage du courrier indésirable Exchange. L’agrégation de listes fiables permet de réduire les cas de faux positifs lors du filtrage du courrier indésirable par les serveurs Exchange sur lesquels les agents de blocage du courrier indésirable sont exécutés.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée de chaque procédure : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md) et la section « Fonctionnalités anti-spam » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Par défaut, les fonctionnalités de courrier indésirable ne sont pas activées dans le service Transport du serveur de boîtes aux lettres. En général, vous activez uniquement les fonctionnalités de courrier indésirable sur un serveur de boîtes aux lettres si votre organisation Exchange n'effectue aucun filtrage de courrier indésirable avant d'accepter les messages entrants. Pour plus d'informations, voir Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres[Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Tenez compte du trafic réseau et de réplication que vous pouvez générer lors de l’exécution de la cmdlet **Update-SafeList**. Si vous exécutez la commande sur plusieurs boîtes aux lettres utilisant intensément les listes fiables, le volume de trafic généré peut être considérable. Si vous exécutez la commande sur plusieurs boîtes aux lettres, il est recommandé de le faire en dehors des heures de pointe et de travail.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utilisez l’environnement de ligne de commande Exchange Management Shell pour configurer les limites de collection des listes fiables de boîtes aux lettres

Vous pouvez configurer le nombre maximum d’expéditeurs approuvés et d’expéditeurs bloqués qu’un utilisateur peut configurer. Par défaut, les utilisateurs peuvent configurer jusqu’à 5 000 expéditeurs approuvés et 500 expéditeurs bloqués.

Pour configurer le nombre maximum d’expéditeurs approuvés et d’expéditeurs bloqués, exécutez la commande suivante :

    Set-Mailbox <MailboxIdentity> -MaxSafeSenders <Integer> -MaxBlockedSenders <Integer>

Cet exemple configure la boîte aux lettres john@contoso.com avec 2 000 expéditeurs approuvés et 200 expéditeurs bloqués.

```powershell
Set-Mailbox john@contoso.com -MaxSafeSenders 2000 -MaxBlockedSenders 200
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré les limites de collection des listes fiables de boîtes aux lettres, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-Mailbox <Identity> | Format-List Name,Max*Senders

2.  Vérifiez que les valeurs affichées correspondent aux valeurs que vous avez configurées.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour exécuter la commande Update-Safelist

Dans Exchange 2013, l’agrégation de listes fiables est exécutée automatiquement. Vous n’avez donc pas besoin de planifier ou d’exécuter manuellement la cmdlet **Update-Safelist**. Cependant, vous pouvez souhaiter exécuter cette cmdlet occasionnellement pour tester l’agrégation de listes fiables.

Cet exemple de code écrit la liste des expéditeurs approuvés pour la boîte aux lettres john@contoso.com sur Active Directory.

```powershell
Update-Safelist john@contoso.com -Type SafeSenders
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Update-SafeList](https://technet.microsoft.com/fr-fr/library/bb125034\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré l’agrégation de listes fiables, procédez comme suit :

## Étape 1 : Utilisez l’environnement de ligne de commande Exchange Management Shell pour vérifier que l’agent de filtrage du contenu est activé sur le serveur Exchange

1.  Exécutez la commande suivante :
    
    ```powershell
Get-ContentFilterConfig | Format-List Enabled
```

2.  Si la sortie indique le paramètre *Enabled* est défini sur `True`, le filtrage de contenu est activé. Dans le cas contraire, exécutez la commande suivante pour activer le filtrage du contenu et l’agent de filtrage du contenu sur le serveur Exchange :
    
    ```powershell
Set-ContentFilterConfig -Enabled $true
```

## Étape 2 : (Facultatif) Utilisez l’Éditeur ADSI pour vérifier la réplication des données d’agrégation de listes fiables sur les serveurs de transport Edge

Cette étape n’est exigée que si vous exécutez l’agent de filtrage du contenu sur un serveur de transport Edge dans votre réseau de périmètre.

Vous pouvez afficher les objets utilisateur dans l’instance d’Active Lightweight Directory Services (AD LDS) du serveur de transport Edge pour vérifier que les données de collection de listes fiables sont mises à jour et que le service Microsoft Exchange EdgeSync a répliqué les données vers l’instance d’AD LDS.

Il existe trois attributs de collection de listes fiables pour chaque objet utilisateur :

  - **msExchSafeRecipientsHash**   Cet attribut stocke le hachage de la collection des listes des destinataires approuvés de l’utilisateur.

  - **msExchSafeSendersHash**   Cet attribut stocke le hachage de la collection des listes des expéditeurs approuvés de l’utilisateur.

  - **msExchBlockedSendersHash**   Cet attribut stocke le hachage de la collection des listes des expéditeurs bloqués de l’utilisateur.

Si une chaîne hexadécimale, telle que `0xac 0xbd 0x03 0xca`, est présente sur l’attribut, l’objet utilisateur a été mis à jour. Si l’attribut a pour valeur `<Not Set>`, il n’a pas été mis à jour.

Vous pouvez rechercher et afficher les attributs en utilisant le composant logiciel enfichable d’édition des interfaces ADSI (Active Directory Service Interfaces) d’AD LDS.

## Étape 3 : Envoyez un message de test pour vérifier que l’agrégation de listes fiables fonctionne

Pour tester le bon fonctionnement de l’agrégation de listes fiables, vous devez envoyer vous-même un message depuis un expéditeur approuvé qui aurait sinon été bloqué par le filtrage du contenu. Si l’agrégation de listes fiables fonctionne, le message doit arriver dans votre boîte de réception.

1.  Trouvez un compte de messagerie électronique externe existant que vous pouvez utiliser, ou créez un compte de messagerie électronique sur un fournisseur de messagerie électronique gratuit sur le web, tel que Microsoft Hotmail.

2.  Ajoutez ce compte à votre liste des expéditeurs approuvés dans Microsoft Outlook.

3.  Utilisez la cmdlet **Update-SafeList** pour copier la collection de listes fiables de cette boîte aux lettres dans Active Directory.

4.  Facultatif : Si vous exécutez l’agent de filtrage du contenu sur un serveur de transport Edge dans le réseau de périmètre, exécutez la cmdlet **Start-EdgeSynchronization** pour forcer la réplication EdgeSync.

5.  Ajoutez un mot spécifique comme phrase de blocage à votre configuration du filtrage du contenu. Pour obtenir la procédure détaillée, voir [Gérer le filtrage du contenu](manage-content-filtering-exchange-2013-help.md).

6.  Depuis le compte de messagerie externe de l’étape 1, envoyez un message vers votre boîte aux lettres Exchange avec la phrase bloquée configurée à l’étape 5.
    
    Si le message est envoyé avec succès dans votre boîte de réception, l’agrégation de listes fiables fonctionne correctement.

