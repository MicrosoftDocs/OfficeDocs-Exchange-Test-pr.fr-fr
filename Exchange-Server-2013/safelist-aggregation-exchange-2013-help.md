---
title: 'Agrégation de listes fiables: Exchange 2013 Help'
TOCTitle: Agrégation de listes fiables
ms:assetid: f05430a0-0405-4b65-a18d-18c9e86a13c4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125168(v=EXCHG.150)
ms:contentKeyID: 50479508
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agrégation de listes fiables

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-09-30_

Dans Microsoft Exchange Server 2013, le terme *agrégation de listes fiables* désigne la fonction de blocage du courrier indésirable partagée par Microsoft Outlook et Exchange. Cette fonctionnalité collecte les données des listes de blocage du courrier indésirable des destinataires sûrs, des expéditeurs sûrs, des expéditeurs bloqués et des informations de contact que les utilisateurs Outlook configurent ; elle met ces données à disposition des agents Exchange de blocage du courrier indésirable.

Lorsque vous activez et configurez correctement l’agrégation de listes fiables, l’agent de filtrage du contenu transmet les messages électroniques sûrs à la boîte aux lettres de l’entreprise sans traitement supplémentaire. Les messages électroniques que les utilisateurs Outlook reçoivent de contacts que ces utilisateurs ont ajoutés à leur liste des destinataires sûrs ou expéditeurs sûrs Outlook ou identifiés par l’agent de filtrage du contenu comme fiables. Un *contact* Outlook est une personne, à l’intérieur ou l’extérieur de l’organisation de l’utilisateur, sur laquelle l’utilisateur peut enregistrer divers types d’informations telles que des adresses électroniques et postales, des numéros de téléphone et de fax, et des adresses URL de pages Web.

Dans Exchange 2013, l’agrégation de listes fiables permet également à l’agent de filtrage des expéditeurs de bloquer les messages entrants de la liste des expéditeurs bloqués par destinataire.

L’agrégation de listes fiables permet de réduire les instances de faux positifs dans le filtrage du courrier indésirable exécuté par Exchange. Dans le contexte de filtrage du courrier indésirable, un *faux positif* se produit quand un filtre de courrier indésirable identifie incorrectement comme du courrier indésirable un message provenant d’un expéditeur légitime.

Pour les organisations qui filtrent quotidiennement des centaines de milliers de messages en provenance d’Internet, même un faible pourcentage de faux positifs signifie que les utilisateurs ne reçoivent pas de nombreux messages identifiés incorrectement comme courrier indésirable si ces messages sont mis en quarantaine ou supprimés.

L'agrégation de listes fiables est probablement la manière la plus efficace de réduire les faux positifs. Dans Outlook 2010 ou les versions plus récentes, les utilisateurs peuvent créer des *listes d’expéditeurs sûrs*. Les listes des expéditeurs sûrs spécifient une liste de noms de domaine et d’adresses électroniques dont l’utilisateur Outlook veut recevoir des messages. Par défaut, les adresses électroniques figurant dans les Contacts Outlook et dans la liste d’adresses globale Exchange sont incluses dans cette liste. Par défaut, Outlook ajoute tous les contacts externes auxquels l’utilisateur envoie du courrier à la liste des expéditeurs sûrs.

**Contenu de cette rubrique**

Information stored in the Outlook user's safelist collection

How Exchange uses the safelist collection

Hashing of safelist collection entries

Enabling safelist aggregation

## Informations conservées dans l’ensemble de listes fiables d’un utilisateur Outlook

Une *collection de listes fiables* correspond aux données combinées provenant de la liste des expéditeurs approuvés, de la liste des destinataires approuvés, de la liste des expéditeurs proscrits et des contacts externes de l'utilisateur. Ces données sont stockées dans Outlook et dans la boîte aux lettres Exchange.

Les types d'informations suivants sont stockés dans une collection de listes fiables de l'utilisateur Outlook :

  - **Expéditeurs approuvés et destinataires approuvés**   L'en-tête De du message indique un expéditeur. Le champ À du message électronique indique un destinataire. Les expéditeurs et les destinataires approuvés sont représentés par des adresses SMTP complètes, telles que masato@contoso.com. Les utilisateurs Outlook peuvent ajouter des expéditeurs et des destinataires à leurs listes sécurisées.

  - **Expéditeurs bloqués**   Les utilisateurs peuvent bloquer les expéditeurs indésirables en les ajoutant à leurs listes des expéditeurs bloqués, de la même manière qu'ils autorisent les expéditeurs approuvés.

  - **Domaine fiable**   Le domaine correspond à la partie d'une adresse SMTP qui suit le symbole @. Par exemple, contoso.com constitue le domaine dans l’adresse masato@contoso.com. Les utilisateurs Outlook peuvent ajouter des domaines d’envoi à leurs listes sécurisées.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Par défaut, Exchange n'inclut pas les domaines lors de l'agrégation de listes fiables. Toutefois, vous pouvez configurer une agrégation de listes fiables pour inclure les données de domaine autorisé pour les agents de blocage du courrier indésirable. Pour plus d’informations, consultez <a href="configure-content-filtering-to-use-safe-domain-data-exchange-2013-help.md">Configurer le filtrage de contenu pour utiliser les données de domaine autorisé</a>.</td>
    </tr>
    </tbody>
    </table>


  - **Contacts externes**   Deux types de contacts externes peuvent être intégrés dans l'agrégation de listes fiables. Le premier type de contacts externes inclut les contacts auxquels les utilisateurs Outlook ont envoyé du courrier. Cette classe de contact est ajoutée à la liste des expéditeurs sûrs uniquement si l’utilisateur Outlook sélectionne l’option correspondante dans les paramètres de courrier indésirable d’Outlook 2007.
    
    Le deuxième type de contacts externes inclut les contacts Outlook des utilisateurs. Les utilisateurs peuvent ajouter ou importer ces contacts dans Outlook. Cette classe de contact est ajoutée à la liste des expéditeurs sûrs uniquement si l’utilisateur Outlook sélectionne l’option correspondante dans les paramètres de filtrage du courrier indésirable d’Outlook 2010 ou d’Outlook 2007.

