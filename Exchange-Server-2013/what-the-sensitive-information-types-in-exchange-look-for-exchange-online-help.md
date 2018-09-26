---
title: 'Éléments recherchés par les types d’informations sensibles dans Exchange'
TOCTitle: Éléments recherchés par les types d’informations sensibles
ms:assetid: 98b81f9c-87bb-4905-8e53-04621c3ae74d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150541(v=EXCHG.150)
ms:contentKeyID: 50477289
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Éléments recherchés par les types d’informations sensibles dans Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2018-05-03_

La protection contre la perte de données (DLP) dans Exchange inclut 80 types d’informations sensibles prêts à être utilisés dans le cadre de vos stratégies DLP. Cette rubrique répertorie tous les types d’informations sensibles et illustre les éléments recherchés par une stratégie DLP lorsqu’elle détecte chacun de ces types. Un type d’informations sensibles est défini par un modèle qui peut être identifié par une fonction ou une expression régulière. En outre, une preuve probante, telle que les mots clés et les sommes de contrôle, peut servir à identifier un type d’informations sensibles. Le niveau de confiance et la proximité sont également utilisés dans le processus d’évaluation.

## Numéro de routage ABA


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>9 chiffres mis en forme ou non mis en forme</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Mis en forme :</p>
<ul>
<li><p>Quatre chiffres commençant par 0, 1, 2, 3, 6, 7 ou 8</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Quatre chiffres</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Un chiffre</p></li>
</ul>
<p>Non mis en forme :</p>
<ul>
<li><p>9 chiffres consécutifs commençant par 0, 1, 2, 3, 6, 7 ou 8</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_aba_routing</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_ABA_Routing</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- ABA Routing Number -->
<Entity id="cb353f78-2b72-4c3c-8827-92ebe4f69fdf" patternsProximity="300" recommendedConfidence="75">
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_aba_routing" />
        <Match idRef="Keyword_ABA_Routing" />
      </Pattern>
 </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-1"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ABA_Routing</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>aba</p>
<p># aba</p>
<p># routage aba</p>
<p>numéro de routage aba</p>
<p>#aba</p>
<p>#routageaba</p>
<p>numéro aba</p>
<p>numéroroutageaba</p>
<p># routage american bank association</p>
<p>numéro de routage american bank association</p>
<p>#routageamericanbankassociation</p>
<p>numéroderoutageamericanbankassociation</p>
<p>numéro de routage bancaire</p>
<p>#routagebancaire</p>
<p>numéroderoutagebancaire</p>
<p>numéro de routage</p>
<p>RTN</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d’identité nationale (DNI) pour l’Argentine


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Huit chiffres séparés par des points</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Huit chiffres :</p>
<ul>
<li><p>Deux chiffres</p></li>
<li><p>Un point</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un point</p></li>
<li><p>Trois chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_argentina_national_id</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_argentina_national_id</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Argentina National Identity (DNI) Number -->
<Entity id="eefbb00e-8282-433c-8620-8f1da3bffdb2" recommendedConfidence="75" patternsProximity="300">
   <Pattern confidenceLevel="75">
      <IdMatch idRef="Regex_argentina_national_id"/>
      <Match idRef="Keyword_argentina_national_id"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-3"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_argentina_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Argentina National Identity number</p>
<p>Identity</p>
<p>Identification National Identity Card</p>
<p>DNI</p>
<p>NIC National Registry of Persons</p>
<p>Documento Nacional de Identidad</p>
<p>Registro Nacional de las Personas</p>
<p>Identidad</p>
<p>Identificación</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de compte bancaire Australie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>6 à 10 chiffres avec ou sans le numéro d’agence bancaire de l’État</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Le numéro de compte est composé de 6 à 10 chiffres.</p>
<p>Numéro de succursale bancaire en Australie :</p>
<ul>
<li><p>Trois chiffres</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Trois chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_australia_bank_account_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_australia_bank_account_number</code> est trouvé.</p></li>
<li><p>L’expression régulière <code>Regex_australia_bank_account_number_bsb</code> trouve un contenu qui correspond au modèle.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_australia_bank_account_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_australia_bank_account_number</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Australia Bank Account Number -->
<Entity id="74a54de9-2a30-4aa0-a8aa-3d9327fc07c7" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_australia_bank_account_number" />
        <Match idRef="Keyword_australia_bank_account_number" />
        <Match idRef="Regex_australia_bank_account_number_bsb" />
  </Pattern>
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_australia_bank_account_number" />
        <Match idRef="Keyword_australia_bank_account_number" />
  </Pattern>
 </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-5"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_australia_bank_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>code swift banque</p>
<p>banque correspondante</p>
<p>devise de base</p>
<p>compte aux États-Unis</p>
<p>adresse du titulaire</p>
<p>adresse de la banque</p>
<p>informations du compte</p>
<p>transferts de fonds</p>
<p>frais bancaires</p>
<p>informations sur la banque</p>
<p>informations bancaires</p>
<p>noms complets</p>
<p>iaea</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de permis de conduire Australie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Neuf lettres et chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Neuf lettres et chiffres :</p>
<ul>
<li><p>Deux chiffres ou lettres (ne respectent pas la casse)</p></li>
<li><p>Deux chiffres</p></li>
<li><p>Cinq chiffres ou lettres (ne respectent pas la casse)</p></li>
<li><p>OU</p></li>
<li><p>1 ou 2 lettres facultatives (ne respectant pas la casse)</p></li>
<li><p>4 à 9 chiffres</p></li>
<li><p>OU</p></li>
<li><p>Neuf chiffres ou lettres (ne respectant pas la casse)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_australia_drivers_license_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_australia_drivers_license_number</code> est trouvé.</p></li>
<li><p>Aucun mot clé figurant dans la liste <code>Keyword_australia_drivers_license_number_exclusions</code> n’est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Australia Drivers License Number -->
<Entity id="1cbbc8f5-9216-4392-9eb5-5ac2298d1356" patternsProximity="300" recommendedConfidence="75">
   <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_australia_drivers_license_number" />
        <Match idRef="Keyword_australia_drivers_license_number" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_australia_drivers_license_number_exclusions" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-7"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_australia_drivers_license_number</p></th>
<th><p>Keyword_australia_drivers_license_number_exclusions</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>permis de conduite internationaux</p>
<p>australian automobile association</p>
<p>sydney nsw</p>
<p>permis de conduite international</p>
<p>DriverLicence</p>
<p>DriverLicences</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>DriversLic</p>
<p>DriversLicence</p>
<p>DriversLicences</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permisconduire</p>
<p>Permisconduire</p>
<p>Permisdeconduire</p>
<p>Permisdeconduire</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Driver'sLic</p>
<p>Driver'sLics</p>
<p>Driver'sLicence</p>
<p>Driver'sLicences</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>DriverLic#</p>
<p>DriverLics#</p>
<p>DriverLicence#</p>
<p>DriverLicences#</p>
<p>#Permis conduire</p>
<p>#Permis conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>DriversLic#</p>
<p>DriversLics#</p>
<p>DriversLicence#</p>
<p>DriversLicences#</p>
<p>#Permis conduire</p>
<p>#Permis conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permisconduire</p>
<p>#Permisconduire</p>
<p>#Permisdeconduire</p>
<p>#Permisdeconduire</p>
<p>#Permis conduire</p>
<p>#Permis conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>Driver'sLic#</p>
<p>Driver'sLics#</p>
<p>Driver'sLicence#</p>
<p>Driver'sLicences#</p>
<p>#Permisconduire</p>
<p>#Permisconduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p></td>
<td><p>aaa</p>
<p>DriverLicense</p>
<p>DriverLicenses</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>DriversLicense</p>
<p>DriversLicenses</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permisdeconduire</p>
<p>Permisdeconduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Driver'sLicense</p>
<p>Driver'sLicenses</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>DriverLicense#</p>
<p>DriverLicenses#</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>DriversLicense#</p>
<p>DriversLicenses#</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permisdeconduire</p>
<p>#Permisdeconduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>Driver'sLicense#</p>
<p>Driver'sLicenses#</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de dossier médical Australie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 à 11 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>10 à 11 chiffres :</p>
<ul>
<li><p>Le premier chiffre est compris entre 2 et 6</p></li>
<li><p>Le neuvième chiffre est un chiffre de contrôle</p></li>
<li><p>Le dixième chiffre est le chiffre d’émission</p></li>
<li><p>Le onzième chiffre (facultatif) est le numéro individuel</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 95 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_australian_medical_account_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_Australia_Medical_Account_Number</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_australian_medical_account_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
  <!-- Australia Medical Account Number -->
<Entity id="104a99a0-3d3b-4542-a40d-ab0b9e1efe63" recommendedConfidence="85" patternsProximity="300">
    <Pattern confidenceLevel="95">
     <IdMatch idRef="Func_australian_medical_account_number"/>
     <Any minMatches="1">
     <Match idRef="Keyword_Australia_Medical_Account_Number"/>
     </Any>
  </Pattern>
<Pattern confidenceLevel="85">
     <IdMatch idRef="Func_australian_medical_account_number"/>
     <Any minMatches="0" maxMatches="0">
  <Match idRef="Keyword_Australia_Medical_Account_Number"/>
     </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-9"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_Australia_Medical_Account_Number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>informations sur le compte bancaire</p>
<p>remboursements d’assurance maladie</p>
<p>compte de prêts immobiliers</p>
<p>paiements bancaires</p>
<p>direction de l’information</p>
<p>prêt sur carte de crédit</p>
<p>département des services sociaux</p>
<p>service local</p>
<p>medicare</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de passeport Australie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Une lettre suivie de sept chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Une lettre (ne respectant pas la casse) suivie de sept chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_australia_passport_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_passport</code> ou figurant dans la liste <code>Keyword_australia_passport_number</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Australia Passport Number -->
<Entity id="29869db6-602d-4853-ab93-3484f905df50" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_australia_passport_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_passport" />
          <Match idRef="Keyword_australia_passport_number" />
        </Any>
   </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-11"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_passport</p></th>
<th><p>Keyword_australia_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numéro de passeport</p>
<p>N° de passeport</p>
<p># Passeport</p>
<p>#Passeport</p>
<p>PassportID</p>
<p>n° passeport</p>
<p>numéropasseport</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n°</p>
<p>Passeport numéro</p>
<p># Passeport</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
<td><p>passeport</p>
<p>informations sur le passeport</p>
<p>immigration et citoyenneté</p>
<p>Australie</p>
<p>service de l’immigration</p>
<p>adresse de résidence</p>
<p>service de l’immigration et de la citoyenneté</p>
<p>visa</p>
<p>Carte nationale d’identité</p>
<p>numéro de passeport</p>
<p>document de voyage</p>
<p>autorité émettrice</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de dossier fiscal Australie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>8 ou 9 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>8 à 9 chiffres généralement entrecoupés d’espaces comme suit :</p>
<ul>
<li><p>Trois chiffres</p></li>
<li><p>Un espace facultatif</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un espace facultatif</p></li>
<li><p>2 à 3 chiffres où le dernier chiffre est un chiffre de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 95 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_australian_tax_file_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_Australia_Tax_File_Number</code> est trouvé.</p></li>
<li><p>Aucun mot clé figurant dans la liste <code>Keyword_number_exclusions</code> n’est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_australian_tax_file_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Aucun mot clé figurant dans la liste <code>Keyword_Australia_Tax_File_Number</code> ou <code>Keyword_number_exclusions</code> n’est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
    <!-- Australia Tax File Number -->
<Entity id="e29bc95f-ff70-4a37-aa01-04d17360a4c5" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="95">
        <IdMatch idRef="Func_australian_tax_file_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_Australia_Tax_File_Number" />
        </Any>
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_number_exclusions" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_australian_tax_file_number" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_Australia_Tax_File_Number" />
          <Match idRef="Keyword_number_exclusions" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-13"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_Australia_Tax_File_Number</p></th>
<th><p>Keyword_number_exclusions</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>numéro d’entreprise australien</p>
<p>taux d’imposition marginale</p>
<p>prélèvement d’assurance maladie</p>
<p>numéro de portefeuille</p>
<p>service des vétérans</p>
<p>retenue à la source</p>
<p>déclaration d’impôts individuels</p>
<p>numéro de dossier fiscal</p></td>
<td><p>00000000</p>
<p>11111111</p>
<p>22222222</p>
<p>33333333</p>
<p>44444444</p>
<p>55555555</p>
<p>66666666</p>
<p>77777777</p>
<p>88888888</p>
<p>99999999</p>
<p>000000000</p>
<p>111111111</p>
<p>222222222</p>
<p>333333333</p>
<p>444444444</p>
<p>555555555</p>
<p>666666666</p>
<p>777777777</p>
<p>888888888</p>
<p>999999999</p>
<p>0000000000</p>
<p>1111111111</p>
<p>2222222222</p>
<p>3333333333</p>
<p>4444444444</p>
<p>5555555555</p>
<p>6666666666</p>
<p>7777777777</p>
<p>8888888888</p>
<p>9999999999</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro national Belgique


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>11 chiffres plus des délimiteurs</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>11 chiffres plus des délimiteurs :</p>
<ul>
<li><p>Six chiffres et deux points au format AA.MM.JJ pour la date de naissance</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Trois chiffres séquentiels (impairs pour les hommes, pairs pour les femmes)</p></li>
<li><p>Un point</p></li>
<li><p>Deux chiffres de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_belgium_national_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_belgium_national_number</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Belgium National Number -->
  <Entity id="fb969c9e-0fd1-4b18-8091-a2123c5e6a54" recommendedConfidence="75" patternsProximity="300">
   <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_belgium_national_number"/>
     <Match idRef="Keyword_belgium_national_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-15"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_belgium_national_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Identity</p>
<p>Registration</p>
<p>Identification</p>
<p>ID</p>
<p>Identiteitskaart</p>
<p>Registratie nummer</p>
<p>Identificatie nummer</p>
<p>Identiteit</p>
<p>Registratie</p>
<p>Identificatie</p>
<p>Carte d’identité</p>
<p>numéro d’immatriculation</p>
<p>numéro d’identification</p>
<p>identité</p>
<p>inscription</p>
<p>Identifikation</p>
<p>Identifizierung</p>
<p>Identifikationsnummer</p>
<p>Personalausweis</p>
<p>Registrierung</p>
<p>Registrationsnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d’entité juridique (CNPJ) Brésil


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>14 chiffres qui incluent un numéro d’enregistrement, un numéro de succursale et des chiffres de contrôle, avec des délimiteurs en plus</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>14 chiffres plus des délimiteurs :</p>
<ul>
<li><p>Deux chiffres</p></li>
<li><p>Un point</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un point</p></li>
<li><p>Trois chiffres (ces huit premiers chiffres composent le numéro d’enregistrement)</p></li>
<li><p>Une barre oblique</p></li>
<li><p>Le numéro de succursale à quatre chiffres</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Deux chiffres de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_brazil_cnpj</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_brazil_cnpj</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_brazil_cnpj</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Brazil Legal Entity Number (CNPJ) -->
<Entity id="9b58b5cd-5e90-4df6-b34f-1ebcc88ceae4" recommendedConfidence="85" patternsProximity="300">
   <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_brazil_cnpj"/>
     <Match idRef="Keyword_brazil_cnpj"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_brazil_cnpj"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-17"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_brazil_cnpj</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CNPJ</p>
