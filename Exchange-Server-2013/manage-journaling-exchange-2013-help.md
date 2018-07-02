---
title: 'Gérer la journalisation: Exchange 2013 Help'
TOCTitle: Gérer la journalisation
ms:assetid: d517f27e-f80a-4a06-988c-cbbf981c701d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ651670(v=EXCHG.150)
ms:contentKeyID: 50479309
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer la journalisation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

La journalisation peut aider votre organisation à répondre aux exigences réglementaires, légales et de conformité organisationnelle en enregistrant les communications électroniques échangées. Cette rubrique explique comment effectuer des tâches de base liées à la gestion de la journalisation dans Exchange 2013 et Exchange Online.

La journalisation standard est configurée sur une base de données de boîtes aux lettres. Elle permet à l’agent de journalisation de journaliser tous les messages échangés depuis des boîtes aux lettres situées dans une base de données de boîtes aux lettres spécifique. Vous pouvez également utiliser la journalisation étendue, qui permet à l’agent de journalisation de réaliser une journalisation plus détaillée en utilisant les règles de journal. Au lieu de journaliser toutes les boîtes aux lettres résidant dans une base de données de boîtes aux lettres, il est possible de configurer des règles de journal correspondant aux besoins de votre organisation en journalisant des destinataires individuels ou des membres de groupes de distribution. Pour utiliser la journalisation étendue, vous devez disposer d’une licence d’accès client entreprise Exchange.

Pour en savoir plus sur la journalisation, voir [Journalisation](journaling-exchange-2013-help.md).

**Sommaire**

Créer une règle de journal

Affichage ou modification d'une règle de journal

Activation ou désactivation d'une règle de journal

Suppression d'une règle de journal

Activation ou désactivation de la journalisation des bases de données par boîte aux lettres

## Ce qu'il faut savoir avant de commencer

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Journalisation » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Une boîte aux lettres de journalisation a été créée, ou une boîte aux lettres existante peut être utilisée comme boîte aux lettres de journalisation. Vous ne pouvez pas désigner une boîte aux lettres Exchange Online comme boîte aux lettres de journalisation. Vous pouvez fournir des états du journal à un système d’archivage local ou à un service d’archivage tiers. Si vous exécutez un déploiement hybride avec vos boîtes aux lettres partagées entre les serveurs locaux et Exchange Online, vous pouvez désigner une boîte aux lettres locale comme boîte aux lettres de journalisation de vos boîtes aux lettres Exchange Online et locales.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous avez configuré une règle de journalisation dans Exchange Online pour envoyer les états de journal à une boîte aux lettres de journalisation qui n’existe pas ou qui constitue une destination non valide, l’état de journal reste dans la file d’attente de transport sur les serveurs du centre de données Microsoft. Si cela se produit, le personnel du centre de données Microsoft tentera de contacter votre organisation et vous demandera de résoudre le problème afin que les états de journal puissent être remis à une boîte aux lettres de journalisation. Si vous n’avez pas résolu le problème deux jours après avoir été contacté, Microsoft désactivera la règle de journalisation problématique.</td>
    </tr>
    </tbody>
    </table>


  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>. Si vous rencontrez des problèmes avec la boîte aux lettres <strong>JournalingReportDNRTo</strong>, consultez <a href="https://go.microsoft.com/fwlink/p/?linkid=331674">Règles de transport et de boîtes aux lettres dans Exchange Online ne fonctionnent pas comme prévu</a>.</td>
</tr>
</tbody>
</table>


## Créer une règle de journal

## Utilisation du Centre d’administration Exchange pour créer une règle de journal

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Règles de journalisation**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans **Règle de journal**, attribuez un nom à la règle de journal, puis renseignez les champs suivants :
    
      - **Si le message est envoyé à ou reçu de**   Spécifiez le destinataire qui sera visé par la règle. Vous pouvez sélectionner un destinataire spécifique ou appliquer la règle à l’ensemble des messages.
    
      - **Journaliser les messages suivants**   Spécifiez la portée de la règle de journal. Vous pouvez journaliser uniquement les messages internes, uniquement les messages externes ou tous les messages, quelle que soit l’origine ou la destination.
    
      - **Envoyer des états de journal à**   Saisissez l’adresse de la boîte aux lettres de journalisation qui recevra tous les états de journal.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Vous pouvez également taper le nom d’affichage ou l’alias d’un utilisateur de messagerie ou d’un contact de messagerie comme boîte aux lettres de journalisation. Dans ce cas, les états de journal sont envoyés à l’adresse e-mail externe de l’utilisateur de messagerie ou du contact de messagerie. Mais comme expliqué précédemment, l’adresse e-mail externe d’un utilisateur de messagerie ou d’un contact de messagerie ne peut pas être l’adresse d’une boîte aux lettres Exchange Online.</td>
        </tr>
        </tbody>
        </table>


