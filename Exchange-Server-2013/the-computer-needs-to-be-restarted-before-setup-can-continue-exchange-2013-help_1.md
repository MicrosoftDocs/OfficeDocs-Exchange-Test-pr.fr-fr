---
title: 'Vous devez redémarrer l’ordinateur pour que le programme d’installation puisse continuer l’opération: Exchange 2013 Help'
TOCTitle: Vous devez redémarrer l’ordinateur pour que le programme d’installation puisse continuer l’opération
ms:assetid: f2d8e504-18c1-4b86-9b97-7654d0391b19
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.pendingrebootwindowscomponents(v=EXCHG.150)
ms:contentKeyID: 50479552
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Vous devez redémarrer l’ordinateur pour que le programme d’installation puisse continuer l’opération

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le programme d’installation de Microsoft Exchange Server 2013 ne peut pas continuer, car il a détecté que l’ordinateur local doit être redémarré pour terminer l’installation d’autres programmes ou mises à jour Windows.

## Que se passe-t-il ?

Lorsque des programmes et des mises à jour Windows sont installés, ils apportent des modifications aux fichiers stockés sur votre ordinateur. Parfois, au cours de l’installation, un programme ou une mise à jour Windows doit apporter une modification à un fichier en cours d’utilisation. Dans ce cas, vous devez redémarrer l’ordinateur avant que d’autres programmes, comme Exchange 2013, puissent être installés. Le programme d’installation d’Exchange nécessite que toutes les autres installations soient terminées pour pouvoir vérifier que toutes les conditions préalables nécessaires à son bon fonctionnement sont installées.

Parfois, l’installation d’un programme ou d’une mise à jour Windows antérieur(e) peut ne pas avoir abouti. Ce genre de situation peut laisser en suspens des modifications et Windows et d’autres programmes ont donc l’impression qu’un redémarrage est nécessaire. Malheureusement, comme l’installation échouée ne nettoie jamais ces modifications, l’installation des mises à jour Windows et d’autres programmes peut être bloquée. Dans ce cas, vous continuerez de voir cette erreur à chaque fois que vous exécuterez le programme d’installation d’Exchange.

## Comment corriger cette erreur ?

Dans la plupart des cas, il vous suffit de redémarrer l’ordinateur pour passer outre cette erreur. Mais parfois, cette erreur réapparaît même si vous avez déjà redémarré l’ordinateur. Cela peut se produire lorsque l’installation d’un programme ou d’une mise à jour Windows doit apporter des modifications supplémentaires et que ces modifications nécessitent elles aussi le redémarrage de l’ordinateur. Si cette erreur s’affiche après que vous avez redémarré votre ordinateur, essayez de le redémarrer une nouvelle fois.

Si vous avez redémarré l’ordinateur plus de deux ou trois fois et que cette erreur s’affiche toujours, essayez de réinstaller tous les programmes ou mises à jour Windows installés récemment. Cela peut permettre à une installation qui a échoué de se terminer correctement.

Si, après avoir redémarré votre ordinateur et réinstallé tous les programmes ou mises à jour Windows récents, cette erreur s’affiche *encore*, nous vous recommandons de contacter le support Microsoft. Il vous aidera à déterminer pourquoi Windows et d’autres programmes pensent que votre ordinateur doit être redémarré. Pour contacter le support Microsoft, accédez au [support pour Microsoft Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=525940).

> [!CAUTION]
> Bien que cela puisse être tentant, nous vous recommandons vivement de ne pas tenter de contourner ce problème en supprimant ou en modifiant manuellement des clés ou des valeurs dans le Registre Windows. Même si cette procédure peut résoudre le problème actuel, elle peut créer des problèmes ultérieurement. Cela est particulièrement important si l’installation qui a échoué était une mise à jour Windows.

