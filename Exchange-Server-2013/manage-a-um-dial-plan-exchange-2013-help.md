---
title: "Gestion d'un plan de numérotation de messagerie unifiée: Exchange Online Help"
TOCTitle: Gestion d'un plan de numérotation de messagerie unifiée
ms:assetid: a89735e4-36ec-49fb-ad0f-192fad37e801
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124090(v=EXCHG.150)
ms:contentKeyID: 50478971
ms.date: 04/27/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.DialPlanGeneralPropertyPage
ms.translationtype: HT
---

# Gestion d'un plan de numérotation de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2018-04-26_

Une fois que vous avez créé un plan de numérotation de messagerie unifiée, vous pouvez afficher et configurer différents paramètres. Par exemple, vous avez la possibilité de configurer le niveau de sécurité VoIP (Voice over IP), le codec audio et les restrictions de numérotation. Les paramètres que vous configurez dans le plan de numérotation de messagerie unifiée affectent tous les utilisateurs associés au plan de numérotation via une stratégie de boîte aux lettres de messagerie unifiée.

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

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


## Que souhaitez-vous faire ?

## Utiliser le CAE (Centre d'administration Exchange) pour afficher ou configurer les paramètres d'un plan de numérotation de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à afficher ou à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Nouveau plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**. Utilisez les options de configuration pour afficher des paramètres de plan de numérotation spécifiques, ainsi que pour activer ou désactiver des fonctionnalités comme décrit dans les étapes suivantes.

4.  **Général**   Cette page permet d'afficher des paramètres de plan de numérotation spécifiques ou d'activer ou désactiver des fonctionnalités pour les utilisateurs à messagerie unifiée :
    
      - **Nom**   Il s'agit du nom du plan de numérotation qui a été créé. La longueur maximale d'un nom de plan de numérotation de messagerie unifiée est de 64 caractères pouvant contenir des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - Bien qu'il soit possible d'inclure des espaces dans le nom d'un plan de numérotation de messagerie unifiée, si vous intégrez la messagerie unifiée à Office Communications Server 2007 R2 ou à Microsoft Lync Server, le nom du plan de numérotation ne peut pas contenir d'espaces. En conséquence, si vous avez créé un plan de numérotation dont le nom complet comprend des espaces et que vous souhaitez intégrer ce plan de numérotation à Office Communications Server 2007 R2 ou Lync Server, vous devez d'abord supprimer ce plan de numérotation, puis en créer un qui n'inclut pas d'espaces dans le nom complet.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Bien que le champ destiné au nom du plan de numérotation puisse accepter 64 caractères, la longueur du nom ne peut pas être supérieure à 49 caractères. Si vous tentez de créer un nom de plan de numérotation contenant plus de 49 caractères, un message d'erreur s'affiche. Ce message indique que la stratégie de boîte aux lettres de messagerie unifiée n'a pas pu être générée parce que le nom du plan de numérotation de messagerie unifiée est trop long. Cela se produit car, comme mentionné précédemment, lorsque vous créez un plan de numérotation, une stratégie de boîte aux lettres de messagerie unifiée par défaut nommée <em>&lt;DialPlanName&gt;</em> Stratégie par défaut est également créée. Après l'ajout des 15 caractères de la stratégie par défaut au nom du plan de numérotation, le nombre total de caractères dépasse la limite. Le paramètre <em>name</em> tant pour le plan de numérotation de messagerie unifiée que pour la stratégie de boîte aux lettres de messagerie unifiée peut compter jusqu'à 64 caractères. Toutefois, si le nom du plan de numérotation compte plus de 49 caractères, le nom de la stratégie de boîte aux lettres de messagerie unifiée par défaut comptera plus de 64 caractères, ce qui n'est pas autorisé.</td>
        </tr>
        </tbody>
        </table>
    
      - **Longueur des numéros d'extension (chiffres)**   Il s'agit du nombre de chiffres compris dans les numéros d'extension des utilisateurs qui sont associés à ce plan de numérotation. Par exemple, si un utilisateur associé à un plan de numérotation compose un poste à 4 chiffres pour appeler un autre utilisateur du même plan de numérotation, sélectionnez 4 pour le nombre de chiffres du poste.
        
        Le nombre de chiffres des numéros d'extension repose sur le plan de numérotation des appels téléphoniques créé sur un PBX IP ou PBX. Ce champ est obligatoire et la plage de valeurs est comprise entre 1 et 20. En règle générale, le numéro de poste comprend entre 3 et 7 chiffres. Si votre environnement téléphonique existant inclut des numéros de poste, vous devez spécifier un nombre de chiffres correspondant au nombre de chiffres que comportent ces postes lorsque vous créez le plan de numérotation de messagerie unifiée.
    
      - **Type de plan de numérotation**   Un Uniform Resource Identifier (URI) est une chaîne de caractères qui identifie ou nomme une ressource. Le but principal de cette identification est de permettre aux périphériques VoIP et aux PBX de communiquer avec d'autres périphériques sur un réseau à l'aide de protocoles spécifiques. Les URI sont définis selon des modèles qui définissent une syntaxe et un format spécifiques, ainsi que les protocoles pour l'appel. En termes simples, ce format est transmis à partir du PBX IP ou du PBX et le type de plan de numérotation que vous créez doit correspondre à ce format. Après avoir créé un plan de numérotation de messagerie unifiée, si vous voulez modifier le type du plan de numérotation, vous devez supprimer le plan de numérotation puis le recréer afin qu'il inclue le type de plan de numérotation correct. Vous pouvez sélectionner l'un des types de plans de numérotation suivants :
        
          - **Numéro de poste**   Il s'agit du type de plan de numérotation le plus courant. Les informations concernant l'appelant et le destinataire provenant de la passerelle VoIP ou IP Private Branch eXchange (PBX) sont affichées dans l'un des formats suivants : Tel:512345 ou 512345@\<*adresse IP*\>. Il s'agit du type par défaut pour les plans de numérotation.
        
          - **URI SIP**   Utilisez ce type de plan de numérotation si vous avez besoin d'un plan de numérotation de protocole URI SIP (Session Initiation Protocol) tel qu'un PBX IP qui prend en charge le routage SIP, un PBX compatible SIP ou si vous intégrez Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server et la messagerie unifiée. Les informations de partie appelante et appelée depuis la passerelle VoIP. Le PBX IP, le PBX compatible SIP, Communications Server 2007 R2 ou Lync Server est répertorié en tant qu'adresse SIP au format suivant : sip:\<*nom\_utilisateur*\>@\<*domaine* ou *adresse IP*\>:Port.
        
          - **E.164**   E.164 est un plan de numérotation international pour les systèmes téléphoniques publics ; chaque numéro attribué contient un code de pays, un code de destination national et un numéro d'abonné. Les informations sur l'appelant et l'appelé qui sont envoyées à partir de la passerelle VoIP et du PBX ou du PBX IP sont répertoriées au format suivant : Tél : +14255550123.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Après avoir créé un plan de numérotation, si vous voulez modifier le type du plan de numérotation, vous devez supprimer le plan de numérotation puis le recréer afin qu'il inclue le type de plan de numérotation correct.</td>
        </tr>
        </tbody>
        </table>
    
      - **Sécurité VoIP**   Cette liste déroulante permet de sélectionner le paramètre de sécurité du plan de numérotation de messagerie unifiée. Vous pouvez sélectionner l'un des paramètres de sécurité suivants pour le plan de numérotation :
        
          - **Non sécurisé(e)**   Par défaut, quand vous créez un plan de numérotation de messagerie unifiée, il est configuré pour ne pas chiffrer la signalisation SIP ou le trafic RTP. En mode non sécurisé, les serveurs Exchange associés au plan de numérotation de messagerie unifiée envoient et reçoivent des données en provenance de passerelles VoIP, de PBX IP, de contrôleurs de frontière de session (SBC) et d'autres serveurs Exchange en n'ayant pas recours au chiffrement. En mode non sécurisé, le canal de support RTP (Realtime Transport Protocol) et les informations de signalisation SIP ne sont pas chiffrés.
        
          - **Protection SIP**   Lorsque vous sélectionnez **Protection SIP**, seul le trafic de signalisation SIP est chiffré et les canaux de support RTP continuent d'utiliser le protocole TCP (Transmission Control Protocol), qui n'est pas chiffré. Avec Protection SIP (Sécurisé SIP), l'authentification TLS (Transport Layer Security) mutuelle est utilisée pour chiffrer le trafic de signalisation SIP et les données VoIP.
        
          - **Sécurisé**   Lorsque vous sélectionnez **Sécurisé**, le trafic de signalisation SIP et les canaux de signalisation RTP sont chiffrés. Le canal de signalisation sécurisé utilisant SRTP (Secure Realtime Transport Protocol) et le trafic de signalisation SIP utilisent également Mutual TLS pour chiffrer les données VoIP.

