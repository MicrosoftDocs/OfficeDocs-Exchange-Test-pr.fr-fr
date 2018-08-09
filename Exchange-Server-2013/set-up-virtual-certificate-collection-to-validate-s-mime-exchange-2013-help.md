---
title: 'Configurer une collection de certificats virtuelle pour valider S/MIME'
TOCTitle: Configuration d’une collection de certificats virtuelle pour la validation des certificats S/MIME
ms:assetid: 04a616e6-197c-490c-ae8c-c8d5f0f0b3dd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn626155(v=EXCHG.150)
ms:contentKeyID: 61212669
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration d’une collection de certificats virtuelle pour la validation des certificats S/MIME

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

En tant qu’administrateur client, vous devrez configurer une collection de certificats virtuelle qui sera utilisée pour valider les certificats S/MIME. Cette collection de certificats virtuelle est configurée comme un type de fichier de magasin de certificats avec une extension de nom de fichier SST. Le fichier SST contient tous les certificats racine et intermédiaires utilisés lors de la validation d’un certificat S/MIME.

## Créer et enregistrer un fichier SST

Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.Pour apprendre à ouvrir l’environnement de ligne de commande Environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange locale, reportez-vous à [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)).Pour apprendre à utiliser Windows PowerShell afin de vous connecter à Exchange Online, consultez la rubrique [Connexion à Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

En tant qu’administrateur, vous pouvez créer ce fichier SST en exportant les certificats à partir d’un ordinateur approuvé à l’aide de la cmdlet `Export-Certificate` et en indiquant SST pour le type. Pour plus d’informations sur la cmdlet `Export-Certificate`, consultez la rubrique de référence [Export-Certificate](https://technet.microsoft.com/fr-fr/library/hh848628.aspx).

Une fois le fichier SST généré, utilisez la cmdlet `Set-Smimeconfig` pour l’enregistrer dans le magasin de certificats virtuel à l’aide du paramètre *-SMIMECertificateIssuingCA*. Par exemple : `Set-SmimeConfig -SMIMECertificateIssuingCA (Get-Content filename.sst -Encoding Byte)`

## S’assurer de la validité d’un certificat

Exchange 2013 SP1 recherche en premier lieu le fichier SST et valide le certificat. Si la validation échoue, il examinera le magasin de certificats de l’ordinateur local pour valider le certificat. Ce comportement est nouveau pour Exchange 2013 SP1 et diffère des versions précédentes d’Exchange. Dans Exchange Online, seul le fichier SST sera utilisé pour la validation.

## Plus d’informations

[S/MIME pour la signature et le chiffrement des messages](s-mime-for-message-signing-and-encryption-exchange-2013-help.md)

[Get-SmimeConfig](https://technet.microsoft.com/fr-fr/library/dn554257\(v=exchg.150\))