<p>CNPJ/MF</p>
<p>CNPJ-MF</p>
<p>National Registry of Legal Entities</p>
<p>Taxpayers Registry</p>
<p>Legal entity</p>
<p>Legal entities</p>
<p>Registration Status</p>
<p>Business</p>
<p>Company</p>
<p>CNPJ</p>
<p>Cadastro Nacional da Pessoa Jurídica</p>
<p>Cadastro Geral de Contribuintes</p>
<p>CGC</p>
<p>Pessoa jurídica</p>
<p>Pessoas jurídicas</p>
<p>Situação cadastral</p>
<p>Inscrição</p>
<p>Empresa</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro CPF Brésil


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>11 chiffres qui incluent un chiffre de contrôle et peuvent ou non être mis en forme</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Mis en forme :</p>
<ul>
<li><p>Trois chiffres</p></li>
<li><p>Un point</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un point</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Deux chiffres de contrôle</p></li>
</ul>
<p>Non mis en forme :</p>
<ul>
<li><p>11 chiffres où les deux derniers sont des chiffres de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_brazil_cpf</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_brazil_cpf</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_brazil_cpf</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Brazil CPF Number -->
<Entity id="78e09124-f2c3-4656-b32a-c1a132cd2711" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_brazil_cpf"/>
     <Match idRef="Keyword_brazil_cpf"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_brazil_cpf"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-19"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_brazil_cpf</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPF</p>
<p>Identification</p>
<p>Registration</p>
<p>Revenue</p>
<p>Cadastro de Pessoas Físicas</p>
<p>Imposto</p>
<p>Identificação</p>
<p>Inscrição</p>
<p>Receita</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Brazil National ID Card (RG)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Registro Geral (ancien format)</p>
<dl>
<dd><p>Neuf chiffres</p>
</dd>
</dl>
<p>Registro de Identidade (RIC) (nouveau format)</p>
<dl>
<dd><p>11 chiffres</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Registro Geral (ancien format) :</p>
<ul>
<li><p>Deux chiffres</p></li>
<li><p>Un point</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un point</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Un chiffre de contrôle</p></li>
</ul>
<p>Registro de Identidade (RIC) (nouveau format)</p>
<ul>
<li><p>10 chiffres</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Un chiffre de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_brazil_rg</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_brazil_rg</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_brazil_rg</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Brazil National ID Card (RG) -->
<Entity id="486de900-db70-41b3-a886-abdf25af119c" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_brazil_rg"/>
     <Match idRef="Keyword_brazil_rg"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_brazil_rg"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-21"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_brazil_rg</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cédula de identidade</p>
<p>Carte d’identité</p>
<p>id national</p>
<p>Número de registro</p>
<p>Registro de Identidade</p>
<p>Registro Geral</p>
<p>RG (ce mot clé respecte la casse)</p>
<p>RIC (ce mot clé respecte la casse)</p>
<p></p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de compte bancaire Canada


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Sept ou douze chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Un numéro de compte bancaire au Canada est composé de sept ou douze chiffres.</p>
<p>Un numéro de transit de compte bancaire du Canada est indiqué au format suivant :</p>
<ul>
<li><p>Cinq chiffres</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Trois chiffres</p>
<p>OU</p></li>
<li><p>Un zéro « 0 »</p>
<p>Huit chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_canada_bank_account_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_canada_bank_account_number</code> est trouvé.</p></li>
<li><p>L’expression régulière <code>Regex_canada_bank_account_transit_number</code> trouve un contenu qui correspond au modèle.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_canada_bank_account_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_canada_bank_account_number</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada Bank Account Number -->
<Entity id="552e814c-cb50-4d94-bbaa-bb1d1ffb34de" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_canada_bank_account_number" />
        <Match idRef="Keyword_canada_bank_account_number" />
        <Match idRef="Regex_canada_bank_account_transit_number" />
   </Pattern>
   <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_bank_account_number" />
        <Match idRef="Keyword_canada_bank_account_number" />
   </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-23"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_bank_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>obligations d’épargne du Canada</p>
<p>agence du revenu du Canada</p>
<p>institution financière du Canada</p>
<p>formulaire de dépôt direct</p>
<p>citoyen canadien</p>
<p>représentant légal</p>
<p>notaire</p>
<p>commissaire à l’assermentation</p>
<p>prestation pour la garde d’enfants</p>
<p>prestation universelle pour la garde d’enfants</p>
<p>prestation fiscale canadienne pour enfants</p>
<p>prestation fiscale pour le revenu gagné</p>
<p>taxe de vente harmonisée</p>
<p>numéro d’assurance sociale</p>
<p>remboursement d’impôt</p>
<p>prestation fiscale pour enfants</p>
<p>paiements aux territoires</p>
<p>numéro d’institution</p>
<p>demande de dépôt</p>
<p>informations bancaires</p>
<p>dépôt direct</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de permis de conduire Canada


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Varie selon la province</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Plusieurs modèles pour les différentes provinces : Alberta, Colombie-Britannique, Manitoba, Nouveau-Brunswick, Terre-Neuve-et-Labrador, Nouvelle-Écosse, Ontario, Île-du-Prince-Édouard, Québec et Saskatchewan</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_[province_name]_drivers_license_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_[province_name]_drivers_license_name</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_canada_drivers_license</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada Driver's License Number -->
    <Entity id="37186abb-8e48-4800-ad3c-e3d1610b3db0" patternsProximity="300" recommendedConfidence="75">
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_alberta_drivers_license_number" />
        <Match idRef="Keyword_alberta_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_british_columbia_drivers_license_number" />
        <Match idRef="Keyword_british_columbia_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_manitoba_drivers_license_number" />
        <Match idRef="Keyword_manitoba_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_new_brunswick_drivers_license_number" />
        <Match idRef="Keyword_new_brunswick_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_newfoundland_labrador_drivers_license_number" />
        <Match idRef="Keyword_newfoundland_labrador_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_nova_scotia_drivers_license_number" />
        <Match idRef="Keyword_nova_scotia_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_ontario_drivers_license_number" />
        <Match idRef="Keyword_ontario_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_prince_edward_island_drivers_license_number" />
        <Match idRef="Keyword_prince_edward_island_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_quebec_drivers_license_number" />
        <Match idRef="Keyword_quebec_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_saskatchewan_drivers_license_number" />
        <Match idRef="Keyword_saskatchewan_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-25"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_[province_name]_drivers_license_name</p></th>
<th><p>Keyword_canada_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>L’abréviation de la province, par exemple AB</p>
<p>Le nom de la province, par exemple Alberta</p></td>
<td><p>PC</p>
<p>PC</p>
<p>PCD</p>
<p>PCD</p>
<p>DriverLic</p>
<p>DriverLics</p>
<p>DriverLicense</p>
<p>DriverLicenses</p>
<p>DriverLicence</p>
<p>DriverLicences</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>DriversLic</p>
<p>DriversLics</p>
<p>DriversLicence</p>
<p>DriversLicences</p>
<p>DriversLicense</p>
<p>DriversLicenses</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permisconduire</p>
<p>Permisconduire</p>
<p>Permisdeconduire</p>
<p>Permisdeconduire</p>
<p>Permisdeconduire</p>
<p>Permisdeconduire</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Driver'sLic</p>
<p>Driver'sLics</p>
<p>Driver'sLicense</p>
<p>Driver'sLicenses</p>
<p>Driver'sLicence</p>
<p>Driver'sLicences</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>id</p>
<p>Ids</p>
<p>numéro carte d’identification</p>
<p>numéros carte d’identification</p>
<p># carte d’identification</p>
<p># carte d’identification</p>
<p>carte d’identification</p>
<p>cartes d’identification</p>
<p>carte d’identification</p>
<p>numéro d’identification</p>
<p>numéros d’identification</p>
<p># identification</p>
<p># identification</p>
<p>carte d’identification</p>
<p>cartes d’identification</p>
<p>identification</p>
<p># PC</p>
<p># PC</p>
<p># PCD</p>
<p># PCD</p>
<p>DriverLic#</p>
<p>DriverLics#</p>
<p>DriverLicense#</p>
<p>DriverLicenses#</p>
<p>DriverLicence#</p>
<p>DriverLicences#</p>
<p>#Permis conduire</p>
<p>#Permis conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>DriversLic#</p>
<p>DriversLics#</p>
<p>DriversLicense#</p>
<p>DriversLicenses#</p>
<p>DriversLicence#</p>
<p>DriversLicences#</p>
<p>#Permis conduire</p>
<p>#Permis conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permisconduire</p>
<p>#Permisconduire</p>
<p>#Permisdeconduire</p>
<p>#Permisdeconduire</p>
<p>#Permisdeconduire</p>
<p>#Permisdeconduire</p>
<p>#Permis conduire</p>
<p>#Permis conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>Driver'sLic#</p>
<p>Driver'sLics#</p>
<p>Driver'sLicense#</p>
<p>Driver'sLicenses#</p>
<p>Driver'sLicence#</p>
<p>Driver'sLicences#</p>
<p>#Permisconduire</p>
<p>#Permisconduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>Permis de conduire #</p>
<p>#id</p>
<p>#ids</p>
<p>#carte carte d’identification</p>
<p>#cartes carte d’identification</p>
<p>#carte d’identification</p>
<p>#carte d’identification</p>
<p>#cartes d’identification</p>
<p>#identification</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de service de santé Canada


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>10 chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_canada_health_service_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_canada_health_service_number</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada Health Service Number -->
<Entity id="59c0bf39-7fab-482c-af25-00faa4384c94" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_health_service_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_canada_health_service_number" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-27"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_health_service_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>numéro d’assurance-maladie</p>
<p>informations sur le patient</p>
<p>services de santé</p>
<p>services spécialisés</p>
<p>accident automobile</p>
<p>hôpital pour malades</p>
<p>psychiatre</p>
<p>indemnisation des salariés</p>
<p>handicap</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de passeport Canada


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Deux lettres majuscules suivies de six chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Deux lettres majuscules suivies de six chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_canada_passport_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_canada_passport_number</code> ou figurant dans la liste <code>Keyword_passport</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
 <!-- Canada Passport Number -->
<Entity id="14d0db8b-498a-43ed-9fca-f6097ae687eb" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_passport_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_canada_passport_number" />
          <Match idRef="Keyword_passport" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-29"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_passport_number</p></th>
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>citoyenneté canadienne</p>
<p>passeport canadien</p>
<p>demande de passeport</p>
<p>photos pour passeport</p>
<p>traducteur agréé</p>
<p>citoyens canadiens</p>
<p>temps de traitement</p>
<p>demande de renouvellement</p></td>
<td><p>Numéro de passeport</p>
<p>N° de passeport</p>
<p># Passeport</p>
<p>#Passeport</p>
<p>PassportID</p>
<p>n° passeport</p>
<p>numéropasseport</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n°</p>
<p>Passeport numéro</p>
<p># Passeport</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## NIMP (numéro d’identification médicale personnel) Canada


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Neuf chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Neuf chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_canada_phin</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Au moins deux mots clés présents dans la liste <code>Keyword_canada_phin</code> ou <code>Keyword_canada_provinces</code> sont trouvés.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada PHIN -->
<Entity id="722e12ac-c89a-4ec8-a1b7-fea3469f89db" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_phin" />
        <Any minMatches="2">
          <Match idRef="Keyword_canada_phin" />
          <Match idRef="Keyword_canada_provinces" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-31"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_phin</p></th>
<th><p>Keyword_canada_provinces</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>numéro d’assurance sociale</p>
<p>loi sur les renseignements médicaux</p>
<p>renseignements relatifs à l’impôt sur le revenu</p>
<p>santé Manitoba</p>
<p>enregistrement aux services de santé</p>
<p>achats de médicaments sur ordonnance</p>
<p>admissibilité aux prestations</p>
<p>santé personnelle</p>
<p>procuration</p>
<p>numéro d’enregistrement</p>
<p>numéro d’assurance-maladie</p>
<p>recommandation par le médecin</p>
<p>professionnel de bien-être</p>
<p>orientation d’un patient</p>
<p>santé et bien-être</p></td>
<td><p>Nunavut</p>
<p>Québec</p>
<p>Territoires du Nord-Ouest</p>
<p>Ontario</p>
<p>Colombie-britannique</p>
<p>Alberta</p>
<p>Saskatchewan</p>
<p>Manitoba</p>
<p>Yukon</p>
<p>Terre-Neuve-et-Labrador</p>
<p>Nouveau-Brunswick</p>
<p>Nouvelle-Écosse</p>
<p>Île-du-Prince-Édouard</p>
<p>Canada</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d'assurance sociale Canada


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Neuf chiffres avec éventuellement des traits d’union ou des espaces</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Mis en forme :</p>
<ul>
<li><p>Trois chiffres</p></li>
<li><p>Un trait d’union ou un espace</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un trait d’union ou un espace</p></li>
<li><p>Trois chiffres</p></li>
</ul>
<p>Non mis en forme :</p>
<ul>
<li><p>Neuf chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_canadian_sin</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Au moins deux des éléments suivants, quelle que soit la combinaison :</p>
<ul>
<li><p>Un mot clé figurant dans la liste <code>Keyword_sin</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_sin_collaborative</code> est trouvé.</p></li>
<li><p>La fonction <code>Func_eu_date</code> trouve une date au format correct.</p></li>
</ul></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_unformatted_canadian_sin</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_sin</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada Social Insurance Number -->
<Entity id="a2f29c85-ecb8-4514-a610-364790c0773e" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_canadian_sin" />
        <Any minMatches="2">
          <Match idRef="Keyword_sin" />
          <Match idRef="Keyword_sin_collaborative" />
          <Match idRef="Func_eu_date" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_unformatted_canadian_sin" />
        <Match idRef="Keyword_sin" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-33"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_sin</p></th>
