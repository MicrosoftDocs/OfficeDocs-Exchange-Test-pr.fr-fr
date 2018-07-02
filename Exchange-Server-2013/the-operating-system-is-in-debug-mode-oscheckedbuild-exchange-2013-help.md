---
title: 'Le système d’exploitation est en mode débogage_OSCheckedBuild: Exchange 2013 Help'
TOCTitle: Le système d’exploitation est en mode débogage_OSCheckedBuild
ms:assetid: 93a1380f-1388-494d-8f78-92dfefd069bd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.oscheckedbuild(v=EXCHG.150)
ms:contentKeyID: 50478714
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Le système d’exploitation est en mode débogage\_OSCheckedBuild

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2016-12-15_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

L’outil d’analyse Microsoft® Exchange Server interroge la classe WMI (Windows® Management Instrumentation) Microsoft **Win32\_OperatingSystem** pour déterminer si une valeur est définie pour la propriété **Debug**. Si la valeur de cette clé sur un ordinateur Exchange Server est définie sur **True**, une erreur s’affiche.

Le mode de débogage Windows est activé en ajoutant le paramètre **/debug** dans le fichier Boot.ini. Lorsque **/debug** est spécifié dans le fichier Boot.ini d’un ordinateur Windows Server, le débogueur de noyau est chargé pendant le démarrage et mémorisé en permanence. Cela permet à un technicien du support technique d’appeler le système en cours de débogage et de s’arrêter dans le débogueur lorsque le système n’est pas interrompu au niveau de l’écran ARRÊT du noyau. À la différence du commutateur **/crashdebug**, le commutateur **/debug** utilise le port COM que vous procédiez à un débogage ou non. Ce commutateur est utilisé lors de la résolution de problèmes qui se reproduisent régulièrement. Il est probable que le paramètre **/debug** ait été défini comme un moyen de résoudre un problème et laissé involontairement ainsi.

En raison des processus supplémentaires en cours d’exécution, les performances sont considérablement affectées. Par conséquent, il n’est pas recommandé d’utiliser Exchange Server sur un ordinateur où Windows est exécuté en mode débogage.

Pour corriger cette erreur, modifiez le fichier Boot.ini et supprimez le paramètre **/debug**.

## Correction de cette erreur

1.  Dans l’Explorateur Windows, naviguez jusqu’à la partition système. Cette partition contient les fichiers spécifiques de matériel, tels que Boot.ini et NTLDR.

2.  Si le fichier Boot.ini n’apparaît pas, les **options des dossiers** sont peut-être définies sur **Masquer les fichiers protégés du système d’exploitation**. Si tel est le cas, dans la fenêtre de l’Explorateur Windows, cliquez sur **Outils**, **Options des dossiers**, puis sur **Affichage**. Désactivez la case à cocher **Masquer les fichiers protégés du système d’exploitation (recommandé)**. Lorsque vous y êtes invité, cliquez sur **Oui**.

3.  Lorsque le fichier Boot.ini est visible dans l’Explorateur Windows, cliquez avec le bouton droit sur le fichier, cliquez sur **Ouvrir avec** et choisissez **Bloc-notes** pour ouvrir le fichier.

4.  Dans la section **\[Systèmes d’exploitation\]**, supprimez le paramètre **/debug**.

5.  Enregistrez le fichier et fermez-le, puis redémarrez l’ordinateur Exchange Server pour que la modification soit prise en compte.

Pour plus d’informations sur les paramètres pouvant être utilisés dans le fichier Boot.ini, voir l’article 833721 de la base de connaissances Microsoft sur les options de commutateurs disponibles pour les fichiers Boot.ini Windows XP et Windows Server 2003 ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=833721](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=833721)).

