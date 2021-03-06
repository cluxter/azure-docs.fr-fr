---
title: Fichier include
description: Fichier include
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/12/2020
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 4ea97e2dbee87f7ab129c4295276c9024c0212c7
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "80117057"
---
Le client VPN Windows 10, Always On, est doté d’une nouvelle fonctionnalité, qui permet de maintenir une connexion VPN. Always On permet au profil VPN actif de se connecter automatiquement et rester connecté en fonction de déclencheurs, tels qu’une connexion d’utilisateur, un changement de l’état du réseau ou l’activation de l’écran de l’appareil.

Il est possible d’utiliser les passerelles avec Windows 10 Always On pour établir des tunnels d’appareil et des tunnels d’utilisateur persistants vers Azure. Dans cet article, vous apprendrez à configurer un tunnel utilisateur VPN Always On.

Les connexions VPN Always On incluent l’un de ces types de tunnels :

* **Tunnel de d’appareil** : se connecte à des serveurs VPN spécifiés avant que les utilisateurs ne se connectent à l’appareil. Les scénarios de connectivité de préconnexion et de gestion des appareils utilisent un tunnel d’appareil.

* **Tunnel utilisateur** : établit une connexion uniquement lorsque l’utilisateur se connecte à son appareil. En utilisant un tunnel d’utilisateur, vous pouvez accéder aux ressources de votre entreprise ou organisation via des serveurs VPN.

Le tunnel appareil et le tunnel utilisateur fonctionnent tous deux de façon indépendante vis-à-vis de leurs profils VPN. Ils peuvent être connectés simultanément et utiliser différentes méthodes d’authentification et d’autres paramètres de configuration VPN selon les besoins.