<th><p>Keyword_sin_collaborative</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>assoc</p>
<p>assurance sociale</p>
<p>numéro d’assurance sociale</p>
<p>assoc</p>
<p>nss</p>
<p>nss</p>
<p>sécurité sociale</p>
<p>numéro d’assurance sociale</p>
<p>numéro d’identification nationale</p>
<p>id national</p>
<p># assoc</p>
<p>ass soc</p>
<p>ass sociale</p></td>
<td><p>permis de conduire</p>
<p>permis de conduire</p>
<p>permis de conduire</p>
<p>permis de conduire</p>
<p>DDN</p>
<p>Date de naissance</p>
<p>Anniversaire</p>
<p>Date of Birth</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte d’identité Chili


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>7 ou 8 chiffres plus des délimiteurs et un chiffre ou une lettre de contrôle</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>7 ou 8 chiffres, plus des délimiteurs :</p>
<ul>
<li><p>1 ou 2 chiffres</p></li>
<li><p>Un point</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un point</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un tiret</p></li>
<li><p>Un chiffre ou une lettre (ne respectant pas la casse) de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_chile_id_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_chile_id_card</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_chile_id_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Chile Identity Card Number -->
<Entity id="4e979794-49a0-407e-a0b9-2c536937b925" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_chile_id_card"/>
     <Match idRef="Keyword_chile_id_card"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_chile_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-35"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_chile_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>National Identification Number</p>
<p>Identity card</p>
<p>ID</p>
<p>Identification</p>
<p>Rol Único Nacional</p>
<p>RUN</p>
<p>Rol Único Tributario</p>
<p>RUT</p>
<p>Cédula de Identidad</p>
<p>Número De Identificación Nacional</p>
<p>Tarjeta de identificación</p>
<p>Identificación</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte d’identité de résident Chine (RPC)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>18 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>18 chiffres :</p>
<ul>
<li><p>Six chiffres qui composent un code d’adresse</p></li>
<li><p>Huit chiffres sous la forme AAAAMMJJ qui correspondent à la date de naissance</p></li>
<li><p>Trois chiffres qui correspondent à un code d’opération</p></li>
<li><p>Un chiffre de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_china_resident_id</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_china_resident_id</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_china_resident_id</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- China Resident Identity Card (PRC) Number -->
<Entity id="c92daa86-2d16-4871-901f-816b3f554fc1" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_china_resident_id"/>
     <Match idRef="Keyword_china_resident_id"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_china_resident_id"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-37"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_china_resident_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Resident Identity Card</p>
<p>PRC</p>
<p>National Identification Card</p>
<p>身份证</p>
<p>居民 身份证</p>
<p>居民身份证</p>
<p>鉴定</p>
<p>身分證</p>
<p>居民 身份證</p>
<p>鑑定</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte de crédit


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>16 chiffres qui peuvent être mis en forme ou non mis en forme (dddddddddddddddd) et doit réussir le test de Luhn.</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Modèle très complexe et puissant qui détecte les cartes de visite de toutes les principales marques du monde, notamment Visa, MasterCard, Discover Card, JCB, American Express, etc.</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui, la somme de contrôle de Luhn</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_credit_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>L’une des affirmations suivantes est vraie :</p>
<ul>
<li><p>Un mot clé figurant dans la liste <code>Keyword_cc_verification</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_cc_name</code> est trouvé.</p></li>
<li><p>La fonction <code>Func_expiration_date</code> trouve une date au format correct.</p></li>
</ul></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 65 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_credit_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Credit Card Number -->
<Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_credit_card" />
        <Any minMatches="1">
          <Match idRef="Keyword_cc_verification" />
          <Match idRef="Keyword_cc_name" />
          <Match idRef="Func_expiration_date" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="65">
        <IdMatch idRef="Func_credit_card" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-39"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_cc_verification</p></th>
<th><p>Keyword_cc_name</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>vérification de la carte</p>
<p>numéro d’identification de la carte</p>
<p>nvc</p>
<p>nic</p>
<p>cvc2</p>
<p>cvv2</p>
<p>pin block</p>
<p>code de sécurité</p>
<p>numéro de sécurité</p>
<p>n° de sécurité</p>
<p>numéro d’émission</p>
<p>n° d’émission</p>
<p>cryptogramme</p>
<p>numéro de sécurité</p>
<p>numéro de sécurité</p>
<p>kreditkartenprüfnummer</p>
<p>kreditkartenprufnummer</p>
<p>prüfziffer</p>
<p>prufziffer</p>
<p>sicherheits Kode</p>
<p>sicherheitscode</p>
<p>sicherheitsnummer</p>
<p>verfalldatum</p>
<p>codice di verifica</p>
<p>cod. sicurezza</p>
<p>cod sicurezza</p>
<p>n autorizzazione</p>
<p>código</p>
<p>codigo</p>
<p>cod. seg</p>
<p>cod seg</p>
<p>código de segurança</p>
<p>codigo de seguranca</p>
<p>codigo de segurança</p>
<p>código de seguranca</p>
<p>cód. Segurança</p>
<p>cod. seguranca cod. segurança</p>
<p>cód. seguranca</p>
<p>cód segurança</p>
<p>cod seguranca cod segurança</p>
<p>cód seguranca</p>
<p>número de verificação</p>
<p>numero de verificacao</p>
<p>ablauf</p>
<p>gültig bis</p>
<p>gültigkeitsdatum</p>
<p>gultig bis</p>
<p>gultigkeitsdatum</p>
<p>scadenza</p>
<p>data scad</p>
<p>fecha de expiracion</p>
<p>fecha de venc</p>
<p>vencimiento</p>
<p>válido hasta</p>
<p>valido hasta</p>
<p>vto</p>
<p>data de expiração</p>
<p>data de expiracao</p>
<p>data em que expira</p>
<p>validade</p>
<p>valor</p>
<p>vencimento</p>
<p>Venc</p></td>
<td><p>amex</p>
<p>american express</p>
<p>americanexpress</p>
<p>Visa</p>
<p>mastercard</p>
<p>master card</p>
<p>mc</p>
<p>mastercards</p>
<p>master cards</p>
<p>diner’s Club</p>
<p>diners club</p>
<p>dinersclub</p>
<p>discover card</p>
<p>discovercard</p>
<p>discover cards</p>
<p>JCB</p>
<p>japanese card bureau</p>
<p>carte blanche</p>
<p>carteblanche</p>
<p>carte de crédit</p>
<p># cc</p>
<p># cc :</p>
<p>date d’expiration</p>
<p>date d’exp</p>
<p>date d’expiration</p>
<p>date d’expiration</p>
<p>date d’exp</p>
<p>date expiration</p>
<p>carte bancaire</p>
<p>carte bancaire</p>
<p>numéro de carte</p>
<p>num de carte</p>
<p>numéro de carte</p>
<p>numéros de carte</p>
<p>numéros de carte</p>
<p>carte de crédit</p>
<p>cartes de crédit</p>
<p>cartes de crédit</p>
<p>ncc</p>
<p>titulaire de la carte</p>
<p>titulaire de la carte</p>
<p>titulaires de la carte</p>
<p>titulaires de la carte</p>
<p>carte de vérification</p>
<p>carte de vérification</p>
<p>cartes de vérification</p>
<p>cartes de vérification</p>
<p>carte de débit</p>
<p>carte de débit</p>
<p>cartes de débit</p>
<p>cartes de débit</p>
<p>carte de retrait</p>
<p>carte de retrait</p>
<p>cartes de retrait</p>
<p>cartes de retrait</p>
<p>enroute</p>
<p>en route</p>
<p>type de carte</p>
<p>carte bancaire</p>
<p>carte de crédit</p>
<p>carte de credit</p>
<p>numéro de carte</p>
<p>numero de carte</p>
<p>nº de la carte</p>
<p>nº de carte</p>
<p>kreditkarte</p>
<p>karte</p>
<p>karteninhaber</p>
<p>karteninhabers</p>
<p>kreditkarteninhaber</p>
<p>kreditkarteninstitut</p>
<p>kreditkartentyp</p>
<p>eigentümername</p>
<p>kartennr</p>
<p>kartennummer</p>
<p>kreditkartennummer</p>
<p>kreditkarten-nummer</p>
<p>Carta di credito</p>
<p>Carta credito</p>
<p>n. carta</p>
<p>n carta</p>
<p>nr. carta</p>
<p>nr carta</p>
<p>numero carta</p>
<p>numero della carta</p>
<p>numero di carta</p>
<p>tarjeta credito</p>
<p>tarjeta de credito</p>
<p>tarjeta crédito</p>
<p>tarjeta de crédito</p>
<p>tarjeta de atm</p>
<p>tarjeta atm</p>
<p>tarjeta debito</p>
<p>tarjeta de debito</p>
<p>tarjeta débito</p>
<p>tarjeta de débito</p>
<p>nº de tarjeta</p>
<p>no. de tarjeta</p>
<p>no de tarjeta</p>
<p>numero de tarjeta</p>
<p>número de tarjeta</p>
<p>tarjeta no</p>
<p>tarjetahabiente</p>
<p>cartão de crédito</p>
<p>cartão de credito</p>
<p>cartao de crédito</p>
<p>cartao de credito</p>
<p>cartão de débito</p>
<p>cartao de débito</p>
<p>cartão de debito</p>
<p>cartao de debito</p>
<p>débito automático</p>
<p>debito automatico</p>
<p>número do cartão</p>
<p>numero do cartão</p>
<p>número do cartao</p>
<p>numero do cartao</p>
<p>número de cartão</p>
<p>numero de cartão</p>
<p>número de cartao</p>
<p>numero de cartao</p>
<p>nº do cartão</p>
<p>nº do cartao</p>
<p>nº. do cartão</p>
<p>no do cartão</p>
<p>no do cartao</p>
<p>no. do cartão</p>
<p>no. do cartao</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte d’identité Croatie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Neuf chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Neuf chiffres consécutifs</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_croatia_id_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_croatia_id_card</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!--Croatia Identity Card Number-->
<Entity id="ff12f884-c20a-4189-b185-34c8e7258d47" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_croatia_id_card"/>
     <Match idRef="Keyword_croatia_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-41"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_croatia_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Croatian identity card</p>
<p>Osobna iskaznica</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d’identification personnel (OIB) Croatie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>10 chiffres :</p>
<ul>
<li><p>Six chiffres sous la forme JJMMAA qui correspondent à la date de naissance</p></li>
<li><p>Quatre chiffres où le dernier chiffre est un chiffre de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_croatia_oib_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_croatia_oib_number</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_croatia_oib_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Croatia Personal Identification (OIB) Number -->
<Entity id="31983b6d-db95-4eb2-a630-b44bd091968d" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_croatia_oib_number"/>
     <Match idRef="Keyword_croatia_oib_number"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_croatia_oib_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-43"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_croatia_oib_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Personal Identification Number</p>
<p>Osobni identifikacijski broj</p>
<p>OIB</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte d’identité nationale tchèque


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 chiffres contenant une barre oblique</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>10 chiffres :</p>
<ul>
<li><p>Six chiffres correspondant à la date de naissance</p></li>
<li><p>Une barre oblique</p></li>
<li><p>Quatre chiffres où le dernier chiffre est un chiffre de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_czech_id_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_czech_id_card</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Czech National Identity Card Number -->
<Entity id="60c0725a-4eb6-455b-9dda-05d8a7396497" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_czech_id_card"/>
     <Match idRef="Keyword_czech_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-45"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_czech_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Czech national identity card</p>
<p>Občanský průka</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d’identification personnel Danemark


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 chiffres contenant un trait d’union</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>10 chiffres :</p>
<ul>
<li><p>Six chiffres au format JJMMAA qui correspondent à la date de naissance</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Quatre chiffres où le dernier chiffre est un chiffre de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_denmark_id</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_denmark_id</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Denmark Personal Identification Number -->
<Entity id="6c4f2fef-56e1-4c00-8093-88d7a01cf460" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_denmark_id"/>
     <Match idRef="Keyword_denmark_id"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-47"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_denmark_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Personal Identification Number</p>
<p>CPR</p>
<p>Det Centrale Personregister</p>
<p>Personnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de la Drug Enforcement Agency (DEA)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Deux lettres suivies de sept chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Le modèle doit inclure tous les éléments suivants :</p>
<ul>
<li><p>Une lettre (ne respecte pas la casse) à partir de cet ensemble de lettres possibles : abcdefghjklmnprstux, qui est un code d’utilisateur enregistré</p></li>
<li><p>Une lettre (ne respecte pas la casse), qui est la première lettre du nom de l’utilisateur enregistré</p></li>
<li><p>Sept chiffres, le dernier est le chiffre de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_dea_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- DEA Number -->
<Entity id="9a5445ad-406e-43eb-8bd7-cac17ab6d0e4" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_dea_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><p>Aucune</p></td>
</tr>
</tbody>
</table>


