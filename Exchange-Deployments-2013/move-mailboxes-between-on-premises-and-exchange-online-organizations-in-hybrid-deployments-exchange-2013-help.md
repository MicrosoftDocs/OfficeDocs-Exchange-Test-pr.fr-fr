---
title: 'Déplacement de boîtes aux lettres entre des organisations locales et Exchange Online dans des déploiements hybrides: Exchange 2013 Help'
TOCTitle: Déplacement de boîtes aux lettres entre des organisations locales et Exchange Online dans des déploiements hybrides
ms:assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/o365e_hrcmoverequest_fl312271(v=EXCHG.150)
ms:contentKeyID: 51406947
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déplacement de boîtes aux lettres entre des organisations locales et Exchange Online dans des déploiements hybrides

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2017-10-02_

Dans un déploiement Exchange hybride, vous pouvez soit déplacer des boîtes aux lettres Exchange locales vers l’organisation Exchange Online, soit déplacer des boîtes aux lettres Exchange Online vers l’organisation Exchange. Quand vous déplacez des boîtes aux lettres entre des organisations Exchange locales et Exchange Online, vous utilisez des lots de migration pour effectuer la demande de déplacement de boîte aux lettres à distance. Cette approche vous permet de déplacer des boîtes aux lettres existantes au lieu de créer des boîtes aux lettres utilisateur, puis d’y importer des informations utilisateur. Cette approche diffère de la migration de boîtes aux lettres utilisateur à partir d’une organisation Exchange locale vers Exchange Online dans le cadre d’une migration Exchange complète vers le nuage. Les déplacements de boîtes aux lettres décrits dans cette rubrique font partie de la gestion administrative d’Exchange dans le cadre d’une relation de coexistence à plus long terme entre les organisations Exchange locales et Exchange Online.

