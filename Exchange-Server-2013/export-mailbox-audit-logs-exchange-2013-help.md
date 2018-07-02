---
title: 'Exporter les journaux d’audit de boîte aux lettres: Exchange 2013 Help'
TOCTitle: Exporter les journaux d’audit de boîte aux lettres
ms:assetid: b458a95a-3321-4647-8884-cf97f8e7186a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150552(v=EXCHG.150)
ms:contentKeyID: 50477376
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exporter les journaux d’audit de boîte aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Lorsque l’audit de boîte aux lettres est activé pour une boîte aux lettres, Microsoft Exchange entre les informations dans le *journal d’audit de la boîte aux lettres* chaque fois qu’un utilisateur autre que le propriétaire accède à la boîte aux lettres. Chaque entrée du journal inclut des informations sur qui a accédé à la boîte aux lettres et quand, les actions effectuées par le non-propriétaire, et si l’action a réussi. Par défaut, les entrées dans le journal d’audit de boîtes aux lettres sont conservées pendant 90 jours. Vous pouvez utiliser le journal d’audit de la boîte aux lettres pour déterminer si un utilisateur autre que le propriétaire a accédé à une boîte aux lettres.

Lorsque vous exportez des entrées des journaux d’audit de boîte aux lettres, Microsoft Exchange enregistre les entrées dans un fichier XML et l’inclut en pièce jointe dans un message électronique envoyé aux destinataires spécifiés.

**Contenu de cette rubrique**

Avant de commencer

Configurer l’enregistrement d’audit de boîte aux lettres

Exporter le journal d’audit de boîte aux lettres

Consulter le journal d’audit de boîte aux lettres

Plus d’informations

## Avant de commencer

  - Durée d’exécution estimée de chaque procédure : Les durées sont variables. Dans Exchange Online, le journal d’audit de la boîte aux lettres est envoyé quelques jours après son exportation.

  - Dans Exchange Online, vous devez utiliser la session Windows PowerShell distante pour réaliser un grand nombre des procédures décrites dans cette rubrique. Pour plus d’informations, consultez la rubrique [Connexion à Exchange Online à l'aide de Remote PowerShell](https://technet.microsoft.com/fr-fr/library/jj984289\(v=exchg.150\)).

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

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


## Configurer l’enregistrement d’audit de boîte aux lettres

Vous devez activer l’enregistrement d’audit de boîte aux lettres sur chaque boîte aux lettres que vous souhaitez auditer avant de pouvoir exporter et consulter des journaux d’audit de boîte aux lettres. Vous devez aussi configurer Microsoft Outlook Web App pour autoriser les pièces jointes XML afin de pouvoir utiliser Outlook Web App pour accéder au journal d’audit.

## Étape 1 : Activer l’enregistrement d’audit de boîte aux lettres

Vous devez activer l’enregistrement d’audit de boîte aux lettres pour chaque boîte aux lettres pour laquelle vous souhaitez exécuter un rapport d’accès aux boîtes aux lettres par un non-propriétaire. Si l’enregistrement d’audit de boîte aux lettres n’est pas activé pour une boîte aux lettres, vous n’obtiendrez pas de résultats concernant cette boîte aux lettres lorsque vous exporterez le journal d’audit de boîte aux lettres.

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Journaux d’audit des boîtes aux lettres » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Pour activer l’enregistrement d’audit de boîte aux lettres pour une boîte aux lettres unique, exécutez la commande dans l’environnement de ligne de commande Exchange Management Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

Pour activer l’enregistrement d’audit de boîte aux lettres pour toutes les boîtes aux lettres des utilisateurs de votre organisation, exécutez les commandes suivantes.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}

    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

## Étape 2 : Configurer Outlook Web App pour autoriser les pièces jointes XML

Lorsque vous exportez le journal d’audit de boîte aux lettres, Microsoft Exchange joint le journal d’audit, qui est un fichier XML, à un message électronique. Toutefois, Outlook Web App bloque les pièces jointes XML par défaut. Pour accéder au journal d’audit exporté, vous devez utiliser Microsoft Outlook ou configurer Outlook Web App pour que les pièces jointes XML soient autorisées.

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée Outlook Web App » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Exécutez les procédures suivantes pour autoriser les pièces jointes XML dans Outlook Web App. Dans Exchange Server 2013, utilisez la valeur `Default` pour le paramètre *Identity*.

