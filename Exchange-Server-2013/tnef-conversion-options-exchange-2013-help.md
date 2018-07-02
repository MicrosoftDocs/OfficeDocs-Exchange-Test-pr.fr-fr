---
title: 'Options de conversion TNEF: Exchange 2013 Help'
TOCTitle: Options de conversion TNEF
ms:assetid: 989a62fc-4bc1-448f-90c8-7c7b56fe1084
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb310786(v=EXCHG.150)
ms:contentKeyID: 52057125
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Options de conversion TNEF

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Vous pouvez spécifier si le format TNEF (Transport Neutral Encapsulation Format) doit être conservé ou supprimé des messages sortants de l’organisation Exchange. Le format TNEF, également appelé format RTF d’Outlook ou format RTF d’Exchange, est un format propre à Microsoft permettant d’encapsuler les propriétés de message MAPI. Toutes les versions de MicrosoftOutlook sont parfaitement compatibles avec le format TNEF. Outlook Web App convertit le format TNEF en MAPI et affiche les messages formatés. Cependant, d’autres clients de messagerie non compatibles affichent généralement des messages au format TNEF en texte brut avec des pièces jointes Winmail.dat ou Win.dat.

**Contenu de cette rubrique**

Options de conversion TNEF pour les domaines distants

Options de conversion TNEF pour des contacts et des utilisateurs de messagerie

Options de conversion TNEF dans Outlook

Ordre de priorité des options de conversion TNEF

## Options de conversion TNEF pour les domaines distants

