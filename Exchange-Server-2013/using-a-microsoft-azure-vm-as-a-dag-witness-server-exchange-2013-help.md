---
title: "Utilisation d'une machine virtuelle Microsoft Azure comme serveur témoin du groupe de disponibilité de base de données (DAG): Exchange 2013 Help"
TOCTitle: Utilisation d'une machine virtuelle Microsoft Azure comme serveur témoin du groupe de disponibilité de base de données (DAG)
ms:assetid: 03d1e215-518b-4b48-bfcd-8d187ff8f5ef
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn903504(v=EXCHG.150)
ms:contentKeyID: 63892219
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilisation d'une machine virtuelle Microsoft Azure comme serveur témoin du groupe de disponibilité de base de données (DAG)

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Exchange Server 2013 permet de configurer vos bases de données de boîtes aux lettres dans un groupe de disponibilité de base de données (DAG) pour le basculement de centre de données automatique. Cette configuration nécessite trois emplacements physiques distincts : deux centres de données pour les serveurs de boîtes aux lettres et un troisième emplacement pour placer le serveur témoin pour le groupe de disponibilité de base de données (DAG). Les organisations n'ayant que deux emplacements physiques peuvent maintenant bénéficier aussi d'un basculement de centre de données automatique en utilisant une machine virtuelle de serveur de fichiers Microsoft Azure comme serveur témoin du groupe de disponibilité de base de données (DAG).

Cet article se concentre sur l'emplacement du témoin du groupe de disponibilité de base de données (DAG) sur Microsoft Azure et suppose que vous connaissez les concepts de résilience de site et que vous disposez déjà une infrastructure DAG entièrement fonctionnelle qui s'étend sur deux centres de données. Si vous n'avez pas encore configuré votre infrastructure DAG, nous vous recommandons de consulter d'abord les articles suivants :

[Haute disponibilité et résilience de site](high-availability-and-site-resilience-exchange-2013-help.md)

[Groupe de disponibilité de base de données (DAG)](database-availability-groups-dags-exchange-2013-help.md)

[Planification d'une haute disponibilité et d'une résilience de site](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)

## Modifications apportées à Microsoft Azure

Cette configuration nécessite un VPN multisite. Il a toujours été possible de connecter le réseau de votre organisation à Microsoft Azure à l'aide d'une connexion VPN site à site. Toutefois, dans le passé, Azure prenait en charge un seul VPN site à site. Comme la configuration d'un DAG et de son témoin dans trois centres de données nécessitait plusieurs connexions VPN site à site, l'emplacement du témoin DAG sur une machine virtuelle Azure n'était pas possible initialement.

