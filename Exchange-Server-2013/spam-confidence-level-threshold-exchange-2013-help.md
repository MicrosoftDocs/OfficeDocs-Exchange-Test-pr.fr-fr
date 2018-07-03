---
title: 'Niveau de confiance du courrier indésirable: Exchange 2013 Help'
TOCTitle: Niveau de confiance du courrier indésirable
ms:assetid: 0009b4af-be6d-41d2-98bc-b5487272c74a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa995744(v=EXCHG.150)
ms:contentKeyID: 50477401
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Niveau de confiance du courrier indésirable

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-11-17_

> [!NOTE]
> Le 1er novembre 2016, Microsoft a cessé de produire des mises à jour des définitions de courrier indésirable pour les filtres SmartScreen dans Exchange et Outlook. Les définitions de courrier indésirable SmartScreen existantes restent en place, mais leur efficacité se dégradera probablement au cours du temps. Pour plus d’informations, voir l’article relatif à l’<a href="https://go.microsoft.com/fwlink/p/?linkid=835894">arrêt de la prise en charge de SmartScreen dans Outlook et Exchange</a>.


Dans Microsoft Exchange Server 2013, vous pouvez définir des actions spécifiques en fonction des seuils de probabilité de courrier indésirable. Par exemple, vous pouvez définir des seuils différents pour le rejet, la suppression ou la mise en quarantaine de messages sur un serveur Exchange exécutant l’agent de filtrage du contenu.

La combinaison de cette configuration du seuil de probabilité de courrier indésirable dans l’agent de filtrage du contenu et de la configuration du dossier Courrier indésirable SCL sur la boîte aux lettres de l’utilisateur vous aide à implémenter une stratégie de gestion du courrier indésirable plus élaborée et précise. Cette fonctionnalité d’ajustement du seuil SCL plus précise et détaillée dans Exchange 2013 peut vous aider à réduire le coût global du déploiement et de la gestion d’une solution anti-spam au sein de votre organisation Exchange.

L’agent de filtrage du contenu affecte un contrôle d’accès SCL aux messages tardivement dans le cycle de blocage du courrier indésirable, après que d’autres agents anti-spam ont traité les messages entrants. De nombreux autres agents de blocage du courrier indésirable qui traitent les messages entrants avant leur traitement par l’agent de filtrage du contenu sont déterministes dans la manière dont ils agissent sur un message. Par exemple, sur un serveur de transport Edge, l’agent de filtrage des connexions rejette tout message envoyé depuis une adresse IP figurant sur une liste rouge en temps réel. L’agent de filtrage des expéditeurs et l’agent de filtrage des destinataires traitent également les messages d’une façon déterministe.

Dans Exchange 2013, ces agents déterministes de blocage du courrier indésirable commencent par traiter les messages, réduisant ainsi sensiblement le nombre de messages que doit traiter l’agent de filtrage du contenu. Pour plus d’informations sur l’ordre dans lequel les agents de blocage du courrier indésirable traitent les messages, consultez la rubrique [Protection contre le courrier indésirable](anti-spam-protection-exchange-2013-help.md).

Comme le filtrage de contenu n’est pas un processus exact et déterministe, la capacité d’ajuster l’action que l’agent de filtrage du contenu exécute en fonction de différentes valeurs SCL est importante. En ajustant soigneusement la configuration du seuil de probabilité de courrier indésirable, vous pouvez minimiser les valeurs suivantes :

  - la taille de l’espace de mise en quarantaine du courrier indésirable

  - le nombre de messages électroniques légitimes mis en quarantaine par erreur

  - le nombre de messages électroniques légitimes qui atteignent le dossier Courrier indésirable de l’utilisateur Microsoft Outlook

  - le nombre de messages électroniques indésirables choquant qui atteignent le dossier Courrier indésirable ou la boîte de réception de l’utilisateur Outlook

  - le nombre de messages électroniques indésirables qui atteignent la boîte de réception de l’utilisateur Outlook

## Actions de seuil SCL