Retour au début

## Utilisation de l’ensemble de listes fiables par Exchange

La collection de listes fiables est stockée sur le serveur de boîtes aux lettres de l'utilisateur. Un utilisateur peut inclure jusqu'à 1 024 entrées uniques dans un ensemble de listes fiables. Exchange 2013 inclut un Assistant de boîte aux lettres, appelé Assistant d’options de courrier indésirable, qui analyse les modifications de l’ensemble de listes fiables pour vos boîtes aux lettres. Il réplique ces modifications dans Active Directory où l’ensemble de listes fiables est stocké sur chaque objet utilisateur. Lorsque l’ensemble de listes fiables est stockée sur l’objet utilisateur dans Active Directory, il est associé à la fonction de blocage du courrier indésirable d’Exchange 2013 et optimisé pour un stockage et une réplication réduits. Exchange utilise les données de l’ensemble de listes fiables pendant le filtrage du contenu. Si vous avez abonné un serveur de transport Edge dans votre réseau de périmètre, le service Microsoft Exchange EdgeSync réplique l’ensemble de listes fiables dans l’instance AD LDS (Active Directory Lightweight Directory Services) sur le serveur de transport Edge.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Bien que les informations des destinataires sûrs soient conservées dans Outlook et qu'il soit possible de les associer à l’ensemble de listes fiables, le filtrage du contenu n'agit pas sur elles.</td>
</tr>
</tbody>
</table>


Retour au début

## Hachage des entrées de l’ensemble de listes fiables

Les entrées d'une collection de listes fiables sont hachées (SHAH-256) de manière unidirectionnelle avant d'être stockées en tant que jeux de tableaux sur trois attributs d'objets utilisateur, **msExchSafeSenderHash**, **msExchSafeRecipientHash** et **msExchBlockedSendersHash**, comme un objet blob. Lorsque des données sont hachées, une sortie de longueur fixe est produite, et il est probable que la sortie soit unique. Pour le hachage des entrées d'une collection de listes fiables, un hachage de 4 octets est produit. En cas de réception d’un message provenant d’Internet, Exchange hache l’adresse de l’expéditeur et la compare aux hachages stockés pour le compte de l’utilisateur Outlook auquel le message a été adressé. Si l'expéditeur correspond au hachage des expéditeurs approuvés, le message n'est pas soumis au filtrage de contenu. Si l'expéditeur correspond au hachage des expéditeurs bloqués, le message est bloqué.

Le hachage à sens unique des entrées d'une collection de listes fiables exécute les fonctions importantes suivantes :

  - **Minimise l'espace de stockage et de réplication**   Généralement, le hachage réduit la taille des données hachées. Par conséquent, enregistrer et transmettre une version hachée d'une entrée de collection de listes fiables préserve l'espace de stockage et le temps de réplication. Par exemple, un utilisateur dont l’ensemble de listes fiables comporte 200 entrées créerait environ 800 octets de données hachées stockées et répliquées dans Active Directory.

  - **Rend inutilisable les ensembles de listes fiables par des utilisateurs malveillants**   Comme il est impossible de récupérer des adresses ou domaines SMTP par rétroconception à partir des valeurs de hachage unidirectionnel, les ensembles de listes fiables ne produisent pas d’adresses électroniques utilisables pour des utilisateurs malveillants, qui pourraient compromettre un serveur de transport Exchange.

Retour au début

## Activation de l’agrégation de listes fiables

L’agrégation de listes fiables est activée par défaut dans Exchange 2013. Contrairement à Exchange Server 2007, dans Exchange 2010, vous n'avez pas besoin d’exécuter manuellement la cmdlet **Update-SafeList** pour hacher et écrire les données d’un ensemble de listes fiables dans Active Directory. Dans Exchange 2013, l’Assistant d’options de courrier indésirable écrit les données d’un ensemble de listes fiables dans Active Directory.

Pour que les serveurs de transport Edge du réseau de périmètre puissent accéder aux données d’agrégation de listes fiables dans Active Directory, vous devez installer et configurer le service Microsoft Exchange EdgeSync afin que les données d’agrégation de listes fiables soient répliquées dans les services AD LDS.

Vous pouvez toujours exécuter l'agrégation de listes fiables manuellement à l'aide de la cmdlet **UpdateSafelist**. Cependant, vous ne devez pas oublier le trafic réseau et de réplication qui peut se produire lorsque vous exécutez cette commande. Si vous exécutez **Update-Safelist** sur plusieurs boîtes aux lettres utilisant intensément les listes fiables, le volume de trafic généré peut être considérable. Si vous exécutez la commande sur plusieurs boîtes aux lettres, il est recommandé de le faire en dehors des heures de pointe et de travail.

La cmdlet **Update-SafeList** lit la collection de listes fiables à partir de la boîte aux lettres de l'utilisateur, hache chaque entrée, trie les entrées pour faciliter la recherche, puis convertit le hachage en attribut binaire. En dernier lieu, la cmdlet **Update-SafeList** compare l'attribut binaire créé aux valeurs stockées sur l'attribut. Si les deux valeurs sont identiques, la cmdlet **Update-SafeList** ne met pas à jour la valeur d'attribut de l'utilisateur avec les données d'agrégation de listes fiables. Si les deux valeurs d'attributs sont différentes, la cmdlet **Update-SafeList** met à jour la valeur d'agrégation de listes fiables.

Retour au début

