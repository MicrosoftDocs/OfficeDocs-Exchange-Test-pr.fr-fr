---
title: 'Changements constatés dans AD avec l’installation d’Exchange 2013'
TOCTitle: Quels sont les changements constatés dans Active Directory avec l’installation d’Exchange 2013 ?
ms:assetid: 07386078-6103-49a2-8698-2d41db9cec95
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn750898(v=EXCHG.150)
ms:contentKeyID: 62371335
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Quels sont les changements constatés dans Active Directory avec l’installation d’Exchange 2013 ?

 

_**Sapplique à :** Exchange Server, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-05-26_

Lorsque vous installez Exchange 2013, des modifications sont apportées à votre forêt et à vos domaines Active Directory. Exchange effectue cette opération pour pouvoir stocker des informations sur les serveurs et boîtes aux lettres Exchange, ainsi que sur les autres objets liés à Exchange dans votre organisation. Ces changements sont effectués pour vous lorsque vous exécutez l’Assistant Installation d’Exchange 2013 ou lorsque vous exécutez les commandes *PrepareSchema*, *PrepareAD* et *PrepareDomains* au cours de la configuration de ligne de commande de Exchange 2013 (pour plus d’informations sur l’utilisation de ces commandes, voir [Préparation d’Active Directory et des domaines](prepare-active-directory-and-domains-exchange-2013-help.md)). Si vous voulez en savoir plus sur les modifications qu’Exchange apporte à Active Directory, cette rubrique est faite pour vous. Elle explique ce que fait Exchange à chaque étape de la préparation d’Active Directory.

Trois étapes doivent être effectuées pour préparer Active Directory pour Exchange :

  - Étendre le schéma Active Directory

  - Préparer des conteneurs, des objets et d’autres éléments Active Directory

  - Préparer les domaines Active Directory