En juin 2014, Microsoft Azure a introduit la prise en charge du VPN multisite, qui a permis aux organisations de connecter plusieurs centres de données au même réseau virtuel Azure. Cette modification a également permis aux organisations dotées de deux centres de données de tirer parti de Microsoft Azure comme troisième emplacement pour leurs serveurs témoins DAG. Pour plus d'informations sur la fonction VPN multisite dans Azure, consultez la rubrique [Configuration d'un VPN multisite](http://go.microsoft.com/fwlink/?linkid=522621).

> [!NOTE]
> Cette configuration tire parti des machines virtuelles Azure et d'une connexion VPN multisite pour déployer le serveur témoin et n'utilise pas le témoin du Cloud Azure.


## Témoin de serveur de fichiers Microsoft Azure

Le diagramme suivant est une vue d'ensemble de l'utilisation d'une machine virtuelle de serveur de fichiers Microsoft Azure comme témoin DAG. Vous avez besoin d'un réseau virtuel Azure, d'une connexion VPN multisite qui connecte vos centres de données à votre réseau virtuel Azure, ainsi que d'un contrôleur de domaine et d'un serveur de fichiers déployés sur des machines virtuelles Azure.

> [!NOTE]
> Il est techniquement possible d'utiliser une seule machine virtuelle Azure à cet effet et de placer le partage témoin de fichiers sur le contrôleur de domaine. Toutefois, cela entraîne une élévation inutile des privilèges. Par conséquent, cette configuration n'est pas recommandée.


**Serveur témoin de groupe de disponibilité de base de données (DAG) sur Microsoft Azure**

![Vue d’ensemble du témoin de groupe de disponibilité de base de données (DAG) Exchange sur Azure](images/Dn903504.7cbda882-bbae-4be7-b0ea-60947b8aa4ef(EXCHG.150).png "Vue d’ensemble du témoin de groupe de disponibilité de base de données (DAG) Exchange sur Azure")

La première chose que vous devez faire pour utiliser une machine virtuelle Microsoft Azure pour votre témoin DAG est d'obtenir un abonnement. Consultez [Modes d'achat d'Azure](http://go.microsoft.com/fwlink/?linkid=398989) pour connaître la meilleure façon d'acquérir un abonnement Azure.

Une fois que vous avez votre abonnement Azure, vous devez effectuer les opérations suivantes dans l'ordre :

1.  Préparer le réseau virtuel Microsoft Azure

2.  Configurer un VPN multisite

3.  Configurer des machines virtuelles

4.  Configurer le témoin DAG

> [!NOTE]
> Une grande partie des instructions fournies dans cet article implique la configuration d'Microsoft Azure. Par conséquent, les liens vers la documentation Azure sont utilisés lorsque nécessaire.


## Conditions préalables

  - Deux centres de données pouvant prendre en charge un déploiement de résilience de site et de haute disponibilité Exchange. Pour plus d’informations, consultez la rubrique [Planification d'une haute disponibilité et d'une résilience de site](planning-for-high-availability-and-site-resilience-exchange-2013-help.md).

  - Une adresse IP publique qui n'est pas derrière un NAT pour les passerelles VPN dans chaque site

  - Un périphérique VPN dans chaque site qui est compatible avec Microsoft Azure. Consultez [À propos des périphériques VPN de réseau virtuel](http://go.microsoft.com/fwlink/?linkid=522619) pour plus d'informations sur les périphériques compatibles

  - Maîtrise de la gestion et des concepts DAG

  - Maîtrise de Windows PowerShell

## Phase 1 : Préparer le réseau virtuel Microsoft Azure

La configuration du réseau Microsoft Azure est la partie du processus de déploiement la plus importante. À la fin de cette phase, vous aurez un réseau virtuel Azure entièrement fonctionnel qui est connecté à vos deux centres de données via une connexion VPN multisite.

## Enregistrer des serveurs DNS

Étant donné que cette configuration nécessite la résolution de noms entre les serveurs locaux et les machines virtuelles Azure, vous devrez configurer Azure pour utiliser vos propres serveurs DNS. La rubrique [Résolution de noms (DNS)](http://msdn.microsoft.com/fr-fr/library/azure/jj156088.aspx) fournit une vue d'ensemble de la résolution de noms dans Azure.

Procédez comme suit pour enregistrer vos serveurs DNS :

1.  Dans le portail Azure, accédez à **réseaux**, puis cliquez sur **NOUVEAU**.

2.  Cliquez sur **SERVICES RÉSEAU** \> **RÉSEAU VIRTUEL** \> **INSCRIRE LE SERVEUR DNS**.

3.  Entrez le nom et l'adresse IP de votre serveur DNS. Le nom spécifié ici est le nom logique utilisé dans le portail de gestion et ne doit pas correspondre au nom réel de votre serveur DNS.

4.  Répétez les étapes 1 à 3 pour les autres serveurs DNS à ajouter.
    
    > [!NOTE]
    > Les serveurs DNS que vous enregistrez ne sont pas utilisés avec le mécanisme du tourniquet. Les machines virtuelles Azure utiliseront le premier serveur DNS répertorié, ainsi que des serveurs supplémentaires uniquement si le premier d'entre eux n'est pas disponible.


5.  Répétez les étapes 1 à 3 pour ajouter l'adresse IP que vous utiliserez pour le contrôleur de domaine que vous déploierez sur Microsoft Azure.

## Créer des objets de réseau locaux dans Azure

Ensuite, procédez comme suit pour créer des objets de réseau logiques qui représentent vos centres de données dans Microsoft Azure :

1.  Dans le portail Azure, accédez à **réseaux**, puis cliquez sur **NOUVEAU**.

2.  Cliquez sur **SERVICES RÉSEAU** \> **RÉSEAU VIRTUEL** \> **AJOUTER UN RÉSEAU LOCAL**.

3.  Entrez le nom de votre premier site de centre de données et l'adresse IP du périphérique VPN de ce site. Cette adresse IP doit être une adresse IP publique statique qui n'est pas derrière un NAT.

4.  Dans l'écran suivant, spécifiez les sous-réseaux IP pour votre premier site.

5.  Répétez les étapes 1 à 4 pour votre deuxième site.

## Créer le réseau virtuel Azure

Maintenant, procédez comme suit pour créer un réseau virtuel Azure qui sera utilisé par les machines virtuelles :

1.  Dans le portail Azure, accédez à **réseaux**, puis cliquez sur **NOUVEAU**.

2.  Cliquez sur **SERVICES RÉSEAU** \> **RÉSEAU VIRTUEL** \> **CRÉATION PERSONNALISÉE**.

3.  Sur la page **Détails du réseau virtuel**, spécifiez un nom pour le réseau virtuel et sélectionnez un emplacement géographique pour le réseau.

4.  Sur la page **Serveurs DNS et connectivité VPN**, vérifiez que les serveurs DNS que vous avez enregistrés précédemment sont répertoriés en tant que serveurs DNS.

5.  Cochez la case **Configurer un réseau VPN de site à site** sous **CONNECTIVITÉ DE SITE À SITE**.
    
    > [!IMPORTANT]
    > Ne sélectionnez pas <strong>Utiliser Itinéraire express</strong>, car cela empêche les modifications de configuration requises de configurer un VPN multisite.


6.  Sous **RÉSEAU LOCAL**, sélectionnez l'un des deux réseaux locaux que vous avez configurés.

7.  Sur la page **Espace d'adresses du réseau virtuel**, spécifiez la plage d'adresses IP à utiliser pour votre réseau virtuel Azure.

## Point de contrôle : Passer en revue la configuration du réseau

À ce stade, lorsque vous accédez à **réseaux**, vous devriez voir le serveur virtuel que vous avez configuré sous **RÉSEAUX VIRTUELS,** vos sites locaux sous **RÉSEAUX LOCAUX**, et vos serveurs DNS enregistrés sous **SERVEURS DNS**.

## Phase 2 : Configurer un VPN multisite

L'étape suivante consiste à établir les passerelles VPN vers vos sites locaux. Pour ce faire, vous devez :

1.  Établir une passerelle VPN vers l'un de vos sites à l'aide du portail Azure.

2.  Exporter les paramètres de configuration de réseau virtuel.

3.  Modifier le fichier de configuration pour le VPN multisite.

4.  Importer la configuration réseau d'Azure mise à jour.

5.  Enregistrer l'adresse IP de la passerelle Azure et les clés pré-partagées.

6.  Configurer des périphériques VPN locaux.

Pour plus d'informations sur la configuration d'un VPN multisite, consultez la rubrique [Configuration d'un VPN multisite](http://go.microsoft.com/fwlink/?linkid=522621).

## Établir une passerelle VPN vers votre premier site

Lorsque vous créez votre passerelle virtuelle, notez que vous avez déjà spécifié qu'elle sera connectée à votre premier site local. Lorsque vous accédez au tableau de bord de réseau virtuel, vous pouvez voir que la passerelle n'a pas été créée.

Pour établir la passerelle VPN du côté d'Azure, suivez les instructions de la section [Démarrer la passerelle de réseau privé](http://msdn.microsoft.com/fr-fr/library/azure/jj156210.aspx#bkmk+_startgateway) de la rubrique [Configurer une passerelle de réseau virtuel dans le Portail de gestion](http://msdn.microsoft.com/fr-fr/library/azure/jj156210.aspx).

> [!IMPORTANT]
> Effectuez uniquement les étapes de la section « Démarrer la passerelle de réseau privé » de cet article, et ne passez pas aux sections suivantes.


## Exporter des paramètres de configuration de réseau virtuel

Le portail de gestion Azure ne vous permet pas actuellement de configurer un VPN multisite. Pour cette configuration, vous devez exporter les paramètres de configuration de réseau virtuel vers un fichier XML, puis modifiez ce fichier. Suivez les instructions de la section [Exporter les paramètres de réseau virtuel dans un fichier de configuration réseau](http://msdn.microsoft.com/fr-fr/library/azure/dn133804.aspx) pour exporter vos paramètres.

## Modifier les paramètres de configuration réseau pour le VPN multisite

Ouvrez le fichier que vous avez exporté dans un éditeur XML. Les connexions de passerelle à vos sites locaux sont répertoriées dans la section « ConnectionsToLocalNetwork ». Recherchez ce terme dans le fichier XML pour localiser la section. Cette section du fichier de configuration ressemblera à ceci (en supposant que le nom de site que vous avez créé pour votre site local est « Site A »).

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

Pour configurer votre deuxième site, ajoutez une autre section « LocalNetworkSiteRef » sous la section « ConnectionsToLocalNetwork ». La section dans le fichier de configuration mis à jour se présentera comme suit (en supposant que le nom du site de votre deuxième site local est « Site B »).

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
        <LocalNetworkSiteRef name="Site B">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

Enregistrez le fichier de paramètres de configuration mis à jour.

## Importer les paramètres de configuration de réseau virtuel

La deuxième référence de site que vous avez ajoutée au fichier de configuration déclenche la création d'un tunnel par Microsoft Azure. Importez le fichier mis à jour en suivant les instructions de la section [Importer un fichier de configuration de réseau](http://msdn.microsoft.com/fr-fr/library/azure/jj156213.aspx). Une fois l'importation terminée, le tableau de bord de réseau virtuel affiche les connexions de passerelle à vos deux sites locaux.

## Enregistrez l'adresse IP de la passerelle Azure et les clés pré-partagées.

Une fois que les nouveaux paramètres de configuration réseau sont importés, le tableau de bord de réseau virtuel affichera l'adresse IP de la passerelle Azure. Il s'agit de l'adresse IP à laquelle se connecteront les périphériques VPN sur vos deux sites. Enregistrez cette adresse IP pour référence.

Vous devrez également obtenir les clés IPsec/IKE pré-partagées pour chaque tunnel créé. Ces clés, ainsi que l'adresse IP de passerelle Azure, vous permettent de configurer vos périphériques VPN locaux.

Vous devez utiliser PowerShell pour obtenir les clés pré-partagées. Si vous ne savez pas comment utiliser PowerShell pour gérer Azure, consultez [Azure PowerShell](http://msdn.microsoft.com/fr-fr/library/azure/jj156055.aspx).

Utilisez la cmdlet [Get-AzureVNetGatewayKey](http://msdn.microsoft.com/fr-fr/library/azure/dn495198.aspx) pour extraire les clés pré-partagées. Exécutez cette cmdlet une fois pour chaque tunnel. L'exemple suivant illustre les commandes que vous devez exécuter pour extraire les clés pour des tunnels entre le réseau virtuel « Site Azure » et les sites « Site A » et « Site B ». Dans cet exemple, les résultats sont enregistrés dans des fichiers distincts. Vous pouvez également mettre ces clés en pipeline avec d'autres cmdlets PowerShell ou les utiliser dans un script.

    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site A" > C:\Keys\KeysForTunnelToSiteA.txt 
    
    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site B" > C:\Keys\KeysForTunnelToSiteB.txt

## Configurer des périphériques VPN locaux

Microsoft Azure fournit des scripts de configuration de périphérique VPN pour les périphériques VPN pris en charge. Cliquez sur le lien **Télécharger le script du périphérique VPN** dans le tableau de bord de réseau virtuel pour le script approprié pour vos périphériques VPN.

Le script que vous téléchargez aura le paramètre de configuration pour le site que vous avez configuré lorsque vous avez configuré votre réseau virtuel et peut être utilisé tel quel pour configurer le périphérique VPN pour ce site. Par exemple, si vous avez spécifié Site A comme **RÉSEAU LOCAL** lorsque vous avez créé votre réseau virtuel, le script de périphérique VPN peut être utilisé pour Site A. Toutefois, vous devrez le modifier pour configurer le périphérique VPN pour Site B. Plus précisément, vous devez mettre à jour la clé pré-partagée pour qu'elle corresponde à la clé du second site.

Par exemple, si vous utilisez un périphérique VPN de service de routage et d'accès à distance (RRAS) pour vos sites, vous devez :

1.  Ouvrir le script de configuration dans un éditeur de texte.

2.  Rechercher la section `#Add S2S VPN interface`.

3.  Rechercher la commande **Add-VpnS2SInterface** dans cette section. Vérifier que la valeur pour le paramètre *SharedSecret* correspond à la clé pré-partagée pour le site pour lequel vous configurez le périphérique VPN.

D'autres périphériques peuvent nécessiter des vérifications supplémentaires. Par exemple, les scripts de configuration pour les périphériques Cisco définissent des règles ACL à l'aide de plages d'adresses IP locales. Vous devez examiner et vérifier toutes les références vers le site local dans le script de configuration avant de l'utiliser. Pour plus d'informations, consultez les sections suivantes :

[Modèles de service de routage et d'accès à distance (RRAS)](http://msdn.microsoft.com/fr-fr/library/azure/dn133801.aspx)

[Modèles Cisco ASR](http://msdn.microsoft.com/fr-fr/library/azure/dn133802.aspx)

[Modèles Cisco ISR](http://msdn.microsoft.com/fr-fr/library/azure/dn133800.aspx)

[Modèles Juniper SRX](http://msdn.microsoft.com/fr-fr/library/azure/dn133794.aspx)

[Modèles Juniper J-Series](http://msdn.microsoft.com/fr-fr/library/azure/dn133799.aspx)

[Modèles Juniper ISG](http://msdn.microsoft.com/fr-fr/library/azure/dn133797.aspx)

[Modèles Juniper SSG](http://msdn.microsoft.com/fr-fr/library/azure/dn133796.aspx)

## Point de contrôle : Examiner l'état VPN

À ce stade, vos deux sites sont connectés à votre réseau virtuel Azure via les passerelles VPN. Vous pouvez valider l'état du VPN multisite en exécutant la commande suivante dans PowerShell.

    Get-AzureVnetConnection -VNetName "Azure Site" | Format-Table LocalNetworkSiteName, ConnectivityState

Si les deux tunnels sont en cours d'exécution, la sortie de cette commande ressemble à la suivante.

    LocalNetworkSiteName    ConnectivityState
    
    --------------------    -----------------
    
    Site A                  Connected
    
    Site B                  Connected

Vous pouvez également vérifier la connectivité en consultant le tableau de bord de réseau virtuel dans le portail de gestion Azure. La colonne **État** pour les deux sites affiche **Connecté**.

> [!NOTE]
> Après que la connexion a été établie, l'affichage de la modification de l'état dans le portail de gestion Azure peut prendre quelques minutes.


## Phase 3 : Configurer des machines virtuelles

Vous devez créer au moins deux machines virtuelles dans Microsoft Azure pour ce déploiement : un contrôleur de domaine et un serveur de fichiers qui servira de témoin DAG.

1.  Créez des machines virtuelles pour votre contrôleur de domaine et votre serveur de fichiers en suivant les instructions fournies dans [Création d'une machine virtuelle exécutant Windows](http://azure.microsoft.com/fr-fr/documentation/articles/virtual-machines-windows-tutorial/). Veillez à sélectionner le réseau virtuel que vous avez créé pour **Région/Groupe d'affinités/Réseau virtuel** lorsque vous spécifiez les paramètres de vos machines virtuelles.

2.  Spécifiez les adresses IP préférées pour le contrôleur de domaine et le serveur de fichiers à l'aide d'Azure PowerShell. Lorsque vous spécifiez une adresse IP préférée pour une machine virtuelle, elle doit être mise à jour, ce qui nécessite le redémarrage de la machine virtuelle. L'exemple suivant définit les adresses IP pour Azure-DC et Azure-FSW sur 10.0.0.10 et 10.0.0.11, respectivement.
    
        Get-AzureVM Azure-DC | Set-AzureStaticVNetIP -IPAddress 10.0.0.10 | Update-AzureVM
        
        Get-AzureVM Azure-FSW | Set-AzureStaticVNetIP -IPAddress 10.0.0.11 | Update-AzureVM
    
    > [!NOTE]
    > Une machine virtuelle avec une adresse IP préférée tentera d'utiliser cette adresse. Toutefois, si cette adresse a été attribuée à une machine virtuelle différente, la machine virtuelle avec la configuration d'adresse IP préférée ne démarrera pas. Pour éviter cette situation, assurez-vous que l'adresse IP que vous utilisez n'est pas affectée à une autre machine virtuelle. Consultez <a href="http://msdn.microsoft.com/fr-fr/library/azure/dn630228.aspx">Configuration d'une adresse IP interne statique pour une machine virtuelle</a> pour plus d'informations.


3.  Configurez la machine virtuelle du contrôleur de domaine sur Azure à l'aide des normes utilisées par votre organisation.

4.  Préparez le serveur de fichiers avec les conditions prérequises pour un témoin DAG d'Exchange :
    
    1.  Ajoutez le rôle de serveur de fichiers à l'aide de l'Assistant d'ajout de rôles et de fonctionnalités ou de la cmdlet [Add-WindowsFeature](http://technet.microsoft.com/fr-fr/library/ee662309.aspx).
    
    2.  Ajoutez le groupe de sécurité universel du sous-système approuvé Exchange (Exchange Trusted Subsystem) au groupe Administrateurs local.

## Point de contrôle : Consulter l'état de la machine virtuelle

À ce stade, vos machines virtuelles doivent être en cours d'exécution et en mesure de communiquer avec les serveurs dans vos deux centres de données locaux :

  - Vérifiez que votre contrôleur de domaine dans Azure réplique avec vos contrôleurs de domaine locaux.

  - Vérifiez que vous pouvez atteindre le serveur de fichiers sur Azure par nom et établir une connexion SMB de vos serveurs Exchange.

  - Vérifiez que vous pouvez atteindre vos serveurs Exchange par nom du serveur de fichiers sur Azure.

## Phase 4 : Configurer le témoin DAG

Enfin, vous devez configurer votre DAG pour utiliser le nouveau serveur témoin. Par défaut, Exchange utilise C:\\DAGFileShareWitnesses comme chemin de témoin de partage de fichiers sur votre serveur témoin. Si vous utilisez un chemin d'accès de fichier personnalisé, vous devez aussi mettre à jour le répertoire témoin pour le partage spécifique.

1.  Connectez-vous à Environnement de ligne de commande Exchange Management Shell.

2.  Exécutez la commande suivante pour configurer le serveur témoin pour vos DAG.
    
        Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessServer Azure-FSW

Pour plus d'informations, consultez les sections suivantes :

[Configuration des propriétés du groupe de disponibilité de base de données](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](http://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\).aspx)

## Point de contrôle : Valider le témoin de partage de fichiers DAG

À ce stade, vous avez configuré votre DAG pour utiliser le serveur de fichiers sur Azure comme témoin DAG. Procédez comme suit pour valider votre configuration :

1.  Validez la configuration DAG en exécutant la commande suivante.
    
        Get-DatabaseAvailabilityGroup -Identity DAG1 -Status | Format-List Name, WitnessServer, WitnessDirectory, WitnessShareInUse
    
    Vérifiez que le paramètre *WitnessServer* est défini sur le serveur de fichiers sur Azure, que le paramètre *WitnessDirectory* est défini sur le chemin d'accès correct et que le paramètre *WitnessShareInUse* affiche **Primary**.

2.  Si le DAG comporte un nombre pair de nœuds, le témoin de partage de fichiers est configuré. Validez le paramètre de témoin de partage de fichiers dans les propriétés de cluster en exécutant la commande suivante. La valeur du paramètre *SharePath* doit pointer vers le serveur de fichiers et afficher le chemin d'accès correct.
    
        Get-ClusterResource -Cluster MBX1 | Get-ClusterParameter | Format-List

3.  Ensuite, vérifiez l'état de la ressource de cluster « Témoin de partage de fichiers » en exécutant la commande suivante. L'*State* de la ressource de cluster doit afficher **Online**.
    
        Get-ClusterResource -Cluster MBX1

4.  Enfin, vérifiez que le partage est créé sur le serveur de fichiers en analysant le dossier dans l'Explorateur de fichiers et les partages dans le Gestionnaire de serveur.

## Voir aussi


[Planification d'une haute disponibilité et d'une résilience de site](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
[Switchovers et basculements](switchovers-and-failovers-exchange-2013-help.md)  
[Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md)

