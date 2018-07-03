---
title: "Mise à niveau de la messagerie unifiée d'Exchange 2010 vers celle d'Exchange 2013: Exchange 2013 Help"
TOCTitle: Mise à niveau de la messagerie unifiée d'Exchange 2010 vers celle d'Exchange 2013
ms:assetid: 01aa5dab-689b-4738-afab-0d2f11a60b39
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn169226(v=EXCHG.150)
ms:contentKeyID: 54652748
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mise à niveau de la messagerie unifiée d'Exchange 2010 vers celle d'Exchange 2013

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Lorsque vous procédez à une mise à niveau d’une organisation Microsoft Exchange 2010 avec messagerie unifiée vers une messagerie unifiée Exchange 2013, certaines étapes sont obligatoires, tandis que d’autres ont déjà été accomplies dans le cadre du déploiement de la messagerie unifiée Exchange 2010. Selon votre environnement de téléphonie et les composants de messagerie unifiée précédemment créés et configurés pour la prise en charge de la messagerie unifiée dans Exchange 2010, il se peut que vous deviez déployer des équipements te téléphonie supplémentaires tels que des passerelles VoIP, des PBX IP, ou des PBX traditionnels ou SIP, ainsi que créer et configurer d'éventuels composants de messagerie unifiée supplémentaires requis pour la messagerie unifiée Exchange 2013.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 45 à 90 minutes.

  - Vérifiez que vous disposez des autorisations appropriées dans les organisations Exchange 2010 et Exchange 2013 pour créer et configurer tous les composants requis.

  - Vérifiez que vous avez déployé et configuré correctement vos composants de téléphonie, dont les passerelles et les PBX VoIP, IP ou compatibles SIP.

  - Vérifiez que vous avez correctement installé et configuré les serveurs d'accès au client exécutant le service routeur des appels de messagerie unifiée Microsoft Exchange, et les serveurs de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange. Pour plus d'informations sur les services de messagerie unifiée, consultez la rubrique [Services de messagerie unifiée](um-services-exchange-2013-help.md).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous devez déployer au moins un serveur de boîtes aux lettres Exchange 2013 dans votre organisation avant de configurer les passerelles VoIP ou les PBX IP pour envoyer le trafic SIP ou RTP de messagerie unifiée vers les serveurs d’accès client Exchange 2013.</td>
    </tr>
    </tbody>
    </table>


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


## Comment procéder ?

## Étape 1 : téléchargement et installation des modules linguistiques de messagerie unifiée nécessaires

Les modules linguistiques de messagerie unifiée permettent aux appelants et aux utilisateurs d'Outlook Voice Access d'interagir avec le système de messagerie vocale dans plusieurs langues. Après que vous avez installé une langue supplémentaire sur une serveur de boîtes aux lettres Exchange 2013, les appelants et les utilisateurs d'Outlook Voice Access ont la possibilité d'écouter les messages électroniques et d'interagir avec le système de messagerie vocale dans cette langue. Toutefois, pour que la langue soit disponible pour tous les appels entrants, vous devez installer les modules linguistiques de messagerie unifiée requis sur tous les serveurs de boîtes aux lettres Exchange 2013. Cela est dû au fait que chaque serveur de boîtes aux lettres Exchange 2013 peut répondre aux messages entrants pour la messagerie unifiée.

Par défaut, lorsque vous installez un serveur de boîtes aux lettres Exchange 2013, le module linguistique Anglais (États-Unis) est installé. Il s'agit de la seule option linguistique disponible pour votre plan de numérotation, sauf si vous installez un autre module linguistique de messagerie unifiée. (La langue anglaise (États-Unis) ne peut pas être supprimée, sauf si vous supprimez le serveur de boîtes aux lettres de l'ordinateur.) Après que vous avez installé un module linguistique de messagerie unifiée sur un serveur de boîtes aux lettres Exchange 2013, la langue associée au module linguistique est également une option disponible lorsque vous configurez la langue par défaut du plan de numérotation. Par défaut, comme un standard automatique de messagerie unifiée est lié, lors de sa création, à un plan de numérotation de messagerie unifiée, le standard automatique utilise le paramètre de langue par défaut du plan de numérotation de messagerie unifiée lié. Cependant, ce paramètre peut être modifié après la création du standard automatique de messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si la langue anglaise (États-Unis) est la seule que vous souhaitez proposer pour votre plan de numérotation, vous pouvez passer directement à l'étape 2.</td>
</tr>
</tbody>
</table>