En ajustant les actions de seuil SCL, vous pouvez élever le niveau de filtrage de contenu appliqué à des messages plus susceptibles que d’autres de constituer du courrier indésirable. Pour comprendre cette nouvelle fonctionnalité, il est utile de comprendre les différentes actions de seuil SCL et la manière dont elles sont implémentées:

  - **Seuil de suppression SCL**   Lorsque la valeur SCL d’un message spécifique est supérieure ou égale au seuil de suppression SCL, l’Agent de filtrage du contenu supprime le message. Aucune communication de niveau protocole n’indique au système émetteur ou à l’expéditeur que le message a été supprimé. Si la valeur SCL d’un message est inférieure à celle du seuil de suppression SCL, l’agent de filtrage du contenu ne supprime pas le message. Au lieu de cela, l’agent de filtrage du contenu compare la valeur SCL au seuil de rejet SCL.

  - **Seuil de rejet SCL**   Lorsque la valeur SCL d’un message spécifique est supérieure ou égale au seuil de rejet SCL, l’Agent de filtrage du contenu supprime le message et envoie une réponse de rejet au système émetteur. Vous pouvez personnaliser la réponse de rejet. Dans certains cas, un rapport de non-remise est envoyé à l’expéditeur d’origine du message. Si la valeur SCL d’un message est inférieure à celles des seuils de suppression et de rejet SCL, l’agent de filtrage du contenu ne supprime ni ne rejette le message. Au lieu de cela, l’agent de filtrage du contenu compare la valeur SCL au seuil de mise en quarantaine SCL.

  - **Seuil de mise en quarantaine SCL**   Lorsque la valeur SCL d’un message spécifique est supérieure ou égale au seuil de mise en quarantaine SCL, l’Agent de filtrage du contenu envoie le message à une boîte aux lettres de mise en quarantaine. Les administrateurs de messagerie doivent examiner périodiquement le contenu de la boîte aux lettres de mise en quarantaine. Si la valeur SCL d’un message est inférieure à celles des seuils de suppression, de rejet et de mise en quarantaine SCL, l’agent de filtrage du contenu ne supprime, ne rejette ni ne met en quarantaine le message. En revanche, il envoie le message au serveur de boîtes aux lettres approprié, où la valeur de seuil SCL du dossier Courrier indésirable par destinataire est évaluée.

  - **Seuil SCL du dossier Courrier indésirable**   Si la valeur SCL d’un message spécifique est supérieure au seuil SCL du dossier Courrier indésirable, le message est placé dans le dossier Courrier indésirable de l’utilisateur. Si la valeur SCL d’un message est inférieure à celles des seuils de suppression, de rejet, de mise en quarantaine et de dossier Courrier indésirable SCL, le message est placé dans la boîte de réception de l’utilisateur.

L'agent de filtrage du contenu et le dossier de courrier indésirable traitent la valeur de seuil de probabilité de courrier indésirable de manière différente. L’agent de filtrage du contenu agit sur la valeur de seuil de probabilité de courrier indésirable que vous configurez. Ce dossier de courrier indésirable agit sur la valeur du seuil de probabilité de courrier indésirable que vous configurez, plus 1. Par exemple, si vous configurez l'action de suppression sur un seuil de probabilité de courrier indésirable de 8 dans l'agent de filtrage du contenu, tous les messages dont la valeur de seuil de probabilité de courrier indésirable est 8 ou supérieure sont supprimés. Cependant, si vous configurez le dossier de courrier indésirable avec un seuil de probabilité de courrier indésirable de 4, tous les messages avec ce seuil de 5 ou supérieur sont déplacés vers le dossier de courrier indésirable.

Par exemple, si vous définissez le seuil de suppression SCL sur 8, le seuil de rejet SCL sur 7, le seuil de mise en quarantaine SCL sur 6 et le seuil SCL du dossier Courrier indésirable sur 4, tous les messages électroniques dont la valeur SCL est inférieure ou égale à 5 sont placés dans la boîte aux lettres de l’utilisateur. Les messages dont la valeur SCL est égale à 5 sont placés dans le dossier Courrier indésirable de l’utilisateur. Les messages dont la valeur SCL est inférieure ou égale à 4 sont placés dans la boîte de réception de l’utilisateur.

