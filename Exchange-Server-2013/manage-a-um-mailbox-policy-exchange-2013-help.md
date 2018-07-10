---
title: 'Gérer une stratégie de boîte aux lettres de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Gérer une stratégie de boîte aux lettres de messagerie unifiée
ms:assetid: 704b001c-3e6f-4ed5-bbe5-42a778f6ac0d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998829(v=EXCHG.150)
ms:contentKeyID: 50555411
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMMailboxPolicyGeneralTab
ms.translationtype: MT
---

# Gérer une stratégie de boîte aux lettres de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Après avoir créé une stratégie de boîte aux lettres de messagerie unifiée, vous pouvez afficher ou configurer plusieurs paramètres. Par exemple, vous pouvez configurer les fonctionnalités de messagerie unifiée comme l'aperçu des messages vocaux ou la lecture sur téléphone ainsi que d'autres options de sécurité, telles que la messagerie vocale protégée et les paramètres de stratégie de code confidentiel.

Pour découvrir d'autres tâches de gestion relatives aux stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour gérer une stratégie de boîte aux lettres de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, cliquez sur l'option **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") de la barre d'outils.
    
      - L'onglet **Général** permet d'afficher et de configurer les paramètres d'une stratégie de boîte aux lettres de messagerie unifiée. Par exemple, vous pouvez afficher les plans de numérotation associés à la stratégie de boîte aux lettres de messagerie unifiée ou désactiver les notifications d'appels en absence pour les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée spécifique. Quand vous modifiez les paramètres disponibles dans une stratégie de boîte aux lettres de messagerie unifiée, ils sont appliqués à tous les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée. Vous pouvez afficher ou configurer les paramètres suivants :
        
          - **Plan de numérotation de messagerie unifiée**   Affiche le nom du plan de numérotation associé à la stratégie de boîte aux lettres de messagerie unifiée. Il s'agit du nom du plan de numérotation affiché dans l'environnement de ligne de commande Exchange Management Shell.
            
            Lors de sa création, la stratégie de boîte aux lettres de messagerie unifiée doit être associée à un plan de numérotation. Une fois la stratégie de boîte aux lettres de messagerie unifiée créée et associée au plan de numérotation, les paramètres définis dans la stratégie de boîte aux lettres sont appliqués aux utilisateurs associés au plan de numérotation. Par défaut, lors de la création d'un plan de numérotation de messagerie unifiée à l'aide de l'environnement de ligne de commande Exchange Management Shell, une stratégie de boîte aux lettres de messagerie unifiée est également créée.
        
          - **Nom**   Tapez le nom du plan de numérotation. Un nom de plan de numérotation de messagerie unifiée est obligatoire et doit être unique. Il est cependant uniquement utilisé à des fins d'affichage dans le CAE et l'environnement Shell. Si vous devez modifier le nom complet du plan de numérotation après sa création, vous devez d'abord supprimer le plan de numérotation de messagerie unifiée existant, puis créer un autre plan de numérotation avec le nom approprié. Si votre organisation utilise plusieurs plans de numérotation de messagerie unifiée, nous vous recommandons de leur attribuer des noms significatifs. La longueur maximale d'un nom de plan de numérotation de messagerie unifiée est de 64 caractères pouvant inclure des espaces. (Si vous effectuez une intégration à Microsoft Office Communications Server 2007 R2 ou à Microsoft Lync Server, il est déconseillé d'utiliser des espaces.) Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Limite de durée des messages d'accueil personnels (minutes)**   Cette zone de texte permet d'entrer le nombre maximal de minutes disponibles aux utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée pour enregistrer leur message d'accueil de messagerie vocale. Vous pouvez modifier ce paramètre après la création de la stratégie de boîte aux lettres de messagerie unifiée. Seuls les caractères numériques sont autorisés. La plage valide s'étend de 1 à 10 minutes. La valeur par défaut est 5 minutes.
        
          - **Autoriser l'aperçu de messagerie vocale**   Cochez cette case pour activer ou désactiver la fonctionnalité Aperçu de messagerie vocale pour les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée. L'activation de ce paramètre permet aux utilisateurs de recevoir le texte d'un message vocal dans le corps d'un message électronique ou d'un SMS. Le paramètre est activé par défaut.
        
          - **Autoriser les utilisateurs à configurer des règles de répondeur automatique**   Cochez cette case pour autoriser les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée à créer des règles de répondeur automatique. Si cette option est désactivée dans le plan de numérotation de messagerie unifiée, cette fonctionnalité ne sera pas disponible pour les utilisateurs à extension messagerie unifiée associés à la stratégie de boîte aux lettres de messagerie unifiée. Le paramètre est activé par défaut.
        
          - **Autoriser l'indicateur d'attente des messages**   Cochez ou décochez cette case pour activer ou désactiver l'indicateur d'attente des messages pour les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée. La fonctionnalité d'indicateur de message en attente est proposée dans la plupart des systèmes de messagerie vocale hérités. Dans sa forme la plus courante, un voyant s'allume sur le téléphone de l'utilisateur de la messagerie vocale pour lui signaler la présence d'un nouveau message vocal. L'indicateur de message en attente peut également envoyer un SMS sur le téléphone mobile d'un utilisateur à extension messagerie unifiée. Le paramètre est activé par défaut.
        
          - **Autoriser Outlook Voice Access**   Cochez ou décochez cette case pour activer ou désactiver l'accès à Outlook Voice Access pour les utilisateurs à extension messagerie unifiée associés à cette stratégie de boîte aux lettres de messagerie unifiée. Outlook Voice Access est une fonctionnalité utilisée par les utilisateurs à extension messagerie unifiée pour accéder à leur boîte aux lettres sur un téléphone. Par défaut, ce paramètre est activé.
        
          - **Autoriser les notifications d'appels en absence**   Cochez ou décochez cette case pour activer ou désactiver les notifications d'appels en absence pour les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée. Une notification d'appel en absence est un message électronique envoyé à la boîte aux lettres d'un utilisateur lorsque celui-ci ne répond pas à un message entrant. Ce message électronique diffère de celui qui contient le message électronique vocal laissé pour un utilisateur.
            
            > [!NOTE]
            > Lors de l'intégration locale de la messagerie unifiée et de Lync Server, les notifications d'appels en absence ne sont pas disponibles pour les utilisateurs qui ont une boîte aux lettres située sur un serveur de boîtes aux lettres Exchange 2007 ou Exchange 2010. Une notification d'appel en absence est générée lorsqu'un utilisateur se déconnecte avant l'envoi de l'appel vers la messagerie unifiée.
            
            En général, lorsqu'un utilisateur manque un appel entrant, il reçoit deux messages électroniques : un message électronique contenant le message électronique vocal et un message de notification d'appel en absence. Par défaut, les notifications d'appels en absence sont activées lors de la création d'une stratégie de boîte aux lettres de messagerie unifiée.
        
          - **Autoriser l'émission au téléphone pour la messagerie vocale**   Cochez ou décochez cette case pour activer ou désactiver la fonctionnalité Émettre au téléphone pour les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée. Cette option est activée par défaut et permet aux utilisateurs de lire leurs messages vocaux sur n'importe quel téléphone, notamment un téléphone de bureau ou mobile.
        
          - **Autoriser les télécopies entrantes**   Cochez ou décochez cette case pour activer ou désactiver les télécopies entrantes pour les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée. Par défaut, lorsque vous activez des utilisateurs pour la messagerie unifiée, leur boîte aux lettres peut recevoir des télécopies. Toutefois, si cette option est désactivée dans le plan de numérotation de messagerie unifiée, les utilisateurs à extension messagerie unifiée ne peuvent pas recevoir de télécopies. La stratégie de boîte aux lettres de messagerie unifiée est désactivée par défaut.
            
            Après avoir activé le paramètre **Autoriser les télécopies entrantes**, vous devez spécifier l'URL du serveur de télécopie du partenaire. Si la stratégie de boîte aux lettres de messagerie unifiée est associée à un plan de numérotation qui peut utiliser les protocoles TCP et TLS, vous devez entrer les URI pour ces deux protocoles.
        
          - **Aider Microsoft à améliorer l'aperçu de messagerie vocale**   Ces options permettent à Microsoft d'améliorer la qualité de l'aperçu de messagerie vocale. Vous pouvez activer les paramètres suivants :
            
              - **Autoriser l'analyse des messages vocaux laissés par les appelants**   Cette option vous permet d'améliorer la qualité de l'aperçu de messagerie vocale dans les futures versions de Microsoft Exchange en transférant des copies de messages vocaux à Microsoft en vue de leur analyse. Vous ne pouvez pas définir cette option si tous les messages vocaux sont protégés.
            
              - **Indiquer aux appelants que les messages vocaux peuvent être analysés**   Cette option permet d'indiquer aux appelants que les messages qu'ils laissent sont susceptibles d'être analysés par Microsoft pour améliorer la qualité de l'aperçu de messagerie vocale et leur permettre de se rétracter.
    
      - 
        
        L'option **Texte du message** permet de configurer les paramètres du texte des messages pour les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée. Par exemple, vous pouvez spécifier le texte du message électronique envoyé aux utilisateurs après la réinitialisation de leur code confidentiel de messagerie unifiée. Vous pouvez configurer les paramètres suivants :
        
          - **L'utilisateur n'est pas activé pour la messagerie unifiée**   Le texte saisi dans cette zone de texte s'affiche dans le message électronique envoyé aux utilisateurs lorsque ces derniers sont activés pour la messagerie unifiée. Lorsque la boîte aux lettres d'un destinataire est activée pour la messagerie unifiée et que les utilisateurs sont activés pour la messagerie vocale, un message d'accueil à la messagerie unifiée est envoyé à l'utilisateur. Cette zone de texte est limitée à 512 caractères et peut contenir une mise en forme HTML simple. Par défaut, aucun texte n'est défini dans cette zone de texte.
            
            Ce message d'accueil contient le texte de bienvenue et les informations de code confidentiel qui permettent à l'utilisateur d'accéder au système de messagerie unifiée ou vocale. Le texte entré dans cette zone de texte est inséré au bas du message d'accueil. Cette zone de texte permet d'inclure des informations telles que les numéros de téléphone du support technique de messagerie vocale ou des numéros Outlook Voice Access.
            
            Si aucun texte n'est entré dans cette zone de texte, le texte par défaut généré par le système de messagerie unifiée ou vocale est inclus dans le message électronique.
            
            Le texte entré dans cette zone peut être du texte brut. Il peut également contenir des balises de mise en forme HTML simples pour le mettre en évidence ou pour ajouter des liens hypertexte vers un autre contenu.
            
            **Exemple 1 :**  si vous avez des questions ou des suggestions sur le service de messagerie vocale, appelez le service d'assistance sur le poste 4200.
            
            **Exemple 2 :**  si vous avez des questions ou des suggestions sur le \<b\>service de messagerie vocale\</b\>, appelez le service d'assistance sur le poste 4200 ou visitez notre site web à l'adresse \<a href=”http://emp.contoso.com/itinfo/vmail”\>\</a\>.
        
          - **Lorsque le code confidentiel Outlook Voice Access d'un utilisateur est réinitialisé**   Le texte saisi dans cette zone de texte est inclus dans le message électronique envoyé aux utilisateurs à extension messagerie unifiée quand leur code confidentiel de messagerie unifiée est réinitialisé.
            
            Un code confidentiel est réinitialisé par le système de messagerie unifiée ou vocale si le nombre d'échecs de tentatives de connexion dépasse 10 (par défaut) ou si les utilisateurs le réinitialisent à l'aide des fonctionnalités de messagerie unifiée incluses dans Microsoft Outlook, Outlook Web App ou Outlook Voice Access à partir d'un téléphone. Cette zone de texte permet d'inclure des informations telles que des conseils de sécurité ou toute autre information de sécurité dans le message électronique.
            
            Si aucun texte n'est saisi dans cette zone, le texte par défaut généré par le système de messagerie unifiée est inclus dans le message électronique.
            
            Cette zone de texte peut contenir jusqu'à 512 caractères. Par défaut, aucun texte n'est défini dans cette zone de texte.
            
            Le texte entré dans cette zone peut être du texte brut. Il peut également contenir des balises de mise en forme HTML simples pour le mettre en évidence ou pour ajouter des liens hypertexte vers un autre contenu.
        
          - **Lorsqu'un utilisateur reçoit un message vocal**   Le texte saisi dans cette zone de texte est inclus dans le message électronique envoyé aux utilisateurs lorsqu'ils reçoivent un message vocal d'un appelant entrant. Par exemple, ce texte peut inclure des dédits de responsabilité contenant des informations sur le transfert de messages vocaux ou de stratégies de sécurité système, qui décrivent la manière appropriée de traiter les messages vocaux dans votre organisation.
            
            Si aucun texte n'est saisi dans cette zone de texte, le texte par défaut généré par le système est inclus dans le message électronique. Cette zone de texte peut contenir jusqu'à 512 caractères. Par défaut, aucun texte n'est défini dans cette zone de texte.
            
            Le texte entré dans cette zone peut être du texte brut. Il peut également contenir des balises de mise en forme HTML simples pour le mettre en évidence ou pour ajouter des liens hypertexte vers un autre contenu.
        
          - **Lorsqu'un utilisateur reçoit un message de télécopie**   Le texte saisi dans cette zone de texte est inclus dans le message électronique envoyé aux utilisateurs lorsqu'ils reçoivent un message de télécopie entrant dans leur boîte de réception. Cette zone de texte permet d'inclure des dédits de responsabilité contenant des informations sur le transfert de messages de télécopie et d'autres stratégies de sécurité système sur la manière appropriée de traiter les messages de télécopie dans votre organisation.
            
            Si aucun texte n'est saisi dans cette zone de texte, le texte par défaut généré par le système est inclus dans le message électronique. Cette zone de texte peut contenir jusqu'à 512 caractères. Par défaut, aucun texte n'est défini dans cette zone de texte.
    
      - 
        
        L'option **Stratégies de code confidentiel** permet de configurer les paramètres de code confidentiel pour les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée. Les codes confidentiels de messagerie unifiée permettent aux utilisateurs d'accéder à leur boîte de réception à partir d'un téléphone. En configurant les paramètres sur cette page, vous pouvez spécifier le nombre minimal de chiffres pour un code confidentiel de messagerie unifiée ou le nombre d'échecs de tentative de connexion avant que l'utilisateur ne se voie refuser l'accès à sa boîte aux lettres de messagerie unifiée.
        
        Veillez à planifier soigneusement les stratégies de code confidentiel de messagerie unifiée que vous implémentez dans votre environnement. Si vous ne planifiez et n'implémentez pas les stratégies de code confidentiel de messagerie unifiée appropriées, il se peut que vous introduisiez des menaces de sécurité et autorisiez par mégarde des accès non autorisés à votre réseau. Vous pouvez configurer les paramètres suivants :
        
          - **Longueur minimale du code confidentiel (chiffres)**   Cette zone de texte permet de spécifier le nombre minimal de chiffres qu'un code confidentiel d'utilisateur de messagerie unifiée peut contenir. Le paramètre par défaut est de six chiffres. La plage s'étend de 4 à 24 chiffres. Ce paramètre ne peut pas être désactivé.
            
            L'augmentation du nombre de chiffres requis pour un code confidentiel augmente le niveau de sécurité de votre système de messagerie unifiée. Une réduction du nombre de chiffres requis pour un code confidentiel réduit le niveau de sécurité de votre réseau. Plus le nombre de chiffres requis pour un code confidentiel est faible, plus il est aisé pour d'éventuels pirates de deviner le code confidentiel d'un utilisateur.
            
            Si la valeur de ce paramètre est trop élevée, les utilisateurs risquent d'oublier leur code confidentiel. En revanche, si elle est trop basse, vous créez un risque d'accès non autorisé au système de messagerie unifiée.
        
          - **Nombre de recyclages du code confidentiel**   Ce paramètre permet de définir le nombre de codes confidentiels uniques que les utilisateurs doivent utiliser avant de pouvoir utiliser à nouveau un ancien code confidentiel. Pour la plupart des organisations, cette valeur doit être définie sur la valeur par défaut de 5 codes confidentiels mémorisés par le système. L'historique des codes confidentiels ne peut pas être désactivé.
            
            Vous pouvez définir cette valeur sur un chiffre compris entre 1 et 20. Une valeur trop élevée risque d'incommoder les utilisateurs, car il peut s'avérer difficile de mémoriser de nombreux codes confidentiels. Une valeur trop basse peut introduire une menace de sécurité dans votre réseau.
        
          - **Autoriser les modèles courants de codes confidentiels**   Ce paramètre permet de définir les exigences de complexité du code confidentiel pour la messagerie unifiée. Ces exigences de complexité sont appliquées lors de la modification ou la création de codes confidentiels.
            
            Si cette option est désactivée, les chiffres séquentiels et répétés ainsi que le suffixe du poste de boîte aux lettres sont rejetés. Si cette option est activée, seul le suffixe du poste de boîte aux lettres est rejeté.
            
            Par souci de sécurité, nous vous recommandons de désactiver ce paramètre. Si ce paramètre est désactivé, les codes confidentiels de l'utilisateur ne peuvent pas contenir les éléments suivants :
            
            des chiffres séquentiels, tels que 123456 ou 456789 ;
            
            des chiffres répétés, tels que 111111 ou 8888888 ;
            
            le suffixe du poste de boîtes aux lettres.
        
          - **Appliquer la durée de vie du code confidentiel (jours)**   Cette zone de texte permet de configurer le nombre de jours avant l'expiration du code confidentiel d'un utilisateur à extension messagerie unifiée. Après expiration du code confidentiel, l'utilisateur doit définir un nouveau code confidentiel de messagerie unifiée. Pour la plupart des organisations, cette valeur doit être définie par défaut sur 60 jours.
            
            La valeur de ce paramètre est comprise entre 0 et 999. Si elle est définie sur 0, les codes confidentiels n'expirent jamais. Un paramétrage trop bas de cette valeur peut incommoder les utilisateurs, car ils doivent créer et mémoriser des codes confidentiels trop fréquemment.
        
          - **Nombre d'échecs de connexion avant réinitialisation du code confidentiel**   Cette zone de texte permet d'entrer le nombre de tentatives d'échecs de connexion qui peuvent survenir avant la réinitialisation automatique du code confidentiel de l'utilisateur par le système de messagerie unifiée. Pour la plupart des organisations, cette valeur doit être définie par défaut sur 5 tentatives.
            
            La valeur de ce paramètre peut être comprise entre 0 et 999. Si vous paramétrez cette valeur sur 0, ce paramètre est désactivé et le système ne réinitialise pas automatiquement le code confidentiel de l'utilisateur. La définition d'une valeur trop basse pour ce paramètre peut incommoder les utilisateurs et la définition d'une valeur trop élevée permet à des utilisateurs malveillants de bénéficier d'un plus grand nombre de tentatives pour deviner le code confidentiel.
            
            Ce paramètre doit être défini sur un nombre inférieur au nombre configuré dans le paramètre **Nombre d'échecs de connexion avant verrouillage**. Ce paramètre est conçu pour empêcher les tentatives de piratage en force des codes confidentiels des utilisateurs.
        
          - **Nombre d'échecs de connexion avant verrouillage**   Cette zone de texte permet d'entrer le nombre maximal d'échecs de tentative de connexion successifs avant que les utilisateurs ne se voient refuser l'accès à leur boîte aux lettres.
            
            Par exemple, si un utilisateur tente de se connecter à sa boîte aux lettres cinq fois de suite sans succès, en vertu du paramètre **Nombre d'échecs de connexion avant réinitialisation du code confidentiel**, le système réinitialise le code confidentiel de l'utilisateur. Si l'utilisateur tente d'utiliser son nouveau code confidentiel plus de cinq fois sans succès, le système réinitialise le code confidentiel. Si l'utilisateur tente d'utiliser ce nouveau code confidentiel plus de cinq fois sans succès, son accès à la boîte aux lettres est verrouillé. Une fois l'accès verrouillé, un administrateur doit manuellement réinitialiser ou déverrouiller la boîte aux lettres pour l'utilisateur.
            
            Cette valeur peut être comprise entre 1 et 999. La définition d'une valeur trop basse pour ce paramètre peut incommoder les utilisateurs et la définition d'une valeur trop élevée permet à des utilisateurs malveillants de bénéficier d'un plus grand nombre d'essais pour deviner le code confidentiel. Pour la plupart des organisations, cette valeur doit être définie par défaut sur 15 tentatives.
            
            Ce paramètre doit être défini sur un nombre supérieur au nombre configuré dans le paramètre **Nombre d'échecs de connexion avant réinitialisation du code confidentiel**. Ce paramètre est conçu pour empêcher les tentatives de piratage en force des codes confidentiels des utilisateurs.
    
      - 
        
        L'option **Autorisation de numérotation** permet de configurer les règles de numérotation pour les utilisateurs à extension messagerie unifiée qui sont associés à cette stratégie de boîte aux lettres de messagerie unifiée.
        
        Vous pouvez utiliser ces paramètres pour contrôler les numéros des postes pouvant être joints ou les numéros de téléphone pouvant être composés par des utilisateurs à extension messagerie unifiée associés à cette stratégie de boîte aux lettres de messagerie unifiée. Vous pouvez configurer les paramètres suivants :
        
          - **Appels dans le même plan de numérotation de messagerie unifiée**   Si vous cochez cette case, les utilisateurs à extension messagerie unifiée qui appellent un numéro d'accès d'abonné configuré sur un plan de numérotation et qui parviennent à se connecter à leur boîte aux lettres sont autorisés à effectuer ou à transférer des appels vers des utilisateurs à extension messagerie unifiée disposant de numéros de postes au sein du même plan de numérotation. Par défaut, ce paramètre est activé.
            
            Lorsque ce paramètre est désactivé, les utilisateurs à extension messagerie unifiée qui appellent un numéro d'accès d'abonné configuré sur un plan de numérotation et parviennent à se connecter à leur boîte aux lettres ne peuvent pas établir d'appels vers des utilisateurs sans extension messagerie unifiée ou d'autres numéros de poste non associés à un utilisateur à extension messagerie unifiée. Ils ne peuvent pas non plus transférer les appels à des utilisateurs à extension messagerie unifiée au sein du même plan de numérotation. Cela est dû au fait que le paramètre **Appels vers toutes les extensions** est activé par défaut.
        
          - **Appels vers tous les postes**   Lorsque ce paramètre est activé, les utilisateurs qui appellent un numéro d'accès d'abonné configuré sur un plan de numérotation et parviennent à se connecter à leur boîte aux lettres peuvent effectuer des appels vers des utilisateurs sans extension messagerie unifiée, d'autres numéros de postes non associés à un utilisateur à extension messagerie unifiée et des utilisateurs à extension messagerie unifiée au sein du même plan de numérotation. Cela est dû au fait que le paramètre **Appels dans le même plan de numérotation de messagerie unifiée** est activé par défaut.
            
            Lorsque ce paramètre est désactivé, les utilisateurs qui appellent un numéro Outlook Voice Access configuré sur un plan de numérotation et qui parviennent à se connecter à leur boîte aux lettres ne peuvent pas effectuer d'appels vers des utilisateurs sans extension messagerie unifiée ou d'autres numéros de postes non associés à un utilisateur à extension messagerie unifiée. Ils peuvent cependant effectuer ou transférer des appels vers des numéros de poste associés à des utilisateurs à extension messagerie unifiée. Cela est dû au fait que le paramètre **Appels dans le même plan de numérotation de messagerie unifiée** est activé par défaut. Par défaut, le paramètre **Appels vers tous les postes** est activé.
            
            Vous pouvez activer ce paramètre dans un environnement où tous les utilisateurs ne sont pas activés pour la messagerie unifiée. Ce paramètre est également utile si vous voulez autoriser des utilisateurs qui appellent un numéro Outlook Voice Access configuré sur un plan de numérotation à appeler des numéros de poste non associés à un utilisateur à extension messagerie unifiée.
        
          - **Groupes de règles de numérotation nationale/régionale autorisés**   Cette section permet d'ajouter ou de supprimer des groupes autorisés de règles de numérotation dans le pays/la région. Par défaut, aucun groupe de règles de numérotation nationale/régionale n'est configuré dans les stratégies de boîte aux lettres de messagerie unifiée.
            
            Les groupes de règles de numérotation nationale/régionale permettent d'autoriser ou de limiter les numéros de téléphone à l'intérieur d'un pays ou d'une région que des utilisateurs d'Outlook Voice Access peuvent composer. Cela permet d'empêcher des appels et frais téléphoniques superflus ou non autorisés.
            
            Pour ajouter des groupes de règles de numérotation nationale/régionale, vous devez commencer par créer les groupes de règles de numérotation nationale/régionale appropriés dans le plan de numérotation associé à la stratégie de boîte aux lettres de messagerie unifiée, puis ajouter les entrées de règle de numérotation appropriées dans le groupe de règles de numérotation. Après avoir créé les groupes de règles de numérotation appropriés pour le plan de numérotation, vous devez les ajouter à la liste des restrictions de numérotation sous **Autorisation de numérotation** dans la stratégie de boîte aux lettres de messagerie unifiée.
            
            Les groupes de règles de numérotation nationale/régionale permettent à la messagerie unifiée d'autoriser ou de limiter l'accès à des numéros de téléphone à l'intérieur d'un pays ou d'une région. Ceci s'applique aux utilisateurs d'Outlook Voice Access qui ont appelé un numéro Outlook Voice Access.
        
          - **Groupes autorisés de règles de numérotation à l'international**   Cette section permet d'ajouter ou de supprimer des groupes autorisés de règles de numérotation à l'international. Par défaut, aucun groupe de règles de numérotation à l'international n'est configuré dans les stratégies de boîte aux lettres de messagerie unifiée.
            
            Pour ajouter des groupes de règles de numérotation à l'international, vous devez commencer par créer les groupes de règles de numérotation internationale appropriés dans le plan de numérotation associé à la stratégie de boîte aux lettres de messagerie unifiée, puis ajouter les entrées de règle de numérotation appropriées pour le groupe de règles de numérotation. Après avoir créé les groupes de règles de numérotation appropriés, vous devez les ajouter à la liste des restrictions de numérotation dans la stratégie de boîte aux lettres de messagerie unifiée.
            
            Les groupes de règles de numérotation internationale permettent à la messagerie unifiée d'autoriser ou de limiter l'accès à des numéros de téléphone à l'extérieur d'un pays ou d'une région. Ceci s'applique aux utilisateurs d'Outlook Voice Access qui ont appelé un numéro Outlook Voice Access.
            
            Les groupes de règles de numérotation à l'international permettent d'autoriser ou de limiter les numéros de téléphone à l'extérieur d'un pays ou d'une région que des utilisateurs d'Outlook Voice Access peuvent composer. Cela permet d'empêcher des appels et frais téléphoniques superflus ou non autorisés.
    
      - 
        
        L'option **Messagerie vocale protégée** permet de configurer les paramètres suivants :
        
          - **Protéger les messages vocaux des appelants non authentifiés**   Activez l'une des options suivantes dans la liste déroulante pour déterminer si un appel entrant réceptionné par la messagerie unifiée protégera les messages vocaux. Ce paramètre s'applique aux messages vocaux envoyés aux utilisateurs à extension messagerie unifiée quand ils ne répondent pas à leur téléphone. Il s'applique également aux messages vocaux envoyés directement aux utilisateurs à extension messagerie unifiée quand l'appelant utilise un standard automatique de messagerie unifiée. Vous pouvez configurer les paramètres suivants :
            
            **Aucun**   Quand ce paramètre est défini, aucune protection n'est appliquée aux messages vocaux envoyés aux utilisateurs à extension messagerie unifiée.
            
            **Privé**   Quand ce paramètre est défini, une protection est appliquée uniquement aux messages vocaux qui ont été marqués comme privés par l'appelant.
            
            **Tous**   Quand ce paramètre est défini, une protection est appliquée à tous les messages vocaux, y compris à ceux qui ne sont pas marqués comme étant privés.
        
          - **Protéger les messages vocaux des appelants authentifiés**   Activez l'une des options suivantes dans la liste déroulante pour déterminer si un appel entrant réceptionné par la messagerie unifiée protégera les messages vocaux. Ce paramètre s'applique aux messages vocaux envoyés aux utilisateurs à extension messagerie unifiée quand ils ne répondent pas à leur téléphone. Il s'applique également lorsque les appelants se connectent à leur boîte aux lettres à l'aide d'Outlook Voice Access, puis qu'ils créent et envoient un message vocal. Vous pouvez configurer les paramètres suivants :
            
            **Aucun**   Quand ce paramètre est défini, aucune protection n'est appliquée aux messages vocaux envoyés aux utilisateurs à extension messagerie unifiée.
            
            **Privé**   Quand ce paramètre est défini, une protection est appliquée uniquement aux messages vocaux qui ont été marqués comme privés par l'appelant.
            
            **Tous**   Quand ce paramètre est défini, une protection est appliquée à tous les messages vocaux, y compris à ceux qui ne sont pas marqués comme étant privés.
        
          - **Émettre au téléphone requis pour les messages vocaux protégés**   Cochez cette case si vous désirez forcer les utilisateurs qui reçoivent des messages vocaux protégés à utiliser la fonctionnalité Émettre au téléphone. Sinon, au cas où le logiciel client ne prend pas en charge la gestion des droits, les utilisateurs doivent utiliser Outlook Voice Access. La fonctionnalité Émettre au téléphone ne s'applique qu'aux clients utilisant une version d'Outlook prenant en charge la gestion des droits. Pour Outlook 2007 et les versions antérieures qui ne prennent pas en charge la gestion des droits, ainsi que pour les clients Outlook Web App, Outlook Voice Access est le seul moyen par lequel des utilisateurs peuvent écouter leurs messages vocaux protégés.
            
            Le paramètre par défaut exige que tous les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée utilisent la fonctionnalité Émettre au téléphone, afin d'écouter les messages vocaux qui sont protégés. Cela empêche d'autres personnes d'écouter le message vocal à partir d'un lecteur multimédia sur des haut-parleurs d'ordinateur ou sur un téléphone mobile. Même si ce paramètre est activé, un utilisateur à extension messagerie unifiée peut toujours utiliser Outlook Voice Access pour écouter le message vocal protégé.
            
            Cela s'avère particulièrement utile lorsque des utilisateurs à extension messagerie unifiée utilisent des ordinateurs publics, des ordinateurs portables dans des lieux publics ou le lecteur multimédia de leur téléphone pour écouter les messages vocaux protégés contenant potentiellement des informations privées.
        
          - **Autoriser les réponses vocales aux éléments de messagerie et de calendrier**   Cette option permet aux utilisateurs à extension messagerie unifiée d'envoyer des réponses vocales aux messages vocaux protégés. Par défaut, cette option est activée. Si vous désactivez cette option et qu'un utilisateur à extension messagerie unifiée reçoit un message vocal protégé, il ne pourra pas utiliser Outlook Voice Access pour répondre aux éléments de messagerie et de calendrier.
        
          - **Message à envoyer aux utilisateurs ne disposant pas de la prise en charge de la gestion des droits Windows**   La messagerie vocale protégée n'est accessible qu'aux clients de messagerie qui prennent en charge les droits relatifs à l'information (IRM) ou si un utilisateur à extension messagerie unifiée utilise Outlook Voice Access pour accéder au message vocal protégé.
            
            Si un message vocal protégé est envoyé à un client de messagerie qui ne prend pas en charge la technologie IRM, le texte que vous incluez dans cette case sera envoyé à l'utilisateur dans un message électronique. Ces informations doivent inclure des instructions sur la procédure à suivre pour recevoir le message vocal protégé.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour gérer une stratégie de boîte aux lettres de messagerie unifiée

Ce premier exemple définit les paramètres de code confidentiel pour les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN that is used to allow you access to your mailbox using Outlook Voice Access has been reset."

Ce second exemple sélectionne les groupes nationaux ou régionaux et les groupes internationaux à partir de ceux configurés dans le plan de commutation de messagerie unifiée associé à la stratégie de boîte aux lettres de messagerie unifiée. Les utilisateurs à extension messagerie unifiée associés à cette stratégie de boîte aux lettres de messagerie unifiée peuvent établir des appels sortants en fonction des règles définies pour ces groupes.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowDialPlanSubscribers $true -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2 -AllowExtensions $true 

Cet exemple montre comment configurer le texte des messages vocaux envoyés aux utilisateurs à extension messagerie unifiée, ainsi que le texte inclus dans un message électronique envoyé à un utilisateur à extension messagerie unifiée.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You have been enabled for Unified Messaging." -VoiceMailText "You have received a voice message from Microsoft Exchange 2013 Unified Messaging." 

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher les propriétés des stratégies de boîte aux lettres de messagerie unifiée

Cet exemple montre comment renvoyer une liste mise en forme de toutes les stratégies de boîte aux lettres de messagerie unifiée dans la forêt Active Directory.

    Get-UMMailboxPolicy | Format-List

Cet exemple montre comment renvoyer les propriétés et les valeurs pour une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy`.

    Get-UMMailboxPolicy -Identity MyUMMailboxPolicy

