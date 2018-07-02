---
title: 'Ne figure pas dans le domaine/site du contrôleur de schéma_NotInSchemaMasterDomain: Exchange 2013 Help'
TOCTitle: Ne figure pas dans le domaine/site du contrôleur de schéma_NotInSchemaMasterDomain
ms:assetid: 5e44eb33-4c30-4c3d-ba68-5c30bef1731f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.notinschemamasterdomain(v=EXCHG.150)
ms:contentKeyID: 50478290
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ne figure pas dans le domaine/site du contrôleur de schéma\_NotInSchemaMasterDomain

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft® Exchange Server 2007 ne peut pas poursuivre son exécution, car l’ordinateur qui l’exécute ne se trouve pas dans le même site ou domaine du service d’annuaire Active Directory® que le serveur auquel le rôle de contrôleur de schéma du domaine, également appelé FSMO.

Le programme d’installation d’Exchange 2007 nécessite que le contrôleur de domaine qui sert de contrôleur de schéma du domaine se trouve dans les mêmes site et domaine que l’ordinateur local qui exécute le programme d’installation d’Exchange.

Le contrôleur de schéma du domaine contrôle toutes les mises à jour et les modifications apportées au schéma Active Directory.

Pour résoudre ce problème, exécutez le programme d’installation d’Exchange Server 2007 à l’aide des commutateurs **/prepareschema** et **/prepareAD** des mêmes site et domaine que le contrôleur de schéma de domaine.

Pour plus d’informations sur les commutateurs d’installation **/prepareschema** et **/prepareAD**, reportez-vous à la rubrique documentation du produit Exchange 2007 « Comment pour préparer Active Directory et domaines » (<https://go.microsoft.com/fwlink/?linkid=78453>)

L’outil Contrôleur de schéma permet d’identifier le rôle. Toutefois, la DLL Schmmgmt.dll doit être enregistrée pour que l’outil Schéma soit disponible comme un logiciel enfichable MMC.

Pour afficher le contrôleur de schéma actuel

1.  À l’invite de commandes, tapez **regsvr32 schmmgmt.dll**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>RegSvr32</strong> est enregistré lorsque la boîte de dialogue suivante s’affiche :<br />
    DllRegisterServer in schmmgmt.dll succeeded.</td>
    </tr>
    </tbody>
    </table>


2.  Pour ouvrir une nouvelle console de gestion, cliquez sur **Démarrer** et sur **Exécuter**, puis tapez **mmc**.

3.  Dans le menu de la console, cliquez sur **Ajouter/Supprimer un composant logiciel enfichable**.

4.  Cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Ajout d’un composant logiciel enfichable autonome**.

5.  Sélectionnez **Schéma Active Directory**, puis cliquez sur **Ajouter**.

6.  « Schéma Active Directory » s’affiche dans Ajouter/Supprimer un composant logiciel enfichable. Cliquez sur **Fermer**, puis sur **OK** pour revenir à la console.

7.  Sélectionnez **Schéma Active Directory** pour que les sections **Classes** et **Attributs** s’affichent à droite.

8.  Cliquez avec le bouton droit sur **Schéma Active Directory**, puis cliquez sur **Maître d’opérations**.

9.  Le contrôleur de schéma actuel s’affiche.

Après avoir identifié le contrôleur de schéma actuel, déterminez dans quel sous-réseau se trouve le contrôleur de schéma. Ensuite, appliquez l’une des méthodes suivantes pour installer Exchange :

  - Modifiez le sous-réseau sur le serveur Exchange pour le déplacer dans le site où se trouve le contrôleur de schéma. Ensuite, installez Exchange.

  - Forcez temporairement la modification d’une appartenance de site sur le serveur Exchange, puis installez Exchange. Après l’installation d’Exchange, renvoyez le serveur Exchange vers son site d’origine.

Pour forcer l’appartenance à un site

1.  Sur le serveur sur lequel vous voulez installer Exchange, démarrez l’Éditeur du Registre. Pour ce faire, cliquez sur **Démarrer**, **Exécuter**, tapez **regedit**, puis cliquez sur **OK**.

2.  Recherchez la sous-clé de Registre suivante :
    
    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Netlogon\\Parameters**

3.  Créez la valeur **String** suivante :
    
    Nom de la valeur : **SiteName**
    
    Type de valeur : **REG\_SZ**
    
    Données de la valeur : **\<site\_qui\_contient\_le\_contrôleur\_de\_schémar\>**

4.  Quittez l’Éditeur du Registre et redémarrez le service Netlogon. Cette action force le serveur Exchange à participer au site spécifié.

5.  Installez Exchange.

6.  Supprimez l’entrée de Registre ajoutée à l’étape 3.

7.  Redémarrez le service Netlogon. Cette action renvoie Exchange vers le site d’origine.

