---
title: 'Utilisation du script RollAlternateserviceAccountCredential.ps1 dans l’environnement de ligne de commande Exchange Management Shell: Exchange 2013 Help'
TOCTitle: Utilisation du script RollAlternateserviceAccountCredential.ps1 dans l’environnement de ligne de commande Exchange Management Shell
ms:assetid: 6ac55aae-472a-4ed6-83df-2d0e7b48e05c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff808311(v=EXCHG.150)
ms:contentKeyID: 63918667
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilisation du script RollAlternateserviceAccountCredential.ps1 dans l’environnement de ligne de commande Exchange Management Shell

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Vous pouvez utiliser le script RollAlternateServiceAccountPassword.ps1 dans Exchange Server 2013 pour mettre à jour des informations d'identification de compte de service de substitution (informations d'identification ASA) et distribuer la mise à jour aux serveurs d'accès au client spécifiés.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L’environnement de ligne de commande Exchange Management Shell ne charge pas automatiquement les scripts. Vous devez faire précéder tous les scripts de « <strong>. \</strong> », par exemple, pour exécuter le script RollAlternateServiceAccountPassword.ps1, tapez <code>.\RollAlternateServiceAccountPassword.ps1</code>.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Ce script est uniquement disponible en anglais.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur l’utilisation et l’écriture de scripts, consultez la rubrique [Scripts dans Exchange Management Shell](https://technet.microsoft.com/fr-fr/library/bb123798\(v=exchg.150\)).

## Syntaxe

    RollAlternateServiceAccountPassword.ps1 -Scope <Object> -Identity <Object> -Source <Object> -

## Description détaillée

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultezEntrée « Sécurité d'accès au client » dans la rubrique des autorisations d'accès au client.

## Détails techniques du script d’informations d’identification pour un autre compte de service

Ce script facilite l’installation et la gestion des informations d’identification ASA. Une fois que vous avez créé les informations d’identification ASA et défini les noms principaux de service appropriés, le script vous permettra de distribuer les informations d’identification à tous les serveurs d’accès cibles.

Pour utiliser le script, vous devez identifier les serveurs que vous souhaitez cibler et les informations d'identification que vous souhaitez utiliser comme informations d'identification ASA.

## Portée du serveur

Le script peut cibler tous les serveurs d’accès au client dans la forêt, tous les membres d’un groupe de serveurs d’accès au client ou des serveurs spécifiques. Les paramètres disponibles sont *ToEntireForest*, *ToArraryMembers* et *ToSpecificServers*. Si vous ciblez le script vers des serveurs spécifiques ou vers les membres d'un groupe de serveurs spécifique, le paramètre *Identity* doit être spécifié avec les noms de serveurs ou de groupes de serveur à cibler.

## Source d’informations d’identification

Le script peut copier le mot de passe de l’autre compte de service à partir d’un serveur existant. Autre possibilité : spécifier le compte à utiliser et laisser le script générer un nouveau mot de passe pour le compte. Les paramètres disponibles sont *GenerateNewPasswordFor* et *CopyFrom*. Avec le paramètre *GenerateNewPasswordFor*, vous devez indiquer une chaîne au format suivant pour le compte : DOMAINE\\Nom de compte. Si vous utilisez un compte d'ordinateur, vous devez ajouter « $ » à la fin du nom du compte, par exemple : CONTOSO\\ClientServerAcct$. Le paramètre *CopyFrom* adopte le nom d’un serveur d’accès au client existant comme source d’information.

## Génération d’un nouveau mot de passe utilisé comme information d’identification

Le mot de passe est créé par le script. Aucune entrée de l’utilisateur n’est requise. Le script tentera de distribuer le mot de passe à tous les ordinateurs cibles, puis de mettre à jour les informations d’identification de compte Active Directory à l’aide du mot de passe nouvellement créé.

Le nouveau mot de passe peut comporter jusqu’à 73 caractères et doit satisfaire des exigences standard de complexité. Si vos règles en matière de mot de passe diffèrent, vous devrez éventuellement définir manuellement le mot de passe, puis le copier sur les serveurs cibles.

