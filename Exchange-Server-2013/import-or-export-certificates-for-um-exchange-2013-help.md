---
title: 'Importer ou exporter des certificats pour la messagerie unifiée: Exchange 2013 Help'
TOCTitle: Importer ou exporter des certificats pour la messagerie unifiée
ms:assetid: ee688c33-2e08-47e7-95fc-04ba10238341
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn205143(v=EXCHG.150)
ms:contentKeyID: 54652783
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importer ou exporter des certificats pour la messagerie unifiée

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-12-18_

Vous pouvez utiliser le Centre d'administration Exchange (CAE) ou l'environnement de ligne de commande Exchange Mangement Shell pour importer ou exporter une infrastructure à clé publique (PKI) interne auto-signée ou un certificat commercial tiers. Pour la messagerie unifiée, vous pouvez utiliser un des certificats suivants tant pour le service de messagerie unifiée Microsoft Exchange que le service routeur d'appels de messagerie unifiée Microsoft Exchange. Vous pouvez utiliser le même certificat pour les deux services, ou un certificat distinct pour chacun d'eux.

L'importation de certificats pour Exchange peut être utile quand vous souhaitez :

  - importer un certificat qui a été exporté dans un fichier ;

  - importer un fichier de certificat PKI qui a été généré par une autorité de certification interne ;

  - importer un certificat commercial tiers.

L'exportation d'un certificat existant à partir du magasin de certificats se trouvant sur le serveur Exchange local peut s'avérer utile quand vous souhaitez :

  - exporter ce certificat afin de pouvoir l'importer sur un autre serveur Exchange ;

  - exporter ce certificat afin de pouvoir l'importer sur une passerelle VoIP, un PBX IP ou un PBX compatible SIP ;

  - exporter ce certificat afin de pouvoir le sauvegarder lui ainsi que sa clé privée.

Pour découvrir d'autres tâches de gestion relatives à la gestion des certificats pour la messagerie unifiée, consultez la rubrique [Déployer des certificats pour les procédures de la messagerie unifiée](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gestion des certificats » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) et l'entrée « Service de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md). Vous devez également vous connecter en utilisant un compte membre du groupe Administrateurs local sur l'ordinateur.

  - Avant d'exporter un certificat, utilisez la cmdlet **Get-ExchangeCertificate** pour vérifier que l'attribut *PrivateKeyExportable* de ce certificat est défini sur `$true`.

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


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour exporter un certificat

1.  Dans le CAE, cliquez sur **Serveurs** \> **Certificats** \> **Autres options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires"), puis cliquez sur **Exporter le certificat Exchange**.

2.  Dans la page **Exporter le certificat Exchange**, dans la zone **Fichier d'exportation**, entrez le nom du fichier de certificat.

3.  Dans la zone **Mot de passe**, entrez le mot de passe que vous voulez utiliser pour protéger la clé privée, puis cliquez sur **OK**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour exporter un certificat

Cet exemple exporte le certificat possédant l'empreinte numérique A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC dans un fichier après vous avoir invité à entrer un nom d'utilisateur et un mot de passe

    $file = Export-ExchangeCertificate -Thumbprint A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC -BinaryEncoded:$true -Password (Get-Credential).password

Cet exemple effectue les opérations suivantes :

1.  Utilisation de la cmdlet **Get-ExchangeCertificate** pour rechercher le certificat à exporter.

2.  Utilisation de la cmdlet **Export-ExchangeCertificate** pour définir le mot de passe du certificat.

3.  Sortie du certificat dans un fichier après avoir entré le nom d'utilisateur et le mot de passe.

<!-- end list -->

    $file = Get-ExchangeCertificate -DomainName umcorp.northwindtraders.com | Export-ExchangeCertificate -BinaryEncoded:$true -Password (Get-Credential).password

    Set-Content -Path "d:\umcerts\selfsigned.pfx" -Value $file.FileData =Encoding Byte

## Utiliser le Centre d'administration Exchange (CAE) pour importer un certificat

1.  Dans le CAE, cliquez sur **Serveurs** \> **Certificats** \> **Autres options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires"), puis cliquez sur **Importer le certificat Exchange**.

2.  Dans la page **Importer le certificat Exchange**, dans la zone **Fichier d'importation**, entrez le chemin d'accès au dossier partagé et le nom du fichier de certificat. Si le certificat est protégé par mot de passe, entrez le mot de passe dans la zone **Mot de passe**, puis cliquez sur **Suivant**.

3.  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour sélectionner les serveurs auxquels vous voulez appliquer le certificat, puis cliquez sur **OK**. Si vous voulez supprimer un serveur dans l'affichage Liste, cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression"), puis sur **Terminer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour importer un certificat

Cet exemple importe un certificat à partir du fichier de certificat d:\\certificates\\exchange\\SelfSignedUMCert.pfx après avoir entré un nom d'utilisateur et un mot de passe.

    Import-ExchangeCertificate -FileData ([Byte[]]$(Get-Content -Path d:\certificates\exchange\SelfSignedUMCert.pfx -Encoding Byte -ReadCount 0)) -Password:(Get-Credential).password

