---
title: 'Renouveler le certificat de fédération: Exchange 2013 Help'
TOCTitle: Renouveler le certificat de fédération
ms:assetid: 0f390713-3058-44d0-9c07-3c982616e790
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt779252(v=EXCHG.150)
ms:contentKeyID: 74429217
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Renouveler le certificat de fédération

 

_**Dernière rubrique modifiée :** 2017-02-28_

Cette rubrique explique comment mettre à jour le certificat de fédération auto-signé qui est utilisé dans une approbation de fédération :

  - Si le certificat de fédération n’a pas expiré, suivez la procédure décrite dans la section Mettre à jour un certificat de fédération actif.

  - Si le certificat de fédération a déjà expiré, suivez la procédure décrite dans la section Remplacer un certificat de fédération expiré.

Pour plus d’informations sur les approbations de fédération et la fédération, voir [Fédération](federation-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Fédération et certificats » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Les procédures décrites dans cette rubrique utilisent l’Environnement de ligne de commande Exchange Management Shell. Pour apprendre à ouvrir l’environnement de ligne de commande Environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange locale, reportez-vous à [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)).

  - Pour savoir si votre certificat de fédération a expiré, exécutez la commande suivante dans l’Environnement de ligne de commande Exchange Management Shell :
    
        Get-ExchangeCertificate -Thumbprint (Get-FederationTrust).OrgCertificate.Thumbprint | Format-Table -Auto Thumbprint,NotAfter

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!WARNING]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Mettre à jour un certificat de fédération actif

Si le certificat de fédération n’a pas expiré, vous pouvez le remplacer par un nouveau pour mettre à jour l’approbation de fédération.

## Étape 1 : Créer un nouveau certificat de fédération