5.  **Codes de numérotation**   Cette page permet de configurer les codes de numérotation d'un plan de numérotation de messagerie unifiée. Vous pouvez configurer plusieurs paramètres de code de numérotation dans le plan de numérotation. notamment les options des appels entrants et sortants. Vous pouvez configurer ce qui suit :
    
      - **Codes de numérotation pour les appels sortants**   Ces paramètres vous permettent d'indiquer les codes de numérotation pour les appels sortants qui peuvent être passés par des utilisateurs à messagerie unifiée. Ces appels sortants sont des appels passés via Outlook Voice Access ou par message vocal.
        
          - **Code d'accès à une ligne extérieure**   Ce champ permet de taper un ou plusieurs numéros utilisés pour accéder à un numéro de téléphone extérieur pour les appels externes sortants. Ce numéro précèdera le numéro de téléphone composé. Ce numéro est également appelé code d'accès spécialisé. Ce champ peut recevoir 1 à 16 chiffres. Dans de nombreuses organisations, ce numéro est le 9. Par défaut, ce champ n'est pas renseigné.
            
            Ce paramètre est fréquemment utilisé dans les environnements de téléphonie où un PBX ou un PBX IP se trouve sur site ou est géré au sein d'une organisation. Il ne doit pas nécessairement être configuré si l'environnement de téléphonie de votre organisation est géré par une entreprise ou un fournisseur externe.
        
          - **Code d'accès à l'international**   Ce champ permet de taper le code numérique utilisé pour accéder aux numéros de téléphone internationaux pour les appels sortants. Ce numéro précèdera le numéro de téléphone composé. Par défaut, ce champ n'est pas renseigné. Ce champ peut recevoir 1 à 4 chiffres. Par exemple, le code d'accès à l'international est le 011 pour les États-Unis et le 00 pour l'Europe.
        
          - **Préfixe du numéro national**   Ce champ permet de taper le code numérique utilisé pour composer des numéros de téléphone à l'intérieur du pays mais dotés d'un indicatif régional différent. Ce numéro précèdera le numéro de téléphone composé. Par défaut, ce champ n'est pas renseigné. Ce champ peut recevoir 1 à 4 chiffres. Par exemple, le 0 est utilisé en Europe et le 1 en Amérique du Nord.
        
          - **Code Pays/Région**   Ce champ permet de taper le code numérique du pays/de la région à utiliser pour les appels sortants. Ce numéro précèdera le numéro de téléphone composé. Par défaut, ce champ n'est pas renseigné. Ce champ peut recevoir 1 à 4 chiffres. Par exemple, aux États-Unis, le code du pays/de la région est 1. Au Royaume-Uni, ce code est 44.
    
      - **Formats de numéro pour la numérotation entre des plans de numérotation de messagerie unifiée**   Ces paramètres permettent de configurer des appels entre des utilisateurs de plans de numérotation distincts quand ils passent des appels entre les plans de numérotation.
        
          - **Format du numéro dans le pays/la région**   Ce champ permet d'indiquer la manière dont les serveurs Exchange doivent composer le numéro de téléphone d'un utilisateur quand les utilisateurs dépendent d'un plan de numérotation différent mais ayant le même code de pays. Cette information est utilisée par des standards automatiques et lorsqu'un utilisateur de Outlook Voice Access recherche l'utilisateur dans l'annuaire et tente de l'appeler.
            
            Cette entrée se compose d'un préfixe de numéro et d'un nombre variable de caractères (par exemple, 020*xxxxxxx*). Pour déterminer le numéro de téléphone, la messagerie unifiée ajoutera les derniers caractères *x* du numéro de téléphone indiqué dans l'annuaire au préfixe indiqué.
        
          - **Format de numéro de téléphone international**   Ce champ permet d'indiquer la manière dont un serveur de messagerie unifiée doit composer le numéro de téléphone d'un utilisateur quand les utilisateurs dépendent de plans de numérotation différents ayant des codes de pays différents. Cette information est utilisée par un standard automatique et lorsqu'un utilisateur de Outlook Voice Access recherche l'utilisateur dans l'annuaire et tente de l'appeler.
            
            Cette entrée se compose d'un numéro de préfixe et d'un nombre variable de caractères (par exemple, 4420*xxxxxxx*). Pour déterminer le numéro de téléphone, la messagerie unifiée ajoutera les *x* derniers chiffres du numéro de téléphone spécifié dans l'annuaire au préfixe indiqué.
        
          - **Formats de numéros pour les appels entrants dans le même plan de numérotation**   Ce champ permet d'ajouter ou de supprimer un format de numéro pour les appels entrants qui sont passés entre des utilisateurs appartenant au même plan de numérotation. Ce champ accepte à la fois les chiffres et la lettre « x » comme caractère générique. Aucune autre lettre ne peut être utilisée dans ce champ.
            
            Pour les appels entrants appartenant au même plan de numérotation, ajoutez un format de numéro. Par exemple, pour ajouter un format de numéro pour des extensions à 5 chiffres, saisissez 142570xxxxx et cliquez sur ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour supprimer un format de numéro, cliquez sur ![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

6.  **Outlook Voice Access**   Cette page permet de configurer les paramètres d'Outlook Voice Access pour le plan de numérotation de messagerie unifiée. Outlook Voice Access permet aux utilisateurs d'accéder à leur boîte aux lettres pour récupérer leurs messages électroniques et vocaux, leurs contacts et leurs informations de calendrier au moyen d'un téléphone. Vous pouvez afficher ou configurer les paramètres suivants :
    
      - **Message d'accueil**   Ce champ en affichage seul indique le nom du fichier audio utilisé pour le message d'accueil.
        
          - **Message d'accueil par défaut**   Le message d'accueil est utilisé quand un utilisateur de Outlook Voice Access ou un autre appelant appelle le numéro Outlook Voice Access et effectue une recherche dans l'annuaire. Ce fichier audio est le message d'accueil par défaut d'un plan de numérotation de messagerie unifiée. Vous pouvez toutefois modifier ce message d'accueil afin de le personnaliser pour votre société ; par exemple, « Bienvenue sur Outlook Voice Access pour Contoso, Ltd. »
            
            Si vous décidez de personnaliser ce message d'accueil, vous devez commencer par enregistrer un message personnalisé, l'enregistrer en tant que fichier .wav, puis configurer le plan de numérotation pour qu'il utilise ce message d'accueil personnalisé. Le nom et le chemin d'accès du fichier ne doivent pas excéder 255 caractères.
            
            Vous pouvez ajouter un message d'accueil personnalisé en cliquant sur **Modifier**, puis sur **Parcourir** pour sélectionner un message d'accueil personnalisé enregistré précédemment et indiquer le fichier audio (.wav) à utiliser pour le message d'accueil. Si vous n'indiquez aucun fichier audio, les utilisateurs d'Outlook Voice Access entendent le message d'accueil par défaut : « Bienvenue, vous êtes connecté à Microsoft Exchange. »
    
      - **Message d'information automatique**   Lorsqu'il est activé, cet enregistrement facultatif est lu immédiatement après le message d'accueil pendant et en dehors des heures d'ouverture. Un message d'information automatique peut énoncer les stratégies de sécurité de l'organisation pour l'accès au système, par exemple : « Quand vous accédez à notre système via Outlook Voice Access, vous avez accepté les conditions de notre accord et toutes les stratégies de sécurité de notre organisation sont applicables. L'accès à notre système est surveillé et l'obtention d'un accès illégal sera passible de poursuites. » Un message d'information automatique peut également fournir les informations requises pour la conformité à la stratégie de l'entreprise, par exemple, « Les appels peuvent être analysés à des fins de formation. » Lorsqu'il est important que les appelants entendent le message d'information automatique dans son intégralité, celle-ci peut être configurée sur Interruption impossible.
        
        Par défaut, aucun message d'information automatique n'est configuré dans les plans de numérotation de messagerie unifiée. Pour activer un message d'information automatique et utiliser un fichier audio personnalisé spécifique à votre organisation, cliquez sur **Modifier**, puis sur **Parcourir**.
    
      - **Autoriser l'interruption de l'annonce**   Cochez cette case pour autoriser l'utilisateur d'Outlook Voice Access à interrompre le message d'information automatique. Cette option doit être activée si vos messages d'information automatiques sont longs. Les utilisateurs d'Outlook Voice Access pourraient être frustrés de ne pas pouvoir interrompre un long message d'information automatique pour accéder aux options fournies par le plan de numérotation de messagerie unifiée.
    
      - **Numéros Outlook Voice Access**   Ce champ permet d'ajouter un numéro de téléphone ou d'extension ou un URI SIP qu'un utilisateur d'Outlook Voice Access appellera pour accéder au système de messagerie vocale via Outlook Voice Access. Dans la plupart des cas, vous entrez un numéro de poste ou un numéro de téléphone externe. Toutefois, dans la mesure où ce champ accepte tous les caractères alphanumériques, un URI SIP peut être utilisé si vous utilisez un PBX IP, Office Communications Server 2007 R2 ou Microsoft Lync Server.
        
        Par défaut, lors de la création d'un plan de numérotation, aucun numéro Outlook Voice Access n'est défini. Pour permettre aux utilisateurs d'Outlook Voice Access d'appeler au sein d'Outlook Voice Access, vous devez configurer au moins un numéro de téléphone. Ce dernier ne peut pas comporter plus de 20 caractères alphanumériques.
        
        Lorsque vous configurez ce numéro sur le plan de numérotation, il s'affiche dans Microsoft OfficeOutlook 2007 ou les versions ultérieures et dans Outlook Web App pour accéder aux options de messagerie vocale.
        
        Pour ajouter un nouveau numéro Outlook Voice Access, saisissez le numéro dans la zone et cliquez sur ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour supprimer un numéro Outlook Voice Access, cliquez sur ![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

7.  **Paramètres**   Cette page permet de configurer des paramètres de plan de numérotation de messagerie unifiée. En configurant les paramètres de cette page, vous pouvez contrôler la manière dont les utilisateurs d'Outlook Voice Access et les appelants externes qui appellent un standard automatique associé au plan de numérotation localisent les utilisateurs de votre organisation, le codec audio utilisé pour les messages vocaux, le nombre d'échecs de connexion et les valeurs de délai. Vous pouvez configurer ce qui suit :
    
      - **Méthode principale pour rechercher des noms**   Cette liste permet de sélectionner la méthode principale permettant aux appelants de localiser un utilisateur lorsqu'ils accèdent au système.
        
        Par défaut, **Nom Prénom** est sélectionné. Ainsi, lorsque des appelants recherchent un utilisateur dans l'annuaire, ils entrent le nom puis le prénom de l'utilisateur.
        
        Lorsqu'un utilisateur Outlook Voice Access appelle pour un numéro Outlook Voice Access pour accéder à leur boîte aux lettres, un demandeur appelle un numéro Outlook Voice Access pour effectuer une recherche dans l'annuaire, ou un demandeur appelle pour un standard automatique lié à un plan de numérotation de messagerie unifiée, ils peuvent rechercher un utilisateur dans le répertoire en précisant leur nom ou pseudonyme.
        
        Vous devez sélectionner l'une des méthodes prises en charge pour être en mesure d'utiliser la méthode principale de numérotation selon le nom. Les méthodes suivantes sont prises en charge :
        
          - **Nom Prénom (méthode par défaut)**
        
          - **Prénom Nom**
        
          - **Adresse SMTP**
    
      - **Méthode secondaire de recherche des noms**   Cette liste permet de sélectionner la méthode secondaire permettant aux appelants de localiser un utilisateur lorsqu'ils accèdent au système.
        
        Par défaut, la méthode **Adresse SMTP** est sélectionnée. Lorsque des utilisateurs recherchent un utilisateur dans l'annuaire, ils entrent l'alias de messagerie ou l'adresse SMTP de l'utilisateur.
        
        Lorsqu'un utilisateur Outlook Voice Access appelle pour un numéro Outlook Voice Access pour accéder à leur boîte aux lettres, un demandeur appelle un numéro Outlook Voice Access pour effectuer une recherche dans l'annuaire, ou un demandeur appelle pour un standard automatique lié à un plan de numérotation de messagerie unifiée, ils peuvent rechercher un utilisateur dans le répertoire en précisant leur nom ou pseudonyme. Quand vous sélectionnez l'une de ces options, les appelants peuvent utiliser la méthode principale ou secondaire de recherche des noms pour localiser des utilisateurs dans l'annuaire.
        
        Vous n'êtes pas obligé de sélectionner l'une des quatre méthodes prises en charge. Toutefois, si vous ne sélectionnez pas de méthode secondaire de recherche d'utilisateurs, les appelants ne disposeront que d'une méthode pour rechercher un utilisateur. Les options suivantes sont disponibles :
        
          - **Nom Prénom**
        
          - **Prénom Nom**
        
          - **Adresse SMTP** (méthode par défaut)
        
          - **Aucun**
    
      - **Audio codec**   Cette liste permet de sélectionner le codec audio qui sera utilisé par le plan de numérotation. Lorsqu'un appelant contacte un utilisateur associé au plan de numérotation et laisse un message vocal, la messagerie unifiée utilise le codec audio que vous sélectionnez dans cette liste pour enregistrer les messages vocaux qui seront envoyés aux utilisateurs à messagerie vocale. Les codecs audio suivants sont pris en charge :
        
          - **MP3** (par défaut)
        
          - **WMA** (Windows Media Audio)
        
          - **G711** (Pulse Code Modulation (PCM) Linear)
        
          - **GSM** (Group System Mobile 06.10)
        
        Par défaut, le format MP3 est sélectionné. Il s'agit d'un format de fichier audio répandu qui permet de réduire considérablement la taille du fichier audio. Ce format est principalement utilisé par les lecteurs MP3 ou les périphériques audio personnels. Le codec audio MP3 est un type de codec multi-plateformes utilisé pour assurer la compatibilité avec de nombreux périphériques et téléphones mobiles, ainsi qu'avec différents systèmes d'exploitation d'ordinateurs.
        
        Le format WMA est utilisé car il constitue un format hautement compressé qui présente des propriétés de format d'excellente qualité. G.711 PCM Linear est un format de codec audio de qualité téléphonique, caractérisé par la compression la plus faible et la qualité la plus basse. Norme pour les services de téléphonie mobile numérique, GSM 06.10 est un format de codec audio utilisé par les opérateurs de téléphones mobiles.
        
        Si vous rencontrez des problèmes relatifs aux quotas de disque des utilisateurs, sélectionnez le codec audio WMA. La taille d'un fichier vocal enregistré au format .wma est environ deux fois moins importante que celle du même enregistrement vocal obtenu à l'aide des autres codecs audio.
    
      - **Poste opérateur**   Cette zone de texte permet d'entrer le numéro de téléphone ou un numéro de poste pour l'opérateur du plan de numérotation. Ce numéro est différent de celui d'une extension d'opérateur qui est configurée sur un standard automatique de messagerie unifiée. Cependant, vous pouvez entrer le même numéro de téléphone ou d'extension pour les deux types d'opérateurs.
        
        Vous pouvez configurer ce paramètre pour transférer des appels à un standard automatique (le cas échéant), un opérateur humain, des numéros de téléphone externes ou des numéros de poste.
        
        Lorsqu'un appelant qui recourt au clavier du téléphone appuie sur la touche 0 ou prononce « réception » ou « opérateur », ou lorsque le seuil du **Nombre d'erreurs de saisie avant la déconnexion** est dépassé, l'appelant est transféré au numéro de téléphone ou d'extension indiqué dans cette zone de texte.
        
        Ce numéro de téléphone peut être un numéro externe à l'organisation ou un numéro de poste interne. Par exemple, si le numéro de poste du réceptionniste ou de l'opérateur est 81964 et que votre organisation dispose d'un seul plan de numérotation, entrez 81964.
        
        Par défaut, ce paramètre n'est pas renseigné. Si vous n'entrez pas de valeur dans cette zone de texte, la fonction de transfert des appels à l'opérateur est désactivée ; les appelants sont poliment déconnectés, personne n'étant en mesure de répondre à l'appel.
        
        nous vous recommandons de renseigner cette zone de texte avec un numéro de téléphone permettant de mettre les appelants en relation avec un opérateur s'ils ne parviennent pas à localiser un utilisateur donné dans l'annuaire.
    
      - **Nombre d'échecs de connexion avant déconnexion**   Cette zone de texte permet d'entrer le nombre d'échecs de tentative d'ouverture de session successifs autorisés avant la déconnexion d'un appelant.
        
        La valeur de ce paramètre est comprise entre 1 et 20. La définition d'une valeur trop basse peut incommoder les utilisateurs. Pour la plupart des organisations, cette valeur doit être définie par défaut sur trois tentatives.
    
      - **Délais et tentatives**   Ces paramètres s'appliquent aux utilisateurs d'Outlook Voice Access et aux appelants externes qui tentent d'accéder à un standard automatique de messagerie unifiée.
        
          - **Durée d'appel maximale (minutes)**   Cette zone de texte permet d'entrer le nombre maximal de minutes correspondant à la durée pendant laquelle un appel entrant peut être connecté au système sans être transféré à un numéro de poste valide avant qu'il ne soit mis fin à l'appel. Pour la plupart des organisations, cette valeur doit être définie par défaut sur 30 minutes.
            
            Ce paramètre s'applique à tous les types d'appels. notamment les appels Outlook Voice Access entrants, les appels vocaux internes à l'organisation, ainsi que les appels vocaux et les appels de télécopie entrants externes à l'organisation.
            
            La valeur de ce paramètre est comprise entre 10 et 120. La définition d'une valeur trop basse peut entraîner la déconnexion des appels entrants avant que ceux-ci ne soient terminés. Par exemple, si votre organisation reçoit régulièrement des messages de télécopie volumineux, vous pouvez envisager de définir une valeur plus élevée que la valeur par défaut, de façon à recevoir toutes les pages des messages de télécopie.
        
          - **Durée d'enregistrement maximale (minutes)**   Cette zone de texte permet d'entrer le nombre maximal de minutes correspondant à la durée autorisée pour chaque enregistrement vocal lorsqu'un appelant laisse un message vocal. Pour la plupart des organisations, cette valeur doit être définie par défaut sur 20 minutes.
            
            La valeur de ce paramètre est comprise entre 1 et 100. La définition d'une valeur trop basse peut entraîner la déconnexion des messages vocaux longs avant que ceux-ci ne soient terminés. La définition d'une valeur très élevée permet aux utilisateurs d'enregistrer des messages vocaux relativement longs dans leur boîte de réception.
            
            Il s'agit d'un paramètre important si vous avez mis en place des quotas de disque stricts pour les utilisateurs. Cette valeur doit être inférieure à celle définie pour le paramètre **Durée d'appel maximale (minutes)**.
        
          - **Délai d'inactivité d'enregistrement (secondes)**   Cette zone de texte permet d'entrer le nombre de secondes correspondant à la durée de silence autorisée par le système lors de l'enregistrement d'un message vocal avant qu'il ne soit mis fin à l'appel. Pour la plupart des organisations, cette valeur doit être définie par défaut sur 5 secondes.
            
            La valeur de ce paramètre est comprise entre 2 et 10. La définition d'une valeur trop basse peut entraîner la déconnexion des appelants par le système avant que ceux-ci n'aient eu le temps de laisser leur message vocal. La définition d'une valeur très élevée autorise les silences relativement longs dans les messages vocaux.
        
          - **Nombre d'erreurs de saisie avant la déconnexion**   Cette zone de texte permet de configurer le nombre de saisies de choix de menu incorrectes autorisées de la part d'un appelant avant qu'il ne soit déconnecté. Pour la plupart des organisations, cette valeur doit être définie par défaut sur trois tentatives. Il s'agit d'un paramètre important pour les plans de numérotation de messagerie unifiée avec reconnaissance vocale.
            
            Des données sont incorrectes, par exemple, lorsqu'un appelant demande un numéro de poste introuvable dans le système, lorsque le système ne peut pas localiser le numéro de poste de l'utilisateur auquel transférer l'appel, ou lorsque l'appelant sélectionne une option de menu non valide.
            
            La valeur de ce paramètre peut être comprise entre 1 et 20. La définition d'une valeur trop basse peut entraîner une déconnexion prématurée de l'appelant.
    
      - **Langue audio**   Cette liste permet d'indiquer la langue par défaut pour les utilisateurs d'Outlook Voice Access. Ce paramètre ne s'applique pas à la configuration linguistique sur un standard automatique de messagerie unifiée. Vous pouvez définir la même langue ou une langue différente pour Outlook Voice Access et pour un standard automatique de messagerie unifiée. Quand un utilisateur appelle un utilisateur associé à un plan de numérotation, la langue audio est la langue par défaut utilisée par l'opérateur dont la voix a été enregistrée. Les messages système diffusés aux appelants sont également lus dans cette langue. La langue choisie dans le plan de numérotation de messagerie unifiée est utilisée dans différentes circonstances : pour lire les éléments de calendrier, de messagerie vocale et de courrier électronique, pour prononcer le nom de l'utilisateur si aucun message d'accueil personnel n'a été enregistré, pour transcrire un message vocal à l'aide de la fonctionnalité d'aperçu du message vocal et pour permettre le bon fonctionnement de la reconnaissance vocale.
        
        Pour les déploiements locaux, l'ajout de langues supplémentaires permet à Outlook Voice Access d'utiliser une langue autre que l'anglais (États-Unis). Par exemple, si un utilisateur d'Outlook Voice Access appelle avec un numéro Outlook Voice Access depuis un téléphone fixe, il est accueilli par une voix d'opérateur préenregistrée s'exprimant en anglais. Même si l'utilisateur sélectionne une autre langue dans Outlook Web App, telle que le français, les menus sont toujours lus en anglais. Pour que l'utilisateur puisse entendre les menus préenregistrés de l'opérateur en français, vous devez installer le module linguistique approprié.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Toutes les langues sont disponibles pour Exchange Online.</td>
        </tr>
        </tbody>
        </table>


8.  **Règles de numérotation**   Cette page permet d'indiquer des règles de numérotation pour des appels nationaux, régionaux et internationaux passés par des utilisateurs à messagerie unifiée. Chaque entrée définie sur la règle de numérotation détermine les types d'appels que les utilisateurs d'un groupe de numérotation spécifique peuvent passer. Une fois que vous avez utilisé la fenêtre **Règles de numérotation** pour configurer des règles de numérotation, vous devez configurer le plan de numérotation, une stratégie de boîte aux lettres de messagerie unifiée ou un standard automatique de messagerie unifiée de sorte que la règle de numérotation appropriée soit utilisée. Lorsque vous avez configuré la stratégie de boîte aux lettres de messagerie unifiée pour qu'elle utilise un groupe de règles de numérotation, les restrictions de numérotation configurées s'appliquent à tous les utilisateurs à messagerie unifiée qui sont associés à la stratégie de boîte aux lettres de messagerie unifiée. Par exemple, vous pouvez configurer un groupe de règles de numérotation pour lequel les utilisateurs associés au plan de numérotation n'ont pas besoin de composer un code d'accès à une ligne extérieure lorsqu'ils appellent un numéro de téléphone national/régional. Vous pouvez configurer ce qui suit :
    
      - **Règles de numérotation nationales/régionales**   Cette zone permet d'ajouter, de supprimer ou de modifier des groupes de règles de numérotation nationale/régionale qui sont utilisés par les stratégies de boîte aux lettres de messagerie unifiée. Pour créer une règle de numérotation, cliquez sur ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour modifier une règle de numérotation existante, cliquez sur ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). Pour supprimer une règle de numérotation, cliquez sur ![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression"). Quand vous créez une règle de numérotation, ajoutez les informations suivantes dans la page **Nouvelle règle de numérotation** :
        
          - **Nom de la règle de numérotation**   Utilisez cette zone de texte pour entrer le nom de la règle de numérotation que vous créez. Vous pouvez utiliser le même nom pour collecter plusieurs règles dans un groupe, puis activez-les ou désactivez-les sous **Autorisation de numérotation**. Ce nom peut contenir jusqu'à 32 caractères.
        
          - **Type de numéro à transformer (masque de numéro)**   Utilisez cette zone de texte pour saisir le type de numéro à transformer avant de composer, par exemple, 91425xxxxxxx. Si un utilisateur saisit un numéro qui correspond à ce type, la messagerie unifiée transformera le numéro composé en un numéro composé avant de passer l'appel. Vous ne pouvez entrer que des chiffres et le caractère générique, « x ».
        
          - **Numéro composé**   Cette zone de texte permet de saisir le numéro à composer qui correspond au modèle de numéro que vous avez défini dans **Modèle de numéro à transformer (masque de numéro)**. Le numéro composé est utilisé pour déterminer la chaîne de numérotation réelle envoyée à la passerelle VoIP ou au PBX IP. Ce numéro peut différer du numéro obtenu par la messagerie unifiée pour l'appel sortant. Toutefois, vous pouvez également configurer votre PBX ou PBX IP afin d'omettre l'indicatif pour les appels locaux, et le configurer pour des plans de numérotation de messagerie vocale privée. Tout caractère générique *x* dans la chaîne de numérotation est remplacé par les chiffres du numéro d'origine correspondant au masque de numéro dans l'entrée de règle de numérotation. Un numéro composé valide est, par exemple, 9*xxxxxxx*. Ce champ ne peut contenir que des chiffres et la lettre *x*.
        
          - **Commentaire**   Cette zone de texte permet d'entrer un commentaire ou une description pour l'entrée de règle de numérotation que vous ajoutez ou modifiez. Par défaut, cette zone de texte est vide.
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>Si vous intégrez avec Office Communications Server 2007 R2 ou Microsoft Lync Server, vous constaterez probablement qu'il n'est pas nécessaire de configurer des règles de numérotation ou des groupes de règles de numérotation dans la messagerie unifiée. Office Communications Server 2007 R2 et Lync Server sont conçus pour acheminer des appels (routage) et convertir des numéros pour les utilisateurs de votre organisation, et procèdent de même lorsque les appels sont effectués pour le compte des utilisateurs.</td>
            </tr>
            </tbody>
            </table>
    
      - **Règles internationales**   Cette zone de texte permet d'ajouter, de supprimer ou de modifier des groupes de règles de numérotation internationale utilisés par des stratégies de boîte aux lettres de messagerie unifiée.
        
          - **Nom de la règle de numérotation**   Utilisez cette zone de texte pour entrer le nom de la règle de numérotation que vous créez. Vous pouvez utiliser le même nom pour collecter plusieurs règles dans un groupe, puis activez-les ou désactivez-les sous **Autorisation de numérotation**. Ce nom peut contenir jusqu'à 32 caractères.
        
          - **Type de numéro à transformer (masque de numéro)**   Utilisez cette zone de texte pour saisir le type de numéro à transformer avant de composer, par exemple, 91425xxxxxxx. Si un utilisateur saisit un numéro qui correspond à ce type, la messagerie unifiée transformera le numéro composé en un numéro composé avant de passer l'appel. Vous ne pouvez entrer que des chiffres et le caractère générique, « x ».
        
          - **Numéro composé**   Cette zone de texte permet de saisir le numéro à composer qui correspond au modèle de numéro que vous avez défini dans **Modèle de numéro à transformer (masque de numéro)**. Le numéro composé est utilisé pour déterminer la chaîne de numérotation réelle envoyée à la passerelle VoIP ou au PBX IP. Ce numéro peut différer du numéro obtenu par la messagerie unifiée pour l'appel sortant. Toutefois, vous pouvez également configurer votre PBX ou PBX IP afin d'omettre l'indicatif pour les appels locaux, et le configurer pour des plans de numérotation de messagerie vocale privée. Tout caractère générique *x* dans la chaîne de numérotation est remplacé par les chiffres du numéro d'origine correspondant au masque de numéro dans l'entrée de règle de numérotation. Un numéro composé valide est, par exemple, 9*xxxxxxx*. Ce champ ne peut contenir que des chiffres et la lettre *x*.
        
          - **Commentaire**   Cette zone de texte permet d'entrer un commentaire ou une description pour l'entrée de règle de numérotation que vous ajoutez ou modifiez. Par défaut, cette zone de texte est vide.
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>Dans le cadre de déploiements locaux, si vous procédez à une intégration avec Office Communications Server 2007 R2 ou Microsoft Lync Server, vous constaterez probablement qu'il n'est pas nécessaire de configurer des règles de numérotation ou des groupes de règles de numérotation dans la messagerie unifiée. Office Communications Server 2007 R2 ou Lync Server est conçu pour acheminer des appels (routage) et convertir des numéros pour les utilisateurs de votre organisation, et procèdent de même lorsque les appels sont effectués pour le compte des utilisateurs.</td>
            </tr>
            </tbody>
            </table>


9.  **Autorisation de numérotation**   Cette page permet de sélectionner des règles de numérotation pour des utilisateurs qui appellent un numéro Outlook Voice Access configuré sur un plan de numérotation de messagerie unifiée. Vous pouvez restreindre le type d'appels établis par des appelants lorsqu'un utilisateur non authentifié ou un utilisateur Outlook Voice Access appelle un numéro Outlook Voice Access configuré sur un plan de numérotation en configurant des groupes de règles de numérotation et des restrictions de numérotation. Vous pouvez configurer ce qui suit :
    
      - **Appels du plan de numérotation de messagerie unifiée**   Cochez cette case pour permettre aux utilisateurs qui appellent un numéro Outlook Voice Access configuré sur un plan de numérotation de passer ou de transférer des appels vers un numéro d'extension associé à un utilisateur à messagerie unifiée appartenant au même plan de numérotation. Par défaut, ce paramètre est activé.
        
        Lorsque vous désactivez ce paramètre, les utilisateurs qui appellent un numéro Outlook Voice Access ne peuvent pas passer ou transférer des appels vers des utilisateurs sans messagerie unifiée, vers d'autres numéros d'extension ou vers des utilisateurs à messagerie unifiée associés au même plan de numérotation. Cela est dû au fait que le paramètre **Autoriser les appels vers toutes les extensions** est désactivé par défaut.
    
      - **Autoriser les appels vers toutes les extensions**   Lorsque ce paramètre est désactivé, les utilisateurs qui appellent un numéro Outlook Voice Access sur le plan de numérotation ne peuvent pas établir d'appels vers des utilisateurs sans messagerie unifiée, ou vers d'autres numéros d'extension non associés à un utilisateur à messagerie unifiée. Toutefois, ils peuvent établir ou transférer un appel vers un numéro de poste associé à un utilisateur à extension messagerie unifiée. Cela est dû au fait que le paramètre **Appels appartenant au même plan de numérotation de messagerie unifiée** est activé par défaut. Par défaut, le paramètre **Autoriser les appels vers toutes les extensions** est désactivé.
        
        Lorsque ce paramètre est activé, les utilisateurs qui appellent un numéro Outlook Voice Access configuré sur le plan de numérotation peuvent établir des appels vers des utilisateurs sans messagerie unifiée, vers d'autres numéros d'extension non associés à un utilisateur à messagerie unifiée, et vers des utilisateurs à messagerie unifiée. Cela est dû au fait que le paramètre **Appels appartenant au même plan de numérotation de messagerie unifiée** est activé par défaut.
        
        Vous pouvez activer ce paramètre dans un environnement où tous les utilisateurs ne sont pas activés pour la messagerie unifiée. Ce paramètre est également utile si vous voulez autoriser les utilisateurs qui appellent un numéro Outlook Voice Access configuré sur un plan de numérotation à appeler des numéros d'extension qui ne sont pas associés.
    
      - **Groupes de règles de numérotation nationale autorisé**   Cette section permet d'ajouter ou de supprimer des règles de numérotation nationale/régionale autorisées. Par défaut, aucune règle de numérotation nationale/régionale n'est configurée dans les plans de numérotation de messagerie unifiée.
        
        Des groupes de règles de numérotation nationale/régionale sont utilisés pour autoriser ou limiter les numéros de téléphone, dans un pays ou une région, qu'un utilisateur ayant appelé le numéro d'accès d'abonné peut composer. Cela permet d'empêcher des appels et des frais téléphoniques superflus ou non autorisés.
        
        Pour ajouter des règles de numérotation nationale/régionale, vous devez commencer par créer la règle de numérotation nationale/régionale appropriée dans le plan de numérotation, puis ajouter les entrées de règle de numérotation appropriées dans la règle de numérotation. Après avoir créé les groupes de règles de numérotation appropriés pour le plan de numérotation, vous devez les ajouter à la liste des autorisations de numérotation sous l'onglet **Autorisation de numérotation** sur le plan de numérotation.
        
        Vous pouvez utiliser des groupes de règles de numérotation nationale/régionale pour autoriser ou bloquer l'accès à des numéros de téléphone à l'intérieur d'un pays ou d'une région. Ceci s'applique à tous les utilisateurs qui ont appelé un numéro d'Outlook Voice Access.
    
      - **Groupes de règles de numérotation internationale autorisés**   Cette section permet d'ajouter ou de supprimer des règles de numérotation internationale autorisées. Par défaut, aucune règle de numérotation internationale n'est configurée dans les plans de numérotation de messagerie unifiée.
        
        Des règles de numérotation internationale sont utilisées pour autoriser ou limiter les numéros de téléphone extérieurs à un pays ou une région qu'un utilisateur ayant appelé le numéro Outlook Voice Access peut composer. Cela permet d'empêcher des appels et des frais téléphoniques superflus ou non autorisés.
        
        Pour ajouter des groupes de règles de numérotation internationale, vous devez commencer par créer les règles de numérotation internationale appropriées dans le plan de numérotation, puis ajouter les entrées de règles de numérotation appropriées. Après avoir créé les groupes de règles de numérotation appropriés pour le plan de numérotation, vous devez les ajouter à la liste des autorisations de numérotation sous l'onglet **Autorisation de numérotation** sur le plan de numérotation.
        
        Vous pouvez utiliser des groupes de règles de numérotation internationale pour autoriser ou bloquer l'accès à des numéros de téléphone à l'extérieur d'un pays ou d'une région. Ceci s'applique à tous les utilisateurs qui ont appelé un numéro d'Outlook Voice Access.

10. **Transférer et rechercher**   Cette page permet de configurer les fonctionnalités de plan de numérotation de messagerie unifiée. Il est possible de configurer plusieurs fonctionnalités. dont le transfert d'appels, l'envoi de messages vocaux et la recherche d'utilisateurs. Vous pouvez configurer ce qui suit :
    
      - **Autoriser les appelants à**   Ces paramètres permettent de déterminer de quelle manière des utilisateurs qui appellent un numéro Outlook Voice Access peuvent contacter des utilisateurs. Vous pouvez configurer ce qui suit :
        
          - **Transférer aux utilisateurs**   Cochez cette case pour permettre aux utilisateurs d'Outlook Voice Access de transférer des appels à des utilisateurs. Par défaut, cette option est activée. Les utilisateurs associés au plan de numérotation peuvent ainsi transférer les appels à des utilisateurs appartenant au même plan de numérotation de messagerie unifiée. Après avoir activé cette case à cocher, vous pouvez définir le groupe d'utilisateurs auxquels les appelants peuvent transférer des appels en sélectionnant l'option appropriée sous la section **Autoriser les appelants à rechercher des utilisateurs par nom ou alias** de cette page.
            
            Si vous désactivez cette option, Outlook Voice Access ne permettra pas aux appelants d'être transférés à des utilisateurs du plan de numérotation quels qu'ils soient.
        
          - **Laisser des messages vocaux sans faire sonner le téléphone de l'utilisateur**   Cochez cette case pour permettre aux appelants d'envoyer des messages vocaux à des utilisateurs. Par défaut, cette option est activée. Les utilisateurs Outlook Voice Access associés au plan de numérotation peuvent ainsi envoyer des messages vocaux à des utilisateurs appartenant au même plan de numérotation de messagerie unifiée. Après avoir activé cette case à cocher, vous pouvez définir le groupe d'utilisateurs auxquels les appelants peuvent transférer des appels en sélectionnant l'option appropriée sous la section **Autoriser les appelants à rechercher des utilisateurs par nom ou alias** de cette page.
            
            Si vous désactivez cette option, Outlook Voice Access ne permettra pas aux appelants d'envoyer un message vocal via une invite du système.
    
      - **Autoriser les appelants à rechercher des utilisateurs par leur nom ou leur alias**   Ces options permettent de déterminer un regroupement d'utilisateurs à rechercher. Par défaut, l'option **Dans ce plan de commutation seulement** est sélectionnée. Toutefois, vous pouvez modifier le regroupement d'utilisateurs. Choisissez l'une des options suivantes :
        
          - **Dans ce plan de numérotation uniquement**   Cette option permet d'appeler des utilisateurs qui se connectent à Outlook Voice Access pour localiser et contacter des utilisateurs appartenant au plan de numérotation dont ils sont membres.
        
          - **Dans toute l'organisation**   Cette option permet d'autoriser les appelants qui se connectent à Outlook Voice Access à localiser et contacter tout utilisateur répertorié dans l'ensemble de l'organisation. y compris tous les utilisateurs à boîte aux lettres ou à messagerie unifiée dans l'ensemble des plans de numérotation.
        
          - **Uniquement sur ce standard automatique**   Cette liste permet d'autoriser les utilisateurs d'Outlook Voice Access à se connecter à un standard automatique de messagerie unifiée, puis à se connecter éventuellement à un autre standard automatique que vous avez configuré. Vous devez créer ce standard automatique pour permettre aux appelants d'être transférés à un autre standard automatique spécifié.
        
          - **Uniquement pour cette extension**   Utilisez cette option pour permettre aux utilisateurs d'Outlook Voice Access de se connecter à un numéro de poste que vous indiquez dans le champ correspondant à cette option. Ce champ accepte uniquement des caractères numériques. Le nombre de chiffres que vous définissez dans ce champ doit correspondre au nombre de chiffres configuré dans le plan de numérotation associé au standard automatique.
    
      - **Informations à inclure pour les utilisateurs du même nom**   Ce champ permet de sélectionner la manière dont le plan de numérotation différencie des utilisateurs portant le même nom ou des noms similaires. Lorsqu'un appelant est invité à entrer des lettres ou à prononcer le nom d'une personne pour trouver un utilisateur dans l'organisation, il arrive parfois que plusieurs noms correspondent à la saisie de l'appelant. Si deux utilisateurs portent le même nom, la messagerie unifiée utilisera l'une des méthodes suivantes pour ajouter des informations supplémentaires au nom d'utilisateur. Par exemple, si vous sélectionnez **Service**, quand un utilisateur d'Outlook Voice Access appelle Outlook Voice Access et recherche un utilisateur et qu'il existe des noms identiques ou similaires dans l'annuaire, l'appelant entendra le nom et le service de l'utilisateur. Par exemple :
        
        1.  Système : « Bienvenue dans Outlook Voice Access. Veuillez entrer votre code confidentiel et appuyer sur la touche dièse. »
        
        2.  L'appelant saisit son code confidentiel suivi de la touche \#.
        
        3.  Système : « Dites "Messagerie vocale", "Messagerie électronique", "Calendrier", "Contacts personnels", "Annuaire" ou "Paramètres personnels". »
        
        4.  Appelant : « Annuaire »
        
        5.  Système : « Recherche dans l'annuaire. Veuillez noter que, pour les tâches suivantes, vous devez utiliser le clavier de votre téléphone au lieu de parler. Utilisez le clavier pour épeler le nom de la personne que vous cherchez en commençant par le nom de famille, ou, pour épeler la première partie de son adresse de messagerie, appuyez deux fois sur la touche dièse, si vous connaissez l'extension, appuyez sur la touche dièse. »
        
        6.  L'appelant utilise le clavier et saisit « smithtony » avant d'appuyer sur la touche \#.
        
        7.  Système : « Pour Tony Smith, recherche, appuyez sur 1. Pour Tony Smith, administration, appuyez sur 2. Pour Tony Smith, support technique, appuyez sur 3. »
        
        8.  L'appelant appuie sur la touche appropriée du clavier et l'appel est transféré à l'utilisateur.
        
        Par défaut, tous les standards automatiques de messagerie unifiée associés à ce plan de numérotation héritent de ce paramètre. Vous pouvez toutefois modifier ce paramètre sur chaque standard automatique de messagerie unifiée que vous créez.
        
        Sélectionnez l'une des méthodes suivantes pour transmettre des informations supplémentaires aux appelants afin de les aider à sélectionner l'utilisateur approprié dans l'organisation :
        
          - **Aucune**   Aucune information supplémentaire n'est fournie lorsque plusieurs correspondances sont relevées. Par défaut, cette méthode est sélectionnée.
        
          - **Titre**   Le système de messagerie vocale inclut le titre de chaque utilisateur lorsque des correspondances sont relevées.
        
          - **Service**   Le système de messagerie vocale inclut le service de chaque utilisateur lorsque des correspondances sont relevées.
        
          - **Emplacement**   Le système de messagerie vocale inclut l'emplacement de chaque utilisateur lorsque des correspondances sont relevées.
        
          - **Demander un alias**   Le système de messagerie vocale invite l'appelant à indiquer l'alias de l'utilisateur.

11. Une fois configurés les paramètres voulus, cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les paramètres d'un plan de numérotation de messagerie unifiée

Cet exemple montre comment configurer un plan de numérotation de messagerie unifiée nommé `MyDialPlan` afin qu'il utilise le 9 comme code d'accès à une ligne extérieure.

    Set-UMDialplan -Identity MyDialPlan -OutsideLineAccessCode 9

Cet exemple montre comment configurer un plan de numérotation de messagerie unifiée nommé `MyDialPlan` afin qu'il utilise un message d'accueil.

    Set-UMDialplan -Identity MyDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename welcome.wav

Cet exemple montre comment configurer un plan de numérotation de messagerie unifiée nommé `MyDialPlan` avec des règles de numérotation.

    $csv=import-csv "C:\MyInCountryGroups.csv"
    Set-UMDialPlan -Identity MyDialPlan -ConfiguredInCountryGroups $csv
    Set-UMDialPlan -Identity MyDialPlan -AllowedInCountryGroups "local, long distance"

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher les paramètres d'un plan de numérotation de messagerie unifiée

Dans cet exemple, une liste de tous les plans de numérotation de messagerie unifiée est affichée.

    Get-UMDialplan

Dans cet exemple, une liste mise en forme de tous les paramètres d'un plan de numérotation de messagerie unifiée intitulée `MyUMDialPlan` est affichée.

    Get-UMDialplan -Identity MyUMDialPlan | Format-List

