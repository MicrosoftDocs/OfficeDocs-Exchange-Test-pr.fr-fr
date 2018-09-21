---
title: 'Configurer une approbation de fédération: Exchange 2013 Help'
TOCTitle: Configurer une approbation de fédération
ms:assetid: 7c2b539f-faed-4374-8578-9f329ca628db
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657462(v=EXCHG.150)
ms:contentKeyID: 50478535
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer une approbation de fédération

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-07-26_

Une approbation de fédération établit une relation d’approbation entre une organisation Microsoft Exchange 2013 et le système d’authentification Azure Active Directory. En configurant une approbation de fédération, vous pouvez configurer le partage fédéré avec d’autres organisations Exchange fédérées, afin de permettre le partage d’informations de disponibilité de calendrier entre les destinataires. Le partage fédéré peut être configuré entre deux organisations Exchange 2013 fédérées ou entre une organisation Exchange 2013 fédérée et des organisations Exchange 2010 fédérées. Vous pouvez également configurer le partage avec une organisation Office 365.

> [!NOTE]
> La création d’une approbation de fédération fait partie des étapes permettant de configurer le partage fédéré dans votre organisation Exchange. Pour consulter toutes les étapes, voir <a href="configure-federated-sharing-exchange-2013-help.md">Configurer le partage fédéré</a>.


Pour les autres tâches de gestion relatives à la fédération, voir [Procédures de fédération](federation-procedures-exchange-2013-help.md).

> [!IMPORTANT]
> Cette fonctionnalité d’Exchange Server 2013 n’est pas entièrement compatible avec les systèmes Office 365 exécutés par 21Vianet en Chine et certaines limitations de fonctionnalités peuvent s’appliquer. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/?linkid=313640">En savoir plus sur Office 365 exécuté par 21Vianet</a>.


## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 30 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée d’autorisation « Fédération et certificats » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) .

  - Le domaine utilisé pour établir une approbation de fédération doit pouvoir être résolu depuis Internet. Il faut donc que le domaine soit inscrit au bureau d’enregistrement de domaines et que la zone DNS (Domain Name System) pour le domaine soit hébergée sur un serveur DNS accessible depuis Internet. Si l’organisation reçoit du courrier Internet pour le domaine, ces critères sont déjà satisfaits.

  - Vous devrez ajouter un enregistrement TXT à votre DNS public. Passez en revue les exigences pour l’ajout d’un enregistrement TXT avec l’organisation qui héberge vos enregistrements DNS publics.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Les deux organisations Exchange dans une relation de partage fédéré doivent utiliser le même système d’authentification Azure AD pour leurs approbations de fédération. Cette exigence s’applique lors de la configuration du partage fédéré entre deux organisations Exchange sur site ou entre une organisation Exchange sur site et une organisation Exchange hébergée par [Office 365](https://go.microsoft.com/fwlink/?linkid=392576).

  - Lors de la création d’une approbation de fédération avec le système d’authentification Azure AD pour votre organisation Exchange 2013, l’approbation de fédération utilisera l’instance professionnelle du système d’authentification Azure AD. Cependant, d’autres organisations Exchange fédérées utilisant des versions antérieures d’Exchange et des approbations de fédération existantes peuvent utiliser l’instance professionnelle ou grand public du système d’authentification Azure AD.
    
    Les organisations Exchange suivantes utilisent l’instance professionnelle du système d’authentification Azure AD par défaut :
    
      - Les organisations Exchange 2013 via l’Assistant **Activer l’approbation de fédération** et les certificats auto-signés pour une approbation de fédération.
    
      - Les organisations Exchange 2010 SP1 ou version ultérieure via l’Assistant **Nouvelle approbation de fédération** et les certificats auto-signés pour une approbation de fédération.
    
      - Les organisations Exchange hébergées par Office 365, telles qu’Exchange Online.
    
    Les organisations Exchange suivantes utilisent l’instance grand public du système d’authentification Azure AD par défaut :
    
      - La version finalisée (RTM) des organisations Exchange 2010 via les certificats émis par des autorités de certification tierces.
    
    Nous recommandons que toutes les organisations Exchange utilisent l’instance professionnelle du système d’authentification Azure AD pour les approbations de fédération. Avant de configurer le partage fédéré entre les deux organisations Exchange, vous devez déterminer l’instance du système d’authentification Azure AD que chaque organisation Exchange utilise pour les approbations de fédération existantes. Pour déterminer l’instance du système d’authentification Azure AD utilisée par une organisation Exchange pour une approbation de fédération existante, exécutez la commande d’environnement Exchange Management Shell suivante.
    
    ```powershell
Get-FederationInformation -DomainName <hosted Exchange domain namespace>
```
    
    L’instance professionnelle renvoie la valeur `<uri:federation:MicrosoftOnline>` pour le paramètre *TokenIssuerURIs*.
    
    L’instance grand public renvoie la valeur `<uri:WindowsLiveID>` pour le paramètre *TokenIssuerURIs*.
    
    Pour configurer un partage fédérée avec une autre organisation Exchange a une approbation de fédération existante qui utilise l’instance de l’activité du système d’authentification Azure AD, suivez les étapes décrites dans cette rubrique. Ces étapes sont tous vous devez effectuer pour créer des approbations de fédération qui peuvent être utilisées pour activer le partage fédérée entre deux organisations Exchange 2013 ou entre une organisation Exchange 2013 et une organisation Exchange 2010 qui utilise déjà le instance d’activité du système d’authentification Azure AD.
    
    Pour configurer le partage fédéré entre votre organisation Exchange 2013 et une organisation Exchange qui comporte une approbation de fédération existante utilisant l’instance grand public du système d’authentification Azure AD, l’organisation Exchange utilisant l’instance grand public doit installer Exchange 2010 SP2 ou version ultérieure, ou effectuer la mise à niveau vers Exchange 2013. Si vous décidez d’installer Exchange 2010 SP2 ou version ultérieure, utilisez l’Assistant **Nouvelle approbation de fédération** pour supprimer et recréer les domaines fédérés et les approbations de fédération existants. Lors de la recréation des approbations de fédération, l’instance professionnelle du système d’authentification Azure AD sera utilisée.

## Utiliser le Centre d’administration Exchange (EAC) pour créer et configurer une approbation de fédération

1.  Sur un serveur Exchange 2013 de votre organisation locale, accédez à **Organisation** \> **Partage**.

2.  Cliquez sur **Activer** pour démarrer l’Assistant **Activer l’approbation de fédération**.

3.  Une fois l’Assistant terminé, cliquez sur **Fermer**.

4.  Dans la section **Approbation de fédération** de l’onglet **Partage**, cliquez sur **Modifier**.

5.  Dans **Domaines activés pour le partage**, en regard de **Étape 1**, cliquez sur **Parcourir**.

6.  Dans **Sélectionner les domaines acceptés**, sélectionnez dans la liste le domaine partagé principal, puis cliquez sur **OK**.
    
    > [!NOTE]
    > Le domaine que vous sélectionnez sera utilisé pour configurer l’identificateur d’organisation pour l’approbation fédérée. Pour plus d’informations sur l’identificateur d’organisation, voir <a href="federation-exchange-2013-help.md">Fédération</a>.


7.  Prenez note de la preuve du domaine fédéré qui est générée pour le domaine partagé principal. Cette chaîne vous permet de créer un enregistrement TXT sur votre serveur DNS public.
    
    > [!IMPORTANT]
    > La preuve du domaine fédéré est une chaîne de caractères alphanumériques. Pour éviter les erreurs d’entrée, nous vous recommandons de copier la chaîne à partir de l’estimation à l’achèvement, collez-le dans un éditeur de texte tel que le bloc-notes. Vous pouvez copier à partir de l’éditeur de texte dans le Presse-papiers et puis la coller dans le champ de <strong>texte</strong> lors de la création de l’enregistrement TXT. Si l’enregistrement TXT est créé à l’aide d’incorrecte fédéré de chaîne de la preuve du domaine, le système d’authentification de Azure AD ne sera pas en mesure de vérifier la preuve de propriété du domaine, et vous ne pourrez pas les ajouter à l’identificateur d’organisation fédérée.


8.  Dans l' **étape 2**, cliquez sur **Add**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter d’autres domaines de l’approbation fédérée des adresses e-mail qui sera utilisé par les utilisateurs de votre organisation qui nécessitent des fonctionnalités de partage fédérées. Par exemple, si vous avez des utilisateurs qui utilisent un sous-domaine dans leur adresse de messagerie par exemple ventes.contoso.com, vous ajoutez le domaine sales.contoso.com à l’approbation de fédération.
    
    > [!NOTE]
    > Une chaîne de preuve de domaine fédéré sera créée pour chaque domaine supplémentaire sélectionné. Vous devez créer des enregistrements TXT distincts sur votre DNS public pour chaque domaine supplémentaire.


9.  À l’aide des chaînes de preuve de domaine fédéré créées pour chaque domaine, créez des enregistrements TXT pour chacun de ces domaines sur votre serveur DNS public. En fonction de la planification des mises à jour de votre hôte DNS public, la réplication des modifications DNS peut prendre au moins 15 minutes.

10. Une fois les enregistrements TXT créés et répliqués, cliquez sur **Mettre à jour**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer et configurer une approbation de fédération

1.  Exécutez cette commande pour créer un identificateur d’objet unique de la clé pour le certificat d’approbation de fédération :
    
        $ski = [System.Guid]::NewGuid().ToString("N")

2.  Pour créer un certificat auto-signé pour l’approbation de fédération, utilisez cette syntaxe :
    
        New-ExchangeCertificate -FriendlyName "<Descriptive Name>" -DomainName <domain> -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
    
    Cet exemple crée un certificat auto-signé pour l’approbation de fédération avec le système d’authentification Azure AD. Le certificat utilise la valeur du nom convivial Exchange fédéré partage, et la valeur du domaine est extraite de la variable d’environnement **USERDNSDOMAIN** .
    
        New-ExchangeCertificate -FriendlyName "Exchange Federated Sharing" -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski

3.  Pour créer l’approbation de fédération et déployer automatiquement le certificat auto-signé que vous avez créé à l’étape précédente pour les Exchange de serveurs de votre organisation, utilisez la syntaxe suivante :
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "<FriendlyName>"} | New-FederationTrust -Name "<Descriptive Name>"
    
    Cet exemple crée l’approbation de fédération nommée l’authentification AD Azure et déploie le certificat auto-signé nommé fédéré de partage Exchange.
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "Exchange Federated Sharing"} | New-FederationTrust -Name "Azure AD Authentication"