3.  Cliquez sur **Enregistrer** pour créer la règle de journal.

## Utiliser le shell pour créer une règle de journal

Dans cet exemple, la règle de journal Destinataires du journal de détection est créée pour journaliser la totalité des messages échangés avec le destinataire user1@contoso.com.

    New-JournalRule -Name "Discovery Journal Recipients" -Recipient user1@contoso.com -JournalEmailAddress "Journal Mailbox" -Scope Global -Enabled $True

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé la règle de journal, effectuez l’une des opérations suivantes :

  - À partir du Centre d’administration Exchange, vérifiez que la nouvelle règle de journal que vous avez créée est répertoriée dans l’onglet **Règles de journal**.

  - À partir de l’environnement de ligne de commande Exchange Management Shell, vérifiez que la nouvelle règle de journal existe en exécutant la commande suivante (l’exemple ci-dessous vérifie la règle créée dans l’exemple d’environnement de ligne de commande ci-dessus) :
    
        Get-JournalRule "Discovery Journal Recipients"

Revenir au début

## Affichage ou modification d’une règle de journal

## Utilisation du Centre d’administration Exchange pour afficher ou modifier une règle de journal

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Règles de journalisation**.

2.  Toutes les règles de journal de votre organisation apparaissent dans la liste affichée.

3.  Double-cliquez sur la règle que vous souhaitez afficher ou modifier.

4.  Dans **Règle de journal**, modifiez les paramètres souhaités. Pour de plus amples informations sur les paramètres de cette boîte de dialogue, reportez-vous à la procédure Utilisation du Centre d’administration Exchange pour créer une règle de journal décrite plus haut dans cette rubrique.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour afficher ou modifier une règle de journal

Cet exemple affiche une liste récapitulative de toutes les règles de journal présentes dans l’organisation Exchange :

    Get-JournalRule

Cet exemple récupère la règle de journal « Brokerage Journal Rule » et redirige la sortie vers la commande **Format-List** pour afficher les propriétés de la règle sous forme de liste :

    Get-JournalRule "Brokerage Journal Rule" | Format-List

Si vous souhaitez modifier les propriétés d'une règle spécifique, vous devez utiliser le cmdlet [Set-JournalRule](https://technet.microsoft.com/fr-fr/library/bb125010\(v=exchg.150\)). Cet exemple modifie le nom de la règle de journal en remplaçant `JR-Sales` par `TraderVault`. Les paramètres suivants de la règle sont également modifiés :

  - Destinataire

  - JournalEmailAddress

  - Domaine traité

<!-- end list -->

    Set-JournalRule JR-Sales -Name TraderVault -Recipient traders@woodgrovebank.com -JournalEmailAddress tradervault@woodgrovebank.com -Scope Internal

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié une règle de journal, effectuez l’une des opérations suivantes :

  - À partir du Centre d’administration Exchange, accédez à **Gestion de la conformité** \> **Règles de journal**. Double-cliquez sur la règle que vous avez modifiée et vérifiez que vos modifications ont été enregistrées.

  - À partir de l’environnement de ligne de commande Exchange Management Shell, vérifiez que vous avez bien modifié la règle de journal en exécutant la commande suivante. Cette commande répertoriera les propriétés que vous avez modifiées conjointement avec le nom de la règle (l’exemple ci-dessous vérifie la règle modifiée dans l’exemple d’environnement de ligne de commande ci-dessus) :
    
        Get-TransportRule "TraderVault" | Format-List Name,Recipient,JournalEmailAddress,Scope

Revenir au début

## Activation ou désactivation d’une règle de journal

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous désactivez une règle de journal, l’agent de journalisation s’arrêtera de journaliser les messages visés par cette règle. Si une règle de journal est désactivée, tous les messages qui auraient été normalement journalisés par la règle ne sont pas journalisés. Assurez-vous que vous ne compromettez pas les exigences réglementaires ou de conformité de votre organisation en désactivant une règle de journalisation.</td>
</tr>
</tbody>
</table>


## Utilisation du Centre d’administration Exchange pour activer ou désactiver une règle de journal

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Règles de journalisation**.

2.  Dans la liste affichée, dans la colonne **Activé** en regard du nom de la règle, activez la case à cocher pour activer la règle ou désactivez-la pour la désactiver.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver une règle de journal

Cet exemple active la règle Contoso.

    Enable-JournalRule "Contoso Journal Rule"

Cet exemple désactive la règle Contoso.

    Disable-JournalRule "Contoso Journal Rule"

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé une règle de journal, effectuez l’une des opérations suivantes :

  - À partir du Centre d’administration Exchange, affichez la liste des règles de journal et vérifiez l’état de la case à cocher dans la colonne **Activé**.

  - À partir de l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour renvoyer une liste de toutes les règles de journal de votre organisation, ainsi que leur état :
    
        Get-JournalRule | Format-Table Name,Enabled

