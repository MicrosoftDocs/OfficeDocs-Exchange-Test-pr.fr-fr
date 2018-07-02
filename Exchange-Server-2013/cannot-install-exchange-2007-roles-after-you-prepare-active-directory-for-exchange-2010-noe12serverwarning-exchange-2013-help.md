---
title: 'Impossible d’installer les rôles Exchange 2007 après avoir préparé Active Directory pour Exchange 2010_NoE12ServerWarning: Exchange 2013 Help'
TOCTitle: Impossible d’installer les rôles Exchange 2007 après avoir préparé Active Directory pour Exchange 2010_NoE12ServerWarning
ms:assetid: 4e579f69-0de9-421c-ba31-4e63a25e6a45
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.noe12serverwarning(v=EXCHG.150)
ms:contentKeyID: 50478157
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Impossible d’installer les rôles Exchange 2007 après avoir préparé Active Directory pour Exchange 2010\_NoE12ServerWarning

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Lorsque vous exécutez Exchange Server 2010**Setup /PrepareAD**, l’outil Microsoft Exchange Server Analyzer interroge la topologie Active Directory existante pour déterminer si des rôles de serveur Microsoft Exchange Server 2007 existent. Si aucun rôle de serveur Exchange 2007 n’est détecté, vous recevez le message d’avertissement suivant :


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Le programme d’installation va préparer l’organisation pour Exchange Server 2010 via « Setup /PrepareAD ». Aucun rôle Exchange Server 2007 n’a été détecté dans cette topologie. Après cette opération, il sera impossible d’installer des rôles Exchange Server 2007.</p></td>
</tr>
</tbody>
</table>


Avant de déployer Exchange Server 2010, tenez compte des facteurs suivants qui peuvent exiger le déploiement d’un serveur Exchange 2007 avec tous les rôles de serveur installés avant de déployer Exchange 2007 :

  - **Applications développées en interne ou tierces**   Les applications développées pour Exchange 2003 peuvent ne pas être compatibles avec Exchange 2010 et doivent donc être mises à niveau ou remplacées. Vous pouvez conserver ces applications et la population d’utilisateurs associée sur Exchange 2003 ; passez à Exchange 2007 ; ou remplacez le logiciel par une version compatible pour Exchange 2010.

  - **Exigences de coexistence ou de migration**   Si vous envisagez de migrer des boîtes aux lettres dans votre organisation, vous pouvez déployer Exchange 2007 et utiliser Microsoft Transporter Suite, ou vous pouvez utiliser une solution tierce de coexistence ou de migration. Pour télécharger Microsoft Transporter Suite, accédez à [Microsoft Transporter Suite](http://go.microsoft.com/fwlink/?linkid=82688) dans le Centre de téléchargement Microsoft.

En outre, lorsque vous évaluez les options pour votre organisation, assurez-vous que vous avez tenu compte des questions suivantes :

  - Avez-vous une stratégie en place pour déplacer les applications dépendantes vers Exchange 2010 avant qu’Exchange 2003 ne soit plus pris en charge ? Pour plus d’informations, consultez la page web Microsoft Support Lifecycle ([https://go.microsoft.com/fwlink/?LinkID=55839](https://go.microsoft.com/fwlink/?linkid=55839)).

  - Votre stratégie exige-t-elle la coexistence des services WebDAV et des services web (Exchange 2007) ?

  - Avez-vous pris en compte des produits tiers qui prennent en charge Exchange ou d’autres technologies Microsoft qui vous permettront de répondre à vos besoins de coexistence ou de migration ?

  - Quelle est votre approche en matière de durée de vie du matériel (continuer à utiliser autant de serveurs 32 bits existants que possible ou acheter de nouveaux serveurs 64 bits) ?

  - Quel est votre plan de migration (migrer tous les serveurs aussi vite que possible ou migrer en adoptant une stratégie en plusieurs phases) ? De même, quelle est votre chronologie pour la coexistence des différentes versions de Exchange ?

Si vous décidez que vous devez déployer un serveur Exchange 2007 avant le déploiement d’Exchange 2010, le déploiement d’un seul environnement Exchange 2007 avec tous les rôles de serveur est suffisant pour permettre le déploiement des futurs serveurs Exchange 2007 dans l’organisation. Pour déployer le serveur Exchange 2007 dans votre organisation Exchange 2003, procédez comme suit :

1.  Exécutez Exchange 2007**Setup /PrepareSchema**.

2.  Exécutez Exchange 2007**Setup /PrepareAD**.

3.  Exécutez Exchange 2007**Setup /PrepareDomain** sur tous les domaines qui contiennent des destinataires, les serveurs Exchange 2003, ou les catalogues globaux qui peuvent être utilisés par un serveur Exchange.

4.  Installez un serveur Exchange 2007 avec les quatre rôles de serveur (Transport Hub, Accès au client, Boîte aux lettres et Messagerie unifiée).

