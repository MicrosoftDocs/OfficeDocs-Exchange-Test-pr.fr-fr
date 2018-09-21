---
title: 'MAPI sur HTTP: Exchange 2013 Help'
TOCTitle: MAPI sur HTTP
ms:assetid: 4663b5db-5b30-4a5a-a302-be6fef7fe5da
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn635177(v=EXCHG.150)
ms:contentKeyID: 61204569
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# MAPI sur HTTP

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-05-10_

MAPI (Messaging Application Programming Interface) sur HTTP est un nouveau protocole de transport implémenté dans MicrosoftExchange Server 2013 Service Pack 1 (SP1). Le protocole MAPI sur HTTP améliore la fiabilité et la stabilité des connexions Outlook et Exchange en déplaçant la couche transport vers le modèle HTTP standard de l’industrie. Il améliore le niveau de visibilité des erreurs de transport et la capacité de récupération. Une fonctionnalité supplémentaire prend en charge une fonction d’interruption et de reprise explicite. Cela permet aux clients pris en charge de changer de réseau ou de reprendre après une mise en veille prolongée tout en conservant le même contexte de serveur.

L’implémentation du protocole MAPI sur HTTP n’implique pas qu’il s’agit du seul protocole pouvant être utilisé par Outlook pour accéder à Exchange. Les clients Outlook qui ne sont pas compatibles MAPI sur HTTP peuvent toujours utiliser Outlook Anywhere (RPC sur HTTP) pour accéder à Exchange via un serveur d’accès au client prenant en charge MAPI.

## Avantages du protocole MAPI sur HTTP

Le protocole MAPI sur HTTP offre les avantages suivants aux clients qui le prennent en charge :

  - Il rend possibles des innovations futures pour l’authentification à l’aide d’un protocole basé sur HTTP.

  - Il accélère le temps de reconnexion après une interruption des communications car seules les connexions TCP (et non les connexions RPC) doivent être recréées. Voici quelques exemples d’une interruption des communications :
    
      - Mise en veille prolongée de l’appareil
    
      - Passage d’un réseau câblé à un réseau sans fil ou cellulaire

  - Il offre un contexte de session qui ne dépend pas de la connexion. Le serveur conserve le contexte de session pour une durée pouvant être configurée, même si l’utilisateur change de réseau.

## Déploiement du protocole MAPI sur HTTP

Prenez en compte les conditions suivantes pour activer le protocole MAPI sur HTTP.

  - **Capacité de prise en charge**   Vérifiez que les versions de configuration prévues sont prises en charge.

  - **Conditions préalables**   Vérifiez que votre environnement a été mis à niveau et qu’il est prêt pour le protocole MAPI sur HTTP.

  - **Configuration**   Configurez les répertoires virtuels et activez MAPI pour votre organisation.

## Capacité de prise en charge

Utilisez la matrice suivante pour vérifier que vos clients et serveurs prennent en charge le protocole MAPI sur HTTP.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Produit</th>
<th>Exchange 2013 SP1</th>
<th>Exchange 2013 RTM</th>
<th>Exchange 2010 SP3</th>
<th>Exchange 2007 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 SP1</p></td>
<td><ul>
<li><p>MAPI sur HTTP</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2013 RTM</p></td>
<td><p>Outlook Anywhere</p></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2010 SP2 et les mises à jour 2956191 et 2965295 de la Base de connaissances (14 avril 2015)</p></td>
<td><ul>
<li><p>MAPI sur HTTP<span></span></p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2010 SP2 et versions antérieures</p></td>
<td><p>Outlook Anywhere</p></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Outlook Anywhere</p></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Conditions préalables

Effectuez les étapes suivantes pour préparer les clients et les serveurs à prendre en charge le protocole MAPI sur HTTP.

1.  Mettez à niveau les clients Outlook vers Outlook 2013 SP1 ou Outlook 2010 SP2 et les mises à jour 2956191 et 2965295 de la Base de connaissances (14 avril 2015).

2.  Mettez à niveau les serveurs d’accès au client et de boîtes aux lettres vers Exchange 2013 SP1. Pour plus d’informations sur la mise à niveau, consultez la rubrique [Mettre à niveau Exchange 2013 vers la mise à jour cumulative la plus récente ou vers le Service Pack le plus récent](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md).
    
    > [!NOTE]
    > Tous les serveurs d’accès au client doivent être mis à niveau vers Exchange 2013 SP1 avant d’activer le protocole MAPI sur HTTP. Si la mise à niveau n’est pas effectuée, Outlook peut ne pas se connecter aux boîtes aux lettres.
    > Le fait de ne pas mettre à niveau tous les serveurs de boîtes aux lettres dans un groupe de disponibilité de base de données (DAG) peut entraîner des retards de réception des messages électroniques. De plus, le client peut exiger le redémarrage d’Outlook dans le cas d’un basculement de base de données.