Pour éviter les interruptions de service, le script examine chaque serveur d’accès au client et gère le mot de passe existant en plus du mot de passe nouvellement créé. Une fois que le script s’est exécuté, les informations d’identification ASA partagées seront en mesure d’utiliser l’un des deux mots de passe : le mot de passe actuel stocké dans Active Directory ou le nouveau mot de passe qui n'a pas encore été défini dans Active Directory.

Les mots de passe qui ne sont plus valables (arrivés à expiration par exemple) sont supprimés des serveurs de destination. Si le mot de passe dans Active Directory ne peut pas être modifié (peut-être car le mot de passe a expiré), le script tente une réinitialisation du mot de passe. Pour que cela soit possible, le compte exécutant le script doit disposer des autorisations de réinitialiser soit les mots de passe d’accès au compte d’ordinateur Active Directory ou d’utilisateur, selon que votre autre compte de service est un compte d’ordinateur ou un compte d’utilisateur.

Si certains des mots de passe d’accès à l’ensemble des serveurs cibles d’accès au client ne sont pas modifiés, la mise à jour du mot de passe Active Directory risque d’entraîner un échec d’authentification. Si le script est exécuté en mode sans assistance, il ne remplacera pas le mot de passe Active Directory par le nouveau mot de passe, sauf si la mise à jour de tous les serveurs cibles d’accès au client s’est déroulée avec succès. Si le script est exécuté en mode avec assistance, vous recevez un message vous invitant à mettre à jour le mot de passe dans Active Directory.

## Création d’une tâche planifiée pour automatiser la gestion des mots de passe

Pour que le script crée une tâche planifiée pour gérer le mot de passe de manière continue, utilisez le paramètre *CreateScheduledTask*. Ce paramètre doit être complété avec la chaîne correspondant au nom de la tâche à créer.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exécutez le script et vérifiez qu’il fonctionne correctement en mode avec assistance avant de créer la tâche planifiée sans assistance.</td>
</tr>
</tbody>
</table>


Le script crée un fichier .cmd dans le dossier contenant le script. Il crée ensuite une tâche permettant d’exécuter ce fichier .cmd toutes les trois semaines. Vous pouvez utiliser le Planificateur de tâches Windows pour modifier la tâche planifiée, par exemple, pour définir qu'il s'exécute plus ou moins souvent. Par défaut, la tâche est exécutée comme utilisateur actuellement connecté. En outre, le script est exécuté uniquement lorsque l'utilisateur est connecté à l'ordinateur. Nous vous recommandons de modifier la tâche planifiée afin qu'elle s'exécute indépendamment du statut de connexion de l'utilisateur. Vous pouvez également choisir de l'exécuter sous un compte différent, si ce compte a des autorisations Active Directory pour réinitialiser les mots de passe, ainsi que le rôle administrateur Exchange Entreprise. Lors de la création d’une tâche planifiée, le script s’exécute automatiquement en mode sans assistance.

## Tâches hors de portée du script

Le script ne gère pas les SPN des informations d’identification ASA et ne permet pas de supprimer un autre compte de service à partir d’un serveur. Pour supprimer un autre compte de service à partir d'un serveur, voir la section [Turn Kerberos authentication off](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md) dans [Configuration de l’authentification Kerberos pour les serveurs d’accès au client avec équilibrage de charge](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md).

## Résolution de problèmes liés au script

Nous vous recommandons d’exécuter le script et de vérifier qu’il fonctionne correctement en mode avec assistance avant de créer la tâche planifiée sans assistance. Pour obtenir des informations de résolution des problèmes, consultez la rubrique [Dépannage des problèmes liés au script RollAlternateServiceAccountCredential.ps1](troubleshooting-the-rollalternateserviceaccountcredential-ps1-script-exchange-2013-help.md).

## Validation du script

Le résultat du script exécuté de manière interactive avec l’indicateur -verbose doit indiquer les opérations de script qui ont abouti. Pour vous assurer que les serveurs d’accès au client ont été mis à jour, vous pouvez vérifier la date de dernière mise à jour de l’horodatage dans les informations d’identification ASA. Dans l’exemple suivant, la commande génère une liste de serveurs d’accès au client et indique l’heure de la dernière mise à jour de l’autre compte de service.

    Get-ClientAccessServer -IncludeAlternateServiceAccountCredentialstatus |Fl Name, AlternateServiceAccountConfiguration

