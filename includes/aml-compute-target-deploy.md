---
title: Fichier include
description: Fichier include
services: machine-learning
author: sdgilley
ms.service: machine-learning
ms.author: sgilley
manager: cgronlund
ms.custom: include file
ms.topic: include
ms.date: 06/25/2020
ms.openlocfilehash: 82234719320f1ac707147c7c8393c0464956dd99
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85378582"
---
| Cible de calcul | Utilisé pour | Prise en charge GPU | Prise en charge FPGA | Description |
| ----- | ----- | ----- | ----- | ----- |
| [Service&nbsp;web&nbsp;local](../articles/machine-learning/how-to-deploy-and-where.md#local) | Test/débogage | &nbsp; | &nbsp; | Pour les tests et la résolution des problèmes limités. L’accélération matérielle dépend de l’utilisation de bibliothèques dans le système local.
| [Service&nbsp;web&nbsp;d’instances de calcul Azure Machine Learning](../articles/machine-learning/how-to-deploy-and-where.md#notebookvm) | Test/débogage | &nbsp; | &nbsp; | Pour les tests et la résolution des problèmes limités.
| [Azure Kubernetes Service (AKS)](../articles/machine-learning/how-to-deploy-and-where.md#aks) | Inférence en temps réel |  [Oui](../articles/machine-learning/how-to-deploy-inferencing-gpus.md) (déploiement de services web) | [Oui](../articles/machine-learning/how-to-deploy-fpga-web-service.md)   |Pour les déploiements de production à grande échelle. Fournit un temps de réponse et une mise à l’échelle automatique rapides du service déployé. La mise à l’échelle automatique du cluster n’est pas prise en charge via le Kit de développement logiciel (SDK) Azure Machine Learning. Pour modifier les nœuds du cluster AKS, utilisez l’interface utilisateur de votre cluster AKS dans le portail Azure. AKS est la seule option disponible pour le concepteur. |
| [Azure Container Instances](../articles/machine-learning/how-to-deploy-and-where.md#aci) | Test ou développement | &nbsp;  | &nbsp; | Pour les charges de travail à faible échelle basées sur le processeur qui nécessitent moins de 48 Go de RAM. |
| [Clusters de calcul Azure Machine Learning](../articles/machine-learning/how-to-use-parallel-run-step.md) | Inférence&nbsp;Batch | [Oui](../articles/machine-learning/how-to-use-parallel-run-step.md) (pipeline d’apprentissage automatique) | &nbsp;  | Exécutez le scoring par lots sur un calcul sans serveur. Prend en charge des machines virtuelles normales et basse priorité. |
| [Azure Functions](../articles/machine-learning/how-to-deploy-functions.md) | Inférence en temps réel (préversion) | &nbsp; | &nbsp; | &nbsp; |
| [Azure IoT Edge](../articles/machine-learning/how-to-deploy-and-where.md#iotedge) | (Préversion) Module&nbsp;IoT |  &nbsp; | &nbsp; | Déployez et servez des modèles sur des appareils IoT. |
| [Azure Data Box Edge](../articles/databox-online/azure-stack-edge-overview.md)   | Via IoT Edge |  &nbsp; | Oui | Déployez et servez des modèles sur des appareils IoT. |

> [!NOTE]
> Même si les cibles de calcul telles que les cibles locales et les instances et clusters de calcul Azure Machine Learning prennent en charge les GPU pour la formation et l’expérimentation, l’utilisation des GPU pour l’inférence __lors d’un déploiement comme service web__ est prise en charge uniquement par Azure Kubernetes Service.
>
> L’utilisation d’un GPU pour l’inférence __lors du scoring avec un pipeline d’apprentissage automatique__ est prise en charge uniquement sur Capacité de calcul Machine Learning.