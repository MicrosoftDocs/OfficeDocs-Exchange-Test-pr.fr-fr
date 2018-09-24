---
title: 'Gestion des abonnements Edge: Exchange 2013 Help'
TOCTitle: Gestion des abonnements Edge
ms:assetid: 27de4104-fb8e-4eab-9ad2-a64f81a4fb69
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996865(v=EXCHG.150)
ms:contentKeyID: 61180533
ms.date: 04/26/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des abonnements Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2018-04-16_

Cette rubrique fournit des informations détaillées sur une variété de tâches de gestion d’abonnement Edge.

**Contenu de cette rubrique**

Abonner un serveur de transport Edge

Supprimer un abonnement Edge

Réabonner un serveur de transport Edge

Ajouter ou supprimer un serveur de boîtes aux lettres

Exécuter EdgeSync manuellement

Vérifier les résultats EdgeSync

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée de chaque procédure : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « EdgeSync » et la section « Serveurs de transport Edge » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous devez disposer d’un serveur Edge abonné à votre site Active Directory accessible via Internet. Pour plus d’informations, consultez la rubrique [Configurer le flux de messagerie Internet via un serveur de transport Edge abonné](configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Abonner un serveur de transport Edge

Vous pouvez abonner un ou plusieurs serveurs de transport Edge à un seul site Active Directory. Si vous déployez des serveurs de transport Edge supplémentaires dans votre réseau de périmètre et si vous les abonnez au même site Active Directory sur lequel un abonnement Edge existe déjà, les actions suivantes se produisent :

  - Un objet d’abonnement Edge est créé dans Active Directory.

  - Les comptes ESRA supplémentaires sont créés pour chaque serveur de boîtes aux lettres dans le site Active Directory. Ces comptes sont répliqués dans AD LDS (Active Directory Lightweight Directory Services) et utilisés par le processus de synchronisation EdgeSync lors de la synchronisation avec le nouveau serveur.

  - Le nouvel abonnement Edge est ajouté à la liste des serveurs sources du connecteur d’envoi automatique vers Internet. La charge liée aux messages déposés sur ce connecteur pour traitement est équilibrée entre les serveurs de transport Edge abonnés.

  - Un connecteur d’envoi entrant du serveur de transport Edge vers l’organisation Exchange est automatiquement créé.

  - La synchronisation EdgeSync vers le serveur de transport Edge démarre.

## Supprimer un abonnement Edge

Il se peut que, parfois, vous souhaitiez supprimer un abonnement Edge de l’organisation Exchange ou à la fois de l’organisation Exchange et du serveur de transport Edge. Si vous envisagez de réabonner ultérieurement le serveur de transport Edge à l’organisation Exchange, ne supprimez pas l’abonnement Edge du serveur de transport Edge. Lorsque vous supprimez l’abonnement Edge d’un serveur de transport Edge, toutes les données répliquées sont supprimées d’AD LDS. Cette procédure peut prendre un temps relativement long si vous avez beaucoup de données sur les destinataires.

Pour supprimer complètement un abonnement Edge, vous devez exécuter cette procédure sur le serveur de transport Edge que vous souhaitez supprimer et sur un serveur de boîtes aux lettres Exchange 2013 dans le site Active Directory auquel le serveur de transport Edge est abonné.

Après avoir supprimé l’abonnement Edge, la synchronisation des informations à partir d’AD LDS s’arrête. Tous les comptes stockés dans AD LDS sont supprimés et le serveur de transport Edge est supprimé de la liste de serveurs sources de tous les connecteurs d’envoi. Vous ne pouvez plus utiliser les fonctionnalités du serveur de transport Edge qui dépendent des données d’Active Directory.

1.  Pour supprimer l’abonnement Edge du serveur de transport Edge, utilisez la syntaxe suivante.
    
    ```powershell
    Remove-EdgeSubscription <EdgeTransportServerIdentity>
    ```
    
    Par exemple, pour supprimer l’abonnement Edge sur le serveur de transport Edge nommé Edge01, exécutez la commande suivante.
    
    ```powershell
    Remove-EdgeSubscription Edge01
    ```

2.  Pour supprimer l’abonnement Edge du serveur de boîtes aux lettres, utilisez la syntaxe suivante.
    
    ```powershell
    Remove-EdgeSubscription <MailboxServerIdentity>
    ```
    
    Par exemple, pour supprimer l’abonnement Edge sur le serveur de boîtes aux lettres nommé Mailbox01, exécutez la commande suivante.
    
    ```powershell
    Remove-EdgeSubscription Mailbox01
    ```

Vous devrez supprimer l’abonnement Edge si :

  - Vous ne voulez plus que le serveur de transport Edge soit inclus dans la synchronisation EdgeSync. Vous devrez supprimer l’abonnement Edge à la fois du serveur de transport Edge et de l’organisation Exchange.

  - Un serveur de transport Edge est en cours de désactivation. Dans ce scénario, vous devez uniquement supprimer l’abonnement Edge de l’organisation Exchange. Si vous désinstallez le rôle serveur de transport Edge de l’ordinateur, l’instance AD LDS et toutes les données Active Directory stockées dans AD LDS seront également supprimées.

  - Vous voulez modifier l’association de site Active Directory pour l’abonnement Edge. Vous devrez uniquement supprimer l’abonnement Edge de l’organisation Exchange. Après la suppression de l’abonnement Edge de l’organisation Exchange, vous pouvez réabonner le serveur de transport Edge à un autre site Active Directory.

Lorsque vous supprimez un abonnement Edge de l’organisation Exchange :

  - La synchronisation des informations d’Active Directory vers AD LDS s’arrête.

  - Les comptes ESRA sont supprimés d’Active Directory et d’AD LDS.

  - Le serveur de transport Edge est supprimé de la propriété *SourceTransportServers* de tous les connecteurs d’envoi.

  - Le connecteur d’envoi entrant automatique du serveur de transport Edge vers l’organisation Exchange est supprimé d’AD LDS.

Lorsque vous supprimez l’abonnement Edge d’un serveur de transport Edge :

  - Vous ne pouvez plus utiliser les fonctionnalités du serveur de transport Edge qui dépendent des données d’Active Directory.

  - Les données répliquées sont supprimées d’AD LDS.

  - Les tâches désactivées lors de la création de l’abonnement Edge sont réactivées pour la configuration locale.

## Réabonner un serveur de transport Edge

Il peut arriver que vous souhaitiez réabonner un serveur de transport Edge à un site Active Directory. Lorsque l’abonnement Edge est recréé, de nouvelles informations d’identification sont générées et vous devez suivre l’intégralité du processus d’abonnement Edge. Vous devrez vous réabonner à un serveur de transport Edge si :

  - Vous ajoutez de nouveaux serveurs de boîtes aux lettres dans le site Active Directory abonné et vous voulez que le nouveau serveur de boîtes aux lettres soit inclus dans la synchronisation EdgeSync.

  - Vous avez appliqué la clé de licence pour le serveur de transport Edge après avoir créé l’abonnement Edge. Les informations de licence pour le serveur de transport Edge sont enregistrées lors de la création de l’abonnement Edge. Les serveurs de transport Edge abonnés apparaissent uniquement sous licence s’ils sont abonnés à l’organisation Exchange après l’application de la clé de licence sur le serveur de transport Edge. Si la clé de licence est appliquée au serveur de transport Edge après l’exécution du processus d’abonnement Edge, les informations de licence ne seront pas mises à jour dans l’organisation Exchange et vous devrez réabonner le serveur de transport Edge.

  - Les informations d’identification du compte ESRA sont compromises.
    
    > [!IMPORTANT]
    > Pour réabonner un serveur de transport Edge, exportez un nouveau fichier d’abonnement Edge sur le serveur de transport Edge, puis importez le fichier XML sur un serveur de boîtes aux lettres. Vous devez réabonner le serveur de transport Edge au même site Active Directory auquel il était abonné à l’origine. Vous ne devez pas commencer par supprimer l’abonnement Edge d’origine. Le processus de réabonnement remplacera l’abonnement Edge existant.


## Ajouter ou supprimer un serveur de boîtes aux lettres

Si vous ajoutez un serveur de boîtes aux lettres à un site Active Directory auquel un serveur de transport Edge est déjà abonné, le nouveau serveur de boîtes aux lettres n’est pas automatiquement inclus dans la synchronisation EdgeSync. Pour activer l’inclusion d’un serveur de boîtes aux lettres nouvellement déployé dans la synchronisation EdgeSync, vous devez réabonner chaque serveur de transport Edge au site Active Directory.

La suppression d’un serveur de boîtes aux lettres à partir d’un site Active Directory auquel un serveur de transport Edge est abonné n’aura pas d’incidence sur la synchronisation EdgeSync, sauf si ce serveur de boîtes aux lettres est le seul serveur de boîtes aux lettres dans ce site. Si vous supprimez tous les serveurs de boîtes aux lettres à partir du site Active Directory auquel un serveur de transport Edge est déjà abonné, les serveurs de transport Edge abonnés de ce site se retrouvent orphelins.

## Exécuter EdgeSync manuellement

Vous pouvez exécuter EdgeSync manuellement si vous avez apporté des modifications importantes à la configuration ou aux destinataires dans Active Directory et que vous voulez synchroniser vos modifications immédiatement. Vous pouvez exécuter une synchronisation complète ou synchroniser uniquement les modifications apportées depuis la dernière réplication.

Une synchronisation EdgeSync manuelle réinitialise la planification de la synchronisation EdgeSync. La synchronisation automatique suivante se base sur le moment où vous avez exécuté la synchronisation manuelle.

Pour exécuter EdgeSync manuellement, utilisez la syntaxe suivante.

```powershell
Start-EdgeSynchronization [-Server <MailboxServerIdentity>] [-TargetServer <EdgeTransportServerIdentity> [-ForceFullSync]
```

L’exemple suivant démarre EdgeSync avec les options suivantes :

  - La synchronisation est initiée à partir du serveur de boîtes aux lettres Exchange 2013 nommé Mailbox01.

  - Tous les serveurs de transport Edge sont synchronisés.

  - Seules les modifications apportées depuis la dernière réplication sont synchronisées.

<!-- end list -->

```powershell
Start-EdgeSynchronization -Server Mailbox01
```

Cet exemple démarre EdgeSync avec les options suivantes :

  - La synchronisation est initiée à partir du serveur de boîtes aux lettres local.

  - Seul le serveur de transport Edge nommé Edge03 est synchronisé.

  - Toutes les données sur les destinataires et la configuration sont entièrement synchronisées.

<!-- end list -->

```powershell
Start-EdgeSynchronization -TargetServer Edge03 -ForceFullSync
```

## Vérifier les résultats EdgeSync

La cmdlet **Test-EdgeSynchronization** permet de vérifier que la synchronisation Edge fonctionne. Cette cmdlet signale l’état de synchronisation des serveurs de transport Edge abonnés.

Le résultat de cette cmdlet vous permet de voir les objets qui n’ont pas été synchronisés vers le serveur de transport Edge. La tâche compare les données stockées dans Active Directory aux données stockées dans AD LDS et signale toute incohérence des données.

Le paramètre *ExcludeRecipientTest* utilisé sur la cmdlet **Test-EdgeSynchronization** permet d’exclure la validation de la synchronisation des données sur les destinataires. Si vous incluez ce paramètre, seule la synchronisation d’objets de configuration est validée. La validation des données sur les destinataires prendra plus de temps que la validation des données de configuration uniquement.

## Vérifier les résultats EdgeSync pour un destinataire unique

Pour vérifier les résultats EdgeSync pour un destinataire unique, utilisez la syntaxe suivante sur un serveur de boîtes aux lettres dans le site Active Directory abonné.

```powershell
Test-EdgeSynchronization -VerifyRecipient <emailaddress>
```

Cet exemple vérifie les résultats EdgeSync pour l’utilisateur kate@contoso.com.

```powershell
Test-EdgeSynchronization -VerifyRecipient kate@contoso.com
```

Retour au début