Vous pouvez également consulter le journal des événements sur l’ordinateur où le script s’exécute. Les entrées correspondant au script se trouvent dans le journal des événements de l’application et sont issues de la source *MSExchange Management Application*.Le tableau suivant répertorie les événements consignés et indique leur signification.

### ID d’événement de script et leur explication

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Événement</th>
<th>Explication</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>14001</p></td>
<td><p>Démarrez</p></td>
</tr>
<tr class="even">
<td><p>14002</p></td>
<td><p>Succès (informations)</p></td>
</tr>
<tr class="odd">
<td><p>14003</p></td>
<td><p>Réussi mais avec avertissements.</p>
<p>Le script a détecté certains problèmes, mais il a pu les surmonter, ou l’utilisateur a confirmé qu’ils pouvaient être ignorés. Si le script s’exécute en mode interactif, lisez la sortie générée par ce dernier pour en savoir plus sur l’avertissement.</p></td>
</tr>
<tr class="even">
<td><p>14004</p></td>
<td><p>Échec</p></td>
</tr>
</tbody>
</table>


Si le script s’exécute comme une tâche planifiée, les résultats correspondants sont consignés dans le dossier **Enregistrement** du serveur Exchange (dans le sous-dossier **RollAlternateServiceAccountPassword**).

Vous pouvez utiliser le journal pour vous assurer que la tâche s’est bien exécutée.

## Paramètres


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Obligatoire</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ToEntireForest</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>ToEntireForest</em> cible le script vers tous les serveurs d’accès au client présents dans la forêt.</p></td>
</tr>
<tr class="even">
<td><p><em>ToArrayMembers</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>ToArrayMembers</em> cible le script vers tous les membres d’un groupe spécifique de serveurs d’accès au client.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous utilisez le paramètre <em>ToArrayMembers</em> ou le paramètre <em>ToSpecificServers</em>, vous devez spécifier les noms de serveur ou les noms de groupe de serveurs à l’aide du paramètre <em>Identity</em>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p><em>ToSpecificServers</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>ToSpecificServers</em> cible le script vers des serveurs spécifiques.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous utilisez le paramètre <em>ToArrayMembers</em> ou le paramètre <em>ToSpecificServers</em>, vous devez spécifier les noms de serveur ou les noms de groupe de serveurs à l’aide du paramètre <em>Identity</em>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Le paramètre <em>Identity</em> indique le nom du groupe de serveurs d’accès au client ou les noms des serveurs spécifiques que vous ciblez.</p></td>
</tr>
<tr class="odd">
<td><p><em>GenerateNewPasswordFor&lt;String&gt;</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>GenerateNewPasswordFor</em> spécifie que le script doit générer un nouveau mot de passe pour le compte ASA. La valeur de chaîne doit être le compte ASA au format suivant : DOMAINE\Nom de compte. Si vous utilisez un compte d'ordinateur, vous devez ajouter le caractère $ à la fin du nom du compte.</p></td>
</tr>
<tr class="even">
<td><p><em>CopyFrom&lt;String&gt;</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>CopyFrom</em> indique que les informations d’identification sont copiées à partir d’un autre serveur d’accès au client. La valeur de chaîne spécifiée est le nom du serveur d’accès au client.</p></td>
</tr>
<tr class="odd">
<td><p><em>Mode</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le commutateur <em>Mode</em> spécifie si le script s’exécute en mode avec ou sans assistance. Dans le mode sans assistance, l’intervention de l’utilisateur n’est pas requise et des options plus « strictes » sont sélectionnées, si nécessaire.</p></td>
</tr>
<tr class="even">
<td><p><em>CreateScheduledTask&lt;String&gt;</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>CreateScheduledTask</em> demande au script de créer une tâche planifiée pour effectuer la mise à jour des informations d’identification ASA. La valeur de la chaîne correspond au nom de la tâche planifiée qui sera créée.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Ce script crée un fichier .cmd dans le dossier où il se trouve. La tâche planifiée exécutera le fichier .cmd toutes les trois semaines. Pour modifier la fréquence d’exécution de la tâche, vous pouvez modifier directement cette dernière dans le Planificateur de tâches Windows.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le commutateur <em>WhatIf</em> demande à la commande de simuler les actions qu’elle appliquera à l’objet. Grâce au commutateur <em>WhatIf</em>, vous pouvez afficher des changements potentiels sans devoir les appliquer. Il n’est pas nécessaire de spécifier une valeur pour le commutateur <em>WhatIf</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le commutateur <em>Confirm</em> suspend la commande et vous demande de confirmer les actions que la commande va exécuter avant de continuer le traitement. Il n’est pas nécessaire de spécifier une valeur pour le commutateur <em>Confirm</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Verbose</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>Verbose</em> demande au script d’effectuer une journalisation détaillée, afin que des informations supplémentaires concernant les actions du script soient consignées dans le fichier journal.</p></td>
</tr>
<tr class="even">
<td><p><em>Debug</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>Debug</em> demande au script de s’exécuter en mode débogage. Ce paramètre doit être utilisé afin de déterminer pourquoi le script échoue.</p></td>
</tr>
</tbody>
</table>


