---
title: Procédures relatives au déploiement
TOCTitle: Procédures relatives au déploiement
ms:assetid: 6b7682bd-fe3d-43b9-a7db-66c0ac17656f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn195909(v=EXCHG.150)
ms:contentKeyID: 53275523
ms.date: 01/09/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Procédures relatives au déploiement

 

_**Dernière rubrique modifiée :** 2013-04-17_

Cette section contient les procédures que vous pouvez utiliser comme références avec le pack d'administration Exchange Server 2013. Pour connaître les procédures relatives au fonctionnement consécutif au déploiement, consultez la rubrique [Procedures related to post-deployment operation](procedures-related-to-post-deployment-operation.md).

## Vérification de l'état de déploiement de l'agent

Avant d'importer le pack d'administration Exchange Server 2013, vérifiez que les agents SCOM se trouvant sur vos serveurs Exchange sont opérationnels et que l'état du système d'exploitation est intègre dans SCOM.

Votre compte d'utilisateur doit être membre du rôle Administrateurs Operations Manager pour effectuer cette procédure.

1.  Connectez-vous au serveur SCOM et ouvrez la console SCOM.

2.  Cliquez sur **Analyse**, puis sur **Ordinateurs Windows**.

3.  Assurez-vous que tous vos serveurs Exchange affichent l'état **Intègre**.

![Agents intègres dans la console SCOM](images/Dn195909.7d1ff0bb-419e-40dc-babf-5fa2fb7229a8(EXCHG.150).png "Agents intègres dans la console SCOM")

## Vérification de la configuration du proxy de l'agent

Avant d'importer le pack d'administration Exchange Server 2013, vérifiez que le proxy de l'agent est activé pour la découverte dans SCOM. Autrement, les agents se trouvant sur vos serveurs Exchange ne signaleront pas l'état d'intégrité d'Exchange. Vous devez vérifier cette configuration pour tous vos serveurs Exchange.

Votre compte d'utilisateur doit être membre du rôle Administrateurs Operations Manager pour effectuer cette procédure.

1.  Connectez-vous au serveur SCOM et ouvrez la console SCOM.

2.  Dans la console Opérateur, cliquez sur **Administration**.

3.  Cliquez sur **Géré par agent**. Cliquez avec le bouton droit sur le serveur Exchange, puis sélectionnez **Propriétés**.

4.  Sous l'onglet **Sécurité**, vérifiez que la case **Autoriser cet agent à agir en tant que proxy et découvrir des objets gérés sur d'autres ordinateurs** est cochée.

5.  Cliquez sur **OK**.

## Vérification de la configuration de sécurité de l'agent

En raison du modèle de sécurité sous lequel Exchange 2013 a été testé, l'exécution de l'agent SCOM sur vos serveurs Exchange sous n'importe quel compte autre que **LocalSystem** n'est pas prise en charge. Si vous exécutez l'agent sous un compte autre que LocalSystem, l'exécution des transactions synthétiques échoue. Vous pouvez également rencontrer d'autres problèmes.

Votre compte d'utilisateur doit être membre du groupe de rôles Gestion de serveur pour effectuer cette procédure.

1.  Connectez-vous à votre serveur Exchange.

2.  Cliquez sur **Démarrer** \> **Outils d'administration** \> **Services**.

3.  Faites défiler la liste des services jusqu'à atteindre le service **Administration de System Center**.

4.  Vérifiez que la colonne **Ouvrir une session en tant que** affiche **Système local**.

5.  Si la colonne **Ouvrir une session en tant que** affiche une autre valeur, changez le mode d'ouverture de session du service sur Système local.
    
    1.  Cliquez avec le bouton droit sur **Administration de System Center**, puis sélectionnez **Propriétés**.
    
    2.  Sélectionnez l'onglet **Ouvrir une session**.
    
    3.  Cliquez sur l'option **Compte système local**.
    
    4.  Cliquez sur **OK**.

