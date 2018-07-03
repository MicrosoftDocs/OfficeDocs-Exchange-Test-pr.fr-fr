---
title: 'Assigner un certificat pour les services de messagerie unifiée et de routeur d’appels UM: Exchange 2013 Help'
TOCTitle: Assigner un certificat pour les services de messagerie unifiée et de routeur d’appels UM
ms:assetid: 8a900e5f-9779-4213-92d7-ec157b15fbc5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn205140(v=EXCHG.150)
ms:contentKeyID: 54652768
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Assigner un certificat pour les services de messagerie unifiée et de routeur d’appels UM

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-29_

Vous pouvez utiliser le CAE ou le Shell pour attribuer un interne, auto-signé infrastructure à clé publique (PKI), ou un certificat commercial tiers pour les services Exchange spécifiques. Lorsque vous utilisez l’applet de commande **New-ExchangeCertificate** pour assigner un certificat pour les services Exchange avec le paramètre *Services* , vous êtes invité à assigner le certificat pour les services Exchange. Si vous utilisez le CAE pour créer un certificat, vous permet d’assigner le certificat pour les services Exchange ne sont pas demander à l’Assistant nouveau certificat Exchange. Vous devez modifier les propriétés du certificat et d’assigner le certificat en activant les services que vous souhaitez assigner à.

Les différents services ont différentes exigences de certificat. Par exemple, certains services peuvent uniquement nécessiter un nom de serveur dans les zones **Nom de l'objet** ou **Autre nom de l'objet** d'un certificat, tandis que d'autres services peuvent nécessiter un nom de domaine complet. Assurez-vous que le nom du certificat peut prendre en charge les utilisations requises par les services pour lesquels vous l'activez.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les certificats auto-signés ne peut pas être utilisés lorsque vous êtes intégrer la messagerie unifiée (MU) de Microsoft Lync Server.</td>
</tr>
</tbody>
</table>


Pour découvrir d'autres tâches de gestion relatives à la gestion des certificats pour la messagerie unifiée, consultez la rubrique [Déployer des certificats pour les procédures de la messagerie unifiée](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gestion des certificats » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) et l'entrée « Service de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md). Vous devez également vous connecter en utilisant un compte membre du groupe Administrateurs local sur l'ordinateur.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour attribuer un certificat au service de messagerie unifiée et au service routeur des appels de messagerie unifiée

1.  Dans le CAE, accédez à **Serveurs** \> **Certificats**.

2.  Dans l'affichage Liste, sélectionnez le certificat à attribuer au service de messagerie unifiée et au service routeur d'appels de messagerie unifiée, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page *\<Nom du certificat\>*, sélectionnez **Services**, puis sélectionnez **Messagerie unifiée** et **Routeur des appels de messagerie unifiée**.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour attribuer un certificat au service de messagerie unifiée et au service routeur des appels de messagerie unifiée

Cet exemple permet d'attribuer un certificat au service de messagerie unifiée et au service routeur des appels de messagerie unifiée

    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