## Numéro de carte de débit Union européenne


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>16 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Modèle très complexe et puissant</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_eu_debit_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Au moins une des affirmations suivantes est vraie :</p>
<ul>
<li><p>Un mot clé figurant dans la liste <code>Keyword_eu_debit_card</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_card_terms_dict</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_card_security_terms_dict</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_card_expiration_terms_dict</code> est trouvé.</p></li>
<li><p>La fonction <code>Func_expiration_date</code> trouve une date au format correct.</p></li>
</ul></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
    <!-- EU Debit Card Number -->
    <Entity id="0e9b3178-9678-47dd-a509-37222ca96b42" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_eu_debit_card" />
        <Any minMatches="1">
          <Match idRef="Keyword_eu_debit_card" />
          <Match idRef="Keyword_card_terms_dict" />
          <Match idRef="Keyword_card_security_terms_dict" />
          <Match idRef="Keyword_card_expiration_terms_dict" />
          <Match idRef="Func_expiration_date" />
        </Any>
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-50"> </h3>
<div>
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
<th><p>Keyword_eu_debit_card</p></th>
<th> </th>
<th><p>Keyword_card_terms_dict</p></th>
<th><p>Keyword_card_security_terms_dict</p></th>
<th><p>Keyword_card_expiration_terms_dict</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>numéro de compte</p>
<p>numéro de carte</p>
<p>n° carte</p>
<p>numéro de sécurité</p>
<p># cc</p></td>
<td> </td>
<td><p>num de compte</p>
<p>num de compte</p>
<p>n° compte</p>
<p>american express</p>
<p>americanexpress</p>
<p>americano espresso</p>
<p>amex</p>
<p>carte de retrait</p>
<p>cartes de retrait</p>
<p>atm kaart</p>
<p>carte de retrait</p>
<p>cartes de retrait</p>
<p>atmkaart</p>
<p>atmkaarten</p>
<p>bancontact</p>
<p>carte bancaire</p>
<p>bankkaart</p>
<p>titulaire de la carte</p>
<p>titulaires de la carte</p>
<p>num de carte</p>
<p>numéro de carte</p>
<p>numéros de carte</p>
<p>type de carte</p>
<p>cardano numerico</p>
<p>titulaire de la carte</p>
<p>titulaires de la carte</p>
<p>numéro de carte</p>
<p>numéros de carte</p>
<p>carta bianca</p>
<p>Carta credito</p>
<p>Carta di credito</p>
<p>cartao de credito</p>
<p>cartao de crédito</p>
<p>cartao de debito</p>
<p>cartao de débito</p>
<p>carte bancaire</p>
<p>carte blanche</p>
<p>carte bleue</p>
<p>carte de credit</p>
<p>carte de crédit</p>
<p>carte di credito</p>
<p>carteblanche</p>
<p>cartão de credito</p>
<p>cartão de crédito</p>
<p>cartão de debito</p>
<p>cartão de débito</p>
<p>cb</p>
<p>ncc</p>
<p>carte de vérification</p>
<p>cartes de vérification</p>
<p>carte de vérification</p>
<p>cartes de vérification</p>
<p>chequekaart</p>
<p>cirrus</p>
<p>cirrus-edc-maestro</p>
<p>controlekaart</p>
<p>controlekaarten</p>
<p>carte de crédit</p>
<p>cartes de crédit</p>
<p>carte de crédit</p>
<p>cartes de crédit</p>
<p>debetkaart</p>
<p>debetkaarten</p>
<p>carte de débit</p>
<p>cartes de débit</p>
<p>carte de débit</p>
<p>cartes de débit</p>
<p>debito automatico</p>
<p>diners club</p>
<p>dinersclub</p>
<p>discover</p>
<p>discover card</p>
<p>discover cards</p>
<p>discovercard</p>
<p>discovercards</p>
<p>débito automático</p>
<p>edc</p>
<p>eigentümername</p>
<p>carte de crédit européenne</p>
<p>hoofdkaart</p>
<p>hoofdkaarten</p>
<p>in viaggio</p>
<p>japanese card bureau</p>
<p>japanse kaartdienst</p>
<p>jcb</p>
<p>kaart</p>
<p>kaart num</p>
<p>kaartaantal</p>
<p>kaartaantallen</p>
<p>kaarthouder</p>
<p>kaarthouders</p>
<p>karte</p>
<p>karteninhaber</p>
<p>karteninhabers</p>
<p>kartennr</p>
<p>kartennummer</p>
<p>kreditkarte</p>
<p>kreditkarten-nummer</p>
<p>kreditkarteninhaber</p>
<p>kreditkarteninstitut</p>
<p>kreditkartennummer</p>
<p>kreditkartentyp</p>
<p>maestro</p>
<p>master card</p>
<p>master cards</p>
<p>mastercard</p>
<p>mastercards</p>
<p>mc</p>
<p>mister cash</p>
<p>n carta</p>
<p>n. carta</p>
<p>no de tarjeta</p>
<p>no do cartao</p>
<p>no do cartão</p>
<p>no. de tarjeta</p>
<p>no. do cartao</p>
<p>no. do cartão</p>
<p>nr carta</p>
<p>nr. carta</p>
<p>numeri di scheda</p>
<p>numero carta</p>
<p>numero de cartao</p>
<p>numero de carte</p>
<p>numero de cartão</p>
<p>numero de tarjeta</p>
<p>numero della carta</p>
<p>numero di carta</p>
<p>numero di scheda</p>
<p>numero do cartao</p>
<p>numero do cartão</p>
<p>numéro de carte</p>
<p>nº carta</p>
<p>nº de carte</p>
<p>nº de la carte</p>
<p>nº de tarjeta</p>
<p>nº do cartao</p>
<p>nº do cartão</p>
<p>nº. do cartão</p>
<p>número de cartao</p>
<p>número de cartão</p>
<p>número de tarjeta</p>
<p>número do cartao</p>
<p>scheda dell’assegno</p>
<p>scheda dell’atmosfera</p>
<p>scheda dell’atmosfera</p>
<p>scheda della banca</p>
<p>scheda di controllo</p>
<p>scheda di debito</p>
<p>scheda matrice</p>
<p>schede dell’atmosfera</p>
<p>schede di controllo</p>
<p>schede di debito</p>
<p>schede matrici</p>
<p>scoprono la scheda</p>
<p>scoprono le schede</p>
<p>solo</p>
<p>supporti di scheda</p>
<p>supporto di scheda</p>
<p>switch</p>
<p>tarjeta atm</p>
<p>tarjeta credito</p>
<p>tarjeta de atm</p>
<p>tarjeta de credito</p>
<p>tarjeta de debito</p>
<p>tarjeta debito</p>
<p>tarjeta no</p>
<p>tarjetahabiente</p>
<p>tipo della scheda</p>
<p>ufficio giapponese della</p>
<p>scheda</p>
<p>v pay</p>
<p>v-pay</p>
<p>visa</p>
<p>visa plus</p>
<p>visa electron</p>
<p>visto</p>
<p>visum</p>
<p>vpay</p></td>
<td><p>numéro d’identification de la carte</p>
<p>vérification de la carte</p>
<p>cardi la verifica</p>
<p>nic</p>
<p>cod seg</p>
<p>cod seguranca</p>
<p>cod segurança</p>
<p>cod sicurezza</p>
<p>cod. seg</p>
<p>cod. seguranca</p>
<p>cod. segurança</p>
<p>cod. sicurezza</p>
<p>codice di sicurezza</p>
<p>codice di verifica</p>
<p>codigo</p>
<p>codigo de seguranca</p>
<p>codigo de segurança</p>
<p>crittogramma</p>
<p>cryptogramme</p>
<p>cryptogramme</p>
<p>cv2</p>
<p>cvc</p>
<p>cvc2</p>
<p>nvc</p>
<p>cvv</p>
<p>cvv2</p>
<p>cód seguranca</p>
<p>cód segurança</p>
<p>cód. seguranca</p>
<p>cód. Segurança</p>
<p>código</p>
<p>código de seguranca</p>
<p>código de segurança</p>
<p>de kaart controle</p>
<p>geeft nr suit</p>
<p>n° d’émission</p>
<p>numéro d’émission</p>
<p>kaartidentificatienummer</p>
<p>kreditkartenprufnummer</p>
<p>kreditkartenprüfnummer</p>
<p>kwestieaantal</p>
<p>no. dell’edizione</p>
<p>no. di sicurezza</p>
<p>numéro de sécurité</p>
<p>numero de verificacao</p>
<p>numero dell’edizione</p>
<p>numero di identificazione della</p>
<p>scheda</p>
<p>numero di sicurezza</p>
<p>numero van veiligheid</p>
<p>numéro de sécurité</p>
<p>nº autorizzazione</p>
<p>número de verificação</p>
<p>perno il blocco</p>
<p>pin block</p>
<p>prufziffer</p>
<p>prüfziffer</p>
<p>code de sécurité</p>
<p>n° de sécurité</p>
<p>numéro de sécurité</p>
<p>sicherheits kode</p>
<p>sicherheitscode</p>
<p>sicherheitsnummer</p>
<p>speldblok</p>
<p>veiligheid nr</p>
<p>veiligheidsaantal</p>
<p>veiligheidscode</p>
<p>veiligheidsnummer</p>
<p>verfalldatum</p></td>
<td><p>ablauf</p>
<p>data de expiracao</p>
<p>data de expiração</p>
<p>data del exp</p>
<p>data di exp</p>
<p>data di scadenza</p>
<p>data em que expira</p>
<p>data scad</p>
<p>data scadenza</p>
<p>date de validité</p>
<p>datum afloop</p>
<p>datum van exp</p>
<p>de afloop</p>
<p>espira</p>
<p>espira</p>
<p>date d’exp</p>
<p>exp datum</p>
<p>expiration</p>
<p>expire</p>
<p>expire</p>
<p>expiration</p>
<p>fecha de expiracion</p>
<p>fecha de venc</p>
<p>gultig bis</p>
<p>gultigkeitsdatum</p>
<p>gültig bis</p>
<p>gültigkeitsdatum</p>
<p>la scadenza</p>
<p>scadenza</p>
<p>valable</p>
<p>validade</p>
<p>valido hasta</p>
<p>valor</p>
<p>venc</p>
<p>vencimento</p>
<p>vencimiento</p>
<p>verloopt</p>
<p>vervaldag</p>
<p>vervaldatum</p>
<p>vto</p>
<p>válido hasta</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## ID national finlandais


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Six chiffres plus un caractère indiquant un siècle plus trois chiffres plus un chiffre de contrôle</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Le modèle doit inclure tous les éléments suivants :</p>
<ul>
<li><p>Six chiffres au format JJMMAA qui représentent la date de naissance</p></li>
<li><p>Marqueur de siècle (soit « - », « + » ou « a »)</p></li>
<li><p>Numéro d’identification personnel à trois chiffres</p></li>
<li><p>Un chiffre ou une lettre (ne respectant pas la casse) de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_finnish_national_id</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_finnish_national_id</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Finnish National ID-->
<Entity id="338FD995-4CB5-4F87-AD35-79BD1DD926C1" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_finnish_national_id" />
          <Match idRef="Keyword_finnish_national_id" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-52"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_finnish_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sosiaaliturvatunnus</p>
<p>SOTU Henkilötunnus HETU</p>
<p>Personbeteckning</p>
<p>Personnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de passeport Finlande


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Combinaison de neuf lettres et chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Combinaison de neuf lettres et chiffres :</p>
<ul>
<li><p>Deux lettres (ne respectant pas la casse)</p></li>
<li><p>Sept chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_finland_passport_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_finland_passport_number</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Finland Passport Number -->
<Entity id="d1685ac3-1d3a-40f8-8198-32ef5669c7a5" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_finland_passport_number"/>
     <Match idRef="Keyword_finland_passport_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-54"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_finland_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Passport</p>
<p>Passi</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de permis de conduire France


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>12 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>12 chiffres avec validation pour écarter les modèles similaires, comme les numéros de téléphone français</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_french_drivers_license</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Au moins une des affirmations suivantes est vraie :</p>
<ul>
<li><p>Un mot clé figurant dans la liste <code>Keyword_french_drivers_license</code> est trouvé.</p></li>
<li><p>La fonction <code>Func_eu_date</code> trouve une date au format correct.</p></li>
</ul></li>
</ul>

```Command&nbsp;Line
<!-- France Driver's License Number -->
<Entity id="18e55a36-a01b-4b0f-943d-dc10282a1824" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_french_drivers_license" />
        <Any minMatches="1">
          <Match idRef="Keyword_french_drivers_license" />
          <Match idRef="Func_eu_date" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-56"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_french_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>permis de conduire</p>
<p>permis de conduire</p>
<p>permis de conduire</p>
<p>permis de conduire</p>
<p>permis de conduire</p>
<p>numéro de permis</p>
<p>numéro de permis</p>
<p>numéros de permis</p>
<p>numéros de permis</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Carte nationale d’identité (CNI) France


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>12 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>12 chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 65 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_france_cni</code> trouve un contenu qui correspond au modèle.</p></li>
</ul>

```Command&nbsp;Line
<!-- France CNI -->
<Entity id="f741ac74-1bc0-4665-b69b-f0c7f927c0c4" patternsProximity="300" recommendedConfidence="65">
  <Pattern confidenceLevel="65">
        <IdMatch idRef="Regex_france_cni" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><p>Aucun</p></td>
</tr>
</tbody>
</table>


## Numéro de passeport France


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Neuf chiffres et lettres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Neuf chiffres et lettres :</p>
<ul>
<li><p>Deux chiffres</p></li>
<li><p>Deux lettres (ne respectant pas la casse)</p></li>
<li><p>Cinq chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_fr_passport</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_passport</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- France Passport Number -->
<Entity id="3008b884-8c8c-4cd8-a289-99f34fc7ff5d" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_fr_passport" />
        <Match idRef="Keyword_passport" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-59"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numéro de passeport</p>
<p>N° de passeport</p>
<p># Passeport</p>
<p>#Passeport</p>
<p>PassportID</p>
<p>n° passeport</p>
<p>numéropasseport</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n°</p>
<p>Passeport numéro</p>
<p># Passeport</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de sécurité sociale (INSEE) France


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>15 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Doit correspondre à l’un des deux modèles suivants :</p>
<ul>
<li><p>13 chiffres suivis d’un espace suivi de deux chiffres, ou</p></li>
<li><p>15 chiffres consécutifs</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 95 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_french_insee</code> ou <code>Func_fr_insee</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_fr_insee</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_french_insee</code> ou <code>Func_fr_insee</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Aucun mot clé figurant dans la liste <code>Keyword_fr_insee</code> n’est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- France INSEE -->
<Entity id="71f62b97-efe0-4aa1-aa49-e14de253619d" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="95">
        <IdMatch idRef="Func_french_insee" />
        <Match idRef="Func_fr_insee" />
        <Any minMatches="1">
          <Match idRef="Keyword_fr_insee" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_french_insee" />
        <Match idRef="Func_fr_insee" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_fr_insee" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-61"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_fr_insee</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>insee</p>
<p>securité sociale</p>
<p>securite sociale</p>
<p>id national</p>
<p>numéro d’identification nationale</p>
<p>numéro d’identité</p>
<p>n° d’identité</p>
<p>n° d’identité</p>
<p>numéro d’identité</p>
<p>n° d’identité</p>
<p>n° d’identité</p>
<p>numéro de sécurité sociale</p>
<p>code de sécurité sociale</p>
<p>numéro d’assurance sociale</p>
<p>le numéro d’identification nationale</p>
<p>d’identité nationale</p>
<p>numéro de sécurité sociale</p>
<p>le code de la sécurité sociale</p>
<p>numéro d’assurance sociale</p>
<p>numéro de sécu</p>
<p>code sécu</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de permis de conduire Allemagne


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Combinaison de 11 chiffres et lettres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>11 chiffres et lettres (ne respectent pas la casse) :</p>
<ul>
<li><p>Un chiffre ou une lettre</p></li>
<li><p>Deux chiffres</p></li>
<li><p>Six chiffres ou lettres</p></li>
<li><p>Un chiffre</p></li>
<li><p>Un chiffre ou une lettre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_german_drivers_license</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Au moins une des affirmations suivantes est vraie :</p>
<ul>
<li><p>Un mot clé figurant dans la liste <code>Keyword_german_drivers_license_number</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_german_drivers_license_collaborative</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_german_drivers_license</code> est trouvé.</p></li>
</ul></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- German Driver's License Number -->
<Entity id="91da9335-1edb-45b7-a95f-5fe41a16c63c" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_german_drivers_license" />
        <Any minMatches="1">
          <Match idRef="Keyword_german_drivers_license_number" />
          <Match idRef="Keyword_german_drivers_license_collaborative" />
          <Match idRef="Keyword_german_drivers_license" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-63"> </h3>
