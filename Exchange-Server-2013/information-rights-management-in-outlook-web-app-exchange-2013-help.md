---
title: 'Gestion des droits relatifs à l’information dans Outlook Web App: Exchange 2013 Help'
TOCTitle: Gestion des droits relatifs à l’information dans Outlook Web App
ms:assetid: 60a49dab-17ac-4d2c-9b41-7d87250d6c00
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876891(v=EXCHG.150)
ms:contentKeyID: 50478303
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des droits relatifs à l’information dans Outlook Web App

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les professionnels de l’information utilisent de plus en plus la messagerie pour échanger des informations confidentielles. Pour permettre de sécuriser ces informations, les organisations peuvent utiliser la gestion des droits relatifs à l’information (IRM) pour appliquer une protection permanente au contenu de la messagerie. Avant Microsoft Exchange Server 2010, l’utilisation efficace de la protection IRM était limitée aux clients d’Outlook. Dans Exchange Server 2007, les utilisateurs de Microsoft Outlook Web Access devaient télécharger le complément de gestion des droits relatifs à l’information pour Microsoft Internet Explorer afin de pouvoir accéder au contenu protégé par IRM.

Dans Exchange 2013, la gestion des droits relatifs à l’information dans Outlook Web App permet aux utilisateurs d’accéder à la fonctionnalité IRM enrichie offerte par Exchange pour appliquer une protection permanente par IRM au contenu de la messagerie.