1.  Exécutez la commande suivante pour ajouter XML à la liste des types de fichiers autorisés dans Outlook Web App.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -AllowedFileTypes @{add='.xml'}

2.  Exécutez la commande suivante pour supprimer XML de la liste des types de fichiers bloqués dans Outlook Web App.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -BlockedFileTypes @{remove='.xml'}

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré l’enregistrement d’audit de boîte aux lettres, procédez comme suit :

1.  Exécutez la commande suivante pour vérifier que l’enregistrement d’audit est configuré pour les boîtes aux lettres.
    
        Get-Mailbox | FL Name,AuditEnabled
    
    Une valeur de `True` pour la propriété *AuditEnabled* vérifie que la journalisation d'audit est activée.

2.  Exécutez la commande suivante pour vérifier que les pièces jointes XML sont autorisées dans Outlook Web App.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty AllowedFileTypes
    
    Vérifiez que `.xml` est inclus dans la liste des types de fichier autorisés.

3.  Exécutez la commande suivante pour vérifier que les pièces jointes XML sont supprimées de la liste de fichiers bloqués dans Outlook Web App.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty BlockedFileTypes
    
    Vérifiez que `.xml` n’est pas inclus dans la liste des types de fichiers bloqués.

Retour au début

## Exporter le journal d’audit de boîte aux lettres

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Enregistrement d’audit d’administrateur en affichage seul » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

1.  Dans le Centre d’administration Exchange (CAE), rendez-vous sur **Gestion de la conformité** \> **Audit**.

2.  Cliquez sur **Exporter les journaux d’audit de boîte aux lettres**.

3.  Configurez les critères de recherche suivants pour l’exportation des entrées du journal d’audit de boîte aux lettres :
    
      - **Dates de début et de fin**   Sélectionnez la plage de dates pour les entrées à inclure dans le fichier exporté.
    
      - **Boîtes aux lettres à rechercher dans le journal d’audit**   Sélectionnez les boîtes aux lettres pour lesquelles récupérer des entrées de journal d’audit.
    
      - **Type d’accès non-propriétaire**   Sélectionnez une des options suivantes pour définir le type d’accès non-propriétaire pour lequel récupérer des entrées :
        
          - **Tous les non-propriétaires**   Recherchez les accès par les administrateurs et les utilisateurs délégués au sein de votre organisation, et par les administrateurs du centre de données Microsoft dans Exchange Online.
        
          - **Utilisateurs externes**   Recherchez les accès par les administrateurs du centre de données Microsoft.
        
          - **Administrateurs et utilisateurs délégués**   Recherchez les accès par les administrateurs et les utilisateurs délégués au sein de votre organisation.
        
          - **Administrateurs**   Recherchez les accès par les administrateurs au sein de votre organisation.
    
      - **Destinataires**   Sélectionnez les utilisateurs auxquels envoyer le journal d’audit de la boîte aux lettres.

4.  Cliquez sur **Exporter**.
    
    Microsoft Exchange récupère les entrées du journal d’audit de boîte aux lettres qui répondent à vos critères de recherche, les enregistre dans un fichier nommé SearchResult.xml, puis joint le fichier XML à un message électronique envoyé aux destinataires que vous avez indiqués.

## Comment savoir si cela a fonctionné ?

Connectez-vous à la boîte aux lettres à laquelle le journal d’audit de la boîte aux lettres a été envoyé. Si vous avez bien exporté le journal d’audit, vous recevrez un message envoyé depuis Exchange. Dans Exchange Online, la réception de ce message peut prendre plusieurs jours. Le journal d’audit de la boîte aux lettres (nommé SearchResult.xml) sera joint à ce message. Si vous avez correctement configuré Outlook Web App afin que les pièces jointes XML soient autorisées, vous pouvez télécharger le fichier XML joint.

Retour au début

## Consulter le journal d’audit de boîte aux lettres

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Enregistrement d’audit d’administrateur en affichage seul » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

Pour enregistrer et afficher le fichier SearchResult.xml, procédez comme suit :

1.  Connectez-vous à la boîte aux lettres à laquelle le journal d’audit de la boîte aux lettres a été envoyé.

2.  Dans la boîte de réception, ouvrez le message contenant la pièce jointe de fichier XML envoyée par Microsoft Exchange. Remarquez que le corps du message électronique contient les critères de recherche.