<div>
<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_german_drivers_license_number</p></th>
<th> </th>
<th><p>Keyword_german_drivers_license_collaborative</p></th>
<th><p>Keyword_german_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Führerschein</p>
<p>Fuhrerschein</p>
<p>Fuehrerschein</p>
<p>Führerscheinnummer</p>
<p>Fuhrerscheinnummer</p>
<p>Fuehrerscheinnummer</p>
<p>Führerschein-</p>
<p>Fuhrerschein-</p>
<p>Fuehrerschein-</p>
<p>FührerscheinnummerNr</p>
<p>FuhrerscheinnummerNr</p>
<p>FuehrerscheinnummerNr</p>
<p>FührerscheinnummerKlasse</p>
<p>FuhrerscheinnummerKlasse</p>
<p>FuehrerscheinnummerKlasse</p>
<p>Führerschein - Nr</p>
<p>Fuhrerschein - Nr</p>
<p>Fuehrerschein - Nr</p>
<p>Führerschein - Klasse</p>
<p>Fuhrerschein - Klasse</p>
<p>Fuehrerschein - Klasse</p>
<p>FührerscheinnummerNr</p>
<p>FuhrerscheinnummerNr</p>
<p>FuehrerscheinnummerNr</p>
<p>FührerscheinnummerKlasse</p>
<p>FuhrerscheinnummerKlasse</p>
<p>FuehrerscheinnummerKlasse</p>
<p>Führerschein - Nr</p>
<p>Fuhrerschein - Nr</p>
<p>Fuehrerschein - Nr</p>
<p>Führerschein - Klasse</p>
<p>Fuhrerschein - Klasse</p>
<p>Fuehrerschein - Klasse</p>
<p>PC</p>
<p>PC</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Driver’s Licenses</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p></td>
<td> </td>
<td><p>Nr-Führerschein</p>
<p>Nr-Fuhrerschein</p>
<p>Nr-Fuehrerschein</p>
<p>No-Führerschein</p>
<p>No-Fuhrerschein</p>
<p>No-Fuehrerschein</p>
<p>N-Führerschein</p>
<p>N-Fuhrerschein</p>
<p>N-Fuehrerschein</p>
<p>Nr-Führerschein</p>
<p>Nr-Fuhrerschein</p>
<p>Nr-Fuehrerschein</p>
<p>No-Führerschein</p>
<p>No-Fuhrerschein</p>
<p>No-Fuehrerschein</p>
<p>N-Führerschein</p>
<p>N-Fuhrerschein</p>
<p>N-Fuehrerschein</p></td>
<td><p>ausstellungsdatum</p>
<p>ausstellungsort</p>
<p>ausstellende behöde</p>
<p>ausstellende behorde</p>
<p>ausstellende behoerde</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte d’identité Allemagne


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Depuis le 1er novembre 2010</p>
<dl>
<dd><p>Neuf lettres et chiffres</p>
</dd>
</dl>
<p>Du 1er avril 1987 au 31 octobre 2010</p>
<dl>
<dd><p>10 chiffres</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Depuis le 1er novembre 2010 :</p>
<ul>
<li><p>Une lettre (ne respecte pas la casse)</p></li>
<li><p>Huit chiffres</p></li>
</ul>
<p>Du 1er avril 1987 au 31 octobre 2010</p>
<ul>
<li><p>10 chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 65 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_germany_id_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_germany_id_card</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Germany Identity Card Number -->
<Entity id="e577372f-c42e-47a0-9d85-bebed1c237d4" recommendedConfidence="65" patternsProximity="300">
  <Pattern confidenceLevel="65">
     <IdMatch idRef="Regex_germany_id_card"/>
     <Match idRef="Keyword_germany_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-65"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_germany_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Identity Card</p>
<p>ID</p>
<p>Identification</p>
<p>Personalausweis</p>
<p>Identifizierungsnummer</p>
<p>Ausweis</p>
<p>Identifikation</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de passeport Allemagne


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 chiffres ou lettres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Le modèle doit inclure tous les éléments suivants :</p>
<ul>
<li><p>Le premier caractère est un chiffre ou une lettre de cet ensemble (C, F, G, H, J, K)</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Cinq chiffres ou lettres à partir de cet ensemble (C, -H, J-N, P, R, T, V-Z)</p></li>
<li><p>Un chiffre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_german_passport</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé présent dans l’une des cinq listes de mots clés est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_german_passport_data</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé présent dans l’une des cinq listes de mots clés est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- German Passport Number -->
<Entity id="2e3da144-d42b-47ed-b123-fbf78604e52c" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_german_passport" />
        <Any minMatches="1">
          <Match idRef="Keyword_german_passport" />
          <Match idRef="Keyword_german_passport_collaborative" />
          <Match idRef="Keyword_german_passport_number" />
          <Match idRef="Keyword_german_passport1" />
          <Match idRef="Keyword_german_passport2" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_german_passport_data" />
        <Any minMatches="1">
          <Match idRef="Keyword_german_passport" />
          <Match idRef="Keyword_german_passport_collaborative" />
          <Match idRef="Keyword_german_passport_number" />
          <Match idRef="Keyword_german_passport1" />
          <Match idRef="Keyword_german_passport2" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-67"> </h3>
<div>
<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_german_passport</p></th>
<th> </th>
<th><p>Keyword_german_passport_collaborative</p></th>
<th><p>Keyword_german_passport_number</p></th>
<th><p>Keyword_german_passport1</p></th>
<th><p>Keyword_german_passport2</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>reisepass</p>
<p>reisepasse</p>
<p>reisepassnummer</p>
<p>passeport</p>
<p>passports</p></td>
<td> </td>
<td><p>geburtsdatum</p>
<p>ausstellungsdatum</p>
<p>ausstellungsort</p></td>
<td><p>No-Reisepass</p>
<p>Nr-Reisepass</p></td>
<td><p>Reisepass-Nr</p></td>
<td><p>bnationalit.t</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Carte d’identité nationale Grèce


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Combinaison de 7 ou 8 lettres et chiffres, plus un tiret</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Sept lettres et chiffres (ancien format) :</p>
<ul>
<li><p>Une lettre (de l’alphabet grec)</p></li>
<li><p>Un tiret</p></li>
<li><p>Six chiffres</p></li>
</ul>
<p>Huit lettres et chiffres (nouveau format) :</p>
<ul>
<li><p>Deux lettres dont le caractère majuscule figure à la fois dans l’alphabet grec et l’alphabet latin (ABEZHIKMNOPTYX)</p></li>
<li><p>Un tiret</p></li>
<li><p>Six chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_greece_id_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_greece_id_card</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Greece National ID Card -->
<Entity id="82568215-1da1-46d3-874a-d2294d81b5ac" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_greece_id_card"/>
     <Match idRef="Keyword_greece_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-69"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_greece_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Greek identity Card</p>
<p>Tautotita</p>
<p>Δελτίο αστυνομικής ταυτότητας</p>
<p>Ταυτότητα</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte d’identité (HKID) Hong Kong


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Combinaison de 8 ou 9 lettres et chiffres plus éventuellement des parenthèses autour du dernier caractère</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Combinaison de 8 ou 9 lettres :</p>
<ul>
<li><p>1 ou 2 lettres (ne respectant pas la casse)</p></li>
<li><p>Six chiffres</p></li>
<li><p>Le dernier caractère (un chiffre ou la lettre A), qui est le chiffre de contrôle et est éventuellement entre parenthèses.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_hong_kong_id_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_hong_kong_id_card</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 65 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_hong_kong_id_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Hong Kong Identity Card (HKID) number -->
<Entity id="e63c28a7-ad29-4c17-a41a-3d2a0b70fd9c" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_hong_kong_id_card"/>
     <Match idRef="Keyword_hong_kong_id_card"/>
  </Pattern>
  <Pattern confidenceLevel="65">
     <IdMatch idRef="Func_hong_kong_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-71"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_hong_kong_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Hong Kong Identity Card</p>
<p>HKID</p>
<p>ID card</p>
<p>香港身份證</p>
<p>香港永久性居民身份證</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de compte permanent Inde


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 lettres ou chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>10 lettres ou chiffres :</p>
<ul>
<li><p>Cinq lettres (ne respectant pas la casse)</p></li>
<li><p>Quatre chiffres</p></li>
<li><p>Une lettre qui est un chiffre de contrôle alphabétique</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_india_permanent_account_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_india_permanent_account_number</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- India Permanent Account Number -->
<Entity id="2602bfee-9bb0-47a5-a7a6-2bf3053e2804" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_india_permanent_account_number"/>
     <Match idRef="Keyword_india_permanent_account_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-73"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_india_permanent_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Permanent Account Number</p>
<p>PAN</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d’identification unique (Aadhaar) Inde


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>12 chiffres contenant éventuellement des espaces ou des tirets</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>12 chiffres :</p>
<ul>
<li><p>Quatre chiffres</p></li>
<li><p>Éventuellement un tiret ou un espace</p></li>
<li><p>Quatre chiffres</p></li>
<li><p>Éventuellement un tiret ou un espace</p></li>
<li><p>Le chiffre final, qui est le chiffre de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_india_aadhaar</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_india_aadhar</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_india_aadhaar</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- India Unique Identification (Aadhaar) number -->
<Entity id="1ca46b29-76f5-4f46-9383-cfa15e91048f" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_india_aadhaar"/>
     <Match idRef="Keyword_india_aadhar"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_india_aadhaar"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-75"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_india_aadhar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aadhar</p>
<p>Aadhaar</p>
<p>UID</p>
<p>आधार</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte d’identité (KTP) Indonésie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>16 chiffres contenant éventuellement des points</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>16 chiffres :</p>
<ul>
<li><p>Code à deux chiffres désignant la province</p></li>
<li><p>Un point (facultatif)</p></li>
<li><p>Code à deux chiffres désignant une régence ou une ville</p></li>
<li><p>Code à deux chiffres désignant un sous-district</p></li>
<li><p>Un point (facultatif)</p></li>
<li><p>Six chiffres au format JJMMAA qui correspondent à la date de naissance</p></li>
<li><p>Un point (facultatif)</p></li>
<li><p>Quatre chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_indonesia_id_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_indonesia_id_card</code> est trouvé.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_indonesia_id_card</code> trouve un contenu qui correspond au modèle.</p></li>
</ul>

```Command&nbsp;Line
<!-- Indonesia Identity Card (KTP) Number -->
<Entity id="da68fdb0-f383-4981-8c86-82689d3b7d55" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_indonesia_id_card"/>
     <Match idRef="Keyword_indonesia_id_card"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_indonesia_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-77"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_indonesia_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KTP</p>
<p>Kartu Tanda Penduduk</p>
<p>Nomor Induk Kependudukan</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de compte bancaire international (IBAN)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Code pays (à deux lettres) plus chiffres de contrôle (à deux chiffres) plus numéro BBAN (jusqu’à 30 chiffres)</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Le modèle doit inclure tous les éléments suivants :</p>
<ul>
<li><p>Code pays à deux lettres</p></li>
<li><p>Deux chiffres de contrôle (suivis d’un espace facultatif)</p></li>
<li><p>1 à 7 groupes de quatre lettres ou chiffres (séparés par des espaces facultatifs)</p></li>
<li><p>1 à 3 lettres ou chiffres</p></li>
</ul>
<p>Le format pour chaque pays est légèrement différent. Le type d’informations sensibles IBAN recouvre ces 60 pays :</p>
<dl>
<dd><p>ad, ae, al, at, az, ba, be, bg, bh, ch, cr, cy, cz, de, dk, do, ee, es, fi, fo, fr, gb, ge, gi, gl, gr, hr, hu, ie, il, is, it, kw, kz, lb, li, lt, lu, lv, mc, md, me, mk, mr, mt, mu, nl, no, pl, pt, ro, rs, sa, se, si, sk, sm, tn, tr, vg</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_iban</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<Entity id="e7dc4711-11b7-4cb0-b88b-2c394a771f0e" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_iban" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><p>Aucun</p></td>
</tr>
</tbody>
</table>


## Adresse IP


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>IPv4 :</p>
<ul>
<li><p>Modèle complexe qui tient compte des versions mises en forme (points) et non mises en forme (sans points) des adresses IPv4</p></li>
</ul>
<p>IPv6 :</p>
<ul>
<li><p>Modèle complexe qui tient compte des numéros IPv6 mis en forme (qui incluent les signes deux-points)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Pour IPv6, le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_ipv6_address</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Aucun mot clé figurant dans la liste <code>Keyword_ipaddress</code> n’est trouvé.</p></li>
</ul>
<p>Pour IPv4, le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 95 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_ipv4_address</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_ipaddress</code> est trouvé.</p></li>
</ul>
<p>Pour IPv6, le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 95 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_ipv6_address</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Aucun mot clé figurant dans la liste <code>Keyword_ipaddress</code> n’est trouvé.</p></li>
</ul>

```Command&nbsp;Line
    <!-- IP Address -->
    <Entity id="1daa4ad5-e2dd-4ca4-a788-54722c09efb2" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_ipv6_address" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_ipaddress" />
        </Any>
      </Pattern>
      <Pattern confidenceLevel="95">
        <IdMatch idRef="Regex_ipv4_address" />
        <Any minMatches="1">
          <Match idRef="Keyword_ipaddress" />
        </Any>
      </Pattern>
      <Pattern confidenceLevel="95">
        <IdMatch idRef="Regex_ipv6_address" />
        <Any minMatches="1">
          <Match idRef="Keyword_ipaddress" />
        </Any>
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-80"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ipaddress</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IP (ce mot clé respecte la casse)</p>
<p>ip address</p>
<p>adresses IP</p>
<p>protocole internet</p>
<p>IP-כתובת ה</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de service public personnel (PPS) Irlande


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Ancien format (jusqu’au 31 décembre 2012)</p>
<dl>
<dd><p>Sept chiffres suivis de 1 ou 2 lettres</p>
</dd>
</dl>
<p>Nouveau format (à partir du 1er janvier 2013)</p>
<dl>
<dd><p>Sept chiffres suivis de deux lettres</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Ancien format (jusqu’au 31 décembre 2012)</p>
<ul>
<li><p>Sept chiffres</p></li>
<li><p>1 ou 2 lettres (ne respectant pas la casse)</p></li>
</ul>
<p>Nouveau format (à partir du 1er janvier 2013)</p>
<ul>
<li><p>Sept chiffres</p></li>
<li><p>Une lettre (ne respectant pas la casse), qui est un chiffre de contrôle alphabétique</p></li>
<li><p>La lettre « A » ou « H » (ne respectant pas la casse)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_ireland_pps</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>L’une des affirmations suivantes est vraie :</p>
<ul>
<li><p>Un mot clé figurant dans la liste <code>Keyword_ireland_pps</code> est trouvé.</p></li>
<li><p>La fonction <code>Func_eu_date</code> trouve une date au format correct.</p></li>
</ul></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 65 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_ireland_pps</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Ireland Personal Public Service (PPS) Number -->
<Entity id="1cdb674d-c19a-4fcf-9f4b-7f56cc87345a" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_ireland_pps"/>
     <Any minMatches="1">
  <Match idRef="Keyword_ireland_pps"/>
  <Match idRef="Func_eu_date"/>
     </Any>
  </Pattern>
  <Pattern confidenceLevel="65">
     <IdMatch idRef="Func_ireland_pps"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-82"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ireland_pps</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Personal Public Service Number</p>