## Exemples

## Exemple 1

Dans cet exemple, le script fait passer les informations d’identification lors de la première installation à tous les serveurs d’accès au client présents dans la forêt.

    .\RollAlternateserviceAccountPassword.ps1 -ToEntireForest -GenerateNewPasswordFor "Contoso\ComputerAccount$" -Verbose

## Exemple 2

Cet exemple permet de générer un nouveau mot de passe pour les informations d’identification ASA d’un compte utilisateur et de le distribuer à tous les membres des groupes de serveurs d’accès au client dont le nom contient \*mailbox\*.

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers *mailbox* -GenerateNewPasswordFor "Contoso\UserAccount" -Verbose

## Exemple 3

Cet exemple montre comment planifier mensuellement une tâche de réinitialisation de mot de passe automatisée appelée « Exchange-RollAsa ». Elle permet de mettre à jour les informations d’identification ASA pour tous les serveurs d’accès au client de la forêt avec un nouveau mot de passe généré par script. La tâche planifiée est créée, mais le script n’est pas exécuté. Lors de l’exécution de la tâche planifiée, le script s’exécute en mode sans assistance.

    .\RollAlternateServiceAccountPassword.ps1 -CreateScheduledTask "Exchange-RollAsa" -ToEntireForest -GenerateNewPasswordFor 'contoso\computerAccount$'

## Exemple 4

Cet exemple montre comment mettre à jour les informations d’identification ASA pour tous les serveurs d’accès au client du groupe de serveurs correspondant nommé CAS01. Les informations d’identification sont obtenues à partir du compte d’ordinateur Active Directory ServiceAc1 dans le domaine Contoso.

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers "CAS01" -GenerateNewPasswordFor "CONTOSO\ServiceAc1$" 

## Exemple 5

Cet exemple vous indique comment utiliser le script pour distribuer les informations d’identification ASA à un nouvel ordinateur ou un ordinateur remis en service, soit parce que vous augmentez la taille du groupe de serveurs, soit parce que vous réintroduisez des membres du groupe après une opération de maintenance.

Vous devez mettre à jour les informations d'identification ASA avant que le serveur d'accès au client reçoive le trafic. Pour ce faire, copiez les informations ASA partagées depuis n’importe quel serveur d’accès au client dont la configuration est correcte. Par exemple, si les informations d’identification ASA d’un serveur A sont actives et que vous venez d’ajouter un serveur B dans le groupe, vous pouvez utiliser le script pour copier les informations d’identification (y compris le mot de passe) du serveur A sur le serveur B. Cette possibilité est utile si le serveur B était en panne ou ne faisait pas encore partie du groupe lors de la dernière réinitialisation du mot de passe.

    .\RollAlternateServiceAccountPassword.ps1 -CopyFrom ServerA -ToSpecificServers ServerB -Verbose