Vous pouvez configurer les paramètres SCL de suppression, de rejet, de mise en quarantaine et du dossier Courrier indésirable dans les emplacements suivants :

  - **Dans la configuration de l’agent de filtrage du contenu (configuration SCL de serveur par transport)**   Vous pouvez utiliser la cmdlet **Set-ContentFilterConfig** pour activer ou désactiver et définir les seuils de suppression, de rejet et de mise en quarantaine SCL sur le serveur Exchange où s’exécute l’agent de filtrage du contenu. Avec le temps, à mesure que vous analysez la fonctionnalité de blocage du courrier indésirable et les mesures fournies par les fonctions de journalisation et de rapport concernant le courrier indésirable, vous pouvez apporter à ces configurations de seuil SCL des ajustements supplémentaires en fonction des besoins.
    
    Les paramètres SCL disponibles dans la cmdlet **Set-ContentFilterConfig** sont décrits dans le tableau suivant.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Paramètre</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLDeleteEnabled</em></p></td>
    <td><p>Ce paramètre active ou désactive la suppression d’un message sans notification d’échec de remise lorsque la valeur SCL du message est supérieure ou égale à celle spécifiée par le paramètre <em>SCLDeleteThreshold</em>. Ce paramètre peut avoir la valeur <code>$true</code> ou <code>$false</code>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLDeleteThreshold</em></p></td>
    <td><p>L’entrée valide pour ce paramètre est un entier compris entre 0 et 9 inclus. La valeur de ce paramètre doit être supérieure à celles des autres paramètres de seuil SCL. Ce paramètre n’est significatif que lorsque la valeur du paramètre <em>SCLDeleteEnabled</em> est <code>$true</code>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLRejectEnabled</em></p></td>
    <td><p>Ce paramètre active ou désactive le rejet d’un message avec notification d’échec de remise lorsque la valeur SCL du message est supérieure ou égale à celle spécifiée par le paramètre <em>SCLRejectThreshold</em>. Ce paramètre peut avoir la valeur <code>$true</code> ou <code>$false</code>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLRejectThreshold</em></p></td>
    <td><p>L’entrée valide pour ce paramètre est un entier compris entre 0 et 9 inclus. La valeur de ce paramètre doit être inférieure à celle du paramètre <em>SCLDeleteThreshold</em>, mais supérieure à celles des autres paramètres de seuil SCL. Ce paramètre n’est significatif que lorsque la valeur du paramètre <em>SCLRejectEnabled</em> est <code>$true</code>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLQuarantineEnabled</em></p></td>
    <td><p>Ce paramètre active ou désactive l’envoi d’un message à la boîte aux lettres de mise en quarantaine du courrier indésirable lorsque la valeur SCL du message est supérieure ou égale à celle spécifiée par le paramètre <em>SCLQuarantineThreshold</em>. Ce paramètre peut avoir la valeur <code>$true</code> ou <code>$false</code>.</p>
    <p>Pour plus d’informations sur la boîte aux lettres de mise en quarantaine du courrier indésirable, consultez la rubrique <a href="spam-quarantine-exchange-2013-help.md">Mise en quarantaine du courrier indésirable</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLQuarantineThreshold</em></p></td>
    <td><p>L’entrée valide pour ce paramètre est un entier compris entre 0 et 9 inclus. La valeur de ce paramètre doit être inférieure à celle du paramètre <em>SCLRejectThreshold</em>, mais supérieure à celle du paramètre <em>SCLJunkThreshold</em> dans les cmdlets <strong>Set-OrganizationConfig</strong> ou <strong>Set-Mailbox</strong>. Ce paramètre n’est significatif que lorsque la valeur du paramètre <em>SCLQuarantineThreshold</em> est <code>$true</code>.</p></td>
    </tr>
    </tbody>
    </table>


  - **Dans les paramètres de configuration de l’organisation (configuration SCL au niveau de l’organisation)**   Vous pouvez utiliser la cmdlet **Set-OrganizationConfig** si vous souhaitez définir le seuil SCL du dossier Courrier indésirable pour toutes les boîtes aux lettres de l’organisation.
    
    Le paramètre SCL disponible dans la cmdlet **Set-OrganizationConfig** est décrit dans le tableau suivant. Pour voir un exemple d’utilisation de SCLJunkThreshold, consultez la rubrique [Configurer les paramètres de blocage du courrier indésirable sur les boîtes aux lettres](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Paramètre</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkThreshold</em></p></td>
    <td><p>Ce paramètre spécifie la valeur SCL qu’un message doit dépasser pour être déplacé vers le dossier Courrier indésirable de la boîte aux lettres du destinataire. L’entrée valide pour ce paramètre est un entier compris entre 0 et 9 inclus. La valeur de ce paramètre doit être inférieure à celles des autres paramètres de seuil SCL. Par exemple, si vous spécifiez la valeur 4, les messages dont la valeur SCL est supérieure ou égale à 5 sont placés dans le dossier Courrier indésirable de l’utilisateur.</p></td>
    </tr>
    </tbody>
    </table>


  - **Dans les boîtes aux lettres utilisateur (configuration SCL par destinataire)**   Vous pouvez utiliser la cmdlet **Set-Mailbox** pour activer ou désactiver et définir les seuils SCL de suppression, de rejet, de mise en quarantaine et du dossier Courrier indésirable par destinataire, pour des boîtes aux lettres individuelles. Vous pouvez uniquement utiliser la cmdlet **Set-Mailbox** si vous souhaitez activer ou désactiver le seuil SCL du dossier Courrier indésirable pour des boîtes aux lettres individuelles. Les seuils de suppression, de rejet et de mise en quarantaine SCL par destinataire sont stockés dans Active Directory et répliqués sur les serveurs de transport Edge abonnés par le service EdgeSync de Microsoft Exchange. Les configurations de seuil de probabilité de courrier indésirable par destinataire sont utilisées par l’agent de filtrage du contenu même si vous avez défini des configurations SCL par serveur de transport. C’est pourquoi, si vous avez défini des seuils SCL par destinataire, l’agent de filtrage du contenu utilise les seuils SCL par destinataire pour des utilisateurs spécifiques au lieu de la configuration SCL de l’agent de filtrage du contenu. Pour obtenir des exemples, consultez la rubrique [Configurer les paramètres de blocage du courrier indésirable sur les boîtes aux lettres](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).
    
    > [!NOTE]
    > Les seuils SCL par destinataire ne sont pas appliqués aux messages reçus par le biais de groupes de distribution.
    
    Les paramètres SCL disponibles dans les cmdlets **Set-ContentFilterConfig** et **Set-OrganizationConfig** le sont également dans la cmdlet **Set-Mailbox** :
    
      - *SCLDeleteEnabled*
    
      - *SCLDeleteThreshold*
    
      - *SCLRejectEnabled*
    
      - *SCLRejectThreshold*
    
      - *SCLQuarantineEnabled*
    
      - *SCLQuarantineThreshold*
    
      - *SCLJunkThreshold*
    
    Toutefois, tous les paramètres SCL de la cmdlet **Set-Mailbox** acceptent également la valeur `$null`. Si un paramètre SCL d’une boîte aux lettres est vide (`$null`), le paramètre de l’agent de filtrage du contenu correspondant ou celui de la configuration de l’organisation est appliqué à la boîte aux lettres. Si un paramètre SCL d’une boîte aux lettres a la valeur `$true` ou `$false`, le paramètre de la boîte aux lettres remplace le paramètre correspondant au niveau de l’organisation dans l’agent de filtrage du contenu ou la configuration de l’organisation.
    
    Le paramètre SCL uniquement disponible dans la cmdlet **Set-Mailbox** est décrit dans le tableau suivant.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Paramètre</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkEnabled</em></p></td>
    <td><p>Ce paramètre active ou désactive la remise d’un message au dossier Courrier indésirable de l’utilisateur lorsque la valeur SCL du message est supérieure à celle spécifiée par le paramètre <em>SCLQuarantineThreshold</em>. Ce paramètre peut avoir la valeur <code>$true</code>, <code>$false</code> ou <code>$null</code>.</p>
    <p>Notez que le filtrage du courrier indésirable est activé par défaut pour toutes les boîtes aux lettres utilisateur de l’organisation. Par défaut, le paramètre <em>Enabled</em> a la valeur <code>$true</code> dans la cmdlet <strong>Set-MailboxJunkEmailConfiguration</strong> pour toutes les boîtes aux lettres utilisateur.</p></td>
    </tr>
    </tbody>
    </table>
    
    Pour plus d’informations sur la configuration de seuils SCL pour une boîte aux lettres, consultez la rubrique [Configurer les paramètres de blocage du courrier indésirable sur les boîtes aux lettres](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).

## Surveillance des seuils SCL

Vous pouvez utiliser plusieurs scripts intégrés du dossier `%ExchangeInstallPath%Scripts`, tels que **get-AntispamSCLHistogram.ps1**, pour collecter les données des résultats du filtrage. Si les données indiquent que vous devez procéder à des ajustements immédiats, reconfigurez les seuils SCL. Sinon, collectez des données et analysez les rapports de courrier indésirable afin de déterminer si des ajustements sont nécessaires.

