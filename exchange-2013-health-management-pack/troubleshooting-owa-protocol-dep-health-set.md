---
title: Dépannage de l’indicateur d’intégrité OWA.Protocol.Dep
TOCTitle: Dépannage de l’indicateur d’intégrité OWA.Protocol.Dep
ms:assetid: f39c63d5-f161-4eee-9415-05f3355e7cc7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.scom.owa.protocol.dep(v=EXCHG.150)
ms:contentKeyID: 54652825
ms.date: 01/08/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dépannage de l’indicateur d’intégrité OWA.Protocol.Dep

 

_**Sapplique à :**Exchange Server 2013, Project Server 2013_

_**Dernière rubrique modifiée :**2015-11-10_

Le jeu d’intégrité **OWA.Protocol.DEP** contrôle l’état d’intégrité général des services de messagerie instantanée (MI) d’Outlook Web App qui sont intégrés entre Lync 2013 et Exchange 2013. Pour plus d’informations sur l’activation de la messagerie instantanée dans Outlook Web App, voir [Intégration de Microsoft Lync Server 2013 et Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418).

Si vous recevez une alerte indiquant que le jeu d’intégrité **OWA.Protocol.DEP** est défectueux, cela signifie qu’un problème empêche peut-être la messagerie instantanée de fonctionner correctement dans Outlook Web App.

## Explication

