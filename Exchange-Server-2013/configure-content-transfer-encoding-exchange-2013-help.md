---
title: 'Configurer le codage de transfert de contenu: Exchange 2013 Help'
TOCTitle: Configurer le codage de transfert de contenu
ms:assetid: c4922362-18d4-42f7-9189-9076720eb1d8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg144562(v=EXCHG.150)
ms:contentKeyID: 50479166
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer le codage de transfert de contenu

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Le *codage de transfert de contenu* définit des méthodes de codage permettant de transformer les données de messages électroniques binaires au format de texte brut US-ASCII. Cette transformation permet au message de transiter sur des serveurs de messagerie SMTP plus anciens qui ne prennent en charge que les messages en texte US-ASCII. Le codage de transfert de contenu est défini dans la norme RFC 2045. La méthode de codage de transfert est stockée dans le champ d’en-tête **Content-Transfer-Encoding** du message. Dans Microsoft Exchange Server 2013, les méthodes de codage de transfert suivantes sont disponibles :

  - **7-bit**   Cette valeur indique que les données du corps du message sont déjà au format de texte brut US ASCII et que le message n’a connu aucun codage.

  - **Quoted-printable (QP)**   Cette méthode de codage utilise des caractères US-ASCII imprimables pour coder les données du corps du message. Si le texte du message d’origine est essentiellement du texte US-ASCII, le codage QP fournit des résultats relativement lisibles et compacts. Par défaut, Exchange 2013 utilise QP pour le codage des données des messages binaires.

  - **Base64**   Cette méthode de codage est principalement basée sur le standard Privacy-Enhanced Mail (PEM) défini dans la norme RFC 1421. Le codage Base64 utilise la méthode de codage alphabétique de 64 caractères alphabet et les caractères de remplissage de sortie définis par PEM pour coder les données du corps du message. Le codage Base64 crée un accroissement prévisible de la taille du message et convient parfaitement pour des données binaires et du texte non-US-ASCII.

Vous configurez la méthode de codage de transfert à l’aide du paramètre *ByteEncoderTypeFor7BitCharsets* sur les cmdlets **Set-OrganizationConfig** et **Set-RemoteDomain**. Les paramètres de codage de transfert de contenu que vous configurez avec **Set-OrganizationConfig** s’appliquent à tous les messages de l’organisation Exchange. Les paramètres de codage de transfert de contenu que vous configurez avec **Set-RemoteDomain** s’appliquent uniquement aux messages envoyés à des destinataires externes dans le domaine distant.

Le tableau suivant répertorie les valeurs que vous pouvez utiliser pour définir la méthode de codage de transfert.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre dans <strong>Set-OrganizationConfig</strong></th>
<th>Paramètre dans <strong>Set-RemoteDomain</strong></th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p><code>Use7Bit</code></p></td>
<td><p>Toujours utiliser le codage 7 bits pour le code HTML et le texte brut. Cette valeur est la valeur par défaut.</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p><code>UseQP</code></p></td>
<td><p>Toujours utiliser le codage QP pour le code HTML et le texte brut.</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p><code>UseBase64</code></p></td>
<td><p>Toujours utiliser le codage Base64 pour le code HTML et le texte brut.</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p><code>UseQPHtmlDetectTextPlain</code></p></td>
<td><p>Utiliser le codage QP pour le code HTML et le texte brut à moins que le retour automatique à la ligne soit activé en texte brut. Si le retour automatique à la ligne est activé, utiliser le codage 7 bits pour le texte brut.</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p><code>UseBase64HtmlDetectTextPlain</code></p></td>
<td><p>Utiliser le codage Base64 pour le code HTML et le texte brut à moins que le retour automatique à la ligne soit activé en texte brut. Si le retour automatique à la ligne est activé en texte brut, utiliser le codage Base64 pour le code HTML et utiliser le codage 7 bits pour le texte brut.</p></td>
</tr>
<tr class="even">
<td><p>13</p></td>
<td><p><code>UseQPHtml7BitTextPlain</code></p></td>
<td><p>Toujours utiliser le codage QP pour le code HTML. Toujours utiliser le codage 7 bits pour le texte brut.</p></td>
</tr>
<tr class="odd">
<td><p>14</p></td>
<td><p><code>UseBase64Html7BitTextPlain</code></p></td>
<td><p>Toujours utiliser le codage Base64 pour le code HTML. Toujours utiliser le codage 7 bits pour le texte brut.</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur le champ d’en-tête **Content-Transfer-Encoding**, voir la section « Présentation de la structure des messages électroniques » dans [conversion de contenu.](content-conversion-exchange-2013-help.md).

Pour plus d’informations sur les domaines distants, consultez la rubrique [Domaines distants](remote-domains-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Règles de transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la méthode de codage de transfert de contenu pour l’organisation

Pour configurer la méthode de codage de transfert de contenu pour l’organisation, exécutez la commande suivante :

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets <Integer>

Par exemple, pour définir la méthode de codage de transfert à Base64, exécutez la commande suivante :

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets 2

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la méthode de codage de transfert de contenu pour un domaine distant

Pour configurer la méthode de codage de transfert de contenu pour l’ensemble des destinataires dans un domaine distant, exécutez la commande suivante :

    Set-RemoteDomain -ByteEncoderTypeFor7BitCharsets <Value>

Par exemple, pour définir la méthode de codage de transfert à Base64, exécutez la commande suivante :

    Set- RemoteDomain -ByteEncoderTypeFor7BitCharsets UseBase64

## Comment savoir si cela a fonctionné ?

Pour vérifier que la méthode de transfert de contenu a été bien configurée, procédez comme suit :

1.  Envoyez un message de test contenant un mélange de texte US-ASCII et de données binaires ou du texte non US-ASCII à un compte de test interne ou externe. Utilisez un compte interne pour tester les paramètres de l’organisation et un compte externe du domaine distant pour tester les paramètres des domaines distants.

2.  Dans un client de messagerie, affichez le champ d’en-tête **Content-Transfer-Encoding** dans le message et vérifiez si la méthode de codage de transfert de contenu utilisée sur le message correspond à la méthode que vous avez configurée.

