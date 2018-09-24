---
title: 'En savoir plus sur l’outil de dépannage de MU Exchange: Exchange 2013 Help'
TOCTitle: En savoir plus sur l’outil de dépannage de messagerie unifiée Exchange
ms:assetid: cc11bf5e-2c87-4495-b2ad-3e9a6bc81dbc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg584301(v=EXCHG.150)
ms:contentKeyID: 56269372
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# En savoir plus sur l’outil de dépannage de messagerie unifiée Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

L’outil de dépannage de la messagerie unifiée Microsoft Exchange 2010 est une cmdlet de l’environnement de ligne de commande Exchange Management Shell appelée **Test-ExchangeUMCallFlow**. Vous pouvez utiliser cet outil pour mener une série de tests de diagnostic à l’encontre de la messagerie unifiée de votre organisation. Si l’un des tests échoue, l’outil indique la raison de l’échec et les solutions possibles pour résoudre le problème. Vous pouvez utiliser l’outil de dépannage de la messagerie unifiée uniquement sur les serveurs Exchange 2010 ou version ultérieure.

L’outil de dépannage de la messagerie unifiée peut être utilisé pour tester si la messagerie vocale fonctionne correctement dans les déploiements locaux et intersite. Vous pouvez utiliser cet outil dans les déploiements de messagerie unifiée qui incluent Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server 2010 ou version ultérieure, ou dans les déploiements de messagerie unifiée qui incluent des passerelles VoIP, des autocommutateurs privés (PBX) IP ou des contrôleurs de frontière de session (SBC).

> [!NOTE]
> L’outil de dépannage de la messagerie unifiée est utilisé à des fins de test et de dépannage. La cmdlet <strong>Test-UMConnectivity</strong>, en revanche, doit être utilisée à des fins de surveillance. La cmdlet <strong>Test-UMConnectivity</strong> est utilisée avec les packs de gestion SCOM (System Center Operations Manager) qui permettent de contrôler les serveurs de messagerie unifiée Exchange 2010, ou les serveurs de boîtes aux lettres et d’accès au client Exchange 2013, et les composants téléphoniques. La cmdlet <strong>Test-UMConnectivity</strong> effectue des tests SIP locaux et des tests de connexion locaux aux boîtes aux lettres, et peut s’exécuter comme tâche SCOM.