La fonctionnalité IRM suivante est disponible dans Outlook Web App :

  - **Envoyer des messages protégés par IRM**   Comme indiqué dans la figure suivante, les utilisateurs d’Outlook Web App peuvent se servir de la liste déroulante des autorisations et sélectionner un modèle de stratégie de droits à appliquer au message. Cela permet aux utilisateurs d’envoyer des messages protégés par IRM à partir d’Outlook Web App. Les messages sont protégés par IRM par les serveurs d’accès au client.
    
    ![Envoi d’un message protégé par IRM à partir d’OWA](images/Dd876891.fa8cabb5-c049-46dc-8b29-9d9957dbfd3e(EXCHG.150).gif "Envoi d’un message protégé par IRM à partir d’OWA")  

  - **Pièces jointes protégées par IRM**   Lorsque les utilisateurs envoient un message protégé par IRM à partir d’Outlook Web App, les fichiers attachés au message reçoivent également la même protection IRM et sont protégés à l’aide du même modèle de stratégie de droits que le message. Dans Exchange 2013, la protection IRM est appliquée aux fichiers associés à Microsoft Office Word, Excel et PowerPoint, ainsi qu’aux fichiers .xps et aux messages électroniques. La protection IRM est appliquée à une pièce jointe uniquement si celle-ci est déjà protégée par IRM. Pour en savoir plus sur des modèles de stratégie des droits des services AD RMS (Active Directory Rights Management Services), consultez [Gestion des droits relatifs à l’information](information-rights-management-exchange-2013-help.md).
    
    > [!NOTE]
    > La gestion des droits relatifs à l’information dans Outlook Web App protège uniquement les pièces jointes des fichiers pris en charge mentionnés dans cette section. Les pièces jointes qui utilisent des formats de fichier non pris en charge ne sont pas protégées. Lorsque les utilisateurs d’Outlook Web App protègent un message et attachent un fichier dont le format n’est pas pris en charge, une notification s’affiche informant les utilisateurs que seuls les types de fichier pris en charge sont protégés.
    
    > [!IMPORTANT]
    > La protection IRM ne peut pas être appliquée à un message qui est déjà signé ou crypté à l’aide du système S/MIME. Pour appliquer la protection IRM, le chiffrement et la signature S/MIME doivent être supprimés à partir du message. Ceci vaut également pour les messages protégés par IRM. Les utilisateurs ne peuvent pas les signer ou les chiffrer en utilisant le système S/MIME.


  - **Lire les messages protégés par IRM**   Les messages protégés par les expéditeurs à l’aide du cluster AD RMS de votre organisation sont rendus dans le volet de visualisation d’Outlook Web App. Aucun complément n’a besoin d’être installé et l’ordinateur n’a pas besoin d’être inscrit dans le déploiement AD RMS. Lorsqu’un utilisateur ouvre un message ou l’affiche dans le volet de visualisation, le message est déchiffré à l’aide de la licence d’utilisation ajoutée par l’agent de pré-licence. Après décryptage, le message s’affiche dans le volet de visualisation. Si une pré-licence n’est pas disponible, Outlook Web App en demande une à partir du serveur AD RMS et rend ensuite le message. Lors de la lecture des pièces jointes protégés par IRM dans Outlook Web App, la technologie d’affichage de document Web-Ready n’est pas disponible.
    
    > [!NOTE]
    > La gestion des droits relatifs à l’information dans Outlook Web App ne peut pas empêcher les utilisateurs d’effectuer des captures d’écran en utilisant la fonctionnalité d’impression écran de la même manière qu’avec Outlook et les autres applications Office. Cette situation affecte le droit d’extraction qui empêche la copie du contenu du message, si spécifié dans le modèle de stratégie de droits AD RMS.


  - **Prise en charge IRM entre navigateurs pour plusieurs plates-formes**   La gestion des droits relatifs à l’information dans Outlook Web App offre une prise en charge IRM entre navigateurs pour plusieurs plates-formes. La gestion des droits relatifs à l’information dans Outlook Web App est prise en charge dans tous les navigateurs pris en charge par Exchange 2013, y compris sur les systèmes d’exploitation Apple Macintosh et Linux. Pour en savoir plus sur les navigateurs et les systèmes d’exploitation pris en charge, consultez [Navigateurs Outlook Web App pris en charge](https://go.microsoft.com/fwlink/p/?linkid=129362).

  - **Affichage de document WebReady**   Dans Exchange 2013, les utilisateurs peuvent afficher des pièces jointes protégées par IRM prises en charge en utilisant l’affichage de document WebReady. Cela permet aux utilisateurs d’afficher des pièces jointes sans avoir à télécharger la pièce jointe à l’aide de l’application associée.

Souhaitez-vous rechercher les tâches de gestion liées à la gestion des droits relatifs à l’information (IRM) ? Voir [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Activation de la gestion des droits relatifs à l’information dans Outlook Web App

Pour activer la gestion des droits relatifs à l’information dans Outlook Web App, vous devez ajouter la boîte aux lettres de fédération, boîte aux lettres système créée par le programme d’installation d’Exchange 2013, au groupe des super utilisateurs dans AD RMS. Pour plus d’informations, voir [Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md). Cela permet aux serveurs Exchange 2013 d’accéder aux messages protégés par IRM.

Vous devez également activer l’IRM dans Outlook Web App en utilisant la cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)) dans l’environnement de ligne de commande Exchange Management Shell. Cette opération active la gestion des droits relatifs à l’information dans Outlook Web App pour votre organisation Exchange 2013. Vous pouvez désactiver ou activer la gestion des droits relatifs à l’information dans Outlook Web App pour un répertoire virtuel Outlook Web App. Vous pouvez également contrôler la fonctionnalité IRM dans Outlook Web App aux niveaux suivants de granularité :

  - **Répertoire virtuel de Per-Outlook Web App**   Pour activer ou désactiver la Gestion des droits relatifs à l’information (IRM) dans Outlook Web App pour un répertoire virtuel Outlook Web App, utilisez la cmdlet **Set-OWAVirtualDirectory** et définissez le paramètre *IRMEnabled* à `$false` ou `$true` (par défaut). Ainsi, vous pouvez désactiver la Gestion des droits relatifs à l’information (IRM) dans Outlook Web App pour un répertoire virtuel sur un serveur Exchange 2013 Client Access, tout en la conservant activée pour un autre répertoire virtuel sur un autre serveur d’accès au client.

  - **Stratégie de la boîte aux lettres Per-Outlook Web App**   Pour activer ou désactiver la Gestion des droits relatifs à l’information (IRM) dans Outlook Web App pour un répertoire virtuel Outlook Web App, utilisez la cmdlet **Set-OWAMailboxPolicy** et définissez le paramètre *IRMEnabled* à `$false` ou `$true` (par défaut). Ainsi, vous pouvez activer la Gestion des droits relatifs à l’information (IRM) dans Outlook Web App pour un ensemble d’utilisateurs et la désactiver pour un autre ensemble d’utilisateurs en leur attribuant une stratégie de boîte aux lettres Outlook Web App différente.

Pour plus d’informations, voir [Activer ou désactiver la gestion des droits relatifs à l’information (IRM) sur les serveurs d’accès au client](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md).

