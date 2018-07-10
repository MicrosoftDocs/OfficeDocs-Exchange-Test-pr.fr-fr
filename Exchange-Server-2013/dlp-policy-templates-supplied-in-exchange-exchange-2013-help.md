---
title: 'Modèles de stratégies DLP fournis dans Exchange: Exchange 2013 Help'
TOCTitle: Modèles de stratégies DLP fournis dans Exchange
ms:assetid: 7e1917ab-1920-4a52-97d1-7dfe2add6198
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150530(v=EXCHG.150)
ms:contentKeyID: 50477339
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modèles de stratégies DLP fournis dans Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Avec Microsoft Exchange Server 2013 et Exchange Online, vous pouvez utiliser des modèles de stratégie de protection contre la perte de données (DLP) comme point de départ pour générer des stratégies DLP qui vous permettent de satisfaire vos exigences en termes réglementation spécifique et de stratégie d'entreprise. Vous pouvez modifier les modèles afin de répondre aux besoins spécifiques de votre organisation.

> [!CAUTION]
> Vous devez activer vos stratégies DLP en mode Test avant de les exécuter dans votre environnement de production. Au cours de ces tests, nous vous recommandons de configurer des boîtes aux lettres d'exemple d'utilisateur et d'envoyer des messages de test qui appellent vos stratégies de test afin de confirmer les résultats.
> L'utilisation de ces stratégies ne garantit la conformité avec aucune des réglementations. A l'issue de votre test, effectuez les modifications de configuration nécessaires dans Exchange de sorte que la transmission des informations respecte les stratégies de votre organisation. Par exemple, vous pourriez avoir besoin de configurer TLS avec des partenaires commerciaux connus ou d'ajouter des actions de règle de transport plus restrictives, comme l'ajout d'une protection des droits pour des messages qui contiennent un certain type de données.


## Modèles disponibles pour DLP