Revenir au début

## Suppression d’une règle de journal

## Utilisation du Centre d’administration Exchange pour supprimer une règle de journal

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Règles de journalisation**.

2.  Dans la liste affichée, sélectionnez la règle que vous souhaitez supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour supprimer une règle de journal

Cet exemple supprime la règle Règle de journal de courtage.

    Remove-JournalRule "Brokerage Journal Rule"

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé la règle de journal, effectuez l’une des opérations suivantes :

  - À partir du Centre d’administration Exchange, vérifiez que la règle que vous avez supprimée n’est plus répertoriée dans l’onglet **Règles de journal**.

  - À partir de l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier que la règle supprimée n’est plus répertoriée :
    
        Get-JournalRule

Revenir au début

## Activation ou désactivation de la journalisation des bases de données par boîte aux lettres

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La désactivation de la journalisation des messages sur une base de données de boîtes aux lettres peut compromettre la conformité de votre organisation avec toutes les stratégies de rétention de messagerie applicables. Lorsque vous désactivez la journalisation des messages sur une base de données de boîtes aux lettres, les confirmations de journal ne sont plus envoyées pour les messages échangés avec les boîtes aux lettres sur cette base de données de boîtes aux lettres.</td>
</tr>
</tbody>
</table>


## Utilisation du Centre d’administration Exchange pour activer ou désactiver la journalisation des bases de données par boîte aux lettres

1.  Dans la CCE, accédez à **Serveurs** \> **Bases de données**.

2.  Dans la liste affichée, double-cliquez sur la base de données de boîtes aux lettres pour laquelle vous souhaitez activer la journalisation.

3.  Cliquez sur **Maintenance**, puis cliquez sur **Parcourir** en regard du champ **Destinataire du journal** pour sélectionner la boîte aux lettres de journalisation. La saisie d’un destinataire de journal entraîne l’activation de la journalisation de la base de données.
    
    Pour désactiver la journalisation, supprimez le destinataire de journal en cliquant sur **Supprimer X**.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver la journalisation des bases de données par boîte aux lettres

Cet exemple active la journalisation de la base de données de boîtes aux lettres Base de données des ventes et définit la boîte aux lettres de journal Base de données des ventes comme destinataire du journal.

    Set-MailboxDatabase "Sales Database" -JournalRecipient "Sales Database Journal Mailbox"

Cet exemple désactive la journalisation des bases de données par boîte aux lettres sur la base de données de boîtes aux lettres Base de données des ventes.

    Set-MailboxDatabase "Sales Database" -JournalRecipient $Null

Cet exemple désactive la journalisation des bases de données par boîte aux lettres sur toutes les bases de données de boîtes aux lettres de l’organisation Exchange. La cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb124924\(v=exchg.150\)) permet d’extraire toutes les bases de données de boîtes aux lettres dans l’organisation Exchange, et les résultats de la cmdlet sont transmis à la cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)).

    Get-MailboxDatabase | Set-MailboxDatabase -JournalRecipient $Null

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé la journalisation des bases de données par boîte aux lettres, effectuez l’une des opérations suivantes :

1.  Dans la CCE, accédez à **Serveurs** \> **Bases de données**.

2.  Double-cliquez sur la base de données que vous souhaitez vérifier, puis sélectionnez l’onglet **Maintenance**.

3.  Si le destinataire de journalisation adéquat est répertorié dans le champ **Destinataire du journal**, vous avez activé correctement la journalisation de la base de données de boîtes aux lettres. Si aucun destinataire de journalisation n’est répertorié, la journalisation est désactivée pour la base de données.

<!-- end list -->

  - À partir de l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour renvoyer une liste de toutes les bases de données de boîtes aux lettres de votre organisation, notamment des destinataires de journal associés. La journalisation est activée pour les bases de données pour lesquelles un destinataire de journal est répertorié. Sinon, elle est désactivée.
    
        Get-MailboxDatabase | Format-Table Name,JournalRecipient

Revenir au début

## Pour plus d'informations

[Journalisation](journaling-exchange-2013-help.md)

[Désactiver ou activer la journalisation des notifications d’appel en absence et de la messagerie vocale](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md)

[New-JournalRule](https://technet.microsoft.com/fr-fr/library/bb125242\(v=exchg.150\))

[Get-JournalRule](https://technet.microsoft.com/fr-fr/library/aa998866\(v=exchg.150\))

[Set-JournalRule](https://technet.microsoft.com/fr-fr/library/bb125010\(v=exchg.150\))

[Enable-JournalRule](https://technet.microsoft.com/fr-fr/library/bb123902\(v=exchg.150\))

[Disable-JournalRule](https://technet.microsoft.com/fr-fr/library/aa995925\(v=exchg.150\))

[Remove-JournalRule](https://technet.microsoft.com/fr-fr/library/bb123489\(v=exchg.150\))

[Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\))