4.  Cette syntaxe permet de renvoyer la preuve de l’appartenance de domaine enregistrement TXT qui est requis pour tous les domaines que vous allez configurer pour l’approbation de fédération.
    
    ```powershell
Get-FederatedDomainProof -DomainName <domain>
```
    
    Cet exemple renvoie la preuve de l’appartenance de domaine enregistrement TXT qui est requis pour le domaine partagé principal de contoso.com.
    
    ```powershell
Get-FederatedDomainProof -DomainName contoso.com
```
    
    **Remarques** :
    
      - Chaque domaine ou un sous-domaine qui est configuré pour l’approbation de fédération nécessite une preuve de propriété de domaine enregistrement TXT, vous devrez peut-être exécuter cette commande plusieurs fois en utilisant les valeurs des différents *DomainName* .
    
      - Nous vous conseillons de copier la chaîne de la preuve du domaine, avec le bouton droit dans le Shell, sélectionnez **marque**, sélectionnez la valeur de **preuve** et puis appuyez sur ENTRÉE afin que vous puissiez l’utiliser lorsque vous créez l’enregistrement TXT. Si vous créez l’enregistrement TXT avec une chaîne de la preuve du domaine fédéré incorrect, le système d’authentification de Azure AD ne peut pas vérifier votre propriété du domaine, et vous ne pourrez pas les ajouter à l’identificateur d’organisation fédérée.

