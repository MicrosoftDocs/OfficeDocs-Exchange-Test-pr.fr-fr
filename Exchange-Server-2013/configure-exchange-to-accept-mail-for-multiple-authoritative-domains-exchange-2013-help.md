---
title: 'Configuration d’Exchange de manière à accepter des messages électroniques pour plusieurs domaines faisant autorité: Exchange 2013 Help'
TOCTitle: Configuration d’Exchange de manière à accepter des messages électroniques pour plusieurs domaines faisant autorité
ms:assetid: 11801f73-4934-4025-a1c1-3935dada7e9b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996314(v=EXCHG.150)
ms:contentKeyID: 51407156
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration d’Exchange de manière à accepter des messages électroniques pour plusieurs domaines faisant autorité

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-06-15_

Microsoft Exchange Server 2013 permet d'ajouter facilement à votre organisation plusieurs domaines faisant autorité. Toutefois, après avoir ajouté un domaine faisant autorité, vous devez choisir la manière de l'utiliser au sein de votre organisation. Par exemple :

  - Si vous voulez ajouter une adresse de messagerie dans le nouveau domaine faisant autorité pour des destinataires de votre organisation, voulez-vous remplacer l'adresse principale existante (de réponse) des destinataires, ou ajouter la nouvelle adresse en tant qu'adresse proxy (secondaire) ?

  - Voulez-vous que l'adresse de messagerie dans le domaine faisant autorité s'applique à tous les destinataires et à tous les types de destinataires ? Ou voulez-vous que la nouvelle adresse de messagerie s'applique à certains types de destinataires ou à certains destinataires en fonction de leurs propriétés d'utilisateur, par exemple, uniquement les utilisateurs du service financier ?