3.  Vous devez installer Microsoft.NET Framework 4.5.2 sur tous les serveurs Exchange 2013. Pour plus d’informations, consultez la rubrique [Installation de NET Framework 4.5](https://go.microsoft.com/fwlink/p/?linkid=518380).

4.  Sur tous les serveurs d’accès au client Exchange 2013 SP1, ajoutez la variable d’environnement Windows **COMPLUS\_DisableRetStructPinning** en procédant comme suit.
    
    1.  Dans une fenêtre d’invite de commandes, exécutez `systempropertiesadvanced` et cliquez sur **Variables d’environnement**.
    
    2.  Dans la section **Variables système**, cliquez sur **Nouveau**, puis entrez les informations suivantes.
        
          - **Nom de la variable**   `COMPLUS_DisableRetStructPinning`
        
          - **Valeur de la variable**   1
    
    3.  Lorsque vous avez terminé, cliquez sur **OK**.

## Configuration

Effectuez les étapes suivantes pour configurer le protocole MAPI sur HTTP pour votre organisation.

1.  **Configuration du répertoire virtuel**   Par défaut, Exchange 2013 SP1 crée un répertoire virtuel pour le protocole MAPI sur HTTP. Utilisez la cmdlet **Set-MapiVirtualDirectory** pour configurer le répertoire virtuel. Vous devez configurer une URL interne, une URL externe ou les deux. Pour plus d’informations, consultez la rubrique [Set-MapiVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dn595082\(v=exchg.150\)).
    
    Par exemple, pour configurer le répertoire virtuel MAPI par défaut sur le serveur Exchange local en définissant la valeur de l’URL interne sur https://contoso.com/mapi et la méthode d’authentification sur `Negotiate`, exécutez la commande suivante :
    
        Set-MapiVirtualDirectory -Identity "Contoso\mapi (Default Web Site)" -InternalUrl https://Contoso.com/mapi -IISAuthenticationMethods Negotiate

2.  **Configuration du certificat**   Le certificat numérique utilisé par votre environnement Exchange doit afficher les mêmes valeurs *InternalURL* et *ExternalURL* que celles définies sur le répertoire virtuel MAPI. Pour plus d’informations sur la gestion des certificats Exchange 2013, voir [Certificats numériques et SSL](digital-certificates-and-ssl-exchange-2013-help.md). Assurez-vous que le certificat Exchange est approuvé sur la station de travail cliente Outlook et qu’il n’existe aucune erreur de certificat, en particulier lorsque vous accédez aux URL configurées sur le répertoire virtuel MAPI.

3.  **Mise à jour des règles du serveur**   Vérifiez que vos équilibrages de charge, proxys inverses et pare-feu sont configurés de façon à autoriser l’accès au répertoire virtuel MAPI sur HTTP.

4.  **Activation de MAPI sur HTTP dans votre organisation Exchange**
    
    Exécutez la commande suivante :
    
    ```powershell
Set-OrganizationConfig -MapiHttpEnabled $true
```

## Test des connexions MAPI sur HTTP

Vous pouvez tester la connexion MAPI sur HTTP de bout en bout à l’aide de la cmdlet **Test-OutlookConnectivity**. Pour utiliser la cmdlet **Test-OutlookConnectivity**, le service Gestionnaire d’intégrité de Microsoft Exchange (MSExchangeHM) doit être démarré.

L’exemple suivant teste la connexion MAPI sur HTTP à partir du serveur Exchange nommé ContosoMail.

```powershell
Test-OutlookConnectivity -RunFromServerId ContosoMail -ProbeIdentity OutlookMapiHttpSelfTestProbe
```

Si le test a réussi, le résultat renvoi doit ressembler à cet exemple :

    MonitorIdentity                                          StartTime              EndTime                Result      Error     Exception
    ---------------                                          ---------              -------                ------      -----     ---------
    OutlookMapiHttp.Protocol\OutlookMapiHttpSelfTestProbe    2/14/2014 7:15:00 AM   2/14/2014 7:15:10 AM   Succeeded

Pour plus d’informations, consultez la rubrique [Test-OutlookConnectivity](https://technet.microsoft.com/fr-fr/library/dd638082\(v=exchg.150\)).

Les journaux relatifs à l’activité MAPI sur HTTP se trouvent aux emplacements suivants :

  - %ExchangeInstallPath%Logging\\MAPI Address Book Service\\

  - %ExchangeInstallPath%Logging\\MAPI Client Access\\

  - %ExchangeInstallPath%Logging\\HttpProxy\\Mapi\\

## Gestion de MAPI sur HTTP

Vous pouvez gérer la configuration du protocole MAPI sur HTTP à l’aide des cmdlets suivantes :

  - [Set-MapiVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dn595082\(v=exchg.150\))

  - [Get-MapiVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dn595080\(v=exchg.150\))

  - [New-MapiVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dn595081\(v=exchg.150\))

  - [Remove-MapiVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dn595083\(v=exchg.150\))

