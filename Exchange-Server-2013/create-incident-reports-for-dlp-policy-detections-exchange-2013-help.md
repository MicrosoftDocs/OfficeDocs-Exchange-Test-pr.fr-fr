---
title: 'Créer rapports de c.r. d’incident pr détection de strat. DLP: Exchange 2013'
TOCTitle: Créer des rapports de compte-rendu d’incident pour la détection de stratégies DLP
ms:assetid: 8e807f94-384c-43f5-be6f-06c5587175a0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150534(v=EXCHG.150)
ms:contentKeyID: 50477281
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer des rapports de compte-rendu d’incident pour la détection de stratégies DLP

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Dans Exchange Server 2013, vous pouvez établir une action visant à créer un rapport d'incident au sein d'un ensemble de règles de stratégie DLP. En outre, vous pouvez indiquer le destinataire du rapport et ce qu'il faut faire du message d'origine. Le rapport d'incident peut contenir les informations suivantes.

## Contenu d'un rapport de gestion des incidents

L'action **Générer un rapport d'incident** permet à des utilisateurs d'envoyer des rapports d'incident à une boîte aux lettres de gestion des incidents. Un rapport d'incident unique est généré pour chaque message uniquement si l'action **Générer un rapport d'incident** s'applique au sein d'une stratégie.

Voici la liste complète des noms de lignes dans le modèle de rapport d'incident. La colonne Format décrit comment reconnaître chaque champ du rapport. La colonne Champ facultatif indique les champs qui pourraient ne pas figurer dans le rapport pour chaque correspondance de règle. La colonne Spécifique au DLP indique les champs qui existent en tant que résultat de la fonctionnalité DLP.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Nom</strong> de <strong>ligne</strong></p></td>
<td><p><strong>Description</strong></p></td>
<td><p><strong>Format</strong></p></td>
<td><p><strong>Champ facultatif</strong></p></td>
<td><p><strong>Spécifique au DLP</strong></p></td>
</tr>
<tr class="even">
<td><p>Identificateur du message</p></td>
<td><p>ID du message d'origine envoyé</p></td>
<td><p>ID message : ID du message</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Expéditeur</p></td>
<td><p>Véritable expéditeur du message d'origine</p></td>
<td><p>Expéditeur : Adresse de messagerie de l'expéditeur</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Objet</p></td>
<td><p>Objet du message d'origine</p></td>
<td><p>Objet : chaîne d'objet d'entrée pour l'utilisateur final</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>À</p></td>
<td><p>Destinataire ou destinataires du message d'origine</p>
<p>Chaque ligne À ne doit contenir qu'un seul destinataire et ce jusqu'à 10 destinataires présents dans le rapport d'incident. S'il existe des destinataires supplémentaires, la ligne À suivante doit indiquer le nombre de destinataires restants.</p></td>
<td><p>À : Adresse de messagerie du destinataire</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>Adresse de messagerie Cc du message d'origine (la ligne est facultative)</p>
<p>Chaque ligne Cc ne doit contenir qu'une seule adresse de messagerie Cc et ce uniquement jusqu'à 10 adresses de messagerie Cc présentes dans le rapport d'incident. S'il existe des adresses Cc supplémentaires, la ligne Cc suivante doit indiquer le nombre d'adresses de messagerie Cc restantes.</p></td>
<td><p>Cc : Adresse de messagerie du destinataire Cc</p></td>
<td><p>Facultatif</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Cci</p></td>
<td><p>Adresse de messagerie Cci du message d'origine (la ligne est facultative)</p>
<p>Chaque ligne Cci ne doit contenir qu'une seule adresse de messagerie Cci et ce uniquement jusqu'à 10 adresses Cci présentes dans le rapport d'incident. S'il existe des adresses de messagerie Cci supplémentaires, la ligne Cci suivante doit indiquer le nombre d'adresses de messagerie Cci restantes.</p></td>
<td><p>Cci : Adresse de messagerie du destinataire Cci</p></td>
<td><p>Facultatif</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Gravité</p></td>
<td><p>Audit de la gravité de l'accès à la règle ; affiche la gravité la plus élevée en cas d'accès à plusieurs règles.</p></td>
<td><p>Gravité : Faible, Moyenne ou Élevée</p></td>
<td><p>Facultatif</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Remplacer</p></td>
<td><p>S'affiche si un remplacement a été signalé pour le message ; la justification du remplacement est fournie.</p></td>
<td><p>Remplacer : Oui, Justification : Chaîne de justification d'entrée IW</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Faux positif</p></td>
<td><p>S'affiche si un faux positif a été signalé pour le message.</p></td>
<td><p>Faux positif : Oui</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Classification des données</p></td>
<td><p>Classifications de données détectées dans le message d'origine (la ligne est facultative).</p>
<p>Chaque ligne de classification des données ne doit contenir qu'une classification détectée unique avec son nombre, sa confiance et son niveau de confiance minimale conseillée. Jusqu'à 5 classifications détectées peuvent apparaître dans rapport d'incident. Si la classification détectée est une affinité, la valeur de compte ne s'applique pas et ne doit pas s'afficher.</p></td>
<td><p>Classification des données : type d'informations sensibles, Nombre : instances des informations sensibles trouvées dans le message, Confiance : valeur de pourcentage, Confiance minimale conseillée : valeur de pourcentage</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Accès à la règle</p></td>
<td><p>Affiche toutes les règles qui accèdent au message d'origine.</p>
<p>Inclut le nom de la règle accédée, la stratégie DLP (facultatif) qui héberge la règle, la ou les actions qui ont été menées sur le message par application de la règle, la ou les classifications de données de la règle ayant provoqué l'accès à la règle et la définition de la règle.</p></td>
<td><p>Accès à la règle : nom de la règle, Stratégie DLP : Nom de la stratégie DLP, si applicable, Action : action unique, Classification des données : type d'informations sensibles, Définition : définition de règle, si applicable</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>Correspondance ID</p></td>
<td><p>Affiche la classification de données de correspondance, le contenu de correspondance exact et la preuve principale de correspondance de classification des données (la ligne est facultative).</p></td>
<td><p>Correspondance ID : type d'informations sensibles, Valeur : valeur réelle des données sensibles, Contexte : texte autour des données sensibles dans le message</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


## Pour plus d'informations

[Afficher les rapports de détection de stratégies DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

