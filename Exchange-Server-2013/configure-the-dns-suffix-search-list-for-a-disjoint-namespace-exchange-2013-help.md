---
title: 'Config. d’une liste de recherche de suffixe DNS pr un espace de noms disjoint'
TOCTitle: Configuration d’une liste de recherche de suffixe DNS pour un espace de noms disjoint
ms:assetid: cfa715ac-7b69-47c3-b206-933ec2cf677b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb847901(v=EXCHG.150)
ms:contentKeyID: 50479264
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration d’une liste de recherche de suffixe DNS pour un espace de noms disjoint

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Cette rubrique décrit l’utilisation de la console de gestion de stratégies de groupes (GPMC) pour configurer la liste de recherche de suffixe DNS. Dans certains scénarios Microsoft Exchange 2013, si vous possédez un espace de noms disjoint, vous devez configurer la liste de recherche de suffixe DNS pour inclure plusieurs suffixes DNS.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 10 minutes

  - Pour pouvoir exécuter cette procédure, vous devez utiliser un compte auquel l’appartenance au groupe Administrateurs de domaines a été déléguée.

  - Confirmez que vous avez installé .NET Framework 3.0 sur l’ordinateur sur lequel vous allez installer le GPMC.
    
    > [!NOTE]
    > La version actuelle de GPMC téléchargeable à partir du Centre de téléchargement Microsoft fonctionne sur les versions 32 bits des systèmes d’exploitation Windows Server 2003 et Windows XP et peut gérer à distance les objets de stratégie de groupe sur les contrôleurs de domaine 32 bits et 64 bits. Cette version de GPMC ne comprend pas de version 64 bits, et la version 32 bits ne s’exécute pas sur les plates-formes 64 bits. La version 32 bits d’Windows Server 2008 et la version 32 bits d’Windows Vista comprennent une version 32 bits de GPMC. La version 64 bits d’Windows Server 2008 et la version 64 bits d’Windows Vista comprennent une version 64 bits de GPMC.


  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser la console GPMC pour configurer la liste de recherche de suffixe DNS

1.  Sur un ordinateur 32 bits dans votre domaine, installez GPMC avec le Service Pack 1 (SP1). Pour obtenir des informations de téléchargement, voir [Console de gestion des stratégies de groupes avec Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=100126).
    
    > [!NOTE]
    > Si vous disposez d’un ordinateur dans votre domaine qui exécute Windows Server 2008 ou Windows Vista, vous pouvez ignorer cette étape.


2.  Cliquez sur **Démarrer** \> **Programmes** \> **Outils d’administration** \> **Gestion des stratégies de groupe**.

3.  Dans **Gestion des stratégies de groupes**, développez la forêt et le domaine dans lequel vous souhaitez appliquer la stratégie de groupe. Cliquez avec le bouton droit sur **Objets de stratégie de groupe**, puis sur **Nouveau**.

4.  Dans **Nouvel objet GPO**, entrez un nom pour la stratégie, puis cliquez sur **OK**.

5.  Cliquez avec le bouton droit sur la nouvelle stratégie créée à l’étape 4, puis cliquez sur **Modifier**.

6.  Dans **Éditeur de gestion des stratégies de groupes**, développez **Configuration ordinateur**, développez **Stratégies**, développez **Modèles d’administration**, développez **Réseau**, puis cliquez sur **Client DNS**.

7.  Cliquez avec le bouton droit sur **Liste de recherche de suffixe DNS**, cliquez sur **Toutes les tâches**, puis sur **Modifier**.

8.  Dans la page **Propriétés de la liste de recherche de suffixe DNS**, sélectionnez **Activée**. Dans la boîte de dialogue **Suffixes DNS**, entrez le suffixe DNS principal de l’ordinateur disjoint, le nom de domaine DNS et les espaces de noms supplémentaires pour les autres serveurs avec lesquels Exchange peut interagir, tels que les serveurs de surveillance ou des serveurs pour applications tierces. Cliquez sur **OK**.

9.  Dans **Gestion des stratégies de groupes**, développez **Objets de stratégie de groupe**, puis sélectionnez la stratégie créée à l’étape 4. Sous l’onglet **Étendue**, définissez l’étendue de la stratégie afin qu’elle s’applique uniquement aux ordinateurs disjoints.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez terminé avec succès le migration, procédez comme suit :

  - Après avoir installé Exchange 2013, vérifiez si vous pouvez envoyer des messages électroniques à l’intérieur et à l’extérieur de votre organisation.

## Pour plus d’informations

[Stratégie de groupe Windows Server](https://go.microsoft.com/fwlink/p/?linkid=100128)

[Stratégie de groupe](https://go.microsoft.com/fwlink/?linkid=268043)

[Scénarios d’espace de noms disjoint](disjoint-namespace-scenarios-exchange-2013-help.md)