Le service **OWA.Protocol.DEP** est surveillé à l’aide des sondes et moniteurs suivants :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sonde</th>
<th>Indicateur d’intégrité</th>
<th>Moniteurs associés</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>OwaIMInitializationFailedMonitor</p></td>
</tr>
<tr class="even">
<td><p>aucun (notification ou vérification)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>WacDiscoveryFailureEventMonitor</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les sondes et les moniteurs, consultez la rubrique [État et performances du serveur](https://technet.microsoft.com/fr-fr/library/jj150551\(v=exchg.150\)).

## Action de l'utilisateur

Il se peut que le service ait récupéré après avoir émis l’alerte. Par conséquent, quand vous recevez une alerte signalant que le jeu d’intégrité **OWA.Protocol.DEP** n’est pas intègre, vérifiez tout d’abord que le problème existe toujours. Si tel est le cas, exécutez les actions de récupération appropriées décrites dans les sections suivantes.

## Actions de récupération pour l’erreur : « InstantMessageOCSProvider.InitializeEndpointManager. Aucun paramètre de Registre pour le fournisseur de MI. »

Cette erreur indique qu’une clé de Registre requise est manquante sur le serveur de boîtes aux lettres. Cette clé de Registre doit avoir été configurée lors de l’installation de Microsoft Unified Communications Managed API (UCMA) 4.0 sur le serveur. La clé de Registre manquante est la suivante :

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\MSExchange OWA\InstantMessaging

Cette clé doit contenir une chaîne **ImplementationDLLPath** qui pointe vers le DDL `Microsoft.Rtc.Internal.Ucweb`. L’emplacement par défaut est `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP\Microsoft.Rtc.Internal.Ucweb.dll`.

Pour résoudre ce problème, réinstallez UCMA 4.0 ou créez manuellement la clé de Registre. Vous pouvez télécharger UCMA 4.0 ici : [Exécution d’Unified Communications Managed API 4.0](http://go.microsoft.com/fwlink/p/?linkid=260990).

## Actions de récupération pour l’erreur : « InstantMessageOCSProvider.InitializeEndpointManager. Fournisseur de messagerie instantanée introuvable. »

Cette erreur indique que le fichier DLL `Microsoft.Rtc.Internal.Ucweb` est manquant sur le serveur de boîtes aux lettres. Ce fichier doit avoir été installé lors de l’installation d’UCMA 4.0 sur le serveur. L’emplacement par défaut est `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP`.

Pour résoudre ce problème, réinstallez UCMA 4.0. Pour plus d’informations, consultez la rubrique [Exécution d’UCMA 4.0](http://go.microsoft.com/fwlink/p/?linkid=260990).

## Actions de récupération pour l’erreur : « Le nom du serveur de messagerie instantanée est null ou vide dans le fichier web.config. »

Cette erreur indique que le serveur Lync 2013 n’est pas défini dans le fichier de configuration d’application (web.config) Outlook Web App sur le serveur de boîtes aux lettres. L’emplacement de ce fichier `web.config` est `%ExchangeInstallPath%ClientAccess\Owa`. Il doit contenir une clé portant le nom **IMServerName** et indiquant le nom de domaine complet du serveur Lync 2013. Pour résoudre ce problème, procédez comme suit :

1.  Dans une fenêtre d’invite de commandes, ouvrez le fichier web.config Outlook Web App dans le Bloc-notes en exécutant la commande suivante :
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  Recherchez une clé portant le nom **IMServerName**. Si vous la trouvez, vérifiez le nom de domaine complet du serveur Lync 2013. Si la clé est introuvable, ajoutez-la en effectuant les opérations suivantes.
    
    1.  Trouvez la balise nommée **\<appSettings\>**.
    
    2.  Dans le nœud **\<appSettings\>**, ajoutez la ligne suivante :
        
            <add key="IMServerName" value="Lync Server FQDN" />
        
        Par exemple :
        
            <add key="IMServerName" value="lync01.contoso.com" />
    
    3.  Pour appliquer les modifications dans Outlook Web App, exécutez la commande suivante :
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## Actions de récupération pour l’erreur : « L’empreinte numérique du certificat de messagerie instantanée est null ou vide dans le fichier web.config. »

Cette erreur indique que le certificat qui est utilisé pour intégrer Lync 2013 et Outlook Web App n’est pas défini dans le fichier de configuration d’application (web.config) Outlook Web App sur le serveur de boîtes aux lettres. L’emplacement de ce fichier `web.config` est `%ExchangeInstallPath%ClientAccess\Owa`. Il doit contenir une clé portant le nom **IMCertificateThumbprint** et indiquant l’empreinte numérique du certificat (hachage).

Vous pouvez obtenir la valeur d’empreinte numérique du certificat à l’aide de la cmdlet **Get-ExchangeCertificate**, ou dans le centre d’administration Exchange (EAC) en accédant à **Serveurs** \> **Certificats**.

Pour résoudre ce problème, procédez comme suit :

1.  Dans une fenêtre d’invite de commandes, ouvrez le fichier web.config Outlook Web App dans le Bloc-notes en exécutant la commande suivante :
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  Recherchez une clé portant le nom **IMCertificateThumbprint**. Si vous la trouvez, vérifiez que la valeur de l’empreinte numérique est correcte. Si la clé est introuvable, ajoutez-la en effectuant les opérations suivantes :
    
    1.  Trouvez la balise nommée **\<appSection\>**.
    
    2.  Dans le nœud **\<appSection\>**, ajoutez la ligne suivante :
        
            <add key="IMCertificateThumbprint" value="thumbprint"/>
        
        Par exemple :
        
            <add key="IMCertificateThumbprint" value="35CB4C441D55506C88E59B7946B567A4F45B3B5C" />
    
    3.  Pour appliquer les modifications dans Outlook Web App, exécutez la commande suivante :
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## Actions de récupération pour l’erreur : « Le certificat de messagerie instantanée portant l’empreinte numérique \<valeur\> est introuvable. »

Cette erreur indique que le certificat utilisé pour intégrer Lync 2013 et Outlook Web App est introuvable sur le serveur de boîtes aux lettres. Ce certificat doit être installé sur le serveur de boîtes aux lettres et sur le serveur Lync 2013, et doit être approuvé par chacun d’entre eux. Pour plus d’informations sur les exigences en matière de certificat, consultez la section Activation de la messagerie instantanée sur Outlook Web App de la rubrique [Intégration de Microsoft Lync Server 2013 et Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418).

Vous pouvez utiliser la valeur d’empreinte numérique indiquée dans l’erreur pour retrouver le certificat à l’aide de la cmdlet **Get-ExchangeCertificate**, ou via le centre d’administration Exchange (EAC), en accédant à **Serveurs** \> **Certificats**.

## Actions de récupération pour l’erreur : « Le certificat de messagerie instantanée a expiré. »

Cette erreur indique que le certificat utilisé pour intégrer Lync 2013 et Outlook Web App a expiré. Pour résoudre cette erreur, vous devez renouveler le certificat.

Vous pouvez utiliser la valeur d’empreinte numérique indiquée dans l’erreur pour retrouver le certificat à l’aide de la cmdlet **Get-ExchangeCertificate**, ou via le centre d’administration Exchange (EAC), en accédant à **Serveurs** \> **Certificats**.

## Actions de récupération pour l’erreur : « Le certificat de messagerie instantanée n’est pas encore valide. »

Cette erreur indique que le certificat utilisé pour intégrer Lync 2013 et Outlook Web App possède des dates non valides. Pour résoudre cette erreur, vous devez configurer un nouveau certificat et ajouter la nouvelle valeur d’empreinte numérique à la clé **IMCertificateThumbprint** dans `%ExchangeInstallPath%ClientAccess\Owa\web.config`. Pour plus d’informations sur les exigences en matière de certificat, consultez la section Activation de la messagerie instantanée sur Outlook Web App de la rubrique [Intégration de Microsoft Lync Server 2013 et Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418).

## Actions de récupération pour l’erreur : « Le certificat de messagerie instantanée ne dispose pas de clé privée. »

Cette erreur indique que le certificat utilisé pour intégrer Lync 2013 et Outlook Web App ne dispose pas de clé privée. Pour résoudre cette erreur, vous devez configurer un nouveau certificat disposant d’une clé privée et ajouter la nouvelle valeur d’empreinte numérique à la clé **IMCertificateThumbprint** dans `%ExchangeInstallPath%ClientAccess\Owa\web.config`. Pour plus d’informations sur les exigences en matière de certificat, consultez la section Activation de la messagerie instantanée sur Outlook Web App de la rubrique [Intégration de Microsoft Lync Server 2013 et Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418).