Vous pouvez ajouter des modules linguistiques de messagerie unifiée à l'aide de la commande setup.exe ou en exécutant le programme d'installation *\<UMLanguagePack\>*.exe après avoir téléchargé le module linguistique de messagerie unifiée à partir de la page [Exchange Server 2013 UM Language Packs - Français](https://go.microsoft.com/fwlink/p/?linkid=266542). Pour plus d'informations, consultez la rubrique [Installer un module linguistique de messagerie unifiée](install-a-um-language-pack-exchange-2013-help.md).

Cet exemple utilise la commande setup.exe pour installer le module linguistique de messagerie unifiée (ja-JP).

    setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

## Étape 2 : Déplacement la boîte aux lettres système Exchange 2010 utilisée pour les messages d'accueil, annonces, menus et invites vers Exchange 2013

Les messages d'accueil, annonces, menus et invites personnalisés sont utilisés par les plans de numérotation et les standards automatiques de messagerie unifiée. La boîte aux lettres système {e0dc1c29-89c3-4034-b678-e6c29d823ed9} est créée lorsque vous installez Exchange 2010 ou Exchange 2013 ; elle permet la prise en charge de fonctionnalités telles que l'approbation des messages et la recherche dans plusieurs boîtes aux lettres. Cette boîte aux lettres système permet également de stocker des messages d'accueil, annonces, menus et invites personnalisés de plan de numérotation et de standard automatique. S’il n’existe pas de boîte aux lettres système, vous pouvez en créer à l’aide de la commande **Setup /PrepareAD**.

Par défaut, les boîtes aux lettres système sont invisibles dans le Centre d'administration Exchange (CAE). Pour obtenir la liste des boîtes aux lettres système, exécutez l'une des commandes suivantes :

Cette commande renvoie la liste de toutes les boîtes aux lettres système.

    Get-Mailbox -Arbitration

Cette commande renvoie la liste des boîtes aux lettres système et de leurs propriétés ou paramètres individuels.

    Get-Mailbox -Arbitration |fl

Cette boîte aux lettres système permet de sauvegarder les messages, annonces, menus et invites personnalisés, et de les restaurer, ainsi que d'autres boîtes aux lettres, dans une base de données. Cela réduit la quantité de ressources nécessaire. Le stockage des messages, annonces, menus et invites personnalisés dans une boîte aux lettres système supprime les incohérences éventuelles. Pour plus d'informations sur les déplacements de boîtes aux lettres, consultez la rubrique [Déplacements de boîtes aux lettres dans Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## Facultatif : Exportation et importation manuelles de messages, annonces, menus et invites personnalisés de plan de numérotation et de standard automatique

Parfois, la boîte aux lettres système Exchange 2010 peut avoir été déplacée et vous devez alors exporter et importer les messages, annonces, menus et invites personnalisés qui sont utilisés avec les plans de numérotation de messagerie unifiée et les standards automatiques de la boîte aux lettres système Exchange 2010 vers la boîte aux lettres système Exchange 2013. Dans les deux versions, la boîte aux lettres système est nommée {e0dc1c29-89c3-4034-b678-e6c29d823ed9}.

Les messages d'accueil, annonces, menus et invites personnalisés sont des fichiers audio (au format .wav ou .wma) utilisés par la messagerie unifiée aux fins suivantes :

  - Dans les plans de numérotation de messagerie unifiée, ils permettent de personnaliser les messages d'accueil et les messages d'information automatiques. Ils sont lus quand les utilisateurs d’Outlook Voice Access appellent un numéro Outlook Voice Access.

  - Sur les standards automatiques de messagerie unifiée, ils permettent de personnaliser les messages d'accueil pour les heures d'ouverture et les heures de fermeture, les messages d'information automatiques, les messages d'assistance vocaux et les menus de navigation. Ils sont lus quand les utilisateurs appellent un standard automatique de messagerie unifiée.

Lorsque vous exportez et importez des messages d’accueil, annonces, menus et invites personnalisés à partir d’Exchange 2010 vers Exchange 2013, vous devez utiliser les cmdlets **Export-UMPrompt** et **Import-UMPrompt**. Vous ne pouvez pas utiliser le CAE pour exporter ou importer des invites personnalisées. Sur un serveur Exchange 2010, utilisez la cmdlet **Export-UMPrompt** pour exporter le plan de numérotation et les invites de standard automatique Exchange 2010. Après avoir exporté les invites, vous pouvez les importer dans le serveur de boîtes aux lettres Exchange 2013. Lorsque vous exécutez la cmdlet **Export-UMPrompt** à partir de votre serveur Exchange 2010, le script effectue une recherche de GUID ou d'identificateur d'objet pour le plan de numérotation ou le standard automatique dans Active Directory, puis l'interroge pour déterminer la présence de messages d'accueil, d'annonces, de menus ou d'invites personnalisés. S'il en trouve, ces derniers sont enregistrés dans le répertoire que vous spécifiez. Après avoir exporté l’ensemble des messages d’accueil, annonces, menus et invites personnalisés, utilisez la cmdlet **Import-UMPrompt** pour importer les invites dans votre boîte aux lettres système Exchange 2013.

Cet exemple montre comment exporter le message d'accueil pour le plan de numérotation de messagerie unifiée `MyUMDialPlan` et l'enregistrer en tant que fichier `welcomegreeting.wav`.

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav" -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

Cet exemple montre comment importer le message d'accueil `welcomegreeting.wav` à partir de d:\\UMPrompts dans le plan de numérotation de messagerie unifiée `MyUMDialPlan`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

Cet exemple montre comment exporter un message d'accueil personnalisé pour le standard automatique de messagerie unifiée `MyUMAutoAttendant` et l'enregistrer en tant que fichier `welcomegreetingbackup.wav`.

    Export-UMPrompt -PromptFileName "welcomegreeting.wav" -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "e:\UMPromptsBackup\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

Cet exemple montre comment importer le message d'accueil `welcomegreeting.wav` à partir de d:\\UMPrompts dans le standard automatique de messagerie unifiée `MyUMAutoAttendant`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

Pour plus d'informations sur les invites personnalisées pour la messagerie unifiée, consultez les rubriques suivantes :

  - [Importer et exporter des invites, des annonces, des menus et des messages d’accueil personnalisés](import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md)

  - [Import-UMPrompt](https://technet.microsoft.com/fr-fr/library/dd876899\(v=exchg.150\))

  - [Export-UMPrompt](https://technet.microsoft.com/fr-fr/library/dd876882\(v=exchg.150\))

  - [Langues de messagerie unifiée, invites et messages d’accueil](um-languages-prompts-and-greetings-exchange-2013-help.md)

## Étape 4 : Exportation et importation de certificats

Si vous utilisez des plans de numérotation de type Sécurisé ou Sécurisé SIP dans votre organisation Exchange 2010, vous devez exporter et importer les certificats utilisés dans vos serveurs d’accès au client et de boîtes aux lettres Exchange 2013. La sécurité via l'authentification TLS (Transport Layer Security) mutuelle permet de chiffrer les données échangées entre vos serveurs Exchange 2013 et les passerelles VoIP, ainsi que les PBX IP et compatibles SIP. Les certificats lient l'identité du propriétaire de certificat à une paire de clés électroniques (publique et privée) utilisées pour chiffrer et signer numériquement les informations. Pour les services de messagerie unifiée et de routeur d'appels de messagerie unifiée, vous pouvez utiliser l'un des certificats suivants :

  - un certificat (Exchange) auto-signé ;

  - Un certificat d'infrastructure à clé publique (PKI) interne

  - Un certificat commercial tiers

Par défaut, lorsque vous installez Exchange 2013, deux certificats auto-signés sont créés : **certificat d'authentification serveur Microsoft Exchange (Microsoft Exchange Server Auth Certificate)** et **Microsoft Exchange**. Le certificat auto-signé **Microsoft Exchange** peut être utilisé avec la messagerie unifiée pour chiffrer des données, mais vous devez l'attribuer aux services de messagerie unifiée et de routeur d'appels de messagerie unifiée. Vous pouvez copier le certificat auto-signé, puis l'importer sur les passerelles VoIP, ainsi que les PBX IP et compatibles SIP. En revanche, vous ne pouvez pas l’utiliser quand vous intégrez une messagerie unifiée avec Microsoft Lync Server.

Pour permettre à la messagerie unifiée de chiffrer des données échangées entre vos serveurs Exchange 2013 et des passerelles VoIP, ainsi que des PBX IP et compatibles SIP, vous devez procéder comme suit :

  - Utilisez un certificat de messagerie unifiée auto-signé existant, créez un certificat auto-signé Exchange, soumettez une demande de certificat PKI à une autorité de certification interne, ou achetez un certificat commercial tiers que vous pouvez utiliser pour Mutual TLS entre vos serveurs de boîtes aux lettres et d'accès au client Exchange 2013, et des passerelles VoIP, ainsi que des PBX IP et compatibles SIP.
    
    Créez un certificat auto-signé Exchange à l'aide du CAE, comme suit :
    
    1.  Dans le CAE, accédez à **Serveurs** \> **Certificats**, puis, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").
    
    2.  Dans la page **Nouveau certificat Exchange**, choisissez **Créer un certificat auto-signé**, puis cliquez sur **Suivant**.
    
    3.  Entrez un nom convivial pour le certificat, puis cliquez sur **Suivant**.
    
    4.  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour sélectionner les serveurs Exchange auxquels vous voulez appliquer ce certificat, puis cliquez sur **Suivant**.
    
    5.  Spécifiez les domaines que vous voulez inclure dans votre certificat, puis cliquez sur **Suivant**. Si vous voulez ajouter un domaine pour un service, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    6.  Vérifiez que les domaines inclus sont corrects, puis cliquez sur **Terminer**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lorsque vous utilisez le CAE pour créer un certificat, vous n’êtes pas invité à activer les services pour ce dernier. Une fois le certificat créé, vous pouvez utiliser le CAE pour activer les services. Pour plus d'informations sur l'activation d'un certificat pour des services, consultez la rubrique <a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assigner un certificat pour les services de messagerie unifiée et de routeur d’appels UM</a>.</td>
    </tr>
    </tbody>
    </table>
    
    Créez un certificat auto-signé Exchange en exécutant la commande suivante dans l'environnement de ligne de commande.
    
        New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous spécifiez les services que vous voulez activer à l'aide du paramètre <em>Services</em>, vous êtes invité à les activer pour le certificat que vous avez créé. Dans cet exemple, vous êtes invité à activer le certificat pour les services de messagerie unifiée et de routeur d'appels de messagerie unifiée. Pour plus d'informations sur l'activation d'un certificat pour des services, consultez la rubrique <a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assigner un certificat pour les services de messagerie unifiée et de routeur d’appels UM</a>.</td>
    </tr>
    </tbody>
    </table>


  - Importez le certificat à utiliser sur tous les serveurs d'accès au client et de boîtes aux lettres Exchange 2013 au sein de votre organisation. Si vous utilisez le certificat auto-signé Exchange 2013, vous devez le copier, puis l’importer sur les passerelles VoIP, ainsi que les PBX IP ou compatibles SIP. Si vous utilisez le certificat auto-signé d'Exchange 2010, l'autre nom d'objet (SAN) doit contenir les noms d'ordinateur de tous les serveurs Exchange 2013. Si vous disposez de serveurs de messagerie unifiée Exchange 2010 au sein de votre organisation, vous pouvez utiliser le certificat auto-signé Exchange 2013, mais vous devez ajouter les noms d'ordinateur des serveurs de messagerie unifiée Exchange 2010 au SAN dans le certificat Exchange 2013.

  - Activez le certificat à utiliser ou attribuez-le aux services de messagerie unifiée et de routeur d'appels de messagerie unifiée sur les serveurs d'accès au client et de boîtes aux lettres au sein de votre organisation.
    
    À l'aide du CAE, activez les services de messagerie unifiée et de routeur d'appels de messagerie unifiée sur tous les serveurs Exchange 2013 pour qu'ils utilisent le certificat auto-signé Exchange, en procédant comme suit :
    
    1.  Dans le CAE, accédez à **Serveurs**\>**Certificats**, sélectionnez le certificat sur lequel vous voulez activer les services, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    2.  Dans la page **Procédure**, sélectionnez **Services**, **Messagerie unifiée**, puis **Routeur d'appels de messagerie unifiée**.
    
    Activez un certificat auto-signé Exchange en exécutant la commande suivante dans l'environnement de ligne de commande.
    
        Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

  - Configurez tout plan de numérotation de messagerie unifiée nouveau ou existant comme Sécurisé ou Sécurisé SIP.

  - Configurez le mode de démarrage de messagerie unifiée sur TLS ou Double sur les serveurs d'accès au client et de boîtes aux lettres au sein de votre organisation.

  - Créez et configurez une passerelle IP de messagerie unifiée (ou configurez-en une existante) avec un nom de domaine complet (FQDN).

  - Configurez le port d'écoute sur les passerelles IP de messagerie unifiée pour utiliser le port TLS 5061.

  - Redémarrez le service de routeur d'appels de messagerie unifiée sur tous les serveurs d'accès au client Exchange 2013, puis redémarrez le service de messagerie unifiée sur tous les serveurs de boîtes aux lettres Exchange 2013. Pour plus d'informations sur les services de messagerie unifiée, consultez la rubrique [Services de messagerie unifiée](um-services-exchange-2013-help.md).

## Étape 5 : Configurez le mode de démarrage de messagerie unifiée sur tous les serveurs d'accès au client Exchange 2013

Si vous utilisez des plans de numérotation de type Sécurisé ou Sécurisé SIP, vous devez configurer le mode de démarrage de messagerie unifiée sur vos serveurs d’accès au client Exchange 2013. Vous pouvez spécifier le mode de démarrage de messagerie unifiée pour le service de routeur d'appels de messagerie unifiée sur un serveur d'accès au client Exchange 2013 à l'aide du CAE ou de l'environnement de ligne de commande Exchange Management Shell. Par défaut, le serveur d’accès au client démarre en mode TCP, mais si vous utilisez TLS (Transport Layer Security) pour chiffrer le trafic VoIP (Voice over IP), vous devez configurer le serveur d’accès au client Exchange 2013 pour utiliser le mode TLS ou Double. Nous vous recommandons de configurer tous les serveurs d'accès au client Exchange 2013 pour utiliser le mode de démarrage de messagerie unifiée Double. Ce s'explique par le fait que tous les serveurs d'accès au client Exchange 2013 peuvent répondre aux appels entrants pour tous les plans de numérotation de messagerie unifiée, et que les paramètres de sécurité de ces derniers peuvent être différents. Si vous modifiez le mode de démarrage de messagerie unifiée, vous devez redémarrer le service de routeur d'appels de messagerie unifiée pour que la modification prenne effet. Pour plus d'informations sur les services de messagerie unifiée, consultez la rubrique [Services de messagerie unifiée](um-services-exchange-2013-help.md).

À l'aide du CAE, configurez le mode de démarrage de messagerie unifiée sur un serveur d'accès au client Exchange 2013 en procédant comme suit :

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Dans l'affichage Liste, sélectionnez le serveur Exchange à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Exchange Server**, cliquez sur **Messagerie unifiée**.

4.  Sous **Paramètres de routeur d'appels de messagerie unifiée** \> **Mode de démarrage de messagerie unifiée**, activez l'une des options suivantes dans la liste déroulante :
    
      - **TCP**   Activez cette option si vous n’utilisez pas mTLS et utilisez uniquement des plans de numérotation de type Non sécurisé.
    
      - **TLS**   Activez cette option si vous utilisez mTLS et uniquement des plans de numérotation de type Sécurisé ou Sécurisé SIP.
    
      - **DOUBLE**   Activez cette option si vous utilisez mTLS et des plans de numérotation de type Non sécurisé, Sécurisé SIP ou Sécurisé.

5.  Après avoir sélectionné le mode de démarrage de messagerie unifiée, cliquez sur **Enregistrer**.

À l'aide du CAE, configurez le mode de démarrage de messagerie unifiée sur un serveur d'accès au client Exchange 2013 en exécutant la commande suivante dans l'environnement de ligne de commande.

    Set-UMCallRouterSettings -Server MyUMCallRouter.northwindtraders.com -UMStartupMode Dual

## Étape 6 : Configuration du mode de démarrage de messagerie unifiée sur tous les serveurs de boîtes aux lettres Exchange 2013

Si vous utilisez des plans de numérotation de type Sécurisé ou Sécurisé SIP, vous devez configurer le mode de démarrage de messagerie unifiée sur vos serveurs de boîtes aux lettres Exchange 2013. Vous pouvez spécifier le mode de démarrage de messagerie unifiée pour le service de messagerie unifiée sur un serveur de boîtes aux lettres Exchange 2013 à l'aide du CAE ou de l'environnement de ligne de commande. Par défaut, un serveur de boîtes aux lettres Exchange 2013 démarre en mode TCP. Cependant, si vous utilisez TLS pour chiffrer le trafic VoIP, vous devez configurer le serveur de boîtes aux lettres Exchange 2013 pour utiliser le mode TLS ou Double. Nous vous recommandons de configurer tous les serveurs de boîtes aux lettres Exchange 2013 pour utiliser le mode de démarrage de messagerie unifiée Double. Ce s'explique par le fait que tous les serveurs de boîtes aux lettres Exchange 2013 peuvent répondre aux appels entrants pour tous les plans de numérotation de messagerie unifiée, et que les paramètres de sécurité de ces derniers peuvent être différents. Si vous modifiez le mode de démarrage de messagerie unifiée, vous devez redémarrer le service de messagerie unifiée pour que la modification prenne effet. Pour plus d'informations sur les services de messagerie unifiée, consultez la rubrique [Services de messagerie unifiée](um-services-exchange-2013-help.md).

À l'aide du CAE, configurez le mode de démarrage de messagerie unifiée sur un serveur de boîtes aux lettres Exchange 2013 en procédant comme suit :

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Dans l'affichage Liste, sélectionnez le serveur Exchange à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Exchange Server**, cliquez sur **Messagerie unifiée**.

4.  Sous **Paramètres de service de messagerie unifiée** \> **Mode de démarrage de messagerie unifiée**, activez l'une des options suivantes dans la liste déroulante :
    
      - **TCP**   Activez cette option si vous n’utilisez pas mTLS et utilisez uniquement des plans de numérotation de type Non sécurisé.
    
      - **TLS**   Activez cette option si vous utilisez mTLS et uniquement des plans de numérotation de type Sécurisé ou Sécurisé SIP.
    
      - **DOUBLE**   Activez cette option si vous utilisez mTLS et des plans de numérotation de type Non sécurisé, Sécurisé SIP ou Sécurisé.

5.  Après avoir sélectionné le mode de démarrage de messagerie unifiée, cliquez sur **Enregistrer**.

Configurez le mode de démarrage de messagerie unifiée sur un serveur de boîtes aux lettres Exchange 2013 en exécutant la commande suivante dans l'environnement de ligne de commande:

    Set-UMService -Identity MyUMServer -ExternalHostFqdn host.external.contoso.com -IPAddressFamily Any -UMStartupMode Dual

## Étape 7 : Création ou configuration de plans de numérotation de messagerie unifiée

En fonction de votre déploiement Exchange 2010 existant, il se peut que vous deviez créer ou configurer des plans de numérotation de messagerie unifiée. Un plan de numérotation de messagerie unifiée représente un ensemble de PBX (autocommutateurs privés) classiques, de PBX IP ou de PBX compatibles SIP qui partagent des numéros de poste d'utilisateur communs. Tous les postes d'utilisateur hébergés sur des PBX classiques, IP ou compatibles SIP dans un plan de numérotation contiennent le même nombre de chiffres. Les utilisateurs peuvent appeler les postes téléphoniques d’autres utilisateurs sans ajouter de numéro spécial ou composer un numéro de téléphone complet.

Des plans de numérotation de messagerie unifiée sont utilisés dans la messagerie unifiée pour garantir que les postes téléphoniques des utilisateurs sont uniques. Dans certains réseaux téléphoniques, plusieurs PBX ou PBX IP sont présents. Dans ces réseaux de téléphonie, deux utilisateurs peuvent posséder le même numéro de poste. Les plans de numérotation de messagerie unifiée résolvent cette situation. Placer les deux utilisateurs dans deux plans de numérotation de messagerie unifiée distincts rend leur extension unique. Pour plus d'informations, consultez la rubrique [Plans de numérotation de messagerie unifiée](um-dial-plans-exchange-2013-help.md).

Si nécessaire, vous pouvez créer un plan de numérotation de messagerie unifiée à l'aide du CAE :

1.  Dans le CAE, accédez à **Messagerie unifiée**\>**Plans de numérotation de messagerie unifiée**, puis cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans la page **Nouveau plan de numérotation de messagerie unifiée**, complétez les champs suivants :
    
      - **Nom**   Entrez le nom du plan de numérotation. Un nom de plan de numérotation de messagerie unifiée est obligatoire et doit être unique. Toutefois, le nom est utilisé uniquement à des fins d'affichage dans le CAE et l'environnement de ligne de commande. La longueur maximale d'un nom de plan de numérotation de messagerie unifiée est de 64 caractères pouvant inclure des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        Bien que le champ destiné au nom du plan de numérotation puisse accepter 64 caractères, la longueur du nom ne peut pas être supérieure à 49 caractères. Si vous tentez de créer un nom de plan de numérotation contenant plus de 49 caractères, un message d’erreur s’affiche. Ce message indique que la stratégie de boîte aux lettres de messagerie unifiée n'a pas pu être générée parce que le nom du plan de numérotation de messagerie unifiée est trop long. Cela se produit car, lorsque vous créez un plan de numérotation, une stratégie de boîte aux lettres de messagerie unifiée par défaut nommée *\<DialPlanName\>***Stratégie par défaut** est également créée. Après l'ajout des 15 caractères de la stratégie par défaut au nom du plan de numérotation, le nombre total de caractères dépasse la limite. Le paramètre *name* tant pour le plan de numérotation de messagerie unifiée que pour la stratégie de boîte aux lettres de messagerie unifiée peut compter jusqu'à 64 caractères. Toutefois, si le nom du plan de numérotation compte plus de 49 caractères, le nom de la stratégie de boîte aux lettres de messagerie unifiée par défaut comptera plus de 64 caractères, ce que le système n'autorise pas.
    
      - **Longueur des numéros de poste (chiffres)**   Entrez le nombre de chiffres pour les numéros de poste dans le plan de numérotation. Le nombre de chiffres des numéros de poste repose sur le plan de numérotation téléphonique créé sur un PBX. Par exemple, si un utilisateur associé à un plan de numérotation téléphonique doit composer un numéro à 4 chiffres pour appeler le poste d'un autre utilisateur du même plan de numérotation téléphonique, vous sélectionnez 4 pour le nombre de chiffres du poste.
        
        Ce champ est obligatoire et la plage de valeurs est comprise entre 1 et 20. En règle générale, le numéro de poste comprend entre 3 et 7 chiffres. Si votre environnement téléphonique existant inclut des numéros de poste, vous devez spécifier un nombre de chiffres correspondant à celui de ces numéros de poste.
        
        Lorsque vous créez un plan de numérotation de poste téléphonique, vous devez entrer un numéro de poste pour les utilisateurs qui y sont liés. Un numéro de poste est également nécessaire avec les plans de numérotation SIP (Session Initation Protocol) ou E.164 quand un utilisateur à extension messagerie unifiée est lié à un plan de numérotation URI SIP ou E.164. Les utilisateurs d'Outlook Voice Access utilisent ce numéro de poste pour accéder à leur boîte aux lettres Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Type UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Sécurité UI\_VoIP)
    
      - **Code de pays/région**   Ce champ permet de saisir le code numérique du pays/de la région à utiliser pour les appels sortants. Ce numéro est automatiquement ajouté devant le numéro de téléphone composé. Ce champ peut recevoir 1 à 4 chiffres. Par exemple, aux États-Unis, le code du pays/de la région est 1. Au Royaume-Uni, ce code est 44.

3.  Cliquez sur **Enregistrer**.

Si nécessaire, vous pouvez créer un plan de numérotation de messagerie unifiée en exécutant la commande suivante dans l'environnement de ligne de commande.

    New-UMDialplan -Name MyUMDialPlan -URIType E164 -NumberOfDigitsInExtension 5 -VoIPSecurity Secured

Si nécessaire, vous pouvez configurer un plan de numérotation de messagerie unifiée existant à l'aide du CAE en procédant comme suit :

1.  Dans le CAE, accédez à **Messagerie unifiée**\>**Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à afficher ou à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**. Utilisez les options de configuration pour afficher des paramètres de plan de numérotation spécifiques, ainsi que pour activer ou désactiver des fonctionnalités.

Si nécessaire, vous pouvez configurer un plan de numérotation de messagerie unifiée existant à l'aide de l'environnement de ligne de commande :

    Set-UMDialplan -Identity MyDialPlan -AccessTelephoneNumbers 4255551234 -AudioCodec Wma -CallAnsweringRulesEnabled $false -OutsideLineAccessCode 9 -VoIPSecurity SIPSecured

Lorsque vous avez déployé la messagerie unifiée Exchange 2010, vous avez dû ajouter un serveur de messagerie unifiée à un plan de numérotation de messagerie unifiée pour qu'il puisse répondre aux appels entrants. Cela n'est plus nécessaire. Dans Exchange 2013, les serveurs d’accès au client et de boîtes aux lettres ne peuvent pas être liés à un plan de numérotation de poste téléphonique ou E.164, mais ils doivent être liés à des plans de numérotation URI SIP. Les serveurs d'accès au client et de boîtes aux lettres répondent à tous les appels entrants pour tous les types de plans de numérotation.

## Étape 8 : Création ou configuration de passerelles IP de messagerie unifiée

En fonction de votre déploiement Exchange 2010 existant, il se peut que vous deviez créer ou configurer des passerelles IP de messagerie unifiée. Si vous utilisez des plans de numérotation de type Sécurisé SIP ou Sécurisé, vous devez créer une passerelle IP de messagerie unifiée avec un nom de domaine complet, puis utiliser l’environnement de ligne de commande pour la configurer de façon à ce qu’elle écoute le port 5061. Pour les passerelles IP de messagerie unifiée existantes, vérifiez qu’elles sont configurées avec un nom de domaine complet et qu’elles écoutent le port 5061. Si la passerelle IP de messagerie unifiée n’utilise pas de nom de domaine complet, servez-vous du CAE ou de l’environnement de ligne de commande pour modifier l’adresse. Si la passerelle IP de messagerie unifiée n’utilise pas le port 5061, servez-vous de l’environnement de ligne de commande pour modifier le port. Vous pouvez afficher les paramètres d'une passerelle IP de messagerie unifiée à l'aide de la cmdlet **Get-UMIPGateway**.

Une passerelle IP de messagerie unifiée représente une passerelle VoIP, un PBX IP ou un PBX compatible SIP physiques. Pour pouvoir utiliser une passerelle VoIP, un PBX IP ou un PBX compatible SIP afin de répondre aux appels entrants et d'émettre des appels pour des utilisateurs de messagerie vocale, une passerelle IP de messagerie unifiée doit être créée dans le service d'annuaire.

L'association de la passerelle IP de messagerie unifiée et d'un groupement de postes de messagerie unifiée établit un lien entre une passerelle VoIP, un PBX IP, ou un PBX compatible SIP, et un plan de numérotation de messagerie unifiée. En créant plusieurs groupements de postes de messagerie unifiée, vous pouvez associer une passerelle IP de messagerie unifiée unique à plusieurs plans de numérotation de messagerie unifiée. Pour plus d'informations, consultez la rubrique [Passerelles IP de messagerie unifiée](um-ip-gateways-exchange-2013-help.md).

Si nécessaire, vous pouvez créer une passerelle IP de messagerie unifiée à l'aide du CAE comme suit :

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans la page **Nouvelle passerelle IP de messagerie unifiée**, entrez les informations suivantes :
    
      - **Nom**   Cette zone de texte permet de spécifier un nom unique pour la passerelle IP de messagerie unifiée. Il s'agit du nom complet qui apparaît dans le CAE. Si vous devez modifier le nom complet de la passerelle IP de messagerie unifiée après sa création, vous devez d'abord supprimer cette dernière, puis en créer une autre avec le nom approprié. Le nom de passerelle IP de messagerie unifiée est obligatoire, mais utilisé uniquement à des fins d'affichage. Dans la mesure où votre organisation peut utiliser plusieurs passerelles IP de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour ces dernières. La longueur maximale d'un nom de passerelle IP de messagerie unifiée est de 64 caractères dont les espaces sont exclus. En revanche, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Adresse**   Vous pouvez configurer une passerelle IP de messagerie unifiée à l'aide d'une adresse IPv4 ou IPv6, ou d'un nom de domaine complet (FQDN). Utilisez cette boîte de dialogue pour spécifier l'adresse IP ou le FQDN configurés sur la passerelle VoIP, le PBX IP ou le PBX SIP. Cette boîte de dialogue n'accepte que des noms de domaine complets valides et correctement mis en forme.
        
        Vous pouvez entrer des caractères alphabétiques et numériques. Les adresses IPv4, IPv6 et les adresses avec un nom de domaine complet sont prises en charge. Si vous souhaitez utiliser le protocole TLS mutuel entre une passerelle IP de messagerie unifiée et un plan de numérotation fonctionnant en mode Sécurisé SIP ou en mode Sécurisé, vous devez configurer la passerelle IP de messagerie unifiée avec un nom de domaine complet. Vous devez également la configurer pour écouter le port 5061 et vérifier que les passerelles VoIP ou PBX IP ont également été configurés pour écouter les demandes Mutual TLS sur le port 5061. Pour configurer une passerelle IP de messagerie unifiée, exécutez la commande suivante dans l'environnement de ligne de commande : `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`
        
        Si vous utilisez un nom de domaine complet, vous devez également vous assurer que vous avez correctement configuré un enregistrement d'hôte DNS pour la passerelle VoIP, le PBX IP ou le PBX compatible SIP afin de résoudre correctement le nom d'hôte en adresse IP. De même, si vous utilisez un nom de domaine complet à la place d'une adresse IP et si la configuration DNS de la passerelle IP de messagerie unifiée est modifiée, vous devez désactiver la passerelle IP de messagerie unifiée, puis l'activer pour garantir une mise à jour correcte des informations de configuration de cette passerelle IP de messagerie unifiée.
    
      - **Plan de numérotation de messagerie unifiée**   Cliquez sur le bouton **Parcourir** pour sélectionner le plan de numérotation de messagerie unifiée que vous voulez associer à la passerelle IP de messagerie unifiée. Lorsque vous sélectionnez un plan de numérotation de messagerie unifiée à associer à une passerelle IP de messagerie unifiée, un groupement de postes de messagerie unifiée est également créé par défaut et associé au plan de numérotation de messagerie unifiée que vous avez sélectionné. Si vous ne sélectionnez pas de plan de numérotation de messagerie unifiée, vous devez créer manuellement un groupement de postes de messagerie unifiée, puis associer ce dernier à une passerelle IP de messagerie unifiée créée antérieurement.

3.  Cliquez sur **Enregistrer**.

Si nécessaire, vous pouvez créer une passerelle IP de messagerie unifiée en exécutant la commande suivante :

    New-UMIPGateway -Identity MyUMIPGateway -Address "MyUMIPGateway.contoso.com"

Pour configurer une passerelle IP de messagerie unifiée existante à l'aide du CAE :

1.  Dans le CAE, accédez à **Messagerie unifiée**\>**Passerelles IP de messagerie unifiée**, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Passerelle IP de messagerie unifiée**, cliquez sur **Configurer**. Utilisez les options de configuration pour afficher des paramètres de passerelle IP de messagerie unifiée spécifiques, ainsi que pour activer ou désactiver des fonctionnalités.

Pour configurer une passerelle IP de messagerie unifiée existante dans l'environnement de ligne de commande, exécutez la commande suivante.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## Étape 9 : Création d'un groupement de postes de messagerie unifiée

En fonction de votre déploiement Exchange 2010 existant, il se peut que vous deviez créer des groupements de recherche de messagerie unifiée. Un groupement de postes de téléphonie offre un moyen de répartir des appels téléphoniques à partir d'un numéro unique vers plusieurs postes ou numéros de téléphone. Dans la messagerie unifiée, un groupement de postes de messagerie unifiée constitue une représentation logique d'un groupement de postes de téléphonie et relie une passerelle IP de messagerie unifiée à un plan de numérotation de messagerie unifiée.

Vous devez disposer au moins d'un groupement de postes de messagerie unifiée pour chaque groupement de postes PBX ou PBX IP. Lorsque vous terminez la procédure suivant, un groupement de postes de messagerie unifiée est créé par défaut. Si vous avez plusieurs groupements de postes PBX ou PBX IP, vous devez créer d'autres groupements de postes de messagerie unifiée. Pour plus d'informations sur les groupements de postes de messagerie unifiée, consultez la rubrique [Groupes de recherche de messagerie unifiée](um-hunt-groups-exchange-2013-help.md).

Si nécessaire, vous pouvez créer un groupement de postes de messagerie unifiée à l'aide du CAE comme suit :

1.  Dans le CAE, accédez à **Messagerie unifiée**\>**Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Groupements de postes de messagerie unifiée**, cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans la page **Nouveau groupement de postes de messagerie unifiée**, entrez les informations suivantes :
    
      - **Nom**   Ce champ permet de saisir le nom complet du groupement de postes de messagerie unifiée. Un nom de groupement de postes de messagerie unifiée est requis et doit être unique, mais il est uniquement utilisé à des fins d'affichage dans le Centre d'administration Exchange et l'environnement de ligne de commande Exchange Management Shell. Si vous voulez modifier le nom d’affichage du groupement de postes après sa création, vous devez d’abord supprimer le groupement de postes existant, puis en créer un autre avec le nom approprié. Si votre organisation utilise plusieurs groupements de postes, nous vous recommandons d'utiliser des noms significatifs pour ces derniers. La longueur maximale d'un nom de groupement de postes de messagerie unifiée est de 64 caractères pouvant contenir des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Passerelle IP de messagerie unifiée**   Ce champ permet de sélectionner une passerelle IP de messagerie unifiée. Ce champ affiche le nom de la passerelle IP de messagerie unifiée associée au groupement de postes de messagerie unifiée. Pour lier une passerelle IP de messagerie unifiée au groupement de postes de messagerie unifiée, cliquez sur **Parcourir**.
    
      - **Identificateur pilote**   Ce champ permet de spécifier une chaîne qui fournit une identification unique de l'identificateur pilote configuré sur le PBX ou le PBX IP. Vous pouvez utiliser un numéro de poste ou un URI SIP dans ce champ. Les caractères alphanumériques sont acceptés. Pour les PBX hérités, une valeur numérique est utilisée comme identificateur pilote. Toutefois, certains PBX IP et compatibles SIP peuvent utiliser les URI SIP.

4.  Cliquez sur **Enregistrer**.

Si nécessaire, vous pouvez créer un plan groupement de postes de messagerie unifiée en exécutant la commande suivante dans l'environnement de ligne de commande.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialPlan MyUMDialPlan -UMIPGateway MyUMIPGateway

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas configurer ou modifier des paramètres pour un groupement de postes de messagerie unifiée. Pour modifier les paramètres de configuration d'un groupement de postes de messagerie unifiée, vous devez supprimer ce dernier, puis en ajouter un nouveau avec les paramètres corrects.</td>
</tr>
</tbody>
</table>


## Étape 10 : Création ou configuration de standards automatiques de messagerie unifiée

En fonction de votre déploiement Exchange 2010 existant, il se peut que vous deviez créer des standards automatiques de messagerie unifiée. Vous pouvez utiliser les standards automatiques de messagerie unifiée pour créer un système de menu vocal permettant aux appelants internes et externes de localiser des personnes et des emplacements, ou de transférer des appels vers des utilisateurs ou des départements au sein d'une organisation. Pour plus d'informations, consultez la rubrique [Réponse et routage automatique d'appels entrants](automatically-answer-and-route-incoming-calls-exchange-2013-help.md).

Dans des déploiements plus petits, vous pouvez déployer uniquement une messagerie unifiée pour permettre aux appelants de laisser des messages vocaux aux utilisateurs. Dans ces déploiements, la création d’un standard automatique n’est pas nécessaire. Toutefois, dans la plupart des cas, les standards automatiques sont très utiles aux appelants externes qui contactent votre organisation.

Si nécessaire, vous pouvez créer un standard automatique de messagerie unifiée à l'aide du CAE comme suit :

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Sélectionnez le plan de numérotation de messagerie unifiée auquel vous ajouter un standard automatique, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans la page **Nouveau standard automatique de messagerie unifiée**, complétez les champs suivants :
    
      - **Nom**   Ce champ permet de créer le nom complet du standard automatique de messagerie unifiée. Un nom de standard automatique de messagerie unifiée est obligatoire et doit être unique. Toutefois, il est utilisé uniquement à des fins d'affichage dans le CAE et l'environnement de ligne de commande. Si vous devez modifier le nom complet du standard automatique après sa création, vous devez d'abord supprimer ce dernier, puis en créer un autre avec le nom approprié. Si votre organisation utilise plusieurs standards automatiques de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour ces derniers La longueur maximale d'un nom de standard automatique de messagerie unifiée est de 64 caractères pouvant inclure des espaces.
        
        Bien qu’il soit possible de nommer un nouveau standard automatique de messagerie unifiée et d’y inclure des espaces, si vous intégrez la messagerie unifiée avec Lync Server, le nom du standard automatique ne peut pas comporter d’espaces. Par conséquent, si vous avez nommé un standard automatique avec des espaces et que vous intégrez Lync Server, supprimez d’abord ce standard, puis créez-en un autre sans espace.
    
      - **Créer ce standard automatique comme activé**   Activez cette case à cocher pour permettre au standard automatique de répondre aux appels entrants une fois le standard automatique de messagerie unifiée créé. Par défaut, un nouveau standard automatique est créé comme désactivé. Si vous décidez de créer un standard automatique de messagerie unifiée comme désactivé, vous pouvez utiliser le CAE ou l'environnement de ligne de commande pour l'activer après sa création.
    
      - **Définir le standard automatique pour répondre aux commandes vocales**   Activez cette case à cocher pour que le standard automatique de messagerie unifiée puisse utiliser la reconnaissance vocale. Si la reconnaissance vocale est activée pour le standard automatique, les appelants peuvent répondre aux invites personnalisées ou système utilisées par le standard automatique de messagerie unifiée en utilisant des entrées vocales ou à tonalité. Par défaut, la reconnaissance vocale n'est pas activée sur le standard automatique lors de sa création. Pour que les appelants utilisant un standard automatique à reconnaissance vocale dans une langue autre que l'anglais (États-Unis), vous devez installer le module linguistique de messagerie unifiée approprié et configurer les propriétés du standard automatique pour utiliser cette langue. Le module linguistique de messagerie unifiée en-US est installé par défaut lorsque vous installez un serveur de boîtes aux lettres Exchange 2013.
    
      - **Numéros d'accès**   Entrez les numéros de poste ou de téléphone que les appelants peuvent utiliser pour joindre le standard automatique. Tapez un numéro de poste ou de téléphone dans ce champ, puis cliquez sur **Ajouter** pour ajouter le numéro à la liste. Le nombre de chiffres du numéro de poste ou de téléphone que vous entrez ne doit pas correspondre au nombre de chiffres d'un numéro de poste configuré dans le plan de numérotation de messagerie unifiée associé. En effet, les appels directs sont aux standards automatiques de messagerie unifiée sont autorisés.
        
        Vous pouvez entrer un nombre illimité de numéros de poste ou d'accès. Toutefois, vous pouvez créer un standard automatique sans numéro de poste ou de téléphone répertorié. Aucun numéro de poste ou de téléphone n'est requis. Vous pouvez modifier ou supprimer un numéro de poste ou un identificateur pilote existant. Pour modifier un numéro de poste ou de téléphone, cliquez sur **Modifier**. Pour supprimer un numéro de poste ou de téléphone de la liste, cliquez sur **Supprimer**.

4.  Cliquez sur **Enregistrer**.

Si nécessaire, vous pouvez créer un standard automatique de messagerie unifiée en exécutant la commande suivante dans l'environnement de ligne de commande.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true -Status Enabled

Si nécessaire, vous pouvez configurer un standard automatique de messagerie unifiée à l'aide du CAE en procédant comme suit :

1.  Dans le CAE, accédez à **Messagerie unifiée**\>**Plans de numérotation de messagerie unifiée**, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée à afficher ou à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). Utilisez les options de configuration pour afficher des paramètres de standard automatique spécifiques, ainsi que pour activer ou désactiver des fonctionnalités.

Si nécessaire, vous pouvez configurer un standard automatique de messagerie unifiée en exécutant la commande suivante dans l'environnement de ligne de commande.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true -StaroutToDialPlanEnabled $true

## Étape 11 : Création ou configuration de stratégies de boîte aux lettres de messagerie unifiée

En fonction de votre déploiement Exchange 2010 existant, il se peut que vous deviez créer ou configurer des stratégies de boîte aux lettres de messagerie unifiée. Des stratégies de boîte aux lettres de messagerie unifiée sont requises lorsque vous activez la messagerie unifiée pour des utilisateurs. La boîte aux lettres de chaque utilisateur à extension messagerie unifiée doit être liée à une seule stratégie de boîte aux lettres de messagerie unifiée. Après avoir créé une stratégie de boîte aux lettres de messagerie unifiée, vous devez relier une ou plusieurs boîtes aux lettres de messagerie unifiée à cette stratégie. Cela vous permet de contrôler les paramètres de sécurité du code confidentiel, tels que le nombre minimal de chiffres ou le nombre maximal de tentatives d'ouverture de session pour les utilisateurs à messagerie unifiée qui sont associés à la stratégie de boîte aux lettres de messagerie unifiée. Pour plus d'informations, consultez la rubrique [Stratégies de boîte aux lettres de messagerie unifiée](um-mailbox-policies-exchange-2013-help.md).

Si nécessaire, vous pouvez créer une stratégie de boîte aux lettres de messagerie unifiée à l'aide du CAE :

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, cliquez sur **Ajouter** ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Nouvelle stratégie de boîte aux lettres de messagerie unifiée**, dans le champ **Nom**, entrez le nom de la nouvelle stratégie de boîte aux lettres de messagerie unifiée.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Ce champ permet de spécifier un nom unique pour la stratégie de boîte aux lettres de messagerie unifiée. Il s'agit du nom complet qui apparaît dans le CAE. Si vous devez modifier le nom complet de la stratégie de boîte aux lettres de messagerie unifiée après sa création, vous devez d'abord la supprimer, puis en créer une autre avec le nom approprié. Vous ne pouvez pas supprimer une stratégie de boîte aux lettres de messagerie unifiée si des utilisateurs à extension messagerie unifiée y sont associés. Le nom de la stratégie de boîte aux lettres de messagerie unifiée est obligatoire mais sert uniquement à des fins d'affichage. Dans la mesure où votre organisation peut utiliser plusieurs stratégies de boîte aux lettres de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour chacune d'elles. La longueur maximale d'un nom de stratégie de boîte aux lettres de messagerie unifiée est de 64 caractères pouvant inclure des espaces. Toutefois, il ne peut pas contenir les caractères suivants : &quot; / \ [ ] : ; | = , + * ? &lt; &gt;.</td>
    </tr>
    </tbody>
    </table>


4.  Cliquez sur **Enregistrer**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lorsque vous enregistrez la stratégie de boîte aux lettres de messagerie unifiée, tous les paramètres par défaut (stratégies de code confidentiel, fonctionnalités de messagerie vocale et paramètres de messagerie vocale protégée) sont activés. Pour personnaliser ou modifier des paramètres par défaut de la stratégie de boîte aux lettres de messagerie unifiée que vous avez créée, utilisez la cmdlet <strong>Set-UMMailbox</strong> ou le CAE.</td>
    </tr>
    </tbody>
    </table>


Si nécessaire, vous pouvez créer une stratégie de boîte aux lettres de messagerie unifiée dans l'environnement de ligne de commande en exécutant la commande suivante.

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

Si nécessaire, vous pouvez configurer une stratégie de boîte aux lettres de messagerie unifiée à l'aide du CAE:

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie à afficher ou à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). Utilisez les options de configuration pour afficher des paramètres de stratégie de boîte aux lettres de messagerie unifiée spécifiques, ainsi que pour activer ou désactiver des fonctionnalités.

Si nécessaire, vous pouvez configurer une stratégie de boîte aux lettres de messagerie unifiée en exécutant la commande suivante dans l'environnement de ligne de commande.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

## Étape 12 : Déplacement de boîtes aux lettres à extension de messagerie unifiée vers Exchange 2013

Dans la messagerie unifiée Exchange 2010, après avoir autorisé les utilisateurs de l’organisation à se servir de la messagerie vocale, une ensemble par défaut de propriétés de messagerie unifiée sont appliquées aux utilisateurs pour leur permettre d’avoir recours aux fonctionnalités de messagerie unifiée. Pour plus d'informations, consultez la rubrique [Messagerie vocale pour les utilisateurs](voice-mail-for-users-exchange-2013-help.md).

Durant le processus de mise à niveau, il y a une période durant laquelle la messagerie unifiée est activée pour des boîtes aux lettres sur les serveurs Exchange 2010 et Exchange 2013. Toutefois, si vous déplacez tous les utilisateurs à extension messagerie unifiée vers des serveurs de boîtes aux lettres Exchange 2013, vous devez utiliser le CAE ou la cmdlet **New-MoveRequest** dans l’environnement de ligne de commande à partir d’un serveur Exchange 2013, afin de conserver l’ensemble des propriétés et paramètres, dont le code confidentiel de l’utilisateur.

Une demande de déplacement désigne le processus de déplacement d'une boîte aux lettres d'une base de données de boîtes aux lettres vers une autre. Une demande de déplacement local désigne un déplacement de boîte aux lettres qui se produit dans une seule forêt. Pour plus d'informations sur les déplacements de boîtes aux lettres, consultez la rubrique .

  - [Déplacements de boîtes aux lettres dans Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

  - [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\))

  - [New-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219166\(v=exchg.150\))

  - [Gestion des demandes de déplacement](https://go.microsoft.com/fwlink/p/?linkid=296352)

Pour déplacer une boîte aux lettres Exchange 2010 vers un serveur de boîtes aux lettres Exchange 2013 à l'aide du CAE :

1.  Dans le CAE, cliquez sur **Destinataires**\>**Migration**, puis sur **Ajouter**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans l'Assistant **Nouveau déplacement de boîte aux lettres locale**, sélectionnez l'utilisateur à déplacer, cliquez sur **OK**, puis sur **Suivant**.

3.  Dans la page **Déplacer la configuration**, spécifiez le nom du nouveau lot. Sélectionnez les options choisies pour la boîte aux lettres d'archive et l'emplacement de la base de données de boîtes aux lettres, puis cliquez sur **Nouveau**.

Pour déplacer une boîte aux lettres Exchange 2010 vers un serveur de boîtes aux lettres Exchange 2013 à l'aide de l'environnement de ligne de commande, exécutez la commande suivante.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase "DB01"

## Étape 13 : Activez de nouveaux utilisateurs pour la messagerie unifiée ou configurez des paramètres pour un utilisateur à extension messagerie unifiée existant

Un utilisateur doit disposer d'une boîte aux lettres avant de pouvoir être activé pour la messagerie unifiée. Toutefois, par défaut, un utilisateur disposant d'une boîte aux lettres n'est pas activé pour la messagerie unifiée. Une fois que l'utilisateur activé pour la messagerie unifiée, vous pouvez gérer, modifier et configurer ses propriétés de messagerie unifiée et ses fonctions de messagerie vocale. Vous pouvez activer un utilisateur pour la messagerie unifiée à l'aide du CAE ou de l'environnement de ligne de commande. Pour plus d'informations, consultez la rubrique [Messagerie vocale pour les utilisateurs](voice-mail-for-users-exchange-2013-help.md).

Lorsque vous activez un utilisateur pour la messagerie unifiée, vous devez définir au moins un numéro de poste que la messagerie unifiée peut utiliser en cas de soumission d'un message à la boîte aux lettres de l'utilisateur, et pour permettre à ce dernier d'utiliser Outlook Voice Access. Une fois l'utilisateur activé pour la messagerie unifiée, vous pouvez ajouter des numéros de poste secondaires à sa boîte aux lettres, les modifier ou les supprimer en configurant l'adresse proxy de messagerie unifiée Exchange sur la boîte aux lettres de l'utilisateur, ou ajouter ou supprimer d'autres postes secondaires pour l'utilisateur dans le CAE. Pour ajouter, modifier ou supprimer des numéros de poste, des numéros E.164 ou des adresses SIP, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

Pour activer un utilisateur pour la messagerie unifiée à l'aide du CAE :

1.  Dans le CAE, cliquez sur **Destinataires**.

2.  Dans l'affichage Liste, sélectionnez l'utilisateur dont vous voulez activer la boîte aux lettres pour la messagerie unifiée.

3.  Dans le volet Détails, sous **Fonctionnalités téléphoniques et vocales**, cliquez sur **Activer**.

4.  Dans la page **Activer la boîte aux lettres de messagerie unifiée**, cliquez sur le bouton **Parcourir** à côté de **Stratégie de boîte aux lettres de messagerie unifiée**, localisez la stratégie à attribuer à l'utilisateur dans la liste, puis cliquez sur **OK**.

5.  Dans la page **Activer la boîte aux lettres de messagerie unifiée**, complétez les champs suivants :
    
      - **Adresse SIP ou numéro E.164**   Entrez l'adresse SIP ou le numéro E.164 de l'utilisateur. Ces options sont disponibles si l’utilisateur que vous activez pour la messagerie unifiée est attribué à une stratégie de boîte aux lettres de messagerie unifiée reliée à un URI SIP ou à un plan de numérotation E.164. L'ajout d'une adresse SIP ou d'un numéro E.164 à un utilisateur n'est pas disponible si ce dernier est associé à plan de numérotation de poste téléphonique. Lorsque vous attribuez l’utilisateur à une stratégie de boîte aux lettres de messagerie unifiée qui est associée à un URI SIP ou un plan de numérotation E.164, vous devez toujours entrer un numéro de poste pour l’utilisateur. Ce numéro de poste est utilisé quand des utilisateurs accèdent à leur boîte aux lettres à l'aide d'Outlook Voice Access. Le nombre de chiffres que vous configurez dans ce champ doit correspondre au nombre de chiffres configurés pour le plan de numérotation URI SIP ou E.164.
    
      - **Numéro de poste**   Saisissez le numéro de poste d’utilisateur que vous activez pour la messagerie unifiée.
        
        Vous devez fournir un numéro de poste valide pour l'utilisateur, dont le nombre de chiffres doit correspondre à celui spécifié pour le plan de numérotation. Vous pouvez entrer uniquement des caractères numériques ou de chiffres compris entre 1 et 20. Un numéro de poste classique compte entre 3 et 7 chiffres. Le nombre de chiffres de l’extension est défini sur le plan de numérotation lié à la stratégie de boîte aux lettres de messagerie unifiée attribuée à l’utilisateur.
    
      - Sous **Paramètres du code confidentiel**, procédez comme suit :
        
          - **Générer automatiquement un code confidentiel**   Cliquez sur ce bouton pour générer automatiquement un code confidentiel pour l'utilisateur à extension messagerie unifiée, qu'il utilisera pour accéder à la messagerie vocale via Outlook Voice Access. Il s'agit du paramètre par défaut. Lorsque vous cliquez sur ce bouton, un code confidentiel est automatiquement généré d'après les stratégies de code confidentiel configurées dans la stratégie de boîte aux lettres de messagerie unifiée attribuée à l'utilisateur. Nous vous recommandons d'utiliser ce paramètre afin de protéger le code confidentiel de l'utilisateur. Le code confidentiel est envoyé à l’utilisateur dans le message de bienvenue qu’il reçoit après avoir été activé pour la messagerie unifiée. Par défaut, il doit modifier ce code confidentiel lorsqu’il se connecte pour la première fois à sa boîte aux lettres pour accéder à sa messagerie vocale.
        
          - **Tapez un code confidentiel**   Cliquez sur ce bouton pour entrer manuellement un code confidentiel qui permettra à l'utilisateur d'accéder au système de messagerie vocale. Le code confidentiel doit être conforme aux paramètres de stratégie de code confidentiel configurés dans la stratégie de boîte aux lettres de messagerie unifiée associée à cet utilisateur à extension messagerie unifiée. Par exemple, si la stratégie de boîte aux lettres de messagerie unifiée est configurée pour accepter uniquement les codes confidentiels contenant au moins sept chiffres, le code confidentiel entré dans ce champ doit compter au moins sept chiffres.
        
          - **Exiger que l'utilisateur réinitialise son code confidentiel à sa première connexion**   Activez cette case à cocher pour obliger l'utilisateur à réinitialiser son code confidentiel de messagerie vocale quand il accède pour la première fois au système de messagerie vocale à partir d'un téléphone via Outlook Voice Access. Il sera invité à saisir un code confidentiel avec lequel il est davantage familiarisé. Cette meilleure pratique de sécurité contraint les utilisateurs à extension messagerie unifiée à modifier leur code confidentiel lorsqu’ils se connectent pour la première fois pour se protéger contre les accès non autorisés à leurs données et à leur boîte de réception. Cette case à cocher est activée par défaut.

6.  Dans la page **Activer la boîte aux lettres de messagerie unifiée**, révisez vos paramètres. Pour activer l'utilisateur pour la messagerie unifiée, cliquez sur **Terminer**. Pour apporter des modifications à la configuration, cliquez sur **Précédent**.

Pour activer un utilisateur pour la messagerie unifiée dans l'environnement de ligne de commande, exécutez la commande suivante.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -NotifyEmail administrator@contoso.com -PINExpired $true

Si nécessaire, vous pouvez configurer un utilisateur activé pour la messagerie unifiée à l’aide du CAE :

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans l'affichage Liste, sélectionnez la boîte aux lettres pour laquelle vous voulez modifier la stratégie de boîte aux lettres de messagerie unifiée.

3.  Dans le volet d'informations, sous **Fonctions de téléphone et de voix** \> **Messagerie unifiée**, cliquez sur**Afficher les détails**.

4.  Dans la page **Boîte aux lettres de messagerie unifiée**, cliquez sur **Paramètres des boîtes aux lettres de messagerie unifiée** pour afficher ou modifier les propriétés de messagerie unifiée suivantes pour un utilisateur à extension messagerie unifiée :
    
      - **État du code confidentiel**   Ce champ en lecture seule indique l'état de la boîte aux lettres de l'utilisateur. Par défaut, quand un utilisateur est activé pour la messagerie unifiée, l'état du code confidentiel est **Non verrouillé**. En revanche, si l'utilisateur a entré un code confidentiel Outlook Voice Access incorrect à plusieurs reprises, l'état est **Verrouillé**.
    
      - **Stratégie de boîte aux lettres de messagerie unifiée**   Ce champ affiche le nom de la stratégie de boîte aux lettres de messagerie unifiée associée à l'utilisateur à extension messagerie unifiée. Vous pouvez cliquer sur **Parcourir** pour rechercher et spécifier la stratégie de boîte aux lettres de messagerie unifiée à associer à cette boîte aux lettres de messagerie unifiée.
    
      - **Extension opérateur personnel**   Ce champ permet de spécifier le numéro de poste d'opérateur pour l'utilisateur. Par défaut, aucun numéro de poste n'est configuré. Le numéro de poste peut compter entre 1 et 20 caractères. Cela permet de transférer les appels entrants destinés à l'utilisateur à extension messagerie unifiée vers le numéro de poste que vous spécifiez dans ce champ.
        
        Vous pouvez configurer d'autres types de numéros de poste d'opérateur dans les plans de numérotation et les standards automatiques. Toutefois, ces postes sont généralement destinés aux réceptionnistes ou aux opérateurs de l'organisation. Le paramètre de poste d'opérateur personnel peut être utilisé quand un adjoint administratif ou un assistant personnel répond aux appels entrants à la place d’un utilisateur spécifique.

5.  Dans la page **Boîte aux lettres de messagerie unifiée**, sous **Postes supplémentaires**, vous pouvez ajouter, modifier et afficher les numéros de poste pour l'utilisateur.
    
      - Pour ajouter un numéro de poste, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la page **Ajouter une autre extension**, utilisez **Parcourir** pour sélectionner le plan de numérotation de messagerie unifiée, puis saisissez le numéro de poste dans la zone **Numéro d'extension**.
    
      - Pour supprimer un numéro de poste, sélectionnez-le, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

6.  Si vous apportez des modifications, cliquez sur **Enregistrer**.

Si nécessaire, vous pouvez configurer un utilisateur activé pour la messagerie unifiée dans l’environnement de ligne de commande en exécutant la commande suivante :

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringAudioCodec Wma -CallAnsweringRulesEnabled $false -FaxEnabled $false -UMSMSNotificationOption VoiceMail

## Étape 14 : Configuration de vos passerelles VoIP, PBX IP et PBX compatibles SIP pour envoyer tous les appels entrants aux serveurs d'accès au client Exchange 2013

Lors de l’installation des serveurs d'accès au client et de boîtes aux lettres Exchange 2013, ces derniers sont automatiquement activés pour répondre aux appels vocaux entrants et sortants, et router les messages vocaux vers les destinataires souhaités. Lorsque vous installez vos serveurs d'accès au client et de boîtes aux lettres Exchange 2013, puis déployez une messagerie unifiée, vous n'avez pas à associer ou à ajouter de serveurs d'accès au client ou de boîtes aux lettres Exchange 2013 aux plans de numérotation de messagerie unifiée. Les serveurs d'accès au client ou de boîtes aux lettres Exchange 2013 répondent à tous les appels entrants, puis utilisent les plans de numérotation de messagerie unifiée pour localiser des utilisateurs.

Le serveur d'accès au client Exchange 2013 est le point d'entrée de l'ensemble des appels entrants ou des demandes SIP destinés à la messagerie unifiée. Le service qui gère les demandes SIP sur un serveur d'accès au client Exchange 2013 est le service de routeur d'appels de messagerie unifiée qui s'exécute sur chaque serveur d'accès au client Exchange 2013 au sein de votre organisation.

Lorsque vous procédez à une mise à niveau vers une messagerie unifiée Exchange 2013, vous devez avoir préalablement installé et configuré au moins une ou passerelle VoIP pour vous connecter aux PBX de votre réseau téléphonique, ou installé et configuré des PBX IP ou compatibles SIP.

La dernière étape du processus de mise à niveau vers une messagerie unifiée Exchange 2013 consiste à configurer les passerelles VoIP, PBX IP ou PBX compatibles SIP pour envoyer les appels entrants (y compris provenant de personnes souhaitant laisser un message vocal pour un destinataire, d'utilisateurs à extension messagerie appelant via Outlook Voice Access, et d'appelants qui accèdent à un standard automatique de messagerie unifiée) à vos serveurs d'accès au client Exchange 2013. Tous ces appels sont d'abord réceptionnés par une passerelle VoIP, un PBX IP ou un PBX compatible SIP, puis transférés vers les serveurs d'accès au client Exchange 2013 de votre organisation. Pour plus d'informations, consultez les ressources suivantes :

  -  [Services de messagerie unifiée](um-services-exchange-2013-help.md)

  -  [Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  -  [Gestionnaire de téléphonie pour Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

## Étape 15 : Désactivation de la réponse aux appels sur un serveur de messagerie unifiée Exchange 2010

Pour désactiver la réponse aux appels, désactivez la messagerie unifiée sur un serveur de messagerie unifiée Exchange 2010, ou supprimez le serveur de messagerie unifiée d'un plan de numérotation. En désactivant le messagerie unifiée, vous empêchez le serveur de messagerie unifiée de répondre aux appels entrants. Vous pouvez décider soit de déconnecter tous les appels immédiatement, soit d'attendre que des appels existants soient traités avant de désactiver le serveur de messagerie unifiée. Vous pouvez désactiver la réponse aux appels avant de supprimer le serveur d’un plan de numérotation afin qu’il cesse de traiter les appels entrants.

Pour désactiver la messagerie unifiée sur un serveur de messagerie unifiée Exchange 2010 à l'aide de la console de gestion Exchange :

1.  Dans l'arborescence de la console, accédez à **Configuration du serveur**\>**Messagerie unifiée**.

2.  Dans le volet Résultats, sélectionnez le serveur de messagerie unifiée à désactiver.

3.  Dans le volet Actions, cliquez sur l'une des options suivantes :
    
      - Si vous activez l'option **Désactiver immédiatement**, le serveur de messagerie unifiée déconnecte tous les appels connectés au serveur de messagerie unifiée.
    
      - Si vous activez l'option **Désactiver après la fin des appels**, le serveur de messagerie unifiée n'accepte pas de nouveaux appels et n'est pas désactivé tant que tous les appels n'ont pas été traités.

4.  Dans la boîte de dialogue de confirmation, cliquez sur **Oui** pour continuer.

Pour désactiver la messagerie unifiée sur un serveur de messagerie unifiée Exchange 2010 à l'aide de l'environnement de ligne de commande, exécutez la commande suivante :

    Disable-UMServer -Identity MyUMServer -Immediate $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour désactiver la réponse aux appels, vous pouvez utiliser la cmdlet <strong>Disable-UMServer</strong> d'un serveur de messagerie unifiée Exchange 2010 ou la cmdlet <strong>Disable-UMService</strong> d'un serveur de boîtes aux lettres Exchange 2013.</td>
</tr>
</tbody>
</table>


## Étape 16 : Suppression d'un serveur de messagerie unifiée Exchange 2010 d'un plan de numérotation

Pour traiter les appels, vous devez ajouter un serveur de messagerie unifiée Exchange 2010 à au moins un plan de numérotation de messagerie unifiée. Un serveur de messagerie unifiée peut être ajouté à plusieurs plans de numérotation de messagerie unifiée. Vous pouvez supprimer un serveur de messagerie unifiée Exchange 2010 d'un plan de numérotation de messagerie unifiée. Lorsque vous supprimez un serveur de messagerie unifiée d'un plan de numérotation de messagerie unifiée, le serveur de messagerie unifiée cesse de répondre aux appels ou de traiter les appels de messagerie unifiée pour les destinataires à extension messagerie unifiée.

Pour supprimer un serveur de messagerie unifiée Exchange 2010 d'un plan de numérotation à l'aide de la console de gestion Exchange :

1.  Dans l'arborescence de la console, accédez à **Configuration du serveur**\>**Messagerie unifiée**.

2.  Dans le volet Résultats, sélectionnez le serveur de messagerie unifiée.

3.  Dans le volet Actions, cliquez sur **Propriétés**.

4.  Sous l'onglet **Paramètres de messagerie unifiée**, dans la section **Plans de numérotation associés**, cliquez sur **Supprimer**.

5.  Dans la boîte de dialogue de confirmation, cliquez sur **Oui** pour confirmer la suppression du serveur Exchange 2010 du plan de numérotation de messagerie unifiée.

6.  Cliquez sur **OK** pour fermer la fenêtre des propriétés.

Pour supprimer un serveur de messagerie unifiée Exchange 2010 d'un plan de numérotation à l'aide de l'environnement de ligne de commande, exécutez la commande suivante :

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMServer -id MyUMServer
    $s.dialplans-=$dp.identity
    Set-UMServer -id MyUMServer -dialplans:$s.dialplans

Dans cet exemple figurent trois plans de numérotation URI SIP : SipDP1, SipDP2 et SipDP3. Cet exemple supprime le serveur de messagerie unifiée nommé `MyUMServer` du plan de numérotation SipDP3.

    Set-UMServer -id MyUMServer -DialPlans SipDP1,SipDP2

Dans cet exemple figurent deux plans de numérotation URI SIP : SipDP1 et SipDP2. Cet exemple supprime le serveur de messagerie unifiée nommé `MyUMServer` du plan de numérotation SipDP2.

    Set-UMServer -id MyUMServer -DialPlans SipDP1

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour supprimer un serveur de messagerie unifiée Exchange 2010 d'un ou plusieurs plans de numérotation, vous pouvez utiliser la cmdlet <strong>Set-UMServer</strong> dans l'environnement de ligne de commande sur un serveur de messagerie unifiée Exchange 2007, ou la cmdlet <strong>Set-UMService</strong> cmdlet sur un serveur de boîtes aux lettres Exchange 2010. Par exemple, pour supprimer un serveur de messagerie unifiée de tous les plans de numérotation, exécutez la commande suivante : <code>Set-UMServer -identity MyUMServer -DialPlans $null</code></td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

Après avoir configuré une messagerie unifiée, vérifiez les points suivants pour vous assurer qu’elle fonctionne correctement :

  - Un utilisateur que vous avez activé pour la messagerie unifiée peut se connecter à Outlook Web App ou à Outlook et voir le message d’accueil de la messagerie unifiée.

  - Les utilisateurs de la messagerie unifiée peuvent recevoir des messages vocaux.

  - Les utilisateurs de messagerie unifiée peuvent appeler un numéro Outlook Voice Access pour écouter leurs messages électroniques, leurs éléments de calendrier et leurs messages vocaux.

  - La messagerie unifiée route les appels provenant de l'extérieur de votre organisation et vous pouvez passer des appels.