Les exemples suivants présentent des scénarios dans lesquels votre organisation Exchange peut devoir recevoir et traiter des messages électroniques pour plusieurs domaines SMTP faisant autorité :

  - Vous modifiez votre nom de domaine SMTP, mais vous devez continuer à accepter des messages électroniques pour l'ancien nom de domaine pendant un certain temps, au cas où des clients enverraient des messages aux anciennes adresses de messagerie. Vous pouvez définir la nouvelle adresse de messagerie comme adresse principale (de réponse). Cela signifie que la nouvelle adresse est l'adresse de messagerie par défaut affichée sur tous les messages électroniques envoyés par le destinataire. Vous pouvez définir l'ancienne adresse de messagerie comme adresse secondaire. Cela permet au destinataire de continuer à recevoir des messages électroniques envoyés à l'ancienne adresse de messagerie.

  - Vous voulez configurer plusieurs adresses de messagerie pour les différentes divisions de votre organisation. Par exemple, si la forêt Active Directory contoso.com contient des sous-domaines pour les filiales Tailspin Toys et Fourth Coffee, vous pouvez attribuer les noms de domaine SMTP contoso.com, tailspintoys.com et fourthcoffee.com aux destinataires de ces divisions.

  - Vous fournissez des services d'hébergement de messagerie et devez accepter des messages électroniques pour plusieurs noms de domaine SMTP.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 30 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Domaines acceptés » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md) et entrée « Stratégies d'adresse de messagerie » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Si vous disposez d’un serveur de transport Edge abonné dans votre réseau de périmètre, vous configurez les domaines acceptés sur un serveur de boîtes aux lettres dans votre organisation Exchange. La configuration des domaines acceptés est répliquée sur le serveur de transport Edge lors de la synchronisation EdgeSync. Pour plus d’informations, consultez la rubrique [Abonnements Edge](edge-subscriptions-exchange-2013-help.md).

  - Lorsque vous créez un domaine accepté, vous pouvez utiliser un caractère générique (\*) dans l'espace d'adressage pour indiquer que tous les sous-domaines de l'espace d'adressage SMTP sont également acceptés par l'organisation Exchange. Par exemple, pour configurer contoso.com et tous ses sous-domaines comme domaines acceptés, entrez **\*.contoso.com** en tant qu'espace d'adressage SMTP. Toutefois, si les noms de sous-domaines doivent être utilisés dans une stratégie d'adresse de messagerie, chaque sous-domaine doit avoir une entrée de domaine accepté explicite.

  - Un enregistrement MX dans un DNS public est requis pour chaque domaine SMTP pour lequel vous acceptez des messages électroniques en provenance d'Internet. Chaque enregistrement MX doit se résoudre dans le serveur côté Internet qui reçoit les messages électroniques pour votre organisation.

  - Vous devez configurer des connecteurs d'envoi et de réception de façon à ce que votre organisation Exchange puisse échanger des messages électroniques avec Internet. La configuration des connecteurs d'envoi et de réception Internet est déterminée par votre topologie Exchange. Pour plus d’informations sur la configuration des connecteurs, consultez la rubrique [Connecteurs](connectors-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Création d'un domaine faisant autorité

## Utilisation du Centre d'administration Exchange (CAE) pour créer un domaine faisant autorité

1.  Dans le CAE, accédez à **Flux de messagerie**\>**Domaines acceptés**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans le champ **Nom**, entrez le nom complet du domaine accepté. Chaque domaine accepté pour votre organisation doit avoir un nom complet unique. Il peut être différent de celui du domaine accepté. Par exemple, le domaine contoso.com pourrait avoir pour nom complet Contoso Local Accepted Domain.

3.  Dans le champ **Domaine accepté**, spécifiez un espace de noms SMTP pour lequel votre organisation accepte des messages électroniques. Par exemple, contoso.com.

4.  Sélectionnez **Domaine faisant autorité**.

5.  Cliquez sur **Enregistrer**.

## Utilisation de l'environnement de ligne de commande pour créer un domaine accepté

Pour créer un domaine faisant autorisé, utilisez la syntaxe suivante.

    New-AcceptedDomain -Name "<Unique Name>" -DomainName <SMTP domain> -DomainType Authoritative

Par exemple, pour créer un domaine faisant autorisé nommé « Fourth Coffee subsidiary » pour le domaine fourthcoffee.com, exécutez la commande suivante :

    New-AcceptedDomain -Name "Fourth Coffee subsidiary" -DomainName fourthcoffee.com -DomainType Authoritative

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien créé un domaine faisant autorité, procédez comme suit :

  - Dans le CAE, accédez à **Flux de messagerie** \> **Domaines acceptés**. Vérifiez que le domaine accepté que vous avez créé s'affiche, et que la valeur **Type de domaine** est **Faisant autorité**.

  - Dans l'environnement de ligne de commande, exécutez la commande **Get-AcceptedDomain**. Vérifiez que le domaine que vous avez créé s'affiche, et que la valeur **DomainType** est `Authoritative`.

## Étape 2 : Configuration d'une stratégie d'adresse de messagerie pour le domaine faisant autorité

Pour utiliser le domaine accepté faisant autorité que vous avez créé, vous devez configurer pour ce dernier une stratégie d'adresse de messagerie conforme aux objectifs de votre scénario. Par exemple, vous devez peut-être créer une stratégie d'adresse de messagerie ou modifier une stratégie existante. Vous pouvez remplacer l'adresse de messagerie principale pour les destinataires de votre choix, ou décider de conserver ou de supprimer l'ancienne adresse de messagerie principale. Cette section présente deux exemples de scénario.

## Modification de l'adresse de messagerie principale

Pour modifier l'adresse de messagerie principale (de réponse) attribuée à des destinataires en conservant l'adresse existante comme adresse secondaire (proxy), procédez comme suit :

## Utilisation du CAE pour modifier l'adresse de messagerie principale

1.  Dans le CAE, accédez à **Flux de messagerie** \> **Stratégies d'adresse de messagerie**. Sélectionnez la stratégie d'adresse de messagerie à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Stratégie d'adresse de messagerie**, cliquez sur **Format d'adresse de messagerie**. Dans la section **Format d'adresse de messagerie**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans la page **Format d'adresse de messagerie** qui s'affiche, opérez les sélections suivantes :
    
      - **Sélectionnez un domaine accepté**   Cliquez sur la liste déroulante, puis sélectionnez le nouveau domaine faisant autorité.
    
      - Sélectionnez **Définir ce format pour le l'adresse de réponse**.
    
    Lorsque vous avez terminé, cliquez sur **Enregistrer**.

4.  Dans la page **Stratégie d'adresse de messagerie**, cliquez sur **Enregistrer** pour enregistrer les modifications apportées à la stratégie.

5.  Un avertissement apparaît pour vous indiquer que la stratégie d’adresse de messagerie s’appliquera uniquement lorsque vous l’aurez mise à jour. Après sa création, sélectionnez-la puis, dans le volet des détails, cliquez sur **Appliquer**.

## Utilisation de l'environnement de ligne de commande pour modifier l'adresse de messagerie principale

Dans l'environnement de ligne de commande, vous utilisez deux commandes : l'une pour modifier la stratégie d'adresse de messagerie, et l'autre pour appliquer la stratégie mise à jour aux destinataires au sein de votre organisation.

Pour modifier l'adresse de messagerie principale en conservant l'adresse existante comme adresse proxy, exécutez la commande suivante :

    Set-EmailAddressPolicy <EmailAddressPolicyIdentity> -EnabledEmailAddressTemplates SMTP:<NewPrimaryEmailAddress>,smtp:<OldPrimaryEmailAddress>

Par exemple, supposons que la stratégie d'adresse de messagerie de votre organisation utilise le format d'adresse *useralias*`@contoso.com`. Cet exemple montre comment modifier le domaine de l'adresse principale (de réponse) dans la stratégie d'adresse de messagerie nommée « Default Policy » en `@fourthcoffee.com`, en conservant l'adresse de réponse principale existante dans le domaine `@contoso.com` comme adresse secondaire (proxy).

    Set-EmailAddressPolicy "Default Policy" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com,smtp:@contoso.com

> [!NOTE]
> Le qualificateur <code>SMTP</code> en majuscules spécifie l'adresse principale (de réponse). Le qualificateur <code>smtp</code> en minuscules spécifie une adresse secondaire (proxy).


Pour appliquer la stratégie d'adresse de messagerie mise à jour à des destinataires, utilisez la syntaxe suivante.

    Update-EmailAddressPolicy <EamilAddressPolicyIdentity>

Par exemple, pour appliquer la stratégie d'adresse de messagerie mise à jour nommée « Default Policy », exécutez la commande suivante :

    Update-EmailAddressPolicy "Default Policy"

## Remplacement de l'adresse de messagerie principale pour un ensemble filtré de destinataires

Vous ne pouvez pas modifier la stratégie d'adresse de messagerie par défaut à appliquer à un ensemble filtré de destinataires. Vous devez créer nouvelle stratégie d'adresse de messagerie ou modifier une stratégie existante. Les exemples figurant dans cette section montrent comment créer une stratégie d'adresse de messagerie. Dans ces exemples, l'adresse principale (de réponse) dans le nouveau domaine accepté remplace l'adresse principale pour les destinataires spécifiés sans conserver l'adresse principale existante comme adresse de messagerie secondaire (proxy). Les destinataires concernés ne peuvent donc plus recevoir de messages électroniques à leur ancienne adresse de messagerie principale.

De même, les stratégies d'adresse de messagerie qui s'appliquent à des utilisateurs spécifiques doivent avoir une priorité supérieure (indiquée par une valeur entière inférieure) à celle des autres stratégies d'adresse de messagerie, y compris la stratégie par défaut, de façon à ce que la stratégie spécifique soit appliquée en premier. Étant donné que deux stratégies ne peuvent pas avoir la même valeur de priorité, il se peut que vous deviez d'abord abaisser le niveau de priorité de la stratégie d'adresse de messagerie par défaut de votre organisation.

## Utilisation du CAE pour remplacer l'adresse de messagerie principale pour un ensemble filtré de destinataires

Pour créer des adresses de messagerie supplémentaires à utiliser comme adresses de messagerie principales pour un ensemble filtré de destinataires, procédez comme suit.

1.  Dans le CAE, accédez à **Flux de messagerie**\>**Stratégies d'adresse de messagerie**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  dans la page **Stratégie d'adresse de messagerie**, complétez les champs suivants :
    
    1.  **Nom de la stratégie**   Entrez un nom descriptif unique.
    
    2.  **Format d'adresse de messagerie**   Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la page **Format d'adresse de messagerie** qui s'affiche, opérez les sélections suivantes :
        
          - **Sélectionnez un domaine accepté**   Cliquez sur la liste déroulante, puis sélectionnez le nouveau domaine faisant autorité.
        
          - **Format d'adresse de messagerie**   Sélectionnez le format d'adresse de messagerie approprié pour votre organisation.
        
          - Sélectionnez **Définir ce format pour le l'adresse de réponse**.
        
        Lorsque vous avez terminé, cliquez sur **Enregistrer**.

3.  **Exécutez cette stratégie dans cet ordre avec d'autres stratégies**   Généralement, les stratégies d'adresse de messagerie qui s'appliquent à des utilisateurs spécifiques doivent avoir une priorité supérieure (indiquée par une valeur entière inférieure) à celle des autres stratégies d'adresse de messagerie, y compris la stratégie par défaut.

4.  **Spécifiez les types de destinataires auxquels s'applique cette adresse de messagerie**   Spécifiez les types de destinataires auxquels vous voulez appliquer la stratégie d'adresse de messagerie.

5.  **Créez des règles pour définir les destinataires auxquels cette stratégie d'adresse de messagerie s'applique**   Cliquez sur **Ajouter une règle** afin de limiter le nombre de destinataires auxquels cette stratégie doit s'appliquer. Cela a pour effet de créer une instruction booléenne **Et**. Répétez cette étape autant de fois que nécessaire.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous appliquez un trop grand nombre de règles, la stratégie d’adresse de messagerie peut être restreinte au point de ne plus contenir d’utilisateurs.</td>
    </tr>
    </tbody>
    </table>


6.  Cliquez sur **Afficher un aperçu des destinataires auxquels la stratégie s'applique** pour visualiser les destinataires auxquels cette stratégie doit s'appliquer.

7.  
    
    Cliquez sur **Enregistrer** pour enregistrer vos modifications et créer la stratégie.

8.  Un avertissement apparaît pour vous indiquer que la stratégie d’adresse de messagerie s’appliquera uniquement lorsque vous l’aurez mise à jour. Après sa création, sélectionnez-la puis, dans le volet des détails, cliquez sur **Appliquer**.

## Utilisation de l'environnement de ligne de commande pour remplacer l'adresse de messagerie principale pour un ensemble filtré de destinataires

Pour remplacer l'adresse de messagerie principale pour un ensemble filtré de destinataires, utilisez la commande suivante :

    New-EmailAddressPolicy -Name <Policy Name> -Priority <Integer> -IncludedRecipients <RecipientTypes> <Conditional Recipient Properties> -EnabledEmailAddressTemplates SMTP:@<NewPrimaryEmailAddress>

Cet exemple montre comment créer une stratégie d'adresse de messagerie nommée « Fourth Coffee Recipients », attribuer cette stratégie à des utilisateurs de boîtes aux lettres du service Fourth Coffee, et définir la priorité la plus haute pour cette stratégie afin qu'elle s'applique en premier. Notez que l'ancienne adresse de messagerie principale n'est pas conservée pour ces destinataires, de sorte qu'ils ne peuvent plus y recevoir de messages électroniques.

    New-EmailAddressPolicy -Name "Fourth Coffee Recipients" -Priority 1 -IncludedRecipients MailboxUsers -ConditionalDepartment "Fourth Coffee" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com

Pour appliquer la nouvelle stratégie d'adresse de messagerie aux destinataires concernés, exécutez la commande suivante :

    Update-EmailAddressPolicy "Fourth Coffee Recipients"

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien configuré une stratégie d'adresse de messagerie pour le domaine faisant autorité, effectuez l'une des opérations suivantes :

  - Dans le CAE, accédez à **Flux de messagerie** \> **Stratégies d'adresse de messagerie**. Vérifiez que les stratégies s'appliquent dans l'ordre correct. Sélectionnez des stratégies nouvelles ou mises à jour, puis, dans le volet des détails, vérifiez le format d'adresse de messagerie, y compris les destinataires, et si la stratégie a été appliquée,

  - Dans l’environnement Exchange Management Shell, exécutez les commandes **Get-EmailAddressPolicy** et `Get-EmailAddressPolicy "<Policy Name>"| Format-List` pour vérifier les détails des stratégies.

## Comment savoir si cette tâche a fonctionné ?

Pour vérifier que vous avez configuré Exchange pour accepter des messages électroniques pour plusieurs domaines faisant autorité, procédez comme suit :

1.  Envoyez un message de test à un destinataire concerné à partir d'une boîte aux lettres externe à votre organisation Exchange. Vérifiez si l'adresse de messagerie a accepté le message électronique.

2.  Envoyez un message de test à partir de la boîte aux lettres d'un destinataire concerné à un destinataire externe, puis vérifiez l'adresse de l'expéditeur du message.