3.  Cliquez sur la pièce jointe et sélectionnez-la pour télécharger le fichier XML.

4.  Ouvrez SearchResult.xml dans Microsoft Excel.

Retour au début

## Plus d’informations

  - **Entrées dans le journal d’audit de la boîte aux lettres**   L’exemple suivant présente une entrée du journal d’audit de la boîte aux lettres contenu dans le fichier SearchResult.xml. Chaque entrée est précédée par la balise XML **\<Event\>** et se termine par la balise XML **\</Event\>**. Cette entrée indique que l’administrateur a supprimé le message avec l’objet « **Notification of litigation hold** » du dossier Éléments récupérables dans la boîte aux lettres de David le 30 avril 2010.
    
        <Event MailboxGuid="6d4fbdae-e3ae-4530-8d0b-f62a14687939" 
          Owner="PPLNSL-dom\david50001-1363917750" 
          LastAccessed="2010-04-30T11:01:55.140625-07:00" 
          Operation="HardDelete" 
          OperationResult="Succeeded" 
          LogonType="Admin"
         FolderId="0000000073098C3277988F4CB882F5B82EBF64610100A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000"
          FolderPathName="\Recoverable Items\Deletions"
          ClientInfoString="Client=OWA;Action=ViaProxy" 
          ClientIPAddress="10.196.241.168" 
          InternalLogonType="Owner"
          MailboxOwnerUPN="david@contoso.com"
          MailboxOwnerSid="S-1-5-21-290112810-296651436-1966561949-1151" 
          CrossMailboxOperation="false" 
          LogonUserDN="Administrator"
          LogonUserSid="S-1-5-21-290112810-296651436-1966561949-1149">
          <SourceItems>
           <ItemId="0000000073098C3277988F4CB882F5B82EBF64610700A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000A7C317F68C24304BBD18ABE1F185E79B00000026BD540"
            Subject="Notification of litigation hold"
            FolderPathName="\Recoverable Items\Deletions" /> 
          </SourceItems>
        </Event>

  - **Champs utiles dans le journal d’audit de la boîte aux lettres**   Voici une description des champs utiles dans le journal d’audit de la boîte aux lettres. Ils peuvent vous aider à identifier les informations spécifiques à propos de chaque instance d’accès non-propriétaire à une boîte aux lettres.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Champ</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Owner</strong></p></td>
    <td><p>Propriétaire de la boîte aux lettres à laquelle un non-propriétaire a accédé.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>LastAccessed</strong></p></td>
    <td><p>Date et heure de l’accès à la boîte aux lettres.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Operation</strong></p></td>
    <td><p>Action effectuée par le non-propriétaire. Pour plus d’informations, consultez la section « Éléments enregistrés dans le journal d’audit de la boîte aux lettres » de la rubrique <a href="https://technet.microsoft.com/fr-fr/library/jj156300(v=exchg.150)">En savoir plus sur l’exécution d’un rapport d’accès aux boîtes aux lettres par des non-propriétaires</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OperationResult</strong></p></td>
    <td><p>Si l’action effectuée par le non-propriétaire a réussi ou échoué.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonType</strong></p></td>
    <td><p>Type d’accès non-propriétaire. Ceux-ci incluent administrateur, délégué et externe.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>FolderPathName</strong></p></td>
    <td><p>Nom du dossier qui a contenu le message qui a été affecté par le non-propriétaire.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>ClientInfoString</strong></p></td>
    <td><p>Informations sur le client de messagerie utilisé par le non-propriétaire pour accéder à la boîte aux lettres.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ClientIPAddress</strong></p></td>
    <td><p>Adresse IP de l’ordinateur utilisée par le non-propriétaire pour accéder à la boîte aux lettres.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>InternalLogonType</strong></p></td>
    <td><p>Type d’ouverture de session du compte utilisé par le non-propriétaire pour accéder à cette boîte aux lettres.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>MailboxOwnerUPN</strong></p></td>
    <td><p>Adresse de messagerie du propriétaire de boîte aux lettres.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonUserDN</strong></p></td>
    <td><p>Nom d’affichage du non-propriétaire.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Subject</strong></p></td>
    <td><p>Ligne d’objet du message électronique qui a été affecté par le non-propriétaire.</p></td>
    </tr>
    </tbody>
    </table>
    
    Retour au début