Exécutez la commande suivante dans l’Environnement de ligne de commande Exchange Management Shell pour créer un nouveau certificat de fédération :

    $SKI = [System.Guid]::NewGuid().ToString("N"); New-ExchangeCertificate -DomainName 'Federation' -FriendlyName "Exchange Delegation Federation" -Services Federation -SubjectKeyIdentifier $SKI -PrivateKeyExportable $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-ExchangeCertificate](https://technet.microsoft.com/fr-fr/library/aa998327\(v=exchg.150\)).

Le résultat de la commande contient la valeur de l’empreinte numérique du nouveau certificat. Vous aurez besoin de cette valeur dans les étapes restantes, et vous pouvez la copier directement à partir de la fenêtre Environnement de ligne de commande Exchange Management Shell :

1.  Cliquez avec le bouton droit de la souris n’importe où dans la fenêtre de l’Environnement de ligne de commande Exchange Management Shell, puis sélectionnez **Mark** dans la boîte de dialogue qui s’affiche.

2.  Sélectionnez la valeur de l’empreinte numérique et appuyez sur ENTRÉE.

Pour les autres procédures de cette rubrique, nous allons utiliser la valeur d’empreinte numérique du certificat de fédération : `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`. La valeur d’empreinte numérique de votre certificat sera différente.

## Étape 2 : Configurer le nouveau certificat en tant que certificat de fédération

Pour utiliser l’Environnement de ligne de commande Exchange Management Shell pour configurer le nouveau certificat comme certificat de fédération, utilisez la syntaxe suivante :

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint <Thumbprint> -RefreshMetaData

Cet exemple utilise la valeur d’empreinte numérique de certificat `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`, obtenue à l’étape 1.

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint 6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73 -RefreshMetaData

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-FederationTrust](https://technet.microsoft.com/fr-fr/library/dd298034\(v=exchg.150\)).

**Remarque** : Le résultat de la commande contient un message d’avertissement indiquant que vous devez mettre à jour l’enregistrement TXT de la preuve de propriété du domaine dans le système DNS. C’est ce que vous allez faire à l’étape suivante.

## Étape 3 : Mettre à jour l’enregistrement TXT de la preuve de propriété du domaine dans le système DNS externe

Vous pouvez à présent exécuter cette opération en toute sécurité, car l’enregistrement TXT de la preuve de propriété du domaine est uniquement vérifié lors de l’activation (étape 5). Toutefois, une fois que vous avez mis à jour l’enregistrement TXT, et avant de passer à l’étape suivante, vous devez laisser le temps de se propager à l’enregistrement TXT mis à jour (en vous fondant sur la durée de vie ou la valeur TTL de l’enregistrement DNS).

1.  Rechercher les valeurs nécessaires pour l’enregistrement TXT requis en exécutant la commande suivante dans l’Environnement de ligne de commande Exchange Management Shell :
    
        Get-FederatedDomainProof -DomainName <Domain> | Format-List Thumbprint,Proof
    
    Par exemple, si votre domaine fédéré est contoso.com, exécutez la commande suivante :
    
        Get-FederatedDomainProof -DomainName contoso.com | Format-List Thumbprint,Proof
    
    Le résultat de la commande ressemble à ceci :
    
    `Thumbprint : <new certificate thumbprint>` (par exemple, `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`)
    
    `Proof      : <new hash text>` (par exemple, `znMfbkgSbOQSsWFdsW+gm3to0nZSdE3zbcPPHGVAqdgsLFGsCPuLHiyVbKoPmgyZKX90NH2g1PbCZH0YTQF6oA==`)
    
    `Thumbprint : <old certificate thumbprint>` (par exemple, `CC9BC204BB4DC60D06FC1F10F3C373DC785DA2A5`)
    
    `Proof      : <old hash text>` (par exemple, `m4gZX7OLr9iOWYJMVjEklQpoSkPb5hSbcFjD7Q3/vsqmdJ2Z+HcSt7j5pzBKFmEW2s27JYr3xsK2POzAI/8Ffw==`)
    
    Notez que les résultats de la commande renvoient les informations de deux enregistrements de preuves de propriété de domaine : une pour le nouveau certificat et une pour le certificat actuel que vous souhaitez remplacer. Vous pouvez les différencier par la valeur de l’empreinte numérique et la valeur de texte de hachage configurée dans l’enregistrement TXT de la preuve de propriété de domaine dans votre DNS externe (public).

2.  Mettez à jour l’enregistrement TXT de la preuve de propriété de domaine de votre serveur DNS externe. Les instructions dépendent de votre fournisseur, mais vous pouvez modifier l’enregistrement TXT actuel pour en remplacer la valeur du texte de hachage par la nouvelle valeur de texte de hachage. Pour plus d’informations, voir la section Exchange Online de la rubrique [Enregistrements DNS externes pour Office 365](https://go.microsoft.com/fwlink/p/?linkid=265522).

## Étape 4 : Vérifier la distribution du nouveau certificat de fédération sur tous les serveurs Exchange

Exchange distribue automatiquement le nouveau certificat de fédération sur tous les serveurs, mais nous devons vérifier que cette distribution est correcte avant de continuer.

Pour utiliser l’Environnement de ligne de commande Exchange Management Shell afin de vérifier la distribution du nouveau certificat de fédération, exécutez la commande suivante :

    $Servers = Get-ExchangeServer; $Servers | foreach {Get-ExchangeCertificate -Server $_ | Where {$_.Services -match 'Federation'}} | Format-List Identity,Thumbprint,Services,Subject

**Remarque** : dans Exchange 2010, le résultat de la cmdlet **Test-FederationCertificate** contient le nom des serveurs. Le résultat de la cmdlet dans Exchange 2013 ou version ultérieure n’inclut pas les noms de serveur.

## Étape 5 : Activer le nouveau certificat de fédération

Pour utiliser l’Environnement de ligne de commande Exchange Management Shell afin d’activer le nouveau certificat de fédération, exécutez la commande suivante :

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -PublishFederationCertificate

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-FederationTrust](https://technet.microsoft.com/fr-fr/library/dd298034\(v=exchg.150\)).

**Remarque** : le résultat de la commande contient un message d’avertissement indiquant que vous devez mettre à jour l’enregistrement TXT de la preuve de propriété du domaine dans le système DNS (ce que vous avez déjà fait à l’étape 3).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement mis à jour l’approbation de fédération existante avec un nouveau certificat de fédération, procédez comme suit :

  - Dans l’Environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier que le nouveau certificat est celui utilisé :
    
        Get-FederationTrust | Format-List *priv*
    
      - La propriété **OrgPrivCertificate** doit contenir l’empreinte numérique du nouveau certificat de fédération.
    
      - La propriété **OrgPrevPrivCertificate** doit contenir l’empreinte numérique de l’ancien certificat de fédération (remplacé).

  - Dans l’Environnement de ligne de commande Exchange Management Shell, remplacez *\<user's email address\>* par l’adresse e-mail d’un utilisateur de votre organisation et exécutez la commande suivante pour vérifier que l’approbation de fédération fonctionne :
    
        Test-FederationTrust -UserIdentity <user's email address>

## Remplacer un certificat de fédération expiré

Si le certificat de fédération a déjà expiré, vous devez supprimer tous les domaines fédérés de l’approbation de fédération, puis supprimer et recréer l’approbation de fédération.

1.  Si vous avez plusieurs domaines fédérés, vous devez repérer le principal domaine partagé pour le supprimer en dernier. Pour utiliser l’Environnement de ligne de commande Exchange Management Shell afin de trouver le domaine partagé principal et l’ensemble des domaines fédérés, exécutez la commande suivante :
    
        Get-FederatedOrganizationIdentifier | Format-List AccountNamespace,Domains
    
    La valeur de la propriété **AccountNamespace** contient le domaine partagé principal au format `FYDIBOHF25SPDLT<primary shared domain>`. Par exemple, dans la valeur `FYDIBOHF25SPDLT.contoso.com`, contoso.com est le domaine partagé principal.

2.  Supprimez chaque domaine fédéré qui n’est pas le domaine partagé principal en exécutant la commande suivante dans l’Environnement de ligne de commande Exchange Management Shell :
    
        Remove-FederatedDomain -DomainName <domain> -Force

3.  Une fois que vous avez supprimé tous les autres domaines fédérés, supprimez le domaine partagé principal en exécutant la commande suivante dans l’Environnement de ligne de commande Exchange Management Shell :
    
        Remove-FederatedDomain -DomainName <domain> -Force

4.  Supprimer l’approbation de fédération en exécutant la commande suivante dans l’Environnement de ligne de commande Exchange Management Shell :
    
        Remove-FederationTrust "Microsoft Federation Gateway"

5.  Recréez l’approbation de fédération. Pour plus d’informations, voir [Créer une approbation de fédération](https://technet.microsoft.com/fr-fr/library/dd335198\(v=exchg.150\)).

