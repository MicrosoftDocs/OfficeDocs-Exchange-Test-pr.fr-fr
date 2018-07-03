---
title: 'Dépannage d’un déploiement hybride: Exchange 2013 Help'
TOCTitle: Dépannage d’un déploiement hybride
ms:assetid: bbae72f3-6a1e-4cbf-80da-d8f73d969c6b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659053(v=EXCHG.150)
ms:contentKeyID: 50479672
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage d’un déploiement hybride

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2016-04-29_

La configuration d’un déploiement hybride dans Exchange avec l’assistant de configuration hybride minimise considérablement le risque que le déploiement hybride rencontre des problèmes. Toutefois, certains points types n’appartenant pas au champ d’application de l’assistant de configuration hybride peuvent, s’ils ne sont pas correctement configurés, poser des problèmes dans un déploiement hybride. Cette rubrique traite des points communs suivants susceptibles de poser des problèmes, et décrit les étapes de base permettant de vérifier ou de corriger des problèmes :

  - Serveurs Exchange locaux

  - Certificats

  - Erreurs spécifiques de l'Assistant Configuration hybride

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans cette rubrique, les « serveurs Exchange » font référence aux serveurs suivants :
<ul>
<li><p><strong>Serveurs d’accès au client</strong> Exchange 2013 et les versions antérieures</p></li>
<li><p><strong>Serveurs de boîte aux lettres</strong> Exchange 2016 et les versions ultérieures</p></li>
</ul></td>
</tr>
</tbody>
</table>


