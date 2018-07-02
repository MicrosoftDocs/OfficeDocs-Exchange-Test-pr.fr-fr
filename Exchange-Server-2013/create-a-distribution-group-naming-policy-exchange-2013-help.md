---
title: 'Créer une stratégie de noms de groupe de distribution: Exchange 2013 Help'
TOCTitle: Créer une stratégie de noms de groupe de distribution
ms:assetid: b2ffb654-345d-4be1-be8e-83d28901373e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ218693(v=EXCHG.150)
ms:contentKeyID: 50477322
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une stratégie de noms de groupe de distribution

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-01_

Une *stratégie de noms de groupes* vous permet de standardiser et de gérer les noms de groupes de distribution créés par les utilisateurs dans votre organisation. Vous pouvez exiger qu'un préfixe et un suffixe spécifiques soient ajoutés au nom pour le groupe de distribution lorsqu'il est créé, et vous pouvez empêcher que des mots spécifiques soient utilisés. Cela vous aide à réduire l'utilisation de mots inappropriés dans les noms de groupe.

Une stratégie de noms de groupes :

  - Applique une stratégie d'affectation de nom pour les groupes créés par les utilisateurs.

  - Identifie les groupes de distribution dans le carnet d'adresses partagé.

  - Suggère la fonction ou l'appartenance du groupe.

  - Identifie le type des utilisateurs qui sont des membres possibles du groupe.

  - Identifie la région géographique dans laquelle le groupe est utilisé.

  - Bloque des mots inappropriés dans les noms de groupe.

Comment fonctionne une stratégie de noms de groupes ? Lorsqu'un utilisateur crée un groupe, il spécifie un nom dans le champ Nom d'affichage. Une fois le groupe créé, Microsoft Exchange applique la stratégie de noms de groupes en ajoutant un préfixe ou suffixe que vous avez défini dans la stratégie de noms de groupes. Le nom complet est affiché dans la liste de groupes de distribution du Centre d'administration Exchange (CAE), le carnet d'adresses partagé, et les champs À :, Cc :, et De : des messages électroniques. Si un utilisateur essaie d'utiliser un mot que vous avez bloqué, il obtient un message d'erreur lorsqu'il essaie d'enregistrer le nouveau groupe et il lui est demandé de supprimer le mot bloqué et d'enregistrer à nouveau le groupe.

Voici quelques exemples de stratégie de noms de groupes. Dans chaque exemple, **\<Nom de groupe\>** est un nom descriptif fourni par la personne qui crée le groupe. Exchange ajoute les préfixes et suffixes définis par la stratégie pour le nom complet quand le groupe est créé.

  - Chaînes de texte, avec les traits de soulignement, utilisées pour un préfixe unique (**GD**) et suffixe (**Utilisateurs**) :
    
    **DG\_\<Group Name\>\_Users**

  - Plusieurs préfixes (**DG** et **Contoso**) et un suffixe (**Utilisateurs**), à l'aide de chaînes de texte :
    
    **DG\_Contoso\_\<Group Name\>\_Users**

  - Attribut (**Service**) utilisé pour le préfixe :
    
    **Department\_\<Group Name\>**
    
    Par exemple, indiquez que votre école remplit l'attribut Service pour les enseignants. Voici un exemple d'un nom de groupe créé par un enseignant dans le service Psychologie :
    
    **Psychologie\_Cognitive201**
    
    Dans cet exemple, le trait de soulignement (\_) est fourni comme seule chaîne de texte dans un deuxième préfixe pour séparer le nom de service du nom de groupe.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de distribution » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Les noms de groupe sont limités à 64 caractères. Cela inclut le nombre combiné de caractères dans le préfixe, le nom de groupe fourni par l'utilisateur et le suffixe.

  - La stratégie de noms de groupes est appliquée uniquement aux groupes créés par les utilisateurs. Lorsque vous ou un autre administrateur utilisez le CAE pour créer des groupes de distribution, la stratégie de noms de groupes est ignorée et n'est pas appliquée au nom de groupe.

  - Les noms de groupes sont créés sans espacement. Nous recommandons d'utiliser un trait de soulignement (\_) ou un autre espace réservé entre les chaînes de texte, les attributs et le nom de groupe.

  - Vous pouvez utiliser Windows PowerShell pour remplacer la stratégie de noms de groupes quand vous créez et modifiez un groupe de distribution. Pour plus d'informations, voir [Ignorer la stratégie de noms des groupes de distribution](override-the-distribution-group-naming-policy-exchange-2013-help.md).

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


## Utiliser le CAE pour créer une stratégie de noms de groupes

1.  Dans le CAE, sélectionnez **Groupes** \> **Plus** \> **Configurer la stratégie de nommage de groupe**.

2.  Sous **Stratégie de noms de groupes**, configurez le préfixe en sélectionnant soit **Attribut**, soit **Texte** dans le menu déroulant.
    
      - **Attribut**   Sélectionnez l'attribut puis cliquez sur **OK**.
    
      - **Texte**   Entrez la chaîne de texte et cliquez sur **OK**.
    
    Notez que la chaîne de texte que vous avez tapée ou l'attribut que vous avez sélectionné est affiché sous la forme d'un lien hypertexte. Cliquez sur le lien hypertexte pour modifier la chaîne de texte ou l'attribut.

3.  Cliquez sur **Ajouter** pour ajouter des préfixes supplémentaires.

4.  Pour le suffixe, dans le menu déroulant, sélectionnez **Attribut** ou **Texte** et configurez le suffixe.

5.  Cliquez sur **Ajouter** pour ajouter des suffixes supplémentaires.
    
    Après avoir ajouté un préfixe ou un suffixe, remarquez qu'un aperçu de la stratégie de noms de groupes s'affiche.

6.  Pour supprimer un préfixe ou un suffixe de la stratégie, cliquez sur **Supprimer**![Supprimer](images/JJ218693.37ba42c3-6f0d-42f3-b69b-ff912a99b5b7(EXCHG.150).gif "Supprimer").

7.  Cliquez sur **Mots bloqués** pour ajouter ou supprimer des mots bloqués.
    
      - Pour ajouter un mot à la liste, entrez le mot à bloquer et cliquez sur **Ajouter**![Ajouter un symbole pour les dossiers exclus dans la migration de courrier électronique](images/JJ218693.444d5c83-821f-472c-b733-e84308e2531e(EXCHG.150).gif "Ajouter un symbole pour les dossiers exclus dans la migration de courrier électronique").
    
      - Pour supprimer un mot de la liste, sélectionnez-le, puis cliquez sur **Supprimer**.
    
      - Pour modifier un mot bloqué existant, sélectionnez-le et cliquez sur **Modifier**.

8.  Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé une stratégie de noms de groupes, procédez comme suit :

  - Dans le CAE, sélectionnez **Groupes** \> **Plus** \> **Configurer la stratégie de nommage de groupe**.
    
    Sur la page **Stratégie de noms de groupes**, la stratégie de noms de groupes que vous avez définie s'affiche sous **Aperçu de la stratégie**.

  - Dans Windows PowerShell, exécutez la commande suivante pour afficher la stratégie de noms de groupes.
    
        Get-OrganizationConfig | FL DistributionGroupNamingPolicy