Pour télécharger l’outil de dépannage de la messagerie unifiée, consultez la page relative à l’[outil de dépannage de la messagerie unifiée](https://go.microsoft.com/fwlink/p/?linkid=182625).

**Contenu de cette rubrique**

Vue d’ensemble

Architecture de dépannage de la messagerie unifiée

Déploiements de PBX IP et de passerelle VoIP

Déploiements d’Office Communications Server 2007 R2 et de Microsoft Lync Server

Installation de l’outil de dépannage de la messagerie unifiée

Paramètres de la cmdlet

## Vue d’ensemble

L’outil de dépannage de la messagerie unifiée permet d’effectuer plus facilement des tests et des dépannages dans les déploiements de messagerie unifiée. Lorsque l’outil de dépannage de la messagerie unifiée est lancé, il génère automatiquement des fichiers de suivi qui sont stockés dans le dossier C:\\Users\\%UserProfile%\\AppData\\Roaming\\Microsoft Exchange 2010 UM Troubleshooting. Les fichiers de suivi suivants sont générés par l’outil :

  - **UMTool\_Collaboration**   Inclut des traces de pile RTC.

  - **UMTool\_DiagnosticLog**   Répertorie tous les tests qui sont lancés et leurs résultats.

  - **UMTool\_S4**   Inclut le S4 : signalisation de traces de pile.

  - **UMTool\_SIPMessageLogs**   Inclut les traces SIP complètes de l’appel test effectué.

L’outil de dépannage de la messagerie unifiée se connecte directement à un contrôleur de frontière de session (SBC) local, s’il en existe un, ou à un contrôleur SBC d’un centre de données, et émule un appel entrant comme si l’appel provenait d’un PBX via une passerelle VoIP ou un PBX IP. L’outil de dépannage de la messagerie unifiée peut servir à diagnostiquer :

  - les paramètres incorrects dans des déploiements de la messagerie unifiée locaux ou intersites au sein desquels Office Communications Server 2007 R2 ou Microsoft Lync Server est déployé ;

  - les paramètres incorrects dans un équipement téléphonique local ou intersite qui inclut des passerelles VoIP et PBX ou PBX IP ;

  - les problèmes liés au système DNS (Domain Name System) ;

  - les problèmes de certificat lorsque vous utilisez des plans de numérotation de messagerie unifiée en mode SIP sécurisé ou Sécurisé ;

  - les problèmes de signalisation et de support pour DTMF (numérotation en fréquences vocales) et les données audio.

Si l’outil de dépannage de la messagerie unifiée détecte une défaillance dans votre configuration, il indique la raison de l’erreur et les solutions possibles pour résoudre les problèmes détectés. Les erreurs pouvant être signalées lorsque l’outil de dépannage de la messagerie unifiée est utilisé dans un déploiement local sont notamment les suivantes :

  - Le nombre maximal d’appels est atteint.

  - La messagerie unifiée n’est pas activée pour l’utilisateur.

  - Les informations concernant la passerelle IP, le plan de numérotation ou le groupement de postes de messagerie unifiée sont introuvables.

  - Le type de sécurité ne correspond pas au plan de numérotation de messagerie unifiée.

  - Aucun processus de travail n’est disponible pour traiter l’appel.

  - Le service de messagerie unifiée ou les services de routeur d’appels de messagerie unifiée sont arrêtés.

  - La forêt Active Directory est introuvable.

  - Aucun espace disque n’est disponible.

  - Des en-têtes SIP non valides ont été utilisés dans la requête.

  - Un appel a été émis vers un serveur Office Communications Server 2007 R2 ou un serveur Lync Server.

  - La passerelle IP MU est désactivée.

  - L’URI de l’utilisateur qui est appelé n’est pas valide.

Lorsque l’outil de dépannage de la messagerie unifiée est utilisé dans un déploiement intersite, les erreurs pouvant être signalées sont notamment les suivantes :

  - La messagerie unifiée n’est pas activée pour l’utilisateur.

  - La passerelle IP MU est désactivée.

  - L’URI de l’utilisateur n’est pas valide.

  - Le type de sécurité ne correspond pas au plan de numérotation de messagerie unifiée.

  - Des en-têtes SIP non valides ont été utilisés dans la requête.

  - Les informations concernant la passerelle IP, le plan de numérotation ou le groupement de postes de messagerie unifiée sont introuvables.

L’outil de dépannage de la messagerie unifiée envoie un fichier .wav d’exemple pendant 15 secondes. Une fois le fichier audio et le flux audio RTP envoyés et lus, l’outil indique des mesures générales de qualité audio afin de diagnostiquer les problèmes de qualité audio de la connexion réseau (gigue et perte moyenne de paquets). Ces rapports incluent la qualité du flux de données multimédia entrant et sortant d’un serveur de messagerie unifiée et contiennent les données suivantes :

  - Note moyenne d’opinion de réseau (NMOS)

  - Codec

  - Latence en millisecondes (ms)

  - Gigue en millisecondes (ms)

  - % de perte de paquets

  - La classification et l’évaluation NMOS utilisées pour déterminer la qualité audio sont :
    
      - NMOS inférieure à 2 = Médiocre
    
      - NMOS supérieure à 2, mais inférieure à 3 = Moyen
    
      - NMOS supérieure à 3, mais inférieure à 4 = Bon
    
      - NMOS supérieure à 4, mais inférieure à 5 = Excellent

L’outil de dépannage de la messagerie unifiée prend en charge le test des plans de numérotation MU qui utilisent des appels en mode Sécurisé, SIP sécurisé ou Non sécurisé. Si vous choisissez le mode Sécurisé ou SIP sécurisé, l’empreinte du certificat utilisé est vérifiée pour déterminer si le certificat a expiré et le type de certificat utilisé pour les communications TLS (Transport Layer Security). Le certificat permet d’assurer une identification correcte et de garantir l’identité de l’ordinateur distant. Lorsque le mode Sécurisé ou SIP sécurisé est sélectionné, l’outil de dépannage de la messagerie unifiée vérifie si les conditions suivantes sont vraies :

  - Le certificat local a été trouvé dans le magasin de l’ordinateur local.

  - Le certificat qui est en cours d’utilisation est approuvé.

  - Le nom de cible indiqué dans le certificat est valide.

  - Le certificat a expiré.

  - L’ordinateur distant approuve le certificat.

  - Le certificat a été révoqué.

  - Le certificat ne dispose pas de l’utilisation avancée de la clé requise.

L’outil de dépannage de la messagerie unifiée peut être exécuté en mode Gateway ou SIPClient, selon qu’Office Communications Server 2007 R2 ou Lync Server est déployé ou que les passerelles VoIP et les PBX ou les PBX IP sont utilisés avec les serveurs de messagerie unifiée. Lorsque le mode Gateway ou SIPClient est utilisé, l’outil de dépannage de la messagerie unifiée prend en charge les appels aux formats suivants. Le format utilisé dépend du type d’URI du plan de numérotation MU :

  - Poste téléphonique   425-555-1010

  - Numéros de téléphone E.164   +1 (425) 555-1010

  - Adresses SIP   jccolon@contoso.com

Lorsque le mode SIPClient est utilisé, l’outil de dépannage de la messagerie unifiée effectue un appel de mémo vocal. Ce type d’appel n’est pas dirigé vers un téléphone ou un point de terminaison des communications unifiées, mais directement vers la messagerie vocale. Lorsque l’outil de dépannage de la messagerie unifiée s’exécute en mode SIPClient, il détermine :

  - l’utilisateur cible qui est appelé ;

  - si l’appel SIP a réussi ;

  - si l’appel SIP a été accepté par un serveur de messagerie unifiée Exchange 2010 ou un serveur de boîtes aux lettres Exchange 2013 ;

  - si la séquence DTMF appropriée a été reçue ;

  - si le fichier .wav de diagnostic a été envoyé et reçu par un serveur de messagerie unifiée Exchange 2010 ou un serveur de boîtes aux lettres Exchange 2013.

  - les outils de mesure utilisés à la réception du flux de qualité audio ou multimédia.

L’outil de dépannage de la messagerie unifiée émule des appels entrants et exécute des tests de diagnostic pour aider les administreurs locaux et les administrateurs de client à tester le flux des appels du répondeur automatique et à identifier les erreurs de configuration. Bien que l’outil de dépannage de la messagerie unifiée puisse tester le répondeur automatique, il ne peut pas être utilisé pour les types d’appels suivants :

  - Appels Outlook Voice Access, notamment les appels accédant à la messagerie vocale, à la messagerie électronique, au calendrier, au répertoire, aux contacts personnels ou aux options personnelles

  - Standards automatiques de messagerie unifiée

  - Émettre au téléphone

  - Règles de répondeur automatique

  - Télécopie

  - Approvisionnement d’une invite

Vue d’ensemble

## Architecture de dépannage de la messagerie unifiée

L’outil de dépannage de la messagerie unifiée vous permet de dépanner, diagnostiquer et corriger les problèmes de configuration rencontrés dans des déploiements intersites, et vous pouvez également l’utiliser sur des déploiements de messagerie unifiée locaux. Dans les déploiements intersites, l’outil valide également les configurations SBC sur site. L’administrateur peut tester tous les composants utilisés par la messagerie unifiée, notamment les contrôleurs SBC.

## Déploiements de PBX IP et de passerelle VoIP

Dans l’exemple suivant, le mode Gateway est utilisé pour tester le flux des appels dans un environnement qui n’inclut pas Office Communications Server 2007 R2 ou Lync Server. Cet exemple teste l’équipement téléphonique, qui inclut les passerelles VoIP, les PBX et PBX IP, et les composants de la messagerie unifiée. Cet exemple définit le mode de sécurité VoIP (Voice over IP) sur Non sécurisé, utilise l’adresse IP 10.1.1.1 comme saut suivant, et indique un numéro de poste dans les informations de diversion.

```powershell
Test-ExchangeUMCallFlow -Mode Gateway -VoIPSecurity Unsecured -NextHop 10.1.1.1 -Diversion 12345
```

Vue d’ensemble

## Déploiements d’Office Communications Server 2007 R2 et de Microsoft Lync Server

L’outil de dépannage de la messagerie unifiée peut être utilisé dans des déploiements locaux ou intersites qui incluent Office Communications Server 2007 R2 ou Microsoft Lync Server lorsque le mode SIPClient est défini. L’exemple suivant utilise le mode SIPClient et teste le flux des appels avec un plan de numérotation de messagerie unifiée sécurisé dans un environnement comprenant des serveurs Office Communications Server 2007 R2 ou Lync Server. Par défaut, lorsque vous exécutez l’outil de dépannage de la messagerie unifiée, il utilise les informations d’identification de l’utilisateur actuellement connecté à l’ordinateur. Lors de l’exécution de l’exemple suivant, vous serez invité à fournir les informations d’identification que vous souhaitez utiliser pour lancer l’outil de dépannage de la messagerie unifiée. Pour plus d’informations, voir [Définir les informations d’identification à utiliser avec l’outil de dépannage de la messagerie unifiée Exchange](set-the-credentials-to-use-with-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).

```powershell
Test-ExchangeUMCallFlow -Mode SIPClient -VoIPSecurity Secured -CallingParty tony@contoso.com -CalledParty david@contoso.com -Credential $get
```

## Installation de l’outil de dépannage de la messagerie unifiée

L’outil de dépannage de la messagerie unifiée peut être installé sur un serveur local de messagerie unifiée ou sur un autre ordinateur 64 bits qui exécute :

  - les systèmes d’exploitation Windows 7 ou Windows 8 ;

  - les systèmes d’exploitation Windows Server 2008 ou Windows Server 2008 R2.

  - les systèmes d’exploitation Windows Server 2012 ou Windows Server 2012 R2.

Si vous utilisez l’outil de dépannage de la messagerie unifiée sur une version 64 bits de Windows 7, Windows 8 ou l’édition 64 bits de Windows Server 2008, les composants suivants doivent être installés pour pouvoir installer l’outil de dépannage de la messagerie unifiée :

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1)   Consultez la rubrique [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    
    > [!NOTE]
    > Si l’outil est destiné à être utilisé sur un ordinateur Windows Vista ou Windows Server 2008, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=178998">Microsoft .NET Framework 3.5 Family Update pour Windows Vista x64 et Windows Server 2008 x64</a>.


  - Gestion à distance de Windows(WinRM) 2.0 et Windows PowerShell V2 (Windows6.0-KB968930.msu)   Consultez l’article 968930 de la Base de connaissances Microsoft, [Package Windows Management Framework Core (Windows PowerShell 2.0 et WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Microsoft Unified Communications Managed API 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi)   Consultez la rubrique [Unified Communications Managed API 2.0, Core Runtime (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

L’outil de dépannage de la messagerie unifiée (cmdlet **Test-ExchangeUMCallFlow**) n’est inclus ni sur le DVD Exchange 2010 SP1, ni dans les fichiers de téléchargement comprenant uniquement Exchange 2010, ni dans le support d’installation Exchange 2013. Vous pouvez toutefois télécharger l’outil de dépannage de la messagerie unifiée à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625).

Pour plus d’informations, voir [Installer l’outil de dépannage de la messagerie unifiée Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).

Vue d’ensemble

## Paramètres de la cmdlet

Le tableau suivant inclut les paramètres que vous pouvez utiliser avec la cmdlet **Test-ExchangeUMCallFlow**, ainsi qu’une description de ces paramètres. Vous pouvez par ailleurs utiliser la commande Shell `Get-help Test-ExchangeUMCallFlow -detailed` pour trouver des informations détaillées sur chaque paramètre pouvant être utilisé avec la cmdlet **Test-ExchangeUMCallFlow**, ainsi que des d’exemples d’utilisation.

### Paramètres

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
<td><p><em>CalledParty</em></p></td>
<td><p>Le paramètre <em>CalledParty</em> indique l’URI SIP de l’utilisateur d’Office Communications Server 2007 R2 ou de Lync Server pour lequel Enterprise Voice a été activé. Il s’agit de l’utilisateur auquel l’appel vocal émis par la cmdlet <strong>Test-ExchangeUMCallFlow</strong> sera destiné, par exemple : <code>-CalledParty tonysmith@contoso.com</code>. Utilisez ce paramètre si vous exécutez l’outil en mode SIPClient.</p></td>
</tr>
<tr class="even">
<td><p><em>CallingParty</em></p></td>
<td><p>Le paramètre <em>CallingParty</em> indique l’URI SIP de l’utilisateur d’Office Communications Server 2007 R2 ou de Lync Server pour lequel Enterprise Voice a été activé. Il s’agit de l’utilisateur qui effectue l’appel entrant, par exemple : <code>-CallingParty tonysmith@contoso.com</code>. Utilisez ce paramètre si vous exécutez l’outil en mode SIPClient.</p></td>
</tr>
<tr class="odd">
<td><p><em>Diversion</em></p></td>
<td><p>Le paramètre <em>Diversion</em> spécifie la chaîne à envoyer comme informations de diversion pour l’appel entrant. Elle peut prendre la forme d’un en-tête de diversion ou d’informations d’historique. Les informations de diversion incluses dans l’appel entrant peuvent être un numéro de poste ou comprendre d’autres informations de diversion.</p>
<p>Lorsque vous fournissez des informations de diversion telles que l’en-tête History-Info, vérifiez ce qui suit :</p>
<ul>
<li><p>Au moins deux entrées différentes existent avec des parties utilisateur différentes.</p></li>
<li><p>La dernière entrée contient le numéro pilote du plan de numérotation de messagerie unifiée associée de l’utilisateur.</p></li>
<li><p>De la deuxième à la dernière entrée, le numéro d’extension de l’utilisateur à extension messagerie unifiée doit être inclus. Cette entrée doit également inclure le texte d’explication approprié. Ce texte doit être correctement évité selon les règles d’évitement du paramètre d’URL standard.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>Le paramètre <em>Mode</em> indique le mode à utiliser (passerelle VoIP, PBX IP ou Office Communications Server 2007 R2 ou Lync Server). Vous pouvez spécifier le mode Gateway lorsque votre déploiement de messagerie unifiée comprend des passerelles VoIP ou des PBX IP, ou le mode SIPClient lorsque votre déploiement de messagerie unifiée comprend Office Communications Server 2007 R2 ou Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>NextHop</em></p></td>
<td><p>Le paramètre <em>NextHop</em> spécifie l’adresse IP ou le nom de domaine complet (FQDN) du saut suivant et peut également comprendre le port TCP du saut suivant auquel la cmdlet <strong>Test-ExchangeUMCallFlow</strong> doit se connecter pendant l’émulation de la passerelle VoIP ou du PBX IP. Lorsque vous précisez le port TCP, vous devez indiquer le port 5060 en mode Non sécurisé ou le port 5061 en mode Sécurisé ou SIP sécurisé. Par exemple : <code>gateway.contoso.com:5061</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>CertificateThumbprint</em></p></td>
<td><p>Le paramètre <em>CertificateThumbprint</em> indique l’empreinte du certificat utilisé pour le protocole TLS. Ceci est obligatoire si le mode SIP sécurisé ou Sécurisé est configuré dans le plan de numérotation de messagerie unifiée. Cette empreinte de certificat correspond au certificat qui avait été exporté à partir de la passerelle VoIP, du PBX IP ou du SBC. De même, l’ordinateur doté de l’outil de dépannage de la messagerie unifiée et utilisé pour tester le flux des appels doit approuver le certificat d’autorité pour le saut suivant.</p></td>
</tr>
<tr class="odd">
<td><p><em>Credential</em></p></td>
<td><p>Le paramètre <em>Credential</em> spécifie les informations d’identification de l’utilisateur employées pour exécuter la cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>HuntGroup</em></p></td>
<td><p>Le paramètre <em>HuntGroup</em> spécifie le groupement de postes de messagerie unifiée associé à la passerelle VoIP en cours d’émulation. Il s’agit généralement d’un numéro de poste. Utilisez ce paramètre si vous exécutez l’outil en mode Gateway.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoIPSecurity</em></p></td>
<td><p>Le paramètre <em>VoIPSecurity</em> spécifie le mode de sécurité à employer avec la cmdlet en mode Gateway. Vous pouvez utiliser un des modes de sécurité VoIP suivants :</p>
<ul>
<li><p>Sécurisé (TLS/SRTP)</p></li>
<li><p>Non sécurisé (TCP/RTP) (valeur par défaut)</p></li>
<li><p>SIP sécurisé (TLS/RTP)</p></li>
</ul></td>
</tr>
</tbody>
</table>


Vue d’ensemble

