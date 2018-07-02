---
title: 'Test et dépannage avec la cmdlet Test-UMConnectivity: Exchange 2013 Help'
TOCTitle: Test et dépannage avec la cmdlet Test-UMConnectivity
ms:assetid: 08e67a99-e37f-4afd-bd58-455b62580af7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa995978(v=EXCHG.150)
ms:contentKeyID: 56269361
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Test et dépannage avec la cmdlet Test-UMConnectivity

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-06-25_

Une fois que vous avez installé les serveurs d’accès au client et de boîtes aux lettres et que vous avez configuré la messagerie unifiée, vous pouvez utiliser plusieurs tests de diagnostic et une application de téléphonie logicielle pour tester la connectivité téléphonique et le fonctionnement des services de messagerie unifiée.

## Test-UMConnectivity

La cmdlet **Test-UMConnectivity** permet de vérifier la connectivité aux serveurs d’accès au client et de boîtes aux lettres de plusieurs manières, en fonction des paramètres qu’elle utilise. Ces tests permettent de vérifier la fonctionnalité de messagerie unifiée :

  - **Local**   La cmdlet **Test-UMConnectivity** vérifie la communication VoIP avec les serveurs de boîtes aux lettres exécutés sur le même ordinateur local.

  - **Local avec TUILogon**   La cmdlet **Test-UMConnectivity** tente d’établir la communication VoIP avec le serveur de boîtes aux lettres exécuté sur le même ordinateur. Si elle parvient à se connecter, elle tente d’ouvrir une session sur une ou plusieurs boîtes aux lettres à extension messagerie unifiée en envoyant le numéro de poste et le code confidentiel de la boîte aux lettres. Si le paramètre *–TUILogon* est spécifié, les valeurs de paramètre suivantes doivent également être indiquées avec les informations appropriées pour la boîte aux lettres de test :
    
      - *–Phone*   Ce paramètre doit contenir le numéro de poste de la boîte aux lettres de test.
    
      - *–PIN*   Ce paramètre doit contenir le code confidentiel de la boîte aux lettres à extension messagerie unifiée.
    
      - *–UMDialPlan   *Ce paramètre doit contenir le plan de numérotation lié à la boîte aux lettres de test.

  - **Distant**   La cmdlet **Test-UMConnectivity** tente de se connecter à un serveur d’accès au client distant en appelant via une passerelle VoIP. Une fois la connexion établie, la cmdlet effectue des vérifications de connectivité sur le serveur d’accès au client distant et les chemins d’accès aux supports.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous recevez le message suivant, vous devez redémarrer le service de messagerie unifiée MicrosoftExchange car il s’est interrompu ou il ne répond pas : « La tâche Test-UMConnectivity a détecté une erreur lors de la tentative d’émission d’un appel. Détails : Impossible d’établir une connexion. »</td>
    </tr>
    </tbody>
    </table>