Lorsque vous configurez les options de conversion TNEF pour un domaine distant, ces options s'appliquent à tous les messages envoyés vers ce domaine.

  - Pour Exchange Online Dedicated, vous pouvez utiliser le centre d’administration Exchange (CAE) afin de définir les options de conversion TNEF pour un domaine distant : **Flux de messagerie** \>**Domaines distants** \>**Modifier** (![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier")) \>**Utiliser le format RTF d’Exchange**.

  - Dans Exchange Online et Exchange 2013, le paramètre *TnefEnabled* de la cmdlet **Set-RemoteDomain** permet de configurer les options de conversion TNEF pour un domaine distant.

Pour les domaines distants de votre organisation, vous disposez des options de configuration suivantes pour la conversion TNEF :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Dans le CAE</th>
<th>Dans l’environnement de ligne de commande</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utiliser le format TNEF pour tous les messages envoyés vers le domaine distant.</p></td>
<td><p><strong>Toujours</strong></p></td>
<td><p><code>$true</code></p></td>
</tr>
<tr class="even">
<td><p>Ne jamais utiliser le format TNEF pour les messages envoyés vers le domaine distant.</p></td>
<td><p><strong>Jamais</strong></p></td>
<td><p><code>$false</code></p></td>
</tr>
<tr class="odd">
<td><p>Les messages TNEF ne sont pas spécifiquement autorisés ou bloqués pour les destinataires du domaine distant. L'envoi des messages TNEF aux destinataires du domaine distant dépend du paramètre défini pour le contact ou l'utilisateur de messagerie, ou du paramètre défini par l'expéditeur dans Outlook. Il s’agit de la valeur par défaut.</p></td>
<td><p><strong>Suivre les paramètres utilisateur</strong></p></td>
<td><p><code>$null</code> (vide)</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les domaines distants, voir [Domaines distants](remote-domains-exchange-2013-help.md) ou [Domaines distants dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj966211\(v=exchg.150\)).

Retour au début

## Options de conversion TNEF pour des contacts et des utilisateurs de messagerie

Lorsque vous configurez les options de conversion TNEF pour un contact ou utilisateur de messagerie, ces options s'appliquent à tous les messages envoyés à ce destinataire. Le paramètre *UseMapiRichTextFormat* des cmdlets **Set-MailUser** et **Set-MailContact** permet de configurer les options de conversion TNEF pour les utilisateurs et les contacts de messagerie.

Pour les utilisateurs et contacts de messagerie de votre organisation, vous disposez des options de configuration suivantes pour la conversion TNEF :

  - **Toujours**   Le format TNEF est utilisé pour tous les messages envoyés au destinataire. La valeur correspondante du paramètre *UseMapiRichTextFormat* est `Always`.

  - **Jamais**   Le format TNEF n'est jamais utilisé pour les messages envoyés au destinataire. La valeur correspondante du paramètre *UseMapiRichTextFormat* est `Never`.

  - **Paramètres par défaut**   Les messages TNEF ne sont pas spécifiquement autorisés ou bloqués pour l'utilisateur ou le contact de messagerie. L'envoi des messages TNEF au destinataire dépend du paramètre défini pour le domaine distant correspondant ou du paramètre défini par l'expéditeur dans Outlook. La valeur correspondante du paramètre *UseMapiRichTextFormat* est `UseDefaultSettings`. Il s'agit du paramètre par défaut.

Retour au début

## Options de conversion TNEF dans Outlook

Les expéditeurs peuvent contrôler les options de conversion TNEF par défaut pour les messages TNEF envoyés à tous les destinataires en dehors de l'organisation Exchange. Ces options sont intitulées *Format des messages Internet*. Les options s'appliquent uniquement aux destinataires distants et non aux destinataires dans l'organisation Exchange.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les options suivantes déterminent la façon dont les messages contenant le format RTF d'Outlook sont traités lorsqu'ils sont envoyés à des destinataires externes. Si le format de message utilisé est HTML ou du texte brut, ces paramètres ne s’appliquent pas.</td>
</tr>
</tbody>
</table>


Vous disposez des options de conversion TNEF suivantes dans Outlook :

  - **Convertir au format HTML**  Il s'agit de l'option par défaut. Tous les messages TNEF envoyés à des destinataires distants sont convertis au format HTML. Toute mise en forme dans le message doit être semblable au message d'origine. Les messages HTML MIME sont pris en charge par de nombreux, mais pas tous, clients de messagerie.

  - **Convertir au format texte brut**   Tous les messages TNEF envoyés à des destinataires distants sont convertis en texte brut. Toute mise en forme dans le message est perdue.

  - **Envoyer à l'aide du format RTF d'Outlook**   Tous les messages TNEF envoyés à des destinataires distants demeurent des messages TNEF.

Vous pouvez configurer ces options aux emplacement suivants d'Outlook :

  - **Outlook 2010 ou Outlook 2013** **Fichier** \> **Options** \> **Messagerie** \> **Format de message**.

  - **Outlook 2007** **Outils** \> **Options** \> **Format de messagerie** \> **Format Internet**.

Les expéditeurs peuvent également contrôler les options de conversion TNEF par défaut pour les messages TNEF envoyés à des destinataires spécifiques en dehors de l'organisation Exchange. Ces options sont intitulées *Format des messages des destinataires Internet*. Les options s'appliquent uniquement aux destinataires distants dans votre dossier Contacts, et non aux destinataires dans l'organisation Exchange. Vous disposez des options de conversion TNEF suivantes pour les destinataires distants dans votre dossier Contacts :

  - **Laisser Outlook décider du meilleur format d'envoi**   Il s'agit du paramètre par défaut. Ce paramètre force Outlook à utiliser l'option de conversion TNEF spécifiée par le format Internet par défaut. Les valeurs possibles sont **Convertir au format HTML**, **Convertir au format texte brut** ou **Envoyer à l'aide du format RTF d'Outlook**. Le message TNEF peut, par conséquent, rester au format TNEF, être converti au format HTML ou au format texte brut. Pour vous assurer que le message TNEF reste au format TNEF pour ce destinataire, vous devez remplacer le paramètre **Laisser Outlook décider du meilleur format d'envoi** par **Envoyer à l'aide du format RTF d'Outlook**.

  - **Envoyer en texte brut uniquement**   Tous les messages TNEF envoyés au destinataire sont convertis en texte brut. Toute mise en forme dans le message est perdue.

  - **Envoyer à l'aide du format RTF d'Outlook**   Tous les messages TNEF envoyés à des destinataires distants demeurent des messages TNEF.

Vous pouvez configurer ces options pour un contact aux emplacement suivants d'Outlook :

  - **Outlook 2010 ou Outlook 2013**   Ouvrez la carte de visite, double cliquez sur l'adresse de messagerie, cliquez sur l'icône **Afficher plus d'options pour interagir avec cette personne**, puis sélectionnez **Propriétés Outlook**. Dans la boîte de dialogue **Propriétés de la messagerie**, sélectionnez **Format Internet**.

  - **Outlook 2007**   Ouvrez la carte de visite, double cliquez sur le champ **Messagerie** et sélectionnez **Format Internet**.

Retour au début

## Ordre de priorité des options de conversion TNEF

Exchange utilise l'ordre de priorité décrit dans la liste suivante pour déterminer les options de conversion TNEF des messages sortants envoyés à des destinataires en dehors de l'organisation Exchange :

1.  paramètres de domaine distant.

2.  paramètres d'utilisateur ou de contact de messagerie ;

3.  Paramètres Outlook

La liste indique l’ordre de priorité de la plus basse à la plus élevée. Le paramètre TNEF du domaine distant remplace les paramètres TNEF de l’utilisateur de messagerie, du contact de messagerie ou d’Outlook. Par exemple, supposons que vous envoyiez un message en texte enrichi dans Outlook, mais que le destinataire se trouve dans un domaine où le paramètre de domaine distant n’autorise pas les messages au format TNEF. Le message reçu par le destinataire sera en texte brut ou au format HTML, mais pas au format TNEF.

Par ailleurs, Exchange n’envoie jamais de messages STNEF (Summary Transport Neutral Encoding Format) à des destinataires externes. Seuls des messages TNEF peuvent être envoyés à des destinataires en dehors de l'organisation Exchange.

Retour au début