Pour en savoir plus sur la migration d’organisations Exchange locales vers Exchange Online, consultez la page [Méthodes de migration des comptes de messagerie vers Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour accomplir les procédures de déplacement de boîtes aux lettres décrites dans cette rubrique, vous devez avoir configuré un déploiement hybride entre vos organisations Echange locale et Exchange Online. Pour plus d'informations sur les déploiements hybrides, consultez la rubrique <a href="exchange-server-hybrid-deployments-exchange-2013-help.md">Déploiements hybrides Exchange Server</a>.<br />
<br />
Avant de déplacer des boîtes aux lettres à messagerie unifiée vers Exchange Online, vous devez vérifier que Skype Entreprise 2015 en local, Skype Entreprise Online et Exchange Online répondent tous aux exigences spécifiées dans <a href="hybrid-deployment-prerequisites-exchange-2013-help.md">Configuration requise pour un déploiement hybride</a>. Pour plus d’informations sur la façon de mapper vos stratégies de boîte aux lettres à messagerie unifiée locales sur les stratégies dans Exchange Online, voir <a href="https://technet.microsoft.com/fr-fr/library/bb124903(v=exchg.150)">Set-UMMailboxPolicy</a>.</td>
</tr>
</tbody>
</table>


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 10 minutes pour configurer le lot de migration, mais le temps total de migration dépend du nombre de boîtes aux lettres incluses dans chaque lot de migration.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de migration et de déplacement de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](https://technet.microsoft.com/fr-fr/library/dd638132\(v=exchg.150\)).

  - Un déploiement hybride est configuré entre vos organisations Exchange locale et Exchange Online.

  - Si vous exécutez Exchange 2013, vérifiez que le serveur proxy du service de réplication de boîtes aux lettres (proxy MRS) est activé sur vos serveurs d’accès au client Exchange 2013 locaux.

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


## Étape 1: Création d'un point de terminaison de migration

Avant d’effectuer des migrations de déplacement à distance par embarquement et débarquement dans un déploiement Exchange hybride, nous vous recommandons de créer des points de terminaison de migration à distance Exchange. Le point de terminaison de migration contient les paramètres de connexion pour un serveur Exchange local exécutant le service proxy MRS requis pour effectuer des migrations de déplacement à distance vers et à partir d’Exchange Online.

Pour connaître les procédures pas à pas, consultez la rubrique Création de points de terminaison de migration.

## Étape 2 : Activation du service proxy MRS

Si le service proxy MRS n’est pas encore activé pour vos serveurs d’accès au client Exchange 2013 locaux, procédez comme suit dans le Centre d’administration Exchange (CAE) :

1.  Ouvrez le CAE, puis accédez à **Serveurs**\>**Répertoires virtuels**.

2.  Sélectionnez le serveur d'accès au client, sélectionnez le répertoire virtuel **EWS** puis cliquez sur **Modifier** ![Icône Modifier](images/JJ906432.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Cochez la case **Proxy MRS activé**, puis cliquez sur **Enregistrer**.

## Étape 3: Utilisation du CAE pour déplacer des boîtes aux lettres

Dans le CAE sur un serveur Exchange, l'Assistant Déplacement de migration à distance sous l'onglet **Office 365** permet soit de déplacer des boîtes aux lettres utilisateur de l'organisation locale vers l'organisation Exchange Online, soit pour déplacer des boîtes aux lettres Exchange Online vers l'organisation locale. Choisissez l'une des procédures suivantes :

## Déplacement de boîtes aux lettres locales vers Exchange Online

Dans le CAE sur un serveur Exchange, l'Assistant Déplacement de migration à distance sous l'onglet **Office 365** permet de déplacer des boîtes aux lettres utilisateur de l'organisation locale vers l'organisation Exchange. Procédez comme suit :

1.  Ouvrez le CAE, puis accédez à **Office 365**\>**Destinataires**\>**Migration**.

2.  Cliquez sur **Ajouter** ![Icône Ajouter](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sélectionnez **Migrer vers Exchange Online**.

3.  Dans la page **Sélectionnez un type de migration**, sélectionnez **Migration de déplacement à distance**, puis cliquez sur **Suivant**.

4.  Dans la page **Sélectionnez les utilisateurs**, cliquez sur **Ajouter** ![Icône Ajouter](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), sélectionnez les utilisateurs locaux à déplacer vers Office 365, cliquez sur **Ajouter**, puis sur **OK**. Cliquez sur **Suivant**.

5.  Dans la page **Entrez les informations d'identification du compte d'utilisateur Windows**, entrez le nom du compte d'administrateur local dans le champ de texte **Nom de l'administrateur local**, puis entrez le mot de passe associé à ce compte dans le champ de texte **Mot de passe de l'administrateur local**. Par exemple, « corp\\administrator » et un mot de passe. Cliquez sur **Suivant**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous avez déjà créé un point de terminaison de migration, vous allez recevoir une invite de confirmation de point de terminaison pour cette étape. Si vous avez créé plusieurs points de terminaison de migration, vous devez en choisir un dans le menu déroulant des points de terminaison de migration.</td>
    </tr>
    </tbody>
    </table>


6.  Dans la page **Confirmez le point de terminaison de migration**, vérifiez que le nom de domaine complet (FQDN) de votre serveur Exchange local apparaît lorsque l’assistant confirme le point de terminaison de migration. Par exemple, « mail.contoso.com ». Cliquez sur **Suivant**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le service proxy MRS sur les serveurs Exchange limite automatiquement les demandes de déplacement de boîte aux lettres lorsque vous sélectionnez plusieurs boîtes aux lettres à déplacer vers Exchange Online. Le temps total nécessaire au déplacement dépend du nombre total de boîtes aux lettres sélectionnées, de leur taille et de la configuration du proxy MRS. Pour plus d’informations sur la personnalisation du proxy MRS, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/bb232205(v=exchg.150)">Limitation des messages</a>.</td>
    </tr>
    </tbody>
    </table>


7.  Dans la page **Configuration du déplacement**, dans le champ de texte **Nouveau lot de migration**, entrez un nom pour le lot de migration. Utilisez la flèche bas ![Icône de flèche vers le bas](images/JJ906432.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icône de flèche vers le bas") pour sélectionner le **Domaine de remise cible pour les boîtes aux lettres faisant l’objet d’une migration vers Office 365**. Dans la plupart des déploiements hybrides, il s’agit du domaine SMTP principal utilisé pour les boîtes aux lettres de l’organisation locale Exchange Online. Par exemple, contoso.mail.onmicrosoft.com. Vérifiez que l’option **Déplacer la boîte aux lettres principale avec la boîte aux lettres d’archivage** est activée, puis cliquez sur **Suivant**.

8.  Dans la page **Démarrer le lot**, sélectionnez au moins un destinataire pour recevoir le rapport complet du lot. Vérifiez que l'option **Démarrer le lot automatiquement** est sélectionnée, puis activez la case à cocher **Démarrer le lot de migration automatiquement**. Cliquez sur **Nouveau**.

## Déplacement de boîtes aux lettres Exchange Online vers l'organisation locale

Dans le CAE sur un serveur Exchange, l'Assistant Déplacement de migration à distance sous l'onglet **Office 365** permet de déplacer des boîtes aux lettres utilisateur de l'organisation locale vers l'organisation Exchange.

1.  Ouvrez le CAE, puis accédez à **Office 365**\>**Destinataires**\>**Migration**.

2.  Cliquez sur **Ajouter** ![Icône Ajouter](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sélectionnez **Migrer à partir d'Exchange Online**.

3.  Dans la page **Sélectionnez les utilisateurs**, cliquez sur **Sélectionner les utilisateurs à déplacer**, puis sur **Suivant**.

4.  Dans la page **Sélectionnez les utilisateurs**, cliquez sur **Ajouter** ![Icône Ajouter](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), sélectionnez les utilisateurs Exchange Online à déplacer vers l'organisation locale, cliquez sur **Ajouter**, puis sur **OK**. Cliquez sur **Suivant**.

5.  Dans la page **Confirmez le point de terminaison de migration**, vérifiez que le nom de domaine complet (FQDN) de votre serveur Exchange local apparaît lorsque l’assistant confirme le point de terminaison de migration. Par exemple, « mail.contoso.com ». Cliquez sur **Suivant**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le service proxy MRS sur les serveurs Exchange limite automatiquement les demandes de déplacement de boîte aux lettres lorsque vous sélectionnez plusieurs boîtes aux lettres à déplacer vers Exchange Online. Le temps total nécessaire au déplacement dépend du nombre total de boîtes aux lettres sélectionnées, de leur taille et des propriétés du proxy MRS. Pour plus d’informations sur la personnalisation du proxy MRS, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/bb232205(v=exchg.150)">Limitation des messages</a>.</td>
    </tr>
    </tbody>
    </table>


6.  Sur la page **Configuration de la migration**, dans le champ de texte **Nouveau nom de lot de migration**, entrez un nom pour le lot de migration. Entrez ensuite le domaine de remise cible dans le champ **Domaine de remise cible pour les boîtes aux lettres faisant l’objet d’une migration vers Office 365**. Dans la plupart des déploiements hybrides, il s’agit du domaine SMTP principal utilisé pour les boîtes aux lettres de l’organisation locale et pour celles de l’organisation Exchange Online. Par exemple, contoso.com.

7.  Déterminez si vous voulez également déplacer la boîte aux lettres d'archivage pour l'utilisateur sélectionné, puis, dans la champ de texte **Base de données cible**, entrez le nom de la base de données vers laquelle déplacer cette boîte aux lettres. Par exemple, Base de données de boîtes aux lettres 123456789. Cliquez sur **Suivant**.

8.  Dans la page **Démarrer le lot**, sélectionnez au moins un destinataire pour recevoir le rapport complet du lot. Vérifiez que l'option **Démarrer le lot automatiquement** est sélectionnée, puis activez la case à cocher **Démarrer le lot de migration automatiquement**. Cliquez sur **Nouveau**.

## Étape 4 : Suppression des lots de migration achevés

Une fois vos déplacements de boîtes aux lettres terminés, nous vous recommandons de supprimer les lots de migration achevés afin de réduire la probabilité d'erreurs en cas de nouveau déplacement des mêmes utilisateurs.

Pour supprimer un lot de migration achevé :

1.  Ouvrez le CAE, puis accédez à **Office 365**\>**Destinataires**\>**Migration**.

2.  Cliquez sur un lot de migration achevé, puis sur **Supprimer** ![Icône Supprimer](images/JJ906432.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

3.  Dans la boîte de dialogue de confirmation de la suppression, cliquez sur **Oui**.

## Étape 5 : Réactivation de l’accès hors connexion pour Outlook sur le web

L’accès hors connexion dans Outlook sur le web (précédemment appelé Outlook Web App) permet aux utilisateurs d’accéder à leurs boîtes aux lettres quand ils ne sont pas connectés à un réseau. Si vous migrez des boîtes aux lettres Exchange vers Exchange Online, les utilisateurs doivent redéfinir le paramètre d’accès hors connexion dans leur navigateur pour pouvoir utiliser Outlook sur le web hors connexion. Pour plus d’informations sur l’accès hors connexion dans Outlook sur le web, les navigateurs qui le prennent en charge et la manière de l’activer, consultez la rubrique [Utilisation d’Outlook Web App hors connexion](https://go.microsoft.com/fwlink/p/?linkid=286942).

## Comment savoir si cela a fonctionné ?

Lorsque vous déplacez des boîtes aux lettres utilisateur vers les organisations Exchange Online et locale, le succès de l'exécution de l'Assistant Déplacement à distance est la première indication que le déplacement de boîtes aux lettres fonctionnera comme prévu.

Le processus de déplacement des boîtes aux lettres prenant quelques minutes, vous pouvez également vérifier que le déplacement se déroule correctement en ouvrant le CAE, puis en sélectionnant **Office 365**\>**Destinataires**\>**Migration** pour afficher l'état du déplacement des boîtes aux lettres sélectionnées dans l'Assistant Déplacement à distance. L'**État** est défini sur **Synchronisation** durant le déplacement, puis sur **Terminé** une fois que la boîte aux lettres a bien été déplacée vers l'organisation Exchange Online ou locale.

Une fois le déplacement d’une boîte aux lettres terminé, vous pouvez vérifier que la boîte aux lettres distante se trouvant dans l’organisation Exchange Online ou locale a bien été déplacée en vérifiant ses propriétés. Pour ce faire, dans le CAE, accédez à **Destinataires**\>**Boîtes aux lettres** pour l’organisation Exchange Online ou locale. La boîte aux lettres utilisateur doit indiquer le **Type de boîte aux lettresOffice 365** pour les boîtes aux lettres Exchange Online et **Utilisateur** pour les boîtes aux lettres locales.

Vous pouvez également exécuter la cmdlet suivante dans l’environnement de ligne de commande Exchange Management Shell pour vérifier l’état du lot de migration.

    Get-MigrationBatch -Identity <batch name>

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Office 365. Pour accéder à ces forums, vous devez vous connecter en utilisant un compte disposant de l’accès administrateur au service informatique en nuage. Consultez les forums suivants : [Forums Office 365](https://go.microsoft.com/fwlink/p/?linkid=201915)

## Vous débutez avec Office 365 ?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Icône rapide pour LinkedIn Learning" alt="Icône rapide pour LinkedIn Learning" /> <strong>Vous débutez avec Office 365 ?</strong><br />
Découvrez les cours vidéo gratuits pour <a href="https://support.office.com/fr-fr/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> proposés par LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