<p>PPS Number</p>
<p>PPS Num</p>
<p>PPS No.</p>
<p>PPS #</p>
<p>PPS#</p>
<p>PPSN</p>
<p>Public Services Card</p>
<p>Uimhir Phearsanta Seirbhíse Poiblí</p>
<p>Uimh. PSP</p>
<p>PSP</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de compte bancaire Israël


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>13 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Mis en forme :</p>
<ul>
<li><p>Deux chiffres</p></li>
<li><p>Un tiret</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un tiret</p></li>
<li><p>Huit chiffres</p></li>
</ul>
<p>Non mis en forme :</p>
<ul>
<li><p>13 chiffres consécutifs</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_israel_bank_account_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_israel_bank_account_number</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Israel Bank Account Number -->
<Entity id="7d08b2ff-a0b9-437f-957c-aeddbf9b2b25" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_israel_bank_account_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_israel_bank_account_number" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-84"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_israel_bank_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numéro de compte bancaire</p>
<p>Compte bancaire</p>
<p>Numéro de compte</p>
<p>מספר חשבון בנק</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Carte nationale d’identité Israël


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Neuf chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Neuf chiffres consécutifs</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_israeli_national_id_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_Israel_National_ID</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Israel National ID Number -->
<Entity id="e05881f5-1db1-418c-89aa-a3ac5c5277ee" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_israeli_national_id_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_Israel_National_ID" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-86"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_Israel_National_ID</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>מספר זהות</p>
<p>Numéro d’identification nationale</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de permis de conduire Italie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Une combinaison de 10 lettres et chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Une combinaison de 10 lettres et chiffres :</p>
<ul>
<li><p>Une lettre (ne respecte pas la casse)</p></li>
<li><p>La lettre « A » ou « V » (ne respecte pas la casse)</p></li>
<li><p>Sept lettres (ne respectent pas la casse), des chiffres ou le trait de soulignement</p></li>
<li><p>Une lettre (ne respecte pas la casse)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_italy_drivers_license_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_italy_drivers_license_number</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Italy Driver's license Number -->
<Entity id="97d6244f-9157-41bd-8e0c-9d669a5c4d71" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_italy_drivers_license_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_italy_drivers_license_number" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-88"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_italy_drivers_license_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>numero di patente di guida</p>
<p>patente di guida</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de compte bancaire Japon


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Sept ou huit chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Numéro de compte bancaire :</p>
<ul>
<li><p>Sept ou huit chiffres</p></li>
</ul>
<p>Code guichet du compte bancaire :</p>
<ul>
<li><p>Quatre chiffres</p></li>
<li><p>Un espace ou un tiret (facultatif)</p></li>
<li><p>Trois chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_jp_bank_account</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_jp_bank_account</code> est trouvé.</p></li>
<li><p>L’une des affirmations suivantes est vraie :</p>
<ul>
<li><p>La fonction <code>Func_jp_bank_account_branch_code</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_jp_bank_branch_code</code> est trouvé.</p></li>
</ul></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_jp_bank_account</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_jp_bank_account</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Japan Bank Account Number -->
<Entity id="d354f95b-96ee-4b80-80bc-4377312b55bc" patternsProximity="300" recommendedConfidence="75">
  <Version minEngineVersion="15.01.0131.000">
    <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_jp_bank_account" />
          <Match idRef="Keyword_jp_bank_account" />
          <Any minMatches="1">
            <Match idRef="Func_jp_bank_account_branch_code" />
            <Match idRef="Keyword_jp_bank_branch_code" />
          </Any>
      </Pattern>
  </Version>    
     <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_bank_account" />
        <Match idRef="Keyword_jp_bank_account" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-90"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_bank_account</p></th>
<th> </th>
<th><p>Keyword_jp_bank_branch_code</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numéro de compte courant</p>
<p>Compte courant</p>
<p># compte courant</p>
<p>Numéro compte courant</p>
<p># compte courant</p>
<p>N° de compte courant</p>
<p>N° de compte courant</p>
<p>Numéro de compte bancaire</p>
<p>Compte bancaire</p>
<p># Compte bancaire</p>
<p>Numéro de compte bancaire</p>
<p># Compte bancaire</p>
<p>N° de compte bancaire</p>
<p>N° de compte bancaire</p>
<p>Numéro de compte d’épargne</p>
<p>Compte d’épargne</p>
<p>N° de compte d’épargne</p>
<p>Numéro de compte d’épargne</p>
<p># compte d’épargne</p>
<p>N° de compte d’épargne</p>
<p>N° de compte d’épargne</p>
<p>Numéro de compte de débit</p>
<p>Compte de débit</p>
<p># Compte de débit</p>
<p>Numéro de compte de débit</p>
<p># Compte de débit</p>
<p>N° de compte de débit</p>
<p>N° de compte de débit</p>
<p>口座番号を当座預金口座の確認</p>
<p>＃アカウントの確認、勘定番号の確認</p>
<p>＃勘定の確認</p>
<p>勘定番号の確認</p>
<p>口座番号の確認</p>
<p>銀行口座番号</p>
<p>銀行口座</p>
<p>銀行口座＃</p>
<p>銀行の勘定番号</p>
<p>銀行のacct＃</p>
<p>銀行の勘定いいえ</p>
<p>銀行口座番号</p>
<p>普通預金口座番号</p>
<p>預金口座</p>
<p>貯蓄口座＃</p>
<p>貯蓄勘定の数</p>
<p>貯蓄勘定＃</p>
<p>貯蓄勘定番号</p>
<p>普通預金口座番号</p>
<p>引き落とし口座番号</p>
<p>口座番号</p>
<p>口座番号 #</p>
<p>デビットのacct番号</p>
<p>デビット勘定＃</p>
<p>デビットACCTの番号</p>
<p>デビット口座番号</p></td>
<td> </td>
<td><p>Otemachi</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de permis de conduire Japon


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>12 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>12 chiffres consécutifs</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_jp_drivers_license_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_jp_drivers_license_number</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Japan Driver's License Number -->
<Entity id="c6011143-d087-451c-8313-7f6d4aed2270" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_drivers_license_number" />
        <Match idRef ="Keyword_jp_drivers_license_number" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-92"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_drivers_license_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>driver license</p>
<p>drivers license</p>
<p>driver’s license</p>
<p>drivers licenses</p>
<p>driver’s licenses</p>
<p>driver licenses</p>
<p>dl#</p>
<p>dls#</p>
<p>lic#</p>
<p>#permis</p>
<p>運転免許証</p>
<p>運転免許</p>
<p>免許証</p>
<p>免許</p>
<p>運転免許証番号</p>
<p>運転免許番号</p>
<p>免許証番号</p>
<p>免許番号</p>
<p>運転免許証ナンバー</p>
<p>運転免許ナンバー</p>
<p>免許証ナンバー</p>
<p>運転免許証No.</p>
<p>運転免許No.</p>
<p>免許証No.</p>
<p>免許No.</p>
<p>運転免許証#</p>
<p>運転免許#</p>
<p>免許証#</p>
<p>免許#</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de passeport Japon


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Deux lettres suivies de sept chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Deux lettres (ne respectant pas la casse) suivies de sept chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_jp_passport</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_jp_passport</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Japan Passport Number -->
<Entity id="75177310-1a09-4613-bf6d-833aae3743f8" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_passport" />
        <Match idRef="Keyword_jp_passport" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-94"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Matricule de résident Japon


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>11 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>11 chiffres consécutifs</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_jp_resident_registration_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_jp_resident_registration_number</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Japan Resident Registration Number -->
<Entity id="01c1209b-6389-4faf-a5f8-3f7e13899652" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_resident_registration_number" />
        <Match idRef ="Keyword_jp_resident_registration_number" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-96"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_resident_registration_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numéro d’enregistrement du résident</p>
<p>Numéro d’enregistrement du résident</p>
<p>Numéro de base d’enregistrement des résidents</p>
<p>N° d’enregistrement du résident</p>
<p>N° d’enregistrement du résident</p>
<p>N° de base d’enregistrement des résidents</p>
<p>N° d’enregistrement du résident de base</p>
<p>住民登録番号、登録番号をレジデント</p>
<p>住民基本登録番号、登録番号</p>
<p>住民基本レジストリ番号を常駐</p>
<p>登録番号を常駐住民基本台帳登録番号</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d’assurance sociale Japon


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>7 à 12 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>7 à 12 chiffres :</p>
<ul>
<li><p>Quatre chiffres</p></li>
<li><p>Un trait d’union (facultatif)</p></li>
<li><p>Six chiffres</p></li>
<li><p>OU</p></li>
<li><p>7 à 12 chiffres consécutifs</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_jp_sin</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_jp_sin</code> est trouvé.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_jp_sin_pre_1997</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_jp_sin</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Japan Social Insurance Number -->
<Entity id="c840e719-0896-45bb-84fd-1ed5c95e45ff" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_jp_sin" />
        <Match idRef="Keyword_jp_sin" />
    </Pattern>
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_sin_pre_1997" />
        <Match idRef="Keyword_jp_sin" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-98"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_sin</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>N° d’assurance sociale</p>
<p>Numéro d’assurance sociale</p>
<p>Numéro d’assurance sociale</p>
<p>社会保険のテンキー</p>
<p>社会保険番号</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte d’identité Malaisie


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>12 chiffres contenant éventuellement des traits d’union</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>12 chiffres :</p>
<ul>
<li><p>Six chiffres au format AAMMJJ correspondant à la date de naissance</p></li>
<li><p>Un tiret (facultatif)</p></li>
<li><p>Le code à deux lettres du lieu de naissance</p></li>
<li><p>Un tiret (facultatif)</p></li>
<li><p>Trois chiffres aléatoires</p></li>
<li><p>Code de sexe à un chiffre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_malaysia_id_card_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_malaysia_id_card_number</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Malaysia ID Card Number -->
</Entity>
      <Entity id="7f0e921c-9677-435b-aba2-bb8f1013c749" patternsProximity="300" recommendedConfidence="85">
        <Pattern confidenceLevel="85">
            <IdMatch idRef="Regex_malaysia_id_card_number" />
            <Match idRef="Keyword_malaysia_id_card_number" />
        </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-100"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_malaysia_id_card_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyKad</p>
<p>Identity Card</p>
<p>ID Card</p>
<p>Carte d’identification</p>
<p>Digital Application Card</p>
<p>Kad Akuan Diri</p>
<p>Kad Aplikasi Digital</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de service du citoyen (BSN) Pays-Bas


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>8 à 9 chiffres contenant éventuellement des espaces</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>8 à 9 chiffres :</p>
<ul>
<li><p>Trois chiffres</p></li>
<li><p>Un espace (facultatif)</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un espace (facultatif)</p></li>
<li><p>2 à 3 chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_netherlands_bsn</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_netherlands_bsn</code> est trouvé.</p></li>
<li><p>La fonction <code>Func_eu_date2</code> trouve une date au format correct.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Netherlands Citizen's Service (BSN) Number -->
<Entity id="c5f54253-ef7e-44f6-a578-440ed67e946d" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
       <IdMatch idRef="Func_netherlands_bsn" /> 
       <Match idRef="Keyword_netherlands_bsn" /> 
       <Match idRef="Func_eu_date2" /> 
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-102"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_netherlands_bsn</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Citizen service number</p>
<p>BSN</p>
<p>Burgerservicenummer</p>
<p>Sofinummer</p>
<p>Persoonsgebonden nummer</p>
<p>Persoonsnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro du Ministère de la santé Nouvelle-Zélande


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Trois lettres, un espace (facultatif) et quatre chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Trois lettres (ne respectant pas la casse) un espace (facultatif) quatre chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_new_zealand_ministry_of_health_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_nz_terms</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- New Zealand Health Number -->
<Entity id="2b71c1c8-d14e-4430-82dc-fd1ed6bf05c7" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_new_zealand_ministry_of_health_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_nz_terms" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-104"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_nz_terms</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NHI</p>
<p>Nouvelle-Zélande</p>
<p>Santé</p>
<p>treatment</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d’identification Norvège


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>11 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>11 chiffres :</p>
<ul>
<li><p>Six chiffres au format JJMMAA qui correspondent à la date de naissance</p></li>
<li><p>Numéro individuel à trois chiffres</p></li>
<li><p>Deux chiffres de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_norway_id_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_norway_id_number</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_norway_id_numbe</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Norway Identification Number -->
<Entity id="d4c8a798-e9f2-4bd3-9652-500d24080fc3" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_norway_id_number"/>
     <Match idRef="Keyword_norway_id_number"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_norway_id_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-106"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_norway_id_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Personal identification number</p>
<p>Norwegian ID Number</p>
<p>ID Number</p>
<p>Identification</p>
<p>Personnummer</p>
<p>Fødselsnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d’identification multifonction unifié Philippines


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>12 chiffres séparés par des traits d’union</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>12 chiffres :</p>
<ul>
<li><p>Quatre chiffres</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Sept chiffres</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Un chiffre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_philippines_unified_id</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_philippines_id</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Philippines Unified Multi-Purpose ID number -->
<Entity id="019b39dd-8c25-4765-91a3-d9c6baf3c3b3" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_philippines_unified_id"/>
     <Match idRef="Keyword_philippines_id"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-108"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_philippines_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Unified Multi-Purpose ID</p>
<p>UMID</p>
<p>Identity Card</p>
<p>Pinag-isang Multi-Layunin ID</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Carte d'identité Pologne


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Trois lettres et six chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Trois lettres (ne respectant pas la casse) suivis de six chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_polish_national_id</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_polish_national_id_passport_number</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Poland Identity Card-->
<Entity id="25E64989-ED5D-40CA-A939-6C14183BB7BF" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_polish_national_id" />
          <Match idRef="Keyword_polish_national_id_passport_number" />
      </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-110"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_polish_national_id_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nazwa je nr dowodu tożsamości</p>
<p>Dowód Tożsamości</p>
<p>dow. os.</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## ID national polonais (PESEL)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>11 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>11 chiffres consécutifs</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_pesel_identification_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_pesel_identification_number</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Poland National ID (PESEL) -->      
<Entity id="E3AAF206-4297-412F-9E06-BA8487E22456" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_pesel_identification_number" />
          <Match idRef="Keyword_pesel_identification_number" />
      </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-112"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_pesel_identification_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nr PESEL</p>
