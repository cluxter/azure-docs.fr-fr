---
title: Régions prenant en charge les Zones de disponibilité dans Azure
description: Pour créer des applications hautement disponibles et résilientes dans Azure, les zones de disponibilité fournissent des emplacements physiquement distincts que vous pouvez utiliser pour exécuter vos ressources.
author: cynthn
ms.service: azure
ms.topic: article
ms.date: 07/06/2020
ms.author: cynthn
ms.custom: fasttrack-edit, mvc, references_regions
ms.openlocfilehash: 2e337628542475c081a59bffd25368de313011f8
ms.sourcegitcommit: 3541c9cae8a12bdf457f1383e3557eb85a9b3187
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86206199"
---
# <a name="regions-that-support-availability-zones-in-azure"></a>Régions prenant en charge les Zones de disponibilité dans Azure

Les Zones de disponibilité constituent une offre à haute disponibilité qui protège vos applications et données contre les pannes des centres de données. Pour plus d’informations sur les Zones de disponibilité, consultez [Régions et Zones de disponibilité dans Azure](az-overview.md).

## <a name="services-support-by-region"></a>Prise en charge des services par région

Cette section répertorie les régions et services Azure qui prennent en charge les Zones de disponibilité.

Pour voir les services disponibles dans chaque région, ainsi que la feuille de route à venir pour la disponibilité, consultez [Produits disponibles par région](https://azure.microsoft.com/global-infrastructure/services/).

| Service |États-Unis: USA Centre|États-Unis: USA Est|États-Unis: USA Est 2|États-Unis: USA Ouest 2|Europe : France Centre|Europe : Europe Nord|Europe : Sud du Royaume-Uni|Europe : Europe Ouest|Asie-Pacifique : Japon Est|Asie-Pacifique : Asie Sud-Est|Asie-Pacifique : Australie Est|
|----------------------------|----------|----------|---------|---------|--------------|------------|--------|----------|----------|-------------|-------------|
| **Calcul**                         |            |              |           |           |                |              |          |             |            |                |                |
| Machines virtuelles Linux          | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       | &#10003;               |
| Machines virtuelles Windows        | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       | &#10003;               |
| Virtual Machine Scale Sets      | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       | &#10003;               |
| ILB Azure App Service Environments | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       |                |
| Azure Kubernetes Service        | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       |                |
| **Stockage**   |            |              |           |           |                |              |          |             |            |                |                |
| Disques managés                   | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       | &#10003;               |
| Stockage redondant interzone          | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       | &#10003;               |
| **Mise en réseau**                     |            |              |           |           |                |              |          |             |            |                |                |
| Adresse IP standard        | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       | &#10003;               |
| Standard Load Balancer     | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       | &#10003;               |
| Passerelle VPN            | &#10003;   |  &#10003;    | &#10003;  | &#10003;  | &#10003;       | &#10003;     |  &#10003;  | &#10003;    |  &#10003;   | &#10003;       | &#10003;               |
| Passerelle ExpressRoute   | &#10003;   |  &#10003;    | &#10003;  | &#10003;  | &#10003;       | &#10003;     |  &#10003;  | &#10003;    |  &#10003;   | &#10003;       | &#10003;               |
| Application Gateway (V2)    | &#10003;   |  &#10003;    | &#10003;  | &#10003;  | &#10003;       | &#10003;     |  &#10003;  | &#10003;    |  &#10003;   | &#10003;       | &#10003;               |
| Pare-feu Azure           | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    |  &#10003;       | &#10003;       |                |
| **Bases de données**                     |            |              |           |           |                |              |          |             |            |                |                |
| Explorateur de données Azure                   | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;        | &#10003;       |                |
| SQL Database                    | &#10003;   | &#10003;     | &#10003;  | &#10003;(Préversion) | &#10003;       | &#10003;(Préversion)     | &#10003; | &#10003;    | &#10003;       | &#10003;       |&#10003;        |
| Cache Azure pour Redis           | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    |  &#10003;       | &#10003;       |                |
| Azure Cosmos DB      | &#10003;   |  &#10003;  |  &#10003; | &#10003; |  &#10003;  | &#10003;    | &#10003; |  &#10003;   |     &#10003;       | &#10003;    | &#10003;  |
| **Analyse**                       |            |              |           |           |                |              |          |             |            |                |                |
| Event Hubs                      | &#10003;   |   &#10003; | &#10003;  | &#10003;  | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003;       |  &#10003;              |
| **Intégration**                     |            |              |           |           |                |              |          |             |            |                |                |
| Service Bus (Niveau Premium uniquement) | &#10003;   |  &#10003;  | &#10003;  | &#10003;  | &#10003;  | &#10003;     |&#10003;   | &#10003;    |&#10003;      | &#10003;       |  &#10003;              |
| Event Grid | &#10003;   |  &#10003;  | &#10003;  | &#10003;  | &#10003;  | &#10003;     |&#10003;   | &#10003;    |&#10003;      | &#10003;       |                |
| **Identité**                     |            |              |           |           |                |              |          |             |            |                |                |
| Services de domaine Azure AD | &#10003;   |  &#10003;  | &#10003;  | &#10003;  | &#10003;  | &#10003;     |&#10003;   | &#10003;    |&#10003;      | &#10003;       |                |

Azure offre également une prise en charge Zones de disponibilité dans les régions suivantes :

- Gouvernement américain - Virginie
- Australie Est
- Afrique du Sud Nord
- États-Unis - partie centrale méridionale
- Centre du Canada

Pour en savoir plus sur la prise en charge de Zones de disponibilité dans ces cinq régions, contactez votre représentant commercial ou client Microsoft.

## <a name="next-steps"></a>Étapes suivantes

- [Régions et Zones de disponibilité dans Azure](az-overview.md)
