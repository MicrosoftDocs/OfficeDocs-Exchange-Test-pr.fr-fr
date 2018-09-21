---
title: 'Créer une demande de certificat numérique: Exchange 2013 Help'
TOCTitle: Créer une demande de certificat numérique
ms:assetid: efb00de7-070b-46bf-a2fc-00d07ae085c1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125165(v=EXCHG.150)
ms:contentKeyID: 52063032
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une demande de certificat numérique

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-21_

Dans Exchange Server 2013, vous pouvez gérer des certificats à l’aide du centre d’administration Exchange ou de Shell. Le centre d’administration Exchange comprend une nouvelle interface utilisateur de gestion des certificats. Sur cette nouvelle interface utilisateur, vous pouvez créer des certificats, modifier un certificat existant ou en supprimer.

## Ce qu'il faut savoir avant de commencer

  - Durée estimée : 10 minutes, plus le temps de recevoir la réponse d’autorité de certification.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Sécurité du serveur d'accès au client » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour créer une demande de certificat

1.  Dans le CAE, accédez à **Serveurs** \> **Certificats**.

2.  Dans la liste **Sélectionner le serveur**, sélectionnez le serveur pour lequel vous souhaitez créer un certificat, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans l'Assistant **Nouveau certificat Exchange**, sélectionnez l'option **Créer une demande pour un certificat auprès d'une autorité de certification** ou **Créer un certificat auto-signé**, puis cliquez sur **Suivant**.

4.  Entrez un nom convivial pour le certificat, puis cliquez sur **Suivant**.

5.  Si vous n’avez pas sélectionné de certificat auto-signé et que vous souhaitez utiliser un certificat avec caractères génériques, cochez la case **Demander un certificat avec caractères génériques**, entrez le domaine racine (par exemple, \*.contoso.com), puis cliquez sur **Suivant**. Si vous choisissez un certificat auto-signé, ignorez cette étape.

6.  Sélectionnez les serveurs sur lesquels appliquer ce certificat, puis cliquez sur **Suivant**.

7.  Spécifiez les domaines que vous voulez inclure dans votre certificat, puis cliquez sur **Suivant**.

8.  Vérifiez que les domaines inclus sont corrects. Si vous avez choisi un certificat auto-signé, sélectionnez **Terminer**. Sinon, sélectionnez **Suivant**.

9.  Entrez le nom de votre organisation, le nom du service, la ville ou la localité, l'État ou la province et le pays ou la région, puis cliquez sur **Suivant**.

10. Entrez l'emplacement où vous souhaitez enregistrer la demande de certificat, puis cliquez sur **Terminer**.

Si vous n'avez pas sélectionné de certificat auto-signé, vous devrez envoyer le fichier de demande de certificat à l'autorité de certification pour traitement.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une demande de certificat

Exécutez les commandes suivantes :
```
    $reqfile = New-ExchangeCertificate -GenerateRequest -SubjectName "C=US,o=Contoso,cn=contosotocert" -DomainName "contoso.com" -PrivateKeyExportable $true
```
```
```powershell
$reqfile | out-file c:\certreq.txt
```
```    

## Comment savoir si cela a fonctionné ?

Si vous avez créé un certificat auto-signé, le nouveau certificat apparaît dans l’interface utilisateur de gestion de certificat. Si vous avez créé une demande de certificat à partir d’une autorité de certification, le fichier de demande de certificat sera à l’emplacement spécifié. Envoyez ce fichier à l’autorité de certification.