Le tableau suivant répertorie les modèles de stratégie DLP dans Exchange. Pour plus d'informations sur la personnalisation de ces modèles pour créer des stratégies DLP, consultez la rubrique [Gestion de stratégies de protection contre la perte de données (DLP)](manage-dlp-policies-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Modèle</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Données financières en Australie</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des données financières en Australie, notamment des cartes de crédit et des codes SWIFT (ou BIC).</p></td>
</tr>
<tr class="even">
<td><p>Australia Health Records Act (HRIP Act)</p></td>
<td><p>Permet de détecter la présence d'informations généralement couvertes par la loi australienne sur la protection des renseignements personnels et des informations sur la santé, comme un numéro de dossier médical ou un numéro TFN (numéro de dossier fiscal).</p></td>
</tr>
<tr class="odd">
<td><p>Australia Personally Identifiable Information (PII) Data</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des informations d'identification personnelle en Australie, comme un numéro TFN (numéro de dossier fiscal) et un permis de conduire.</p></td>
</tr>
<tr class="even">
<td><p>Australia Privacy Act</p></td>
<td><p>Permet de détecter la présence d'informations généralement couvertes par la loi australienne sur la protection des renseignements personnels, comme un numéro TFN (numéro de dossier fiscal) et un numéro de permis de conduire.</p></td>
</tr>
<tr class="odd">
<td><p>Données financières au Canada</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des données financières au Canada, notamment des numéros de compte bancaire et des cartes de crédit.</p></td>
</tr>
<tr class="even">
<td><p>Canada Health Information Act (HIA)</p></td>
<td><p>Permet de détecter la présence d'informations couvertes par la loi canadienne sur la protection des informations sur la santé en Alberta, notamment des données comme des numéros de passeport et des informations en matière de santé.</p></td>
</tr>
<tr class="odd">
<td><p>Canada Personal Health Act (PHIPA) - Ontario</p></td>
<td><p>Permet de détecter la présence d'informations couvertes par la loi canadienne sur la protection des informations personnelles en matière de santé en Ontario, notamment des données comme des numéros de passeport et des renseignements en matière de santé.</p></td>
</tr>
<tr class="even">
<td><p>Canada Personal Health Information Act (PHIA) - Manitoba</p></td>
<td><p>Permet de détecter la présence d'informations couvertes par la loi canadienne sur la protection des informations personnelles en matière de santé au Manitoba, notamment des données comme des renseignements sur la santé.</p></td>
</tr>
<tr class="odd">
<td><p>Canada Personal Information Protection Act (PIPA)</p></td>
<td><p>Permet de détecter la présence d'informations couvertes par la loi canadienne sur la protection des informations personnelles en Colombie-Britannique, notamment des données comme des numéros de passeport et des informations en matière de santé.</p></td>
</tr>
<tr class="even">
<td><p>Canada Personal Information Protection and Electronic Documents Act (PIPEDA)</p></td>
<td><p>Permet de détecter la présence d'informations couvertes par loi canadienne sur la protection des informations personnelles et des documents électroniques, notamment des données comme des numéros de passeport et des renseignements en matière de santé.</p></td>
</tr>
<tr class="odd">
<td><p>Canada Personally Identifiable Information (PII) Data</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des informations d'identification personnelle au Canada, comme un identificateur d'assurance santé et un numéro de sécurité sociale.</p></td>
</tr>
<tr class="even">
<td><p>Loi informatique et liberté en France</p></td>
<td><p>Permet de détecter la présence d'informations tombant généralement sous la protection de la loi française Informatique et liberté, comme un numéro de sécurité sociale.</p></td>
</tr>
<tr class="odd">
<td><p>Données financières en France</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des données financières en France, notamment des informations comme des numéros de carte de crédit, des informations sur les comptes et des numéros de carte bancaire.</p></td>
</tr>
<tr class="even">
<td><p>France Personally Identifiable Information (PII) Data</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des informations d'identification personnelle en France, notamment des informations comme des numéros de passeport.</p></td>
</tr>
<tr class="odd">
<td><p>Données financières en Allemagne</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des données financières en Allemagne, par exemple des numéros de carte bancaire EU.</p></td>
</tr>
<tr class="even">
<td><p>Germany Personally Identifiable Information (PII) Data</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des informations d'identification personnelle en Allemagne, notamment des informations comme des permis de conduire et des numéros de passeport.</p></td>
</tr>
<tr class="odd">
<td><p>Données financières en Israël</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des données financières en Israël, notamment des numéros de compte bancaire et des codes SWIFT (ou BIC).</p></td>
</tr>
<tr class="even">
<td><p>Israel Personally Identifiable Information (PII) Data</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des informations d'identification personnelle en Israël, par exemple des numéros de carte d'identité nationale.</p></td>
</tr>
<tr class="odd">
<td><p>Israel Protection of Privacy</p></td>
<td><p>Permet de détecter la présence d'informations généralement couvertes par la loi de protection de la vie privée en Israël, notamment des informations comme des numéros de compte bancaire ou de carte d'identité nationale.</p></td>
</tr>
<tr class="even">
<td><p>Données financières au Japon</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des données financières au Japon, notamment des informations comme des numéros de carte de crédit, des informations sur les comptes et des numéros de carte bancaire.</p></td>
</tr>
<tr class="odd">
<td><p>Japan Personally Identifiable Information (PII) Data</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des informations d'identification personnelle au Japon, notamment des informations comme des permis de conduire et des numéros de passeport.</p></td>
</tr>
<tr class="even">
<td><p>Japan Protection of Personal Information</p></td>
<td><p>Permet de détecter la présence d'informations couvertes par la loi japonaise de protection des informations personnelles, notamment les numéros d'enregistrement de résident.</p></td>
</tr>
<tr class="odd">
<td><p>PCI Data Security Standard (PCI DSS)</p></td>
<td><p>Permet de détecter la présence d'informations sujettes aux normes de sécurité des données PCI, notamment des informations comme des numéros de carte de crédit ou de carte bancaire.</p></td>
</tr>
<tr class="even">
<td><p>Saudi Arabia - Anti-Cyber Crime Law</p></td>
<td><p>Permet de détecter la présence d'informations généralement protégées par la Loi Anti-cybercriminalité en Arabie Saoudite, notamment des numéros de compte bancaire international et des codes SWIFT (ou BIC).</p></td>
</tr>
<tr class="odd">
<td><p>Données financières en Arabie Saoudite</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des données financières en Arabie Saoudite, notamment des numéros de compte bancaire international et des codes SWIFT (ou BIC).</p></td>
</tr>
<tr class="even">
<td><p>Saudi Arabia Personally Identifiable Information (PII) Data</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des informations d'identification personnelle en Arabie Saoudite, comme des numéros de carte d'identité nationale.</p></td>
</tr>
<tr class="odd">
<td><p>U.K. Access to Medical Reports Act</p></td>
<td><p>Permet de détecter la présence d'informations protégées par la loi britannique sur l'accès aux rapports médicaux, notamment des données comme les numéros nationaux du service de santé.</p></td>
</tr>
<tr class="even">
<td><p>U.K. Data Protection Act</p></td>
<td><p>Permet de détecter la présence d'informations protégées par la loi britannique sur la protection des données, notamment des données comme les numéros nationaux d'assurance.</p></td>
</tr>
<tr class="odd">
<td><p>Données financières R.U.</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des données financières au Royaume Uni, notamment des informations comme des numéros de carte de crédit, des informations sur les comptes et des numéros de carte bancaire.</p></td>
</tr>
<tr class="even">
<td><p>U.K. Personal Information Online Code of Practice (PIOCP)</p></td>
<td><p>Permet de détecter la présence d'informations protégées par la loi britannique relative au code de pratique en ligne des informations personnelles, notamment des données comme des informations en matière de santé.</p></td>
</tr>
<tr class="odd">
<td><p>U.K. Personally Identifiable Information (PII) Data</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des informations d'identification personnelle au Royaume Uni, notamment des informations comme des permis de conduire et des numéros de passeport.</p></td>
</tr>
<tr class="even">
<td><p>U.K. Privacy and Electronic Communications Regulations</p></td>
<td><p>Permet de détecter la présence d'informations protégées par la loi britannique sur la réglementation des communications électroniques et à caractère privé, notamment des données comme des informations financières.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. Federal Trade Commission (FTC) Consumer Rules</p></td>
<td><p>Permet de détecter la présence d'informations couvertes par la protection des consommateurs de la Commission fédérale du commerce des États-Unis, notamment des données comme des numéros de carte de crédit.</p></td>
</tr>
<tr class="even">
<td><p>Données financières US</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des données financières aux États-Unis, notamment des informations comme des numéros de carte de crédit, des informations sur les comptes et des numéros de carte bancaire.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. Gramm-Leach-Bliley Act (GLBA)</p></td>
<td><p>Permet de détecter la présence d'informations protégées par la loi Gramm-Leach-Bliley Act (GLBA), notamment des informations comme des numéros de sécurité sociale ou des numéros de carte de crédit.</p></td>
</tr>
<tr class="even">
<td><p>U.S. Health Insurance Act (HIPAA)</p></td>
<td><p>Permet de détecter la présence d'informations couvertes par loi de portabilité et comptable de l'assurance santé aux États-Unis, notamment des données comme des numéros de sécurité sociale et des informations en matière de santé.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. Patriot Act</p></td>
<td><p>Permet de détecter la présence d'informations tombant généralement sous la protection de la loi Patriot Act aux États-Unis, notamment des informations comme des numéros de carte de crédit ou des numéros d'identification fiscale.</p></td>
</tr>
<tr class="even">
<td><p>U.S. Personally Identifiable Information (PII) Data</p></td>
<td><p>Permet de détecter la présence d'informations généralement considérées comme des informations d'identification personnelle aux États-Unis, notamment des informations comme des numéros de sécurité sociale ou des numéros de permis de conduire.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. State Breach Notification Laws</p></td>
<td><p>Permet de détecter la présence d'informations protégées par les lois State Breach Notification Laws des États-Unis, notamment des données comme des numéros de sécurité social et des numéros de carte de crédit.</p></td>
</tr>
<tr class="even">
<td><p>U.S. State Social Security Number Confidentiality Laws</p></td>
<td><p>Permet de détecter la présence d'informations protégées par les lois étatiques de confidentialité des numéros de sécurité sociale aux États-Unis, notamment des données comme les numéros de sécurité sociale.</p></td>
</tr>
</tbody>
</table>


## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Création d'une stratégie DLP à partir d'un modèle](how-to-new-dlp-data-loss-prevention-policy-template.md)

[Éléments recherchés par les types d’informations sensibles dans Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