<p>PESEL</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Passeport Pologne


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Deux lettres et sept chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Deux lettres (ne respectant pas la casse) suivies de sept chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_polish_passport_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_polish_national_id_passport_number</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Poland Passport Number -->
<Entity id="03937FB5-D2B6-4487-B61F-0F8BFF7C3517" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_polish_passport_number" />
          <Match idRef="Keyword_polish_national_id_passport_number" />
      </Pattern>
</Entity>
</Version>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-114"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_polish_national_id_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nazwa je nr dowodu tożsamości</p>
<p>Dowód Tożsamości</p>
<p>dow. os.</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte de citoyen Portugal


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Huit chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Huit chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_portugal_citizen_card</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_portugal_citizen_card</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Portugal Citizen Card Number -->
<Entity id="91a7ece2-add4-4986-9a15-c84544d81ecd" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_portugal_citizen_card"/>
     <Match idRef="Keyword_portugal_citizen_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-116"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_portugal_citizen_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Citizen Card</p>
<p>National ID Card</p>
<p>CC</p>
<p>Cartão de Cidadão</p>
<p>Bilhete de Identidade</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## ID national Arabie saoudite


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>10 chiffres consécutifs</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_saudi_arabia_national_id</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_saudi_arabia_national_id</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Saudi Arabia National ID -->
<Entity id="8c5a0ba8-404a-41a3-8871-746aa21ee6c0" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_saudi_arabia_national_id" />
        <Any minMatches="1">
          <Match idRef="Keyword_saudi_arabia_national_id" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-118"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_saudi_arabia_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carte d’identification</p>
<p>numéro de carte d’identité</p>
<p>Numéro d’identification</p>
<p>الوطنية الهوية بطاقة رقم</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de carte d’identité d’enregistrement national (NRIC) Singapour


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Neuf lettres et chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Neuf lettres et chiffres :</p>
<ul>
<li><p>La lettre « F », « G », « S » ou « T » (ne respectant pas la casse)</p></li>
<li><p>Sept chiffres</p></li>
<li><p>Un chiffre de contrôle alphabétique</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_singapore_nric</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_singapore_nric</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_singapore_nric</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Singapore National Registration Identity Card (NRIC) Number -->
<Entity id="cead390a-dd83-4856-9751-fb6dc98c34da" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_singapore_nric"/>
     <Match idRef="Keyword_singapore_nric"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_singapore_nric"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-120"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_singapore_nric</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>National Registration Identity Card</p>
<p>Identity Card Number</p>
<p>NRIC</p>
<p>IC</p>
<p>Foreign Identification Number</p>
<p>FIN</p>
<p>身份证</p>
<p>身份證</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d’identification Afrique du Sud


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>13 chiffres pouvant contenir des espaces</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>13 chiffres :</p>
<ul>
<li><p>Six chiffres au format AAMMJJ correspondant à la date de naissance</p></li>
<li><p>Quatre chiffres</p></li>
<li><p>Un indicateur de citoyenneté à un chiffre</p></li>
<li><p>Le chiffre « 8 » ou « 9 »</p></li>
<li><p>Un chiffre pour la somme de contrôle</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_south_africa_identification_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_south_africa_identification_number</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- South Africa Identification Number -->
<Entity id="e2adf7cb-8ea6-4048-a2ed-d89eb65f2780" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_south_africa_identification_number"/>
     <Match idRef="Keyword_south_africa_identification_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-122"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_south_africa_identification_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Identity card</p>
<p>ID</p>
<p>Identification</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Matricule de résident Corée du Sud


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>13 chiffres contenant un trait d’union</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>13 chiffres :</p>
<ul>
<li><p>Six chiffres au format AAMMJJ correspondant à la date de naissance</p></li>
<li><p>Un trait d’union</p></li>
<li><p>Un chiffre déterminé par le siècle et le sexe</p></li>
<li><p>Code à quatre chiffres désignant la région de naissance</p></li>
<li><p>Un chiffre utilisé pour différencier les personnes dont les chiffres précédents sont identiques.</p></li>
<li><p>Un chiffre de contrôle.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_south_korea_resident_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_south_korea_resident_number</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_south_korea_resident_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- South Korea Resident Registration Number -->
<Entity id="5b802e18-ba80-44c4-bc83-bf2ad36ae36a" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_south_korea_resident_number"/>
     <Match idRef="Keyword_south_korea_resident_number"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_south_korea_resident_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-124"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_south_korea_resident_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>National ID card</p>
<p>Citizen’s Registration Number</p>
<p>Jumin deungnok beonho</p>
<p>RRN</p>
<p>주민등록번호</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de sécurité sociale Espagne


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>11 à 12 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>11 à 12 chiffres :</p>
<ul>
<li><p>Deux chiffres</p></li>
<li><p>Une barre oblique (facultative)</p></li>
<li><p>7 à 8 chiffres</p></li>
<li><p>Une barre oblique (facultative)</p></li>
<li><p>Deux chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_spanish_social_security_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Spain SSN -->
<Entity id="5df987c0-8eae-4bce-ace7-b316347f3070" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_spanish_social_security_number" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><p>Aucun</p></td>
</tr>
</tbody>
</table>


## ID national Suède


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 ou 12 chiffres et éventuellement un délimiteur</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>10 ou 12 chiffres et un délimiteur facultatif :</p>
<ul>
<li><p>2 à 4 chiffres (facultatifs)</p></li>
<li><p>Six chiffres au format de date AAMMJJ</p></li>
<li><p>Séparateur de « - » ou « + » (facultatif), plus</p></li>
<li><p>Quatre chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_swedish_national_identifier</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Sweden National ID -->
<Entity id="f69aaf40-79be-4fac-8f05-fd1910d272c8" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_swedish_national_identifier" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><p>Non</p></td>
</tr>
</tbody>
</table>


## Numéro de passeport Suède


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Huit chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Huit chiffres consécutifs</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_sweden_passport_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>L’une des affirmations suivantes est vraie :</p>
<ul>
<li><p>Un mot clé figurant dans la liste <code>Keyword_passport</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_sweden_passport</code> est trouvé.</p></li>
</ul></li>
</ul>

```Command&nbsp;Line
<!-- Sweden Passport Number -->
<Entity id="ba4e7456-55a9-4d89-9140-c33673553526" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_sweden_passport_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_passport" />
          <Match idRef="Keyword_sweden_passport" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-128"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_sweden_passport</p></th>
<th> </th>
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>exigences en matière de visa</p>
<p>Carte d’enregistrement d’une personne étrangère</p>
<p>Visas Schengen</p>
<p>Visa Schengen</p>
<p>Traitement du visa</p>
<p>Type de visa</p>
<p>Entrée unique</p>
<p>Entrée multiple</p>
<p>Frais de traitement G3</p></td>
<td> </td>
<td><p>Numéro de passeport</p>
<p>N° de passeport</p>
<p># Passeport</p>
<p>#Passeport</p>
<p>PassportID</p>
<p>n° passeport</p>
<p>numéropasseport</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n°</p>
<p>Passeport numéro</p>
<p># Passeport</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Code SWIFT


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Quatre lettres suivies de 5 à 31 lettres ou chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Quatre lettres suivies de 5 à 31 lettres ou chiffres :</p>
<ul>
<li><p>Code bancaire à quatre lettres (ne respectent pas la casse)</p></li>
<li><p>Un espace facultatif</p></li>
<li><p>4 à 28 lettres ou chiffres (numéro de compte bancaire de base (BBAN))</p></li>
<li><p>Un espace facultatif</p></li>
<li><p>1 à 3 lettres ou chiffres (reste du BBAN)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_swift</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_swift</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<Entity id="cb2ab58c-9cb8-4c81-baf8-a4e106791df4" patternsProximity="300" recommendedConfidence="75">
<Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_swift" />
        <Match idRef="Keyword_swift" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-130"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_swift</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>organisation internationale de normalisation 9362</p>
<p>ISO 9362</p>
<p>iso9362</p>
<p>#swift</p>
<p>codeswift</p>
<p>numéroswift</p>
<p>numéroroutageswift</p>
<p>code swift</p>
<p># numéro swift</p>
<p>numéro d’acheminement swift</p>
<p>numéro BIC</p>
<p>code BIC</p>
<p># bic</p>
<p>#bic</p>
<p>code d’identification bancaire</p>
<p>標準化9362</p>
<p>迅速＃</p>
<p>SWIFTコード</p>
<p>SWIFT番号</p>
<p>迅速なルーティング番号</p>
<p>BIC番号</p>
<p>BICコード</p>
<p>銀行識別コードのための国際組織</p>
<p>Organisation internationale de normalisation 9362</p>
<p>rapide #</p>
<p>code SWIFT</p>
<p>le numéro de swift</p>
<p>swift numéro d’acheminement</p>
<p>le numéro BIC</p>
<p># BIC</p>
<p>code identificateur de banque</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## ID national à Taïwan


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Une lettre suivie de neuf chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Une lettre suivie de neuf chiffres :</p>
<ul>
<li><p>Une lettre (en anglais, ne respecte pas la casse)</p></li>
<li><p>Le chiffre « 1 » ou « 2 »</p></li>
<li><p>Huit chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_taiwanese_national_id</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_taiwanese_national_id</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- Taiwanese National ID -->
<Entity id="4C7BFC34-8DD1-421D-8FB7-6C6182C2AF03" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_taiwanese_national_id" />
          <Match idRef="Keyword_taiwanese_national_id" />
      </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-132"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_taiwanese_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>身份證字號</p>
<p>身份證</p>
<p>身份證號碼</p>
<p>身份證號</p>
<p>身分證字號</p>
<p>身分證</p>
<p>身分證號碼</p>
<p>身份證號</p>
<p>身分證統一編號</p>
<p>國民身分證統一編號</p>
<p>簽名</p>
<p>蓋章</p>
<p>簽名或蓋章</p>
<p>簽章</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de passeport Taïwan


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Numéro de passeport biométrique</p>
<dl>
<dd><p>Neuf chiffres</p>
</dd>
</dl>
<p>Numéro de passeport non biométrique</p>
<dl>
<dd><p>Neuf chiffres</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Numéro de passeport biométrique</p>
<ul>
<li><p>Le chiffre « 3 »</p></li>
<li><p>Huit chiffres</p></li>
</ul>
<p>Numéro de passeport non biométrique</p>
<ul>
<li><p>Neuf chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_taiwan_passport</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_taiwan_passport</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Taiwan Passport Number -->
<Entity id="e7251cb4-4c2c-41df-963e-924eb3dae04a" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_taiwan_passport"/>
     <Match idRef="Keyword_taiwan_passport"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-134"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_taiwan_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ROC passport number</p>
<p>Passport number</p>
<p>Passport no</p>
<p>Passport Num</p>
<p>Passport #</p>
<p>护照</p>
<p>中華民國護照</p>
<p>Zhōnghuá Mínguó hùzhào</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de certificat de résident (ARC/TARC) Taïwan


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 lettres et chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>10 lettres et chiffres :</p>
<ul>
<li><p>Deux lettres (ne respectant pas la casse)</p></li>
<li><p>Huit chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_taiwan_resident_certificate</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_taiwan_resident_certificate</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- Taiwan Resident Certificate (ARC/TARC) -->
<Entity id="48269fec-05ea-46ea-b326-f5623a58c6e9" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_taiwan_resident_certificate"/>
     <Match idRef="Keyword_taiwan_resident_certificate"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-136"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_taiwan_resident_certificate</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Resident Certificate</p>
<p>Resident Cert</p>
<p>Resident Cert.</p>
<p>Identification card</p>
<p>Alien Resident Certificate</p>
<p>ARC</p>
<p>Taiwan Area Resident Certificate</p>
<p>TARC</p>
<p>居留證</p>
<p>外僑居留證</p>
<p>台灣地區居留證</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de permis de conduire Royaume-Uni


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Combinaison de 18 lettres et chiffres au format spécifié</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>18 lettres et chiffres</p>
<ul>
<li><p>Cinq lettres (ne respectent pas la casse) ou le chiffre « 9 » à la place d’une lettre</p></li>
<li><p>Un chiffre</p></li>
<li><p>Cinq chiffres au format de date JJMMA pour la date de naissance</p></li>
<li><p>Deux lettres (ne respectent pas la casse) ou le chiffre « 9 » à la place d’une lettre</p></li>
<li><p>Cinq chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_uk_drivers_license</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_uk_drivers_license</code> est trouvé.</p></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.K. Driver's License Number -->
<Entity id="f93de4be-d94c-40df-a8be-461738047551" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_uk_drivers_license" />
        <Match idRef="Keyword_uk_drivers_license" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-138"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DVLA</p>
<p>véhicule utilitaire léger</p>
<p>quad</p>
<p>automobiles</p>
<p>125cc</p>
<p>sidecar</p>
<p>tricycles</p>
<p>motocycles</p>
<p>permis de conduire plastifié</p>
<p>apprentis conducteurs</p>
<p>titulaire du permis</p>
<p>titulaires du permis</p>
<p>permis de conduire</p>
<p>permis de conduire</p>
<p>voiture à double commande</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de liste électorale Royaume-Uni


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Deux lettres suivies de 1 à 4 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Deux lettres (ne respectant pas la casse) suivies de 1 à 4 chiffres</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_uk_electoral</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_uk_electoral</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.K. Electoral Number -->
<Entity id="a3eea206-dc0c-4f06-9e22-aa1be3059963" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_uk_electoral" />
        <Any minMatches="1">
          <Match idRef="Keyword_uk_electoral" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-140"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_electoral</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>nomination au conseil</p>
<p>formulaire de nomination</p>
<p>registre électoral</p>
<p>liste électorale</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro national des services de santé Royaume-Uni


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>10 à 17 chiffres séparés par des espaces</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>10 à 17 chiffres :</p>
<ul>
<li><p>3 ou 10 chiffres</p></li>
<li><p>Un espace</p></li>
<li><p>Trois chiffres</p></li>
<li><p>Un espace</p></li>
<li><p>Quatre chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_uk_nhs_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>L’une des affirmations suivantes est vraie :</p>
<ul>
<li><p>Un mot clé figurant dans la liste <code>Keyword_uk_nhs_number</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_uk_nhs_number1</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_uk_nhs_number_dob</code> est trouvé.</p></li>
</ul></li>
<li><p>La somme de contrôle est correcte.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.K. NHS Number -->
<Entity id="3192014e-2a16-44e9-aa69-4b20375c9a78" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_uk_nhs_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_uk_nhs_number" />
          <Match idRef="Keyword_uk_nhs_number1" />
          <Match idRef="Keyword_uk_nhs_number_dob" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-142"> </h3>
<div>
<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_nhs_number</p></th>
<th> </th>
<th><p>Keyword_uk_nhs_number1</p></th>
<th><p>Keyword_uk_nhs_number_dob</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>service national de santé</p>
<p>NHS</p>
<p>administration des services de santé</p>
<p>administration de la santé</p></td>
<td> </td>
<td><p>id du patient</p>
<p>identification du patient</p>
<p>n° patient</p>
<p>numéro de patient</p></td>
<td><p>GP</p>
<p>DDN</p>
<p>D.O.B</p>
<p>Date of Birth</p>
<p>Birth Date</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d'assurance nationale (NINO) Royaume-Uni


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>7 caractères ou 9 caractères séparés par des espaces ou des tirets</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Deux modèles possibles :</p>
<ul>
<li><p>Deux lettres (valides NINOs utilisent uniquement certains caractères de ce préfixe, ce modèle est valide ; non respect de la casse)</p></li>
<li><p>Six chiffres</p></li>
<li><p>Soit « A », « B », « C », ou a ' (comme le préfixe, seuls certains caractères sont autorisés dans le suffixe ; non respect de la casse)</p></li>
</ul>
<p>OU</p>
<ul>
<li><p>Deux lettres</p></li>
<li><p>Un espace ou un tiret</p></li>
<li><p>Deux chiffres</p></li>
<li><p>Un espace ou un tiret</p></li>
<li><p>Deux chiffres</p></li>
<li><p>Un espace ou un tiret</p></li>
<li><p>Deux chiffres</p></li>
<li><p>Un espace ou un tiret</p></li>
<li><p>Soit « A », « B », « C », ou a '</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_uk_nino</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_uk_nino</code> est trouvé.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_uk_nino</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Aucun mot clé figurant dans la liste <code>Keyword_uk_nino</code> n’est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.K. NINO -->
<Entity id="16c07343-c26f-49d2-a987-3daf717e94cc" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_uk_nino" />
        <Any minMatches="1">
          <Match idRef="Keyword_uk_nino" />
        </Any>
    </Pattern>    
     <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_uk_nino" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_uk_nino" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-144"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_nino</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>numéro d’assurance nationale</p>
<p>cotisations sociales</p>
<p>loi sur la protection</p>
<p>assurance</p>
<p>numéro de sécurité sociale</p>
<p>demande d’assurance</p>
<p>demande de soins médicaux</p>
<p>assurance sociale</p>
<p>soins médicaux</p>
<p>sécurité sociale</p>
<p>grande-bretagne</p>
<p>assurance</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de passeport États-Unis/Royaume-Uni


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Neuf chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Neuf chiffres consécutifs</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_usa_uk_passport</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_passport</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<Entity id="178ec42a-18b4-47cc-85c7-d62c92fd67f8" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_usa_uk_passport" />
        <Match idRef="Keyword_passport" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-146"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numéro de passeport</p>
<p>N° de passeport</p>
<p># Passeport</p>
<p>#Passeport</p>
<p>PassportID</p>
<p>n° passeport</p>
<p>numéropasseport</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n°</p>
<p>Passeport numéro</p>
<p># Passeport</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de compte bancaire États-Unis


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>8-17 chiffres</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>8 à 17 chiffres consécutifs</p></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>L’expression régulière <code>Regex_usa_bank_account_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_usa_Bank_Account</code> est trouvé.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.S. Bank Account Number -->
<Entity id="a2ce32a8-f935-4bb6-8e96-2a5157672e2c" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_usa_bank_account_number" />
        <Match idRef="Keyword_usa_Bank_Account" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-148"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_usa_Bank_Account</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numéro de compte courant</p>
<p>Compte courant</p>
<p># compte courant</p>
<p>Numéro compte courant</p>
<p># compte courant</p>
<p>N° de compte courant</p>
<p>N° de compte courant</p>
<p>Numéro de compte bancaire</p>
<p># Compte bancaire</p>
<p>Numéro de compte bancaire</p>
<p># Compte bancaire</p>
<p>N° de compte bancaire</p>
<p>N° de compte bancaire</p>
<p>Numéro de compte d’épargne</p>
<p>Compte d’épargne.</p>
<p>N° de compte d’épargne</p>
<p>Numéro de compte d’épargne</p>
<p># compte d’épargne</p>
<p>N° de compte d’épargne</p>
<p>N° de compte d’épargne</p>
<p>Numéro de compte de débit</p>
<p>Compte de débit</p>
<p># Compte de débit</p>
<p>Numéro de compte de débit</p>
<p># Compte de débit</p>
<p>N° de compte de débit</p>
<p>N° de compte de débit</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de permis de conduire États-Unis


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Dépend de l’État</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Dépend de l’État, par exemple, New York :</p>
<ul>
<li><p>Neuf chiffres au format ddd ddd ddd correspondront.</p></li>
<li><p>Neuf chiffres au format ddddddddd ne correspondront pas.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_new_york_drivers_license_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_[state_name]_drivers_license_name</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_us_drivers_license</code> est trouvé.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 65 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_new_york_drivers_license_number</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_[state_name]_drivers_license_name</code> est trouvé.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_us_drivers_license_abbreviations</code> est trouvé.</p></li>
<li><p>Aucun mot clé figurant dans la liste <code>Keyword_us_drivers_license</code> n’est trouvé.</p></li>
</ul>

```Command&nbsp;Line
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_new_york_drivers_license_number" />
        <Match idRef="Keyword_new_york_drivers_license_name" />
        <Match idRef="Keyword_us_drivers_license" />
    </Pattern>
    <Pattern confidenceLevel="65">
        <IdMatch idRef="Func_new_york_drivers_license_number" />
        <Match idRef="Keyword_new_york_drivers_license_name" />
        <Match idRef="Keyword_us_drivers_license_abbreviations" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_us_drivers_license" />
        </Any>
    </Pattern>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-150"> </h3>
