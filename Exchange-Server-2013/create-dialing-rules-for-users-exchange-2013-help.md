---
title: 'Créer des règles de numérotation pour les utilisateurs: Exchange 2013 Help'
TOCTitle: Créer des règles de numérotation pour les utilisateurs
ms:assetid: c11e3d62-3eb1-4d7e-8741-9bede593e2df
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ898502(v=EXCHG.150)
ms:contentKeyID: 51407233
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Créer des règles de numérotation pour les utilisateurs

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2015-03-09_

Les groupes de règles de numérotation comprennent des entrées de règles de numérotation. Les règles de numérotation sont utilisées pour modifier un numéro de téléphone avant son envoi à un système téléphonique local (PBX) ou PBX IP pour les appels sortants. Les règles de numérotation ont deux fonctions :

  - Elles spécifient les nombres qui peuvent être composés pour les appels sortants. Lorsque vous créez une règle de numérotation, vous spécifiez les formats de numéro qui peuvent être composés. Tout numéro qui ne correspond pas à un des formats spécifiés est rejeté. Si vous ne définissez pas de règles de numérotation, les appelants peuvent effectuer des appels dans votre organisation, mais ne peuvent pas effectuer d'appel sortant.

  - Ils transforment les numéros composés avant de les transférer à votre système téléphonique local. Les règles de numérotation peuvent supprimer ou ajouter des numéros au numéro composé. Par exemple, vous pouvez utiliser les règles de numérotation pour ajouter le code d'accès à une ligne extérieure pour votre système téléphonique ou ajouter ou supprimer le code de pays/région pour les numéros longue distance ou locaux.

Pour spécifier les types d'appels sortants que vous souhaitez autoriser pour un plan de numérotation de messagerie unifiée, vous créez un groupe de règles de numérotation contenant des règles de numérotation que vous utilisez pour autoriser les appels sortants pour les utilisateurs d'Outlook Voice Access et les appelants qui composent le numéro d'un standard automatique de messagerie unifiée. Vous créez des groupes de règles de numérotation séparés pour les appels nationaux/régionaux et pour les appels internationaux.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous intégrez la messagerie unifiée à Microsoft Lync Server, nous vous recommandons de créer au moins un groupe de règles de numérotation et d'autoriser ce groupe sur les plans de numérotation URI SIP, les stratégies de boîte aux lettres de messagerie unifiée et les standards automatiques de messagerie unifiée pour permettre à tous les appels sortants d'être transférés vers des serveurs Lync Server.</td>
</tr>
</tbody>
</table>


Pour d'autres tâches de gestion concernant l'automate d'appels, consultez la rubrique [Ce qui permet aux utilisateurs d'effectuer les procédures d'appels](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## Exemples de règles de numérotation communément utilisées


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Modèle de numéro</strong></p></td>
<td><p><strong>Numéro composé</strong></p></td>
<td><p><strong>Quand utiliser cette règle de numérotation ?</strong></p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>*</p></td>
<td><p>Autoriser tous les appels sortants.</p></td>
</tr>
<tr class="odd">
<td><p>1425xxxxxxx</p></td>
<td><p>91425xxxxxxx</p></td>
<td><p>Empêcher les utilisateurs d'obtenir un poste interne ou une erreur lorsqu'ils oublient de composer le code d'accès à une ligne extérieure.</p></td>
</tr>
<tr class="even">
<td><p>1xxxxxxxxxx</p></td>
<td><p>1xxxxxxxxxx</p></td>
<td><p>Autoriser tous les numéros qui commencent par 1.</p></td>
</tr>
<tr class="odd">
<td><p>xxxxxxx</p></td>
<td><p>1425xxxxxxx</p></td>
<td><p>Ajouter 1 et l'indicatif local 425 aux numéros à 7 chiffres.</p></td>
</tr>
</tbody>
</table>


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins de 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Si vous appliquez des groupes de règles de numérotation à des stratégies de boîte aux lettres de messagerie unifiée, vous devez confirmer qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Si vous appliquez des groupes de règles de numérotation à des standards automatiques de messagerie unifiée, vous devez confirmer qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

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


## Utiliser le Centre d'administration Exchange (CAE) pour créer une règle de numérotation

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

3.  Dans la page **Plan de numérotation de messagerie unifiée** \> **Règles de numérotation**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous **Règles de numérotation nationale/régionale** ou **Règles de numérotation à l'international**.

4.  Dans la page **Nouvelle règle de numérotation**, renseignez les informations suivantes.
    
      - **Nom du groupe de règles de numérotation**   Entrez le nom du groupe de règles de numérotation dont vous souhaitez que cette règle fasse partie. Pour le combiner avec d'autres règles, utilisez le même nom de groupe. Pour créer un groupe de règles de numérotation, entrez un nouveau nom unique.
    
      - **Modèle de numéro à transformer (masque de numéro)**   Entrez le modèle de numéro à transformer avant la numérotation, par exemple, 91425xxxxxxx. Si un utilisateur entre un numéro correspondant, la messagerie unifiée le transforme en numéro composé avant d'effectuer l'appel. Entrez uniquement des chiffres et le caractère générique (x). Le modèle de numéro est également appelé *masque de numéro*.
    
      - **Numéro composé**   Entrez le numéro à composer. Utilisez seulement des chiffres et le caractère générique (x), comme dans le modèle de numéro 9xxxxxxx. Les caractères génériques (x) sont remplacés par des chiffres à partir du numéro d'origine composé par l'utilisateur. Assurez-vous que le nombre de caractères génériques dans le numéro composé est le même que le nombre de caractères génériques dans le modèle de numéro.
    
      - **Commentaires**   Entrez un commentaire ou description pour cette règle de numérotation. Vous pouvez utiliser les commentaires pour décrire ce que la règle fait, par exemple, « Ajouter un 9 aux appels sortants ».

5.  Cliquez sur **OK** pour enregistrer la règle de numérotation. Vous pouvez continuer à entrer des règles, à l'aide du même nom de groupe de règles de numérotation pour les règles que vous souhaitez autoriser ensemble.

