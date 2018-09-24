---
title: 'Créer des certificats pour la messagerie unifiée: Exchange 2013 Help'
TOCTitle: Créer des certificats pour la messagerie unifiée
ms:assetid: 66807ee7-3d3f-482d-a3ac-d4e9baca3271
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn205141(v=EXCHG.150)
ms:contentKeyID: 54652763
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Créer des certificats pour la messagerie unifiée

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-29_

Vous pouvez utiliser l'Assistant nouveau certificat Exchange dans le CAE ou le Shell pour créer des certificats auto-signés ou les demandes de certificats pour un certificat interne infrastructure à clé publique (PKI). De messagerie unifiée (MU), vous pouvez utiliser une de ces certificats pour le service de messagerie unifiée de Microsoft Exchange et les services Microsoft Exchange Unified Messaging routeur d'appels. Vous pouvez utiliser le même certificat pour les deux services ou un certificat différent pour chaque service. Vous pouvez également acheter et importer un certificat commercial tiers pour les services de messagerie unifiée. Si vous utilisez un certificat auto-signé pour la messagerie unifiée, vous devrez inclure le nom des serveurs de boîtes aux lettres et d'accès au Client dans le nom du sujet (SAN).

Par défaut, lorsque vous installez Exchange Server 2013, deux certificats auto-signés sont créés : **certificat d'authentification serveur Microsoft Exchange (Microsoft Exchange Server Auth Certificate)** et **Microsoft Exchange**. Le certificat auto-signé **Microsoft Exchange** peut être utilisé par la messagerie unifiée pour chiffrer des données, mais vous devez l'attribuer aux services de messagerie unifiée et de routeur d'appels de messagerie unifiée. Après avoir attribué le certificat aux services de messagerie unifiée, vous pouvez le copier et l'importer dans les passerelles VoIP, PBX IP, et PBX compatibles SIP. Toutefois, au lieu d'utiliser les certificats auto-signés par défaut, il se peut que vous deviez en créer un spécialement pour la messagerie unifiée.

> [!CAUTION]
> Les certificats auto-signés ne peut pas être utilisés lorsque vous êtes intégrer la messagerie unifiée de Microsoft Lync Server.


Pour découvrir d'autres tâches de gestion relatives à la gestion des certificats pour la messagerie unifiée, consultez la rubrique [Déployer des certificats pour les procédures de la messagerie unifiée](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gestion des certificats » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) et l'entrée « Service de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md). Vous devez également vous connecter en utilisant un compte membre du groupe Administrateurs local sur l'ordinateur.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour créer une demande de certificat pour la messagerie unifiée

1.  Dans le CAE, accédez à **Serveurs** \> **Certificats**, puis, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans l'Assistant **Nouveau certificat Exchange**, sélectionnez **Créer une demande pour un certificat auprès d'une autorité de certification**, puis cliquez sur **Suivant**.

3.  Entrez un nom convivial pour le certificat, puis cliquez sur **Suivant**.

4.  Si vous n'avez pas besoin un certificat avec caractères génériques, cliquez sur **suivant**. Si vous avez besoin d'un certificat avec caractères génériques, sélectionnez **demander un certificat générique. Un certificat de caractère générique peut être utilisé pour sécuriser tous les sous-domaines sous votre domaine racine avec un seul certificat**, entrez le nom du domaine racine, puis cliquez sur **suivant**.

5.  Sous **Enregistrer la demande de certificat sur ce serveur**, cliquez sur **Parcourir** pour accéder à l'emplacement où vous voulez enregistrer le fichier. Vous pouvez enregistrer la demande de certificat sur tout serveur d'accès au client ou de boîtes aux lettres de votre organisation Exchange. Sélectionnez l'emplacement, cliquez sur **OK**, puis sur **Suivant**.

6.  Si vous avez demandé un certificat avec caractères génériques, passez à l'étape 9.

7.  Si vous n'avez pas demander un certificat générique, vous devez spécifier les domaines que vous souhaitez inclure dans votre certificat. Si vous souhaitez modifier un domaine, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"), puis cliquez sur **suivant**.

8.  Sous **Basé sur vos sélections, les domaines suivants seront inclus dans votre certificat. Vous pouvez ajouter des domaines ici ou apporter des modifications**, vous pouvez ajouter, modifier, supprimer et vérifier les domaines répertoriés sous **Domaine**. Cliquez ensuite sur **Suivant**.

9.  Sous **Spécifiez les informations relatives à votre organisation. Celles-ci sont exigées par l'autorité de certification**, entrez ce qui suit :
    
      - **Nom de l'organisation**
    
      - **Nom du service**
    
      - **Ville/localité**
    
      - **État/Province**
    
      - **Nom de pays/région**   Pour cette option, utilisez la liste déroulante pour sélectionner le pays ou la région.

10. Sous **Enregistrer la demande de certificat dans le fichier suivant**, entrez le nom du fichier de certificat, puis cliquez sur **Terminer**.

## Utiliser l'environnement de ligne de commande pour créer une demande de certificat pour la messagerie unifiée

Cet exemple montre comment créer une demande de certificat Exchange pour un serveur de boîtes aux lettres nommé `MyMailboxServer`, portant le nom convivial de `CertUM`.

```powershell
New-ExchangeCertificate -FriendlyName 'CertUM' -GenerateRequest -PrivateKeyExportable $true -KeySize '2048' -DomainName '*.northwindtraders.com' -SubjectName 'C=US,S=wa,L=redmond,O=northwindtraders,OU=servers,CN= northwindtraders.com' -Server 'MyMailboxServer'
```

## Utiliser le CAE pour créer un certificat auto-signé pour la messagerie unifiée

1.  Dans le CAE, accédez à **Serveurs** \> **Certificats**, puis, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans la page **Nouveau certificat Exchange**, choisissez **Créer un certificat auto-signé**, puis cliquez sur **Suivant**.

3.  Entrez un nom convivial pour le certificat, puis cliquez sur **Suivant**.

4.  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour sélectionner les serveurs Exchange auxquels vous voulez appliquer ce certificat, puis cliquez sur **Suivant**.

5.  Spécifiez les domaines que vous voulez inclure dans votre certificat, puis cliquez sur **Suivant**. Si vous voulez ajouter un domaine pour un service, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

6.  Vérifiez que les domaines inclus sont corrects, puis cliquez sur **Terminer**.

> [!IMPORTANT]
> Lorsque vous utilisez le CAE pour créer un certificat auto-signé, vous n'êtes invité à activer des services pour le certificat. Une fois que le certificat a été créé, vous pouvez utiliser le CAE ou l'applet de commande <strong>Enable-ExchangeCertificate</strong> dans le Shell pour activer les services Exchange. Pour plus d'informations sur comment assigner un certificat pour les services de messagerie unifiée, consultez la rubrique <a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assigner un certificat pour les services de messagerie unifiée et de routeur d’appels UM</a>.


## Utiliser l'environnement de ligne de commande pour créer un certificat auto-signé pour la messagerie unifiée

Cet exemple montre comment créer un certificat auto-signé Exchange pour un serveur de boîtes aux lettres nommé `MyMailboxServer`, portant le nom convivial de `UMCert`.

```powershell
New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
```

> [!TIP]
> Lorsque vous spécifiez les services à activer en utilisant le paramètre <em>Services</em> , vous serez invité à affecter ces services. Dans cet exemple, vous devrez faire pour activer le certificat pour les services de messagerie unifiée et de routeur d'appels UM. Pour plus d'informations sur la façon d'activer un certificat pour les services, voir <a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assigner un certificat pour les services de messagerie unifiée et de routeur d’appels UM</a>.