<div>
<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_us_drivers_license_abbreviations</p></th>
<th> </th>
<th><p>Keyword_us_drivers_license</p></th>
<th><p>Keyword_[state_name]_drivers_license_name</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PC</p>
<p>PC</p>
<p>PCD</p>
<p>PCD</p>
<p>ID</p>
<p>IDs</p>
<p># PC</p>
<p># PC</p>
<p># PCD</p>
<p># PCD</p>
<p>#ID</p>
<p>#IDs</p>
<p>Numéro d’identification</p>
<p>Numéros d’identification</p>
<p>PERMIS</p>
<p># PERMIS</p></td>
<td> </td>
<td><p>DriverLic</p>
<p>DriverLics</p>
<p>DriverLicense</p>
<p>DriverLicenses</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>DriversLic</p>
<p>DriversLics</p>
<p>DriversLicense</p>
<p>DriversLicenses</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permisconduire</p>
<p>Permisconduire</p>
<p>Permisdeconduire</p>
<p>Permisdeconduire</p>
<p>Permis conduire</p>
<p>Permis conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Driver'sLic</p>
<p>Driver'sLics</p>
<p>Driver'sLicense</p>
<p>Driver'sLicenses</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Permis de conduire</p>
<p>Driver’s Licenses</p>
<p>numéro d’identification</p>
<p>numéros d’identification</p>
<p># identification</p>
<p>carte d’identité</p>
<p>cartes d’identité</p>
<p>carte d’identification</p>
<p>cartes d’identification</p>
<p>DriverLic#</p>
<p>DriverLics#</p>
<p>DriverLicense#</p>
<p>DriverLicenses#</p>
<p>#Permis conduire</p>
<p>#Permis conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>DriversLic#</p>
<p>DriversLics#</p>
<p>DriversLicense#</p>
<p>DriversLicenses#</p>
<p>#Permis conduire</p>
<p>#Permis conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>#Permisconduire</p>
<p>#Permisconduire</p>
<p>#Permisdeconduire</p>
<p>#Permisdeconduire</p>
<p>#Permis conduire</p>
<p>#Permis conduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p>Driver'sLic#</p>
<p>Driver'sLics#</p>
<p>Driver'sLicense#</p>
<p>Driver'sLicenses#</p>
<p>#Permisconduire</p>
<p>#Permisconduire</p>
<p>#Permis de conduire</p>
<p>#Permis de conduire</p>
<p># carte d’identité</p>
<p># cartes d’identité</p>
<p>#carte d’identification</p>
<p>#cartes d’identification</p></td>
<td><p>Abréviation de l’État (par exemple, « NY »)</p>
<p>Nom de l’État (par exemple, « New York »)</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro d’identification fiscale individuel (ITIN) États-Unis


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>Neuf chiffres, le premier étant le « 9 », le quatrième le « 7 » ou le « 8 », éventuellement mis en forme avec des espaces ou des tirets</p></td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Mis en forme :</p>
<ul>
<li><p>Le chiffre « 9 »</p></li>
<li><p>Deux chiffres</p></li>
<li><p>Un espace ou un tiret</p></li>
<li><p>Un « 7 » ou un « 8 »</p></li>
<li><p>Un chiffre</p></li>
<li><p>Un espace ou tiret</p></li>
<li><p>Quatre chiffres</p></li>
</ul>
<p>Non mis en forme :</p>
<ul>
<li><p>Le chiffre « 9 »</p></li>
<li><p>Deux chiffres</p></li>
<li><p>Un « 7 » ou un « 8 »</p></li>
<li><p>Cinq chiffres</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_formatted_itin</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Au moins une des affirmations suivantes est vraie :</p>
<ul>
<li><p>Un mot clé figurant dans la liste <code>Keyword_itin</code> est trouvé.</p></li>
<li><p>La fonction <code>Func_us_address</code> trouve une adresse au format correct.</p></li>
<li><p>La fonction <code>Func_us_date</code> trouve une date au format correct.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_itin_collaborative</code> est trouvé.</p></li>
</ul></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_unformatted_itin</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Au moins une des affirmations suivantes est vraie :</p>
<ul>
<li><p>Un mot clé figurant dans la liste <code>Keyword_itin_collaborative</code> est trouvé.</p></li>
<li><p>La fonction <code>Func_us_address</code> trouve une adresse au format correct.</p></li>
<li><p>La fonction <code>Func_us_date</code> trouve une date au format correct.</p></li>
</ul></li>
</ul>

```Command&nbsp;Line
<!-- U.S. Individual Taxpayer Identification Number (ITIN) -->
<Entity id="e55e2a32-f92d-4985-a35d-a0b269eb687b" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_formatted_itin" />
        <Any minMatches="1">
          <Match idRef="Keyword_itin" />
          <Match idRef="Func_us_address" />
          <Match idRef="Func_us_date" />
          <Match idRef="Keyword_itin_collaborative" />
        </Any>
    </Pattern>
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_unformatted_itin" />
        <Match idRef="Keyword_itin" />
        <Any minMatches="1">
          <Match idRef="Keyword_itin_collaborative" />
          <Match idRef="Func_us_address" />
          <Match idRef="Func_us_date" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-152"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_itin</p></th>
<th> </th>
<th><p>Keyword_itin_collaborative</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>contribuable</p>
<p>id fiscal</p>
<p>identification fiscale</p>
<p>itin</p>
<p>nss</p>
<p>tin</p>
<p>sécurité sociale</p>
<p>contribuable</p>
<p>itins</p>
<p>id fiscal</p>
<p>contribuable individuel</p></td>
<td> </td>
<td><p>Permis</p>
<p>PC</p>
<p>DDN</p>
<p>Date de naissance</p>
<p>Anniversaire</p>
<p>Date of Birth</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numéro de sécurité sociale (SSN) États-Unis


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Format</p></td>
<td><p>9 chiffres, qui peuvent être mis en forme ou non mis en forme</p>

> [!NOTE]  
> La mise en forme d’un numéro de sécurité sociale émis avant le milieu de l’année 2011 est fixe et certaines parties du numéro doivent se situer dans certaines plages pour qu’il soit valide (mais il n’y a pas de somme de contrôle).

</td>
</tr>
<tr class="even">
<td><p>Modèle</p></td>
<td><p>Quatre fonctions permettent de rechercher des numéros de sécurité sociale avec quatre différents modèles :</p>
<ul>
<li><p><code>Func_ssn</code> recherche des numéros de sécurité sociale avec une mise en forme fixe d’avant l’année 2011, mis en forme avec des tirets ou des espaces (ddd-dd-dddd OU ddd dd dddd)</p></li>
<li><p><code>Func_unformatted_ssn</code> recherche des numéros de sécurité sociale avec une mise en forme fixe d’avant l’année 2011, avec neuf chiffres consécutifs non mis en forme (ddddddddd)</p></li>
<li><p><code>Func_randomized_formatted_ssn</code> recherche des numéros de sécurité sociale d’après l’année 2011, mis en forme avec des tirets ou des espaces (ddd-dd-dddd OU ddd dd dddd)</p></li>
<li><p><code>Func_randomized_unformatted_ssn</code> recherche des numéros de sécurité sociale d’après l’année 2011, avec neuf chiffres consécutifs non mis en forme (ddddddddd)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Somme de contrôle</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Définition</p></td>
<td><p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 85 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_ssn</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_ssn</code> est trouvé.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 75 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_unformatted_ssn</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_ssn</code> est trouvé.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 65 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_randomized_formatted_ssn</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_ssn</code> est trouvé.</p></li>
<li><p>La fonction <code>Func_ssn</code> ne trouve pas de contenu qui correspond au modèle.</p></li>
</ul>
<p>Le pourcentage de confiance d’une stratégie DLP ayant détecté ce type d’informations sensibles est de 55 % si, dans une proximité de 300 caractères :</p>
<ul>
<li><p>La fonction <code>Func_randomized_unformatted_ssn</code> trouve un contenu qui correspond au modèle.</p></li>
<li><p>Un mot clé figurant dans la liste <code>Keyword_ssn</code> est trouvé.</p></li>
<li><p>La fonction <code>Func_unformatted_ssn</code> ne trouve pas de contenu qui correspond au modèle.</p></li>
</ul>

```Command&nbsp;Line
 <!-- U.S. Social Security Number (SSN) -->
    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77" patternsProximity="300" recommendedConfidence="75">
      <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_ssn" />
        <Match idRef="Keyword_ssn" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_unformatted_ssn" />
        <Match idRef="Keyword_ssn" />
      </Pattern>
      <Pattern confidenceLevel="65">
        <IdMatch idRef="Func_randomized_formatted_ssn" />
        <Match idRef="Keyword_ssn" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Func_ssn" />
        </Any>
      </Pattern>
      <Pattern confidenceLevel="55">
        <IdMatch idRef="Func_randomized_unformatted_ssn" />
        <Match idRef="Keyword_ssn" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Func_unformatted_ssn" />
        </Any>
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Mots clés</p></td>
<td><h3 id="section-154"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ssn</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sécurité sociale</p>
<p># sécurité sociale</p>
<p>Sécu sociale</p>
<p>NSS</p>
<p>NSS</p>
<p>#NSS</p>
<p># SS</p>
<p>IDSS</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>

