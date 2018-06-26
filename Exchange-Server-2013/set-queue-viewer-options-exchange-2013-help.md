---
title: 'Définir les options de l’Afficheur des files d’attente: Exchange 2013 Help'
TOCTitle: Définir les options de l’Afficheur des files d’attente
ms:assetid: 03a9134c-0714-4c13-b286-92bccc7ec05e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa995934(v=EXCHG.150)
ms:contentKeyID: 50477437
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Définir les options de l’Afficheur des files d’attente

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-03_

Vous pouvez définir les options de l’Afficheur des files d’attente pour ajuster le nombre d’éléments affichés dans la page et la fréquence d’actualisation automatique. La fréquence d’actualisation automatique détermine la fréquence de mise à jour des résultats de l’Afficheur des files d’attente.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Files d’attente » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Utiliser la Boîte à outils Exchange pour définir les options de l’Afficheur des files d’attente

1.  Cliquez sur **Démarrer** \> **Tous les programmes** \> **Microsoft Exchange Server 2013** \> **Boîte à outils Exchange**.

2.  Sous **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d’attente**.

3.  Dans l’Afficheur des files d’attente, cliquez sur **Afficher** \> **Options** pour configurer les paramètres suivants dans la boîte de dialogue **Options de l’Afficheur des files d’attente** :
    
    1.  Dans le champ **Intervalle d’actualisation (secondes)**, entrez la fréquence à laquelle l’Afficheur des files d’attente doit actualiser l’affichage.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>La fréquence d’actualisation automatique par défaut est de 30 secondes et il n’est pas possible de la raccourcir. Si vous désactivez la fréquence d’actualisation automatique en désactivant la case à cocher <strong>Actualiser automatiquement l’écran</strong> dans la page <strong>Options de l’Afficheur des files d’attente</strong>, vous devez mettre à jour manuellement les résultats présentés dans l’Afficheur des files d’attente en cliquant sur <strong>Actualiser</strong>.</td>
        </tr>
        </tbody>
        </table>
    
    2.  Dans le champ **Nombre d’éléments à afficher sur chaque page**, entrez le nombre maximal d’éléments à afficher dans l’Afficheur des files d’attente. Ce nombre doit être compris entre 1 et 10 000. Si le nombre d’éléments est supérieur à la limite, ceux-ci s’affichent en groupes de nombre d’éléments maximum. Par exemple, la figure suivante montre une file d’attente comportant 14 messages alors que l’Afficheur des files d’attente est configuré pour afficher 10 éléments par page. Le nombre d’objets sur la page apparaît en haut à droite. Au bas de la page, le nombre total d’éléments présents dans la file d’attente est indiqué. Vous pouvez alors utiliser les boutons de navigation pour voir les éléments supplémentaires de la file d’attente.

4.  Lorsque vous avez terminé, cliquez sur **OK**.
    
    **Afficheur des files d’attente**
    
    ![Afficheur des files d’attente avec un nombre d’éléments supérieur à la limite maximale](images/Aa995934.e82196e6-002a-4e9e-823d-b244b0bd25e2(EXCHG.150).gif "Afficheur des files d’attente avec un nombre d’éléments supérieur à la limite maximale")  

## Comment savoir si cela a fonctionné ?

Vous saurez que cette procédure fonctionne si l’Afficheur des files d’attente utilise les paramètres définissant l’intervalle d’actualisation et le nombre d’éléments par page.