Pour plus d’informations, consultez la rubrique [Déploiements hybrides Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives aux déploiements hybrides, consultez la rubrique [Procédures de déploiement hybride](hybrid-deployment-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer?

  - Durée d'exécution estimée de cette tâche : Varie selon le type de problèmes de déploiement hybride

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Déploiements hybrides » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](https://technet.microsoft.com/fr-fr/library/dd638114\(v=exchg.150\)).

  - Les instructions de cette rubrique s’appliquent aux déploiements hybrides configurés à l’aide de l’assistant de configuration hybride. Les déploiements hybrides ayant été configurés manuellement ne sont pas pris en charge.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](https://technet.microsoft.com/fr-fr/library/jj150484\(v=exchg.150\)).

<table>
<thead>
<tr class="header">
<th><img src="images/Mt589761.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Résoudre des problèmes avec des serveurs Exchange locaux

La configuration des serveurs Exchange locaux est généralement le point qui pose le plus de problèmes dans un déploiement hybride. Généralement, les points à vérifier sont les suivants :

  - **Disponibilité**   Publier correctement les serveurs Exchange locaux sur Internet est essentiel pour que les fonctions s’exécutent correctement dans votre déploiement hybride. Pour que les fonctions hybrides s’exécutent correctement, vous devez configurer votre pare-feu local ou d’autres équipements de sécurité pour permettre l’accès de messages entrants d’Internet aux points de terminaison des services web Exchange et de découverte automatique sur les serveurs Exchange locaux. D’autre part, les serveurs Exchange doivent également être configurés pour accepter des messages SMTP entrants. Si le service Microsoft Exchange Online Protection (EOP) intégré à votre organisation cliente Office 365 ne peut pas atteindre les serveurs Exchange locaux, le transport de messagerie sécurisée entre l’organisation Exchange Online et l’organisation locale ne fonctionnera pas correctement.

  - **Certificats**   Le certificat numérique utilisé pour le transport de messagerie sécurisée entre l’organisation locale et l’organisation Exchange Online doit être installé sur tous les serveurs Exchange accessibles sur Internet qui communiqueront avec Exchange Online, doit être émis par une autorité de certification (CA) tierce, ne doit pas avoir expiré et doit disposer des services IIS et SMTP. Si ces conditions préalables relatives au certificat ne sont pas remplies, le transport de messagerie sécurisée entre l’organisation Exchange Online et l’organisation locale ne fonctionnera pas correctement. Pour plus d’informations sur les conditions préalables relatives au certificat, consultez la section « Résoudre des problèmes de certificats » plus loin dans cette rubrique.

## Comment savoir si vos serveurs Exchange sont correctement configurés ?

Pour vérifier que vous avez correctement publié vos serveurs Exchange locaux, utilisez l’Analyseur de connectivité à distance de Microsoft pour vérifier la connexion Internet entrante à vos serveurs Exchange locaux. Procédez comme suit :

1.  Accédez à l'outil [Analyseur de connectivité à distance](https://www.testexchangeconnectivity.com/).

2.  Cette étape constitue un test global des tâches des services Web Exchange visant à vérifier leur fonctionnement et à s'assurer que le point de terminaison des services web Exchange est configuré.
    
    Utilisez le test **Synchronisation, Notification, Disponibilité et Réponses automatiques (OOF)**, dans la section **Tests de connectivité des services web Microsoft Exchange**, et vérifiez l’absence d’erreurs. Si des erreurs se produisent, corriger les éléments identifiés par le test.

3.  Cette étape constitue un test global du service de découverte automatique visant à vérifier son fonctionnement et à s’assurer que le point de terminaison de la découverte automatique est configuré.
    
    Utilisez le test **Découverte automatique Outlook**, dans la section **Tests de connectivité Microsoft Office Outlook**, et vérifiez l’absence d’erreurs. Si des erreurs se produisent, corriger les éléments identifiés par le test.

4.  Cette étape constitue un test global de la connectivité SMTP et permet de vérifier que les serveurs Exchange peuvent recevoir des messages Internet entrants.
    
    Utilisez le test **Messagerie électronique SMTP entrante**, dans la section **Tests de messagerie Internet**, et vérifiez l’absence d’erreurs. Si des erreurs se produisent, corriger les éléments identifiés par le test.

## Résoudre des problèmes de certificats

La configuration des certificats installés sur les serveurs Exchange locaux peut être la source de problèmes survenant dans un déploiement hybride. Dans la plupart des cas, les problèmes de certificats suivants affectent les fonctions hybrides :

  - **Type de certificat**   Le certificat numérique utilisé pour le transport hybride sécurisé et défini dans l'Assistant Configuration hybride doit être émis par une autorité de certification tierce. Des certificats auto-signés ne peuvent pas être utilisés pour l'authentification du transport hybride. Si un certificat auto-signé est sélectionné ou affecté par inadvertance, le transport de messagerie sécurisée entre l'organisation Exchange Online et l'organisation locale ne fonctionnera pas correctement.

  - **Services affectés**   Les services IIS (Internet Information Service) et SMTP (Simple Mail Transport Protocol) doivent être affectés au certificat numérique utilisé pour le transport hybride. Si ces services ne sont pas affectés, le transport de messagerie sécurisée entre l'organisation Exchange Online et l'organisation locale ne fonctionnera pas correctement.

  - **Installation**   Le certificat numérique utilisé pour le transport de messagerie sécurisée entre l’organisation locale et l’organisation Exchange Online doit être installé sur tous les serveurs Exchange locaux. Dans un déploiement hybride avec des serveurs de transport Edge locaux, le certificat numérique doit également être installé sur vos serveurs de transport Edge. Si le certificat n’est pas installé sur les serveurs locaux, le transport de messagerie sécurisée entre l’organisation Exchange Online et l’organisation locale ne fonctionnera pas correctement.

  - **Expiration**   Le certificat numérique utilisé pour le transport de messagerie sécurisée entre l'organisation locale et l'organisation Exchange Online ne doit pas avoir expiré. Si le certificat a expiré, le transport de messagerie sécurisée entre l'organisation Exchange Online et l'organisation locale ne fonctionnera pas correctement.

## Comment savoir si vos certificats sont correctement configurés ?

Pour vérifier que le certificat pour le transport de messagerie hybride est correctement configuré sur vos serveurs Exchange locaux, procédez comme suit :

1.  Sur un serveur Exchangex local, ouvrez l’Environnement de ligne de commande Exchange Management Shell.

2.  Exécutez la commande suivante dans l’Environnement de ligne de commande Exchange Management Shell.
    
        Get-ExchangeCertificate| format-list

3.  Recherchez les informations du certificat que vous avez défini dans l'Assistant Configuration hybride qui sera utilisé pour le transport de messagerie sécurisée.

4.  Vérifiez que les valeurs des paramètres suivantes sont affectées au certificat :
    
      - **Paramètre IsSelfSigned**   La valeur de ce paramètre doit être *False*.
    
      - **Paramètre RootCAType**   La valeur de ce paramètre doit être *Third Party*.
    
      - **Paramètre Services**   La valeur de ce paramètre doit être *IIS, SMTP*.
    
      - **Paramètre NotAfter**   La valeur de ce paramètre est la date d'expiration du certificat. La date figurant ici ne doit pas être dépassée.

## Résolution des erreurs spécifiques de l'Assistant Configuration hybride

Si vous recevez une erreur lors de l'exécution de l'Assistant Configuration hybride, vous pouvez bien souvent résoudre le problème en effectuant quelques vérifications et actions simples. Consultez les suggestions suivantes pour la résolution de messages ou problèmes spécifiques que vous pouvez rencontrer lors de l'exécution de l'Assistant Configuration hybride.

  - **Message : « Le connecteur de réception par défaut est introuvable sur le serveur \<Nom du serveur\> »**   Ce message apparaît si le connecteur de réception d’un serveur Exchange répertorié dans l’attribut suivant n’écoute pas sur le port TCP 25 pour les protocoles IPv4 et IPv6 : `(Get-HybridConfiguration).ReceivingTransportServers.`
    
      -    Pour vérifier que les connecteurs de réception des serveurs Exchange répertoriés disposent des liaisons appropriées lorsque vous exécutez le `(Get-HybridConfiguration).ReceivingTransportServers.`, exécutez la commande suivante dans l’Environnement de ligne de commande Exchange Management Shell.
        
      Get-ReceiveConnector -Server <Server Name> | FT Identity, Bindings
        
      L’entrée suivante doit être répertoriée pour vos serveurs Exchange  : `{[::]:25, 0.0.0.0:25}`
        
      Si cette liaison n’est pas répertoriée, vous devez l’ajouter à votre connecteur de réception à l’aide du paramètre *Bindings* de la cmdlet **Set-ReceiveConnector**. Pour plus d'informations, consultez la rubrique [Set-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125140\(v=exchg.150\)).

