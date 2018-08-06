---
title: 'Notes de config. pour les contrôleurs de frontière de session pris en charge | Microsoft Docs'
TOCTitle: Notes de configuration pour les contrôleurs de frontière de session pris en charge
ms:assetid: d161f94a-a243-4294-93b3-2bf1dc17b59f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673565(v=EXCHG.150)
ms:contentKeyID: 50555499
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Notes de configuration pour les contrôleurs de frontière de session pris en charge

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2017-07-25_

Les contrôleurs de frontière de session (SBC) vous permettent de connecter votre réseau téléphonique local à un centre de données Microsoft via une connexion WAN publique dédiée. Un contrôleur de frontière de session (SBC) opère au périmètre de votre réseau IP local et se connecte à un deuxième contrôleur de frontière de session dans un centre de données Microsoft.

Le contrôleur de frontière de session requiert l’utilisation de certificats numériques pour chiffrer tout le trafic entre votre organisation locale et le centre de données Microsoft. Vous devez obtenir un certificat numérique pour l’élément de frontière du réseau, comme un contrôleur de frontière de session, que vous utilisez pour communiquer avec des déploiements hybrides et en ligne Exchange. Les certificats numériques permettent d’établir une relation d’approbation entre votre organisation locale et le centre de données Microsoft, et d’activer l’authentification TLS mutuelle. Une fois cette relation d’approbation établie, les éléments de frontière du réseau de votre organisation locale et du centre de données Microsoft échangent des clés de session, puis les utilisent pour chiffrer le trafic de données ultérieur.

Dans des déploiements hybrides et en ligne, une passerelle IP de messagerie unifiée représente un contrôleur de frontière de session (SBC). Le nom commun sujet du certificat doit correspondre à la valeur du nom de domaine complet (FQDN) dans la zone Adresse sur la passerelle IP de messagerie unifiée que vous créez. Par exemple, si vous spécifiez une adresse de nom de domaine complet sbcexternal.contoso.com sur votre passerelle IP de messagerie unifiée, assurez-vous que le nom d’objet et l’autre nom de l’objet dans le certificat contiennent la même valeur : sbcexternal.contoso.com. Le nom que vous utilisez respecte la casse, il faut donc vérifier que la casse est la même sur le certificat et sur la passerelle IP de messagerie unifiée. Si vous utilisez un contrôleur de frontière de session (SBC) Acme Packet et que le nom commun ne correspond pas au nom de domaine complet de la passerelle IP de messagerie unifiée, l’appel est rejeté avec l’erreur 403.

> [!NOTE]
> Puisque les contrôleurs de frontière de session (SBC) sont conçus pour opérer sur le périmètre réseau, ceux-ci fonctionnent également comme des pare-feux. Si vous configurez un contrôleur SBC derrière le pare-feu de votre organisation, des problèmes de configuration risquent de se produire et il n’est pas pris en charge pour la connexion à Office 365.


## Contrôleurs de frontière de session pris en charge

Les tests d’interopérabilité des contrôleurs de frontière de session (SBC) suivants avec des déploiements hybrides et en ligne Exchange ont été tout à fait satisfaisants. Notez que les capacités et compatibilités des contrôleurs de frontière de session (SBC) peuvent varier et la manière dont vous les configurer peut être différente selon d’autres équipements de votre réseau. Consultez le fabricant du contrôleur de frontière de session (SBC) pour vérifier s’il existe des notes de configuration spécifiques pour la messagerie unifiée dans un déploiement hybride ou en ligne.

> [!NOTE]
> Messagerie unifiée Exchange Online de prise en charge pour les systèmes PBX tiers via des connexions directes à partir du client géré SBCs prendra fin dans 2018 de juillet. Consultez le blog d’équipe Exchange <a href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">d’arrêt de la prise en charge des contrôleurs de bordure session Exchange Online de la messagerie unifiée</a> pour plus d’informations.



<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Fournisseur</strong></p></td>
<td><p><strong>Modèle</strong></p></td>
<td><p><strong>Notes de configuration</strong></p></td>
<td><p><strong>Commentaires</strong></p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.acmepacket.com">Acme Packet</a></p></td>
<td><p>Net-Net 3820 ou 4500</p></td>
<td><p><strong>Contactez le fabricant du matériel pour obtenir des instructions à jour sur la façon de configurer leur appareil.</strong></p></td>
<td><p>Contrôleur SBC dédié</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>Contactez le fabricant du matériel pour obtenir des instructions à jour sur la façon de configurer leur appareil.</strong></p></td>
<td><p>Contrôleur SBC dédié</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>Contactez le fabricant du matériel pour obtenir des instructions à jour sur la façon de configurer leur appareil.</strong></p></td>
<td><p>SBC et passerelle IP</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.cisco.com/c/dam/en/us/solutions/collateral/enterprise-networks/unified-access/cube-asr-release-10-0.pdf">Cisco</a></p></td>
<td><p>ASR 1000</p>
> [!NOTE]
> IOS 15.4(3)S3 ou version ultérieure doit être installé.

</td>
<td><p><strong>Contactez le fabricant du matériel pour obtenir des instructions à jour sur la façon de configurer leur appareil.</strong></p></td>
<td><p>Contrôleur SBC dédié</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.ingate.com/">Ingate</a></p></td>
<td><p>SIParator</p></td>
<td><p><strong>Contactez le fabricant du matériel pour obtenir des instructions à jour sur la façon de configurer leur appareil.</strong></p></td>
<td><p>Contrôleur SBC dédié</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.net.com">NET</a></p></td>
<td><p>VX1200 &amp; VX1800</p></td>
<td><p><strong>Contactez le fabricant du matériel pour obtenir des instructions à jour sur la façon de configurer leur appareil.</strong></p></td>
<td><p>Option SBC pour un produit de passerelle VoIP</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.sonus.net/">Sonus</a></p></td>
<td><p>SBC 1000/2000 2.2.1 ou version ultérieure</p></td>
<td><p><strong>Contactez le fabricant du matériel pour obtenir des instructions à jour sur la façon de configurer leur appareil.</strong></p></td>
<td><p>Contrôleur SBC dédié</p></td>
</tr>
</tbody>
</table>

