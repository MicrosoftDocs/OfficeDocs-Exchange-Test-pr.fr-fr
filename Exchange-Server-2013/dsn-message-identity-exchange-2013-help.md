---
title: 'Identité du message DSN: Exchange 2013 Help'
TOCTitle: Identité du message DSN
ms:assetid: 70ffba22-e4fd-4cd3-98f5-8bfca2df89e4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998835(v=EXCHG.150)
ms:contentKeyID: 50478423
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Identité du message DSN

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Vous pouvez reconnaître un message de notification d’état de remise (DSN) personnalisé à partir de sa syntaxe. L’identité est le GUID du message DSN personnalisé ou une chaîne composée des valeurs suivantes :

  - **Paramètres régionaux**   Cette variable spécifie les paramètres régionaux de la langue dans laquelle le message DSN s’affiche. Pour obtenir une liste des codes locaux que vous pouvez utiliser avec la commande **New-SystemMessage**, consultez la rubrique [Langues prises en charge pour les messages système](supported-languages-for-system-messages-exchange-2013-help.md).

  - **Interne ou Externe**   Cette variable indique si le message DSN est envoyé uniquement à des expéditeurs qui font partie de l’organisation Microsoft Exchange Server 2013 interne ou également à des expéditeurs ne faisant pas partie de l’organisation Exchange. Vous pouvez utiliser l’option Interne si vous voulez inclure un contact électronique ou une résolution spécifique dans les messages DSN qui sont envoyés à des expéditeurs internes mais ne voulez pas exposer ces informations à des expéditeurs externes à votre organisation.

  - **Code DSN**   Cette variable spécifie le code DSN du message DSN personnalisé.

La syntaxe de l’identité de message DSN est `<Locale>\<Internal or External>\<DSN code>`.

Pour chaque code DSN, vous pouvez créer plusieurs messages DSN personnalisés ciblant des expéditeurs internes ou externes, ainsi que différents paramètres régionaux. Par exemple, le tableau suivant présente certaines configurations possibles pour le code DSN 5.1.2 et les identités de messages DSN correspondantes.

### Exemples de configuration et identités DSN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuration DSN</th>
<th>Identité DSN</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Affichage de messages DSN pour des expéditeurs internes avec les paramètres régionaux anglais (en)</p></td>
<td><p>En\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>Affichage de messages DSN pour des expéditeurs externes avec les paramètres régionaux anglais (en)</p></td>
<td><p>En\External\5.1.2</p></td>
</tr>
<tr class="odd">
<td><p>Affichage de messages DSN pour des expéditeurs internes avec les paramètres régionaux japonais (ja)</p></td>
<td><p>Ja\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>Affichage de messages DSN pour des expéditeurs externes avec les paramètres régionaux japonais (ja)</p></td>
<td><p>Ja\External\5.1.2</p></td>
</tr>
</tbody>
</table>