5.  En utilisant les informations de l’étape précédente, créez des enregistrements TXT sur votre serveur DNS public dans chaque domaine qui sera inclus dans l’approbation de fédération. En fonction de la planification de la mise à jour de votre hôte DNS public, la réplication des modifications DNS peut prendre 15 minutes ou plus. Continuer après que vous être assuré que les nouveaux enregistrements TXT sont disponibles.

6.  Exécutez cette commande pour extraire les métadonnées et le certificat de Azure AD:
    
    ```powershell
Set-FederationTrust -RefreshMetadata -Identity "Azure AD authentication"
```

7.  Utilisez cette syntaxe pour configurer le domaine partagé principal pour l’approbation de fédération que vous avez créé à l’étape 3. Le domaine que vous spécifiez permet de configurer l’identificateur d’organisation (OrgID) pour l’approbation de fédération. Pour plus d’informations sur le OrgID, reportez-vous à la section [identificateur d’organisation fédérée](federation-exchange-2013-help.md).
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "<Federation Trust Name>" -AccountNamespace <Accepted Domain> -Enabled $true
    
    Cet exemple configure le domaine accepté contoso.com comme la principale partagée domaine pour l’approbation de fédération nommée l’authentification AD Azure.
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "Azure AD authentication" -AccountNamespace contoso.com -Enabled $true

8.  Pour ajouter d’autres domaines de l’approbation de fédération, utilisez la syntaxe suivante :
    
    ```powershell
Add-FederatedDomain -DomainName <AdditionalDomain>
```
    
    Cet exemple ajoute le sous-domaine sales.contoso.com l’approbation fédérée, utilisateurs avec adresses de messagerie dans le domaine sales.contoso.com nécessitant des fonctionnalités de partage fédérées.
    
    ```powershell
Add-FederatedDomain -DomainName sales.contoso.com
```
    
    N’oubliez pas que n’importe quel domaine ou du sous-domaine que vous ajoutez à l’approbation de fédération nécessite une preuve de propriété de domaine enregistrement TXT,

Pour la syntaxe détaillée et des informations sur les paramètres, consultez [New-ExchangeCertificate](https://technet.microsoft.com/fr-fr/library/aa998327\(v=exchg.150\)), [New-FederationTrust](https://technet.microsoft.com/fr-fr/library/dd351047\(v=exchg.150\)), [Get-FederatedDomainProof](https://technet.microsoft.com/fr-fr/library/ff717833\(v=exchg.150\)), [Set-FederationTrust](https://technet.microsoft.com/fr-fr/library/dd298034\(v=exchg.150\)), [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/fr-fr/library/dd351037\(v=exchg.150\))et [Add-FederatedDomain](https://technet.microsoft.com/fr-fr/library/dd351208\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

L’exécution réussie des Assistants **Activer l’approbation de fédération** et **Domaines activés pour le partage** constitue la première indication que l’approbation de fédération a été configurée comme prévu.

Pour vérifier que vous avez correctement créé et configuré l’approbation de fédération, procédez comme suit :

1.  Exécutez la commande de l’environnement de ligne de commande suivante pour vérifier les informations d’approbation de la fédération.
    
    ```powershell
Get-FederationTrust | Format-List
```

2.  Remplacez *\<PrimarySharedDomain\>* avec votre principal de domaine partagé et exécutez la commande Shell suivante pour vérifier que les informations de fédération peuvent être récupérées à partir de votre organisation.
    
    ```powershell
Get-FederationInformation -DomainName <PrimarySharedDomain>
```

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-FederationTrust](https://technet.microsoft.com/fr-fr/library/dd351262\(v=exchg.150\)) et [Get-FederationInformation](https://technet.microsoft.com/fr-fr/library/dd351221\(v=exchg.150\)).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