Une fois que les trois étapes sont terminées, votre forêt Active Directory est prête pour Exchange 2013. Pour plus d’informations sur l’installation d’Exchange 2013, voir [Installer Exchange 2013 à l’aide de l’Assistant Installation](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

## Étendre le schéma Active Directory

L’extension du schéma Active Directory ajoute et met à jour des classes, des attributs et d’autres éléments. Ces changements sont nécessaires afin qu’Exchange puisse créer des conteneurs et des objets pour stocker des informations à propos de l’organisation Exchange. Exchange apporte de nombreuses modifications au schéma Active Directory ; par conséquent, il existe une rubrique dédiée à cette étape. Pour consulter toutes les modifications apportées au schéma, voir [Modifications apportées au schéma Active Directory d’Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

Cette étape est effectuée automatiquement lorsque vous exécutez l’Assistant Installation d’Exchange 2013 sur le premier serveur Exchange 2013 de la forêt Active Directory. Elle est également effectuée lorsque vous exécutez la configuration de ligne de commande Exchange 2013 avec la commande *PrepareSchema* (ou éventuellement avec la commande *PrepareAD*) sur le premier serveur Exchange 2013 de la forêt. Pour savoir plus sur l’extension du schéma, voir [Extend the Active Directory schema](prepare-active-directory-and-domains-exchange-2013-help.md) dans [Préparation d’Active Directory et des domaines](prepare-active-directory-and-domains-exchange-2013-help.md).

Après avoir terminé l’extension du schéma, Exchange définit la version du schéma, qui est stockée dans l’attribut **ms-Exch-Schema-Version-Pt**. Si vous voulez vérifier que le schéma Active Directory a bien été étendu, vous pouvez vérifier la valeur stockée dans cet attribut. Si la valeur indiquée dans l’attribut correspond à la version du schéma indiquée pour la version d’Exchange 2013 que vous avez installée, cela signifie que l’extension du schéma a réussi. Pour obtenir la liste des versions d’Exchange et pour savoir comment vérifier la valeur de cet attribut, voir la section [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) dans [Préparation d’Active Directory et des domaines](prepare-active-directory-and-domains-exchange-2013-help.md).

## Préparer des conteneurs, des objets et d’autres éléments Active Directory

Une fois le schéma étendu, l’étape suivante consiste à ajouter tous les conteneurs, objets, attributs et autres éléments utilisés par Exchange pour stocker des informations dans Active Directory. La plupart des modifications apportées par cette étape sont appliquées à l’ensemble de la forêt Active Directory. Une série moins importante de modifications est apportée au domaine Active Directory local où la commande *PrepareAD* a été exécutée au cours de l’installation.

Les modifications apportées à la forêt Active Directory sont les suivantes :

  - Création du conteneur Microsoft Exchange sous CN=Services,CN=Configuration,DC=\<*root domain*\> s’il n’existe pas déjà.

  - Création des conteneurs et objets suivants sous CN=\<*organization name*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> s’ils n’existent pas déjà :
    
      - CN=Conteneur de listes d’adresses
    
      - CN=Stratégies de boîte aux lettres de carnet d’adresses
    
      - CN=Adressage
    
      - CN=Groupes d’administration
    
      - CN=Demandes d’approbation
    
      - CN=Configuration d’authentification
    
      - CN=Configuration de disponibilité
    
      - CN=Accès au client
    
      - CN=Connexions
    
      - CN=Conteneur de dossiers ELC
    
      - CN=Stratégies de boîte aux lettres ELC
    
      - CN=Assistance Exchange
    
      - CN=Fédération
    
      - CN=Approbations de fédération
    
      - CN=Paramètres globaux
    
      - CN=Configuration hybride
    
      - CN=Stratégies de boîte aux lettres mobiles
    
      - CN=Paramètres de boîte aux lettres mobiles
    
      - CN=Paramètres de surveillance
    
      - CN=Stratégies de boîte aux lettres OWA
    
      - CN=Conteneur de stratégie d’approvisionnement
    
      - CN=Paramètres de notification Push
    
      - CN=RBAC
    
      - CN=Stratégies de destinataire
    
      - CN=Conteneur de stratégies de comptes distants
    
      - CN=Conteneur de stratégies de rétention
    
      - CN=Conteneur de balise de stratégie de rétention
    
      - CN=Points de terminaison de service
    
      - CN=Stratégies système
    
      - CN=Stratégies d’approvisionnement de boîte aux lettres d’équipe
    
      - CN=Paramètres de transport
    
      - CN=Conteneur de standard automatique de messagerie unifiée
    
      - CN=Conteneur de plan de numérotation de messagerie unifiée
    
      - CN=Conteneur de passerelle IP de messagerie unifiée
    
      - CN=Stratégies de boîte aux lettres de messagerie unifiée
    
      - CN=Paramètres de gestion des charges de travail

  - Création des conteneurs et objets suivants sous CN=Paramètres de transport,CN=\<*Organization Name*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> s’ils n’existent pas déjà :
    
      - CN=Domaines acceptés
    
      - CN=Configuration de point de contrôle
    
      - CN=Personnalisation DNS
    
      - CN=Règles d’intercepteur
    
      - CN=Filtre de programmes malveillants
    
      - CN=Classifications de message
    
      - CN=Hygiène des messages
    
      - CN=Règles
    
      - CN=MicrosoftExchange329e71ec88ae4615bbc36ab6ce41109e

  - Définition d’autorisations sur l’ensemble de la partition de configuration dans Active Directory.

  - Importation du fichier Rights.ldf. Ce fichier ajoute les autorisations qui sont nécessaires pour l’installation d’Exchange et la configuration d’Active Directory.

  - Création de l’unité d’organisation des groupes de sécurité MicrosoftExchange dans le domaine racine de la forêt et attribution d’autorisations.

  - Création des groupes de rôles de gestion suivants au sein des unités d’organisation de groupes de sécurité Microsoft Exchange s’ils n’existent pas déjà :
    
      - Gestion de la conformité
    
      - Installation déléguée
    
      - Gestion de la découverte
    
      - Support technique
    
      - Gestion de l’hygiène
    
      - Gestion de l’organisation
    
      - Gestion des dossiers publics
    
      - Gestion des destinataires
    
      - Gestion des enregistrements
    
      - Gestion du serveur
    
      - Gestion de la messagerie unifiée
    
      - Gestion de l’organisation en affichage seul

  - Ajout des nouveaux groupes de rôles de gestion (qui apparaissent en tant que groupes de sécurité universels dans Active Directory) créés dans les unités d’organisation de groupes de sécurité MicrosoftExchange à l’attribut **otherWellKnownObjects** stocké sur le conteneur CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\>.

  - Création du contact d’origine du message vocal de messagerie unifiée dans le conteneur d’objets système Microsoft Exchange du domaine racine.

  - Préparation du domaine où la commande *PrepareAD* a été exécutée pour Exchange 2013. Pour plus d’informations sur ce qui est fait pour préparer le domaine Active Directory pour Exchange, voir Préparer les domaines Active Directory.

  - Définition de la propriété **msExchProductId** sur l’objet d’organisation Exchange. Si vous voulez vérifier que le schéma Active Directory a bien été étendu, vous pouvez vérifier la valeur stockée dans cette propriété. Si la valeur indiquée dans la propriété correspond à la version du schéma indiquée pour la version d’Exchange 2013 que vous avez installée, cela signifie que l’extension du schéma a réussi. Pour obtenir la liste des versions d’Exchange et pour savoir comment vérifier la valeur de cette propriété, voir la section [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) dans [Préparation d’Active Directory et des domaines](prepare-active-directory-and-domains-exchange-2013-help.md).

## Préparer les domaines Active Directory

L’étape finale de préparation d’Active Directory pour Exchange consiste à préparer l’ensemble des domaines Active Directory où des serveurs Exchange seront installés ou l’ensemble des domaines où seront situés des utilisateurs à extension boîte aux lettres. Cette étape est effectuée automatiquement dans le domaine où la commande *PrepareAD* a été exécutée.

Les modifications apportées aux domaines Active Directory sont les suivantes :

  - Création du conteneur des objets système Microsoft Exchange dans la partition de domaine racine dans Active Directory, s’il n’existe pas déjà.

  - Définition des autorisations sur le conteneur des objets système Microsoft Exchange pour les groupes de sécurité des serveurs, de gestion de l’organisation et des utilisateurs authentifiés Exchange.

  - Création du groupe global de domaine Serveurs de domaine d’installation Exchange dans le domaine actuel. Ce groupe est placé dans le conteneur d’objets système Microsoft Exchange.

  - Ajout du groupe Serveurs de domaine d’installation Exchange au groupe universel de sécurité Serveurs Exchange dans le domaine racine.

  - Attribution d’autorisations au niveau du domaine pour les groupes universels de sécurité des serveurs Exchange et les groupes universels de sécurité de gestion de l’organisation.

  - Définition de la propriété **objectVersion** dans le conteneur d’objets système Microsoft Exchange, sous DC=\<*root domain*\>. Si vous voulez vérifier que le schéma Active Directory a bien été étendu, vous pouvez vérifier la valeur stockée dans cette propriété. Si la valeur indiquée dans la propriété correspond à la version du schéma indiquée pour la version d’Exchange 2013 que vous avez installée, cela signifie que l’extension du schéma a réussi. Pour obtenir la liste des versions d’Exchange et pour savoir comment vérifier la valeur de cette propriété, voir la section [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) dans [Préparation d’Active Directory et des domaines](prepare-active-directory-and-domains-exchange-2013-help.md).

