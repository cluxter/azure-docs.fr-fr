---
title: Utiliser des cartes d’intérieur dans le Créateur Azure Maps
description: Cet article présente les concepts qui s’appliquent aux services du Créateur Azure Maps.
author: anastasia-ms
ms.author: v-stharr
ms.date: 05/18/2020
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: philmea
ms.openlocfilehash: d55a0726000a6ed55f049ac4a4146f66421a7085
ms.sourcegitcommit: dabd9eb9925308d3c2404c3957e5c921408089da
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2020
ms.locfileid: "86242574"
---
# <a name="creator-for-indoor-maps"></a>Créateur pour cartes d’intérieur

Cet article présente les concepts et outils qui s’appliquent au Créateur Azure Maps. Nous vous recommandons de lire cet article avant de commencer à utiliser l’API Créateur Azure Maps et le Kit de développement logiciel (SDK).

Vous pouvez utiliser le Créateur pour développer des applications avec des caractéristiques de plan basées sur des données cartographiques d’intérieur. Cet article décrit le processus de chargement, de conversion, de création et d’utilisation de vos données cartographiques. Le flux de travail entier est illustré dans le diagramme ci-dessous.

![Flux de travail des données cartographiques du Créateur](./media/creator-indoor-maps/workflow.png)

## <a name="create-azure-maps-creator"></a>Créer un Créateur Azure Maps

Pour utiliser les services d’un Créateur, vous devez créer un Créateur Azure Maps dans un compte Azure Maps. Pour plus d’informations sur la création d’un Créateur Azure Maps dans Azure Maps, consultez [Gérer un Créateur Azure Maps](how-to-manage-creator.md).

## <a name="upload-a-drawing-package"></a>Charger un package de dessin

Le créateur collecte des données de carte d’intérieur en convertissant un package de dessin chargé. Le package de dessin représente un bâtiment construit ou rénové. Pour plus d’informations sur les exigences du package de dessin, consultez [Exigences du package de dessin](drawing-requirements.md).

Utilisez l’[API de chargement de données Azure Maps](https://docs.microsoft.com/rest/api/maps/data/uploadpreview) pour charger un package de dessin.  En cas de réussite du chargement, l’API de chargement de données retourne un identificateur de données utilisateur (`udid`). L’`udid` sera utilisé à l’étape suivante pour convertir le package chargé en données cartographiques d’intérieur.

## <a name="convert-a-drawing-package"></a>Convertir un package de dessin

Le [service de conversion d’Azure Maps](https://docs.microsoft.com/rest/api/maps/conversion) convertit un package de dessin chargé en données cartographiques d’intérieur. Le service de conversion valide également le package. Les problèmes de validation sont classés en deux types : erreurs et avertissements. Si des erreurs sont détectées, le processus de conversion échoue. Si des avertissements sont détectés, la conversion échoue. Toutefois, il est recommandé d’examiner et de résoudre tous les avertissements. Un avertissement signifie qu’une partie de la conversion a été ignorée ou corrigée automatiquement. L’échec de la résolution des avertissements pourrait entraîner des erreurs dans les derniers processus. Pour plus d’informations, consultez [Avertissements et erreurs du package de dessin](drawing-conversion-error-codes.md).

Quand une erreur se produit, le service de conversion fournit un lien vers l’application web autonome [Visualiseur d’erreurs de dessin d’Azure Maps](drawing-error-visualizer.md). Vous pouvez utiliser le Visualiseur d’erreurs de dessin pour inspecter les [Avertissements et erreurs du package de dessin](drawing-conversion-error-codes.md) qui se sont produits pendant le processus de conversion. Après avoir corrigé les erreurs, vous pouvez tenter de charger et convertir le package.

## <a name="create-indoor-map-data"></a>Créer des données cartographiques d’intérieur

Le Créateur Azure Maps fournit trois services :

* [Service Jeu de données](https://docs.microsoft.com/rest/api/maps/dataset/createpreview).
Utilisez le service DataSet pour créer un jeu de données à partir de données d’un package de dessin converti.
* [Service Tileset](https://docs.microsoft.com/rest/api/maps/tileset/createpreview).
Utilisez le service Tileset pour créer une représentation vectorielle d’un jeu de données. Les applications peuvent utiliser un tileset pour présenter une vue basée sur des vignettes du jeu de données.
* [Service État de caractéristique](https://docs.microsoft.com/rest/api/maps/featurestate). Utilisez le service État de caractéristique pour prendre en charge l’application de style de carte dynamique. L’application de style de carte dynamique permet aux applications de refléter des événements en temps réel sur des espaces fournis par le système IoT.

### <a name="datasets"></a>Groupes de données

Un jeu de données est une collection de caractéristiques de carte d’intérieur. Les caractéristiques de plan d’intérieur représentent des installations définies dans un package de dessin converti. Après avoir créé un jeu de données avec le [Service Jeu de données](https://docs.microsoft.com/rest/api/maps/dataset/createpreview), vous pouvez créer un nombre quelconque de [tilesets](#tilesets) ou de [statesets de caractéristique](#feature-statesets).

Le [Service Jeu de données](https://docs.microsoft.com/rest/api/maps/dataset/createpreview) permet aux développeurs, à tout moment, d’ajouter ou de supprimer des installations dans un jeu de données existant. Pour plus d’informations sur la façon de mettre à jour un jeu de données à l’aide de l’API, consultez les options d’ajout dans [Service Jeu de données](https://docs.microsoft.com/rest/api/maps/dataset/createpreview). Pour un exemple de la façon de mettre à jour un jeu de données, consultez [Maintenance des données](#data-maintenance).

### <a name="tilesets"></a>Tilesets

Un tileset est une collection de données vectorielles qui représente un ensemble de vignettes de grille uniformes. Les développeurs peuvent utiliser le [Service Tileset](https://docs.microsoft.com/rest/api/maps/tileset/createpreview) pour créer des tilesets à partir d’un jeu de données.

Pour refléter différentes étapes de contenu, vous pouvez créer plusieurs tilesets à partir du même jeu de données. Par exemple, vous pouvez créer un tileset avec du mobilier et de l’équipement, et un autre tileset sans mobilier ni équipement.  Vous pouvez choisir de générer un tileset avec les mises à jour de données les plus récentes et un autre sans les mises à jour de données les plus récentes.

En plus des données vectorielles, le tileset fournit des métadonnées pour l’optimisation du rendu de la carte. Par exemple, les métadonnées du tileset contiennent un niveau de zoom minimum et maximum pour le tileset. Les métadonnées fournissent également un cadre englobant définissant l’étendue géographique du tileset. Le cadre englobant permet à une application de définir par programme le point central approprié. Pour plus d’informations sur les métadonnées d’un tileset, consultez [API de liste de tileset](https://docs.microsoft.com/rest/api/maps/tileset/listpreview).

Une fois qu’un tileset a été créé, il peut être récupéré par le [service Render v2](#render-v2-service).

Si un tileset devient obsolète et n’est plus utile, vous pouvez le supprimer. Pour plus d’informations sur la manière de supprimer un tileset, consultez [Maintenance des données](#data-maintenance).

>[!NOTE]
>Un tileset est indépendant du jeu de données à partir duquel il a été créé. Si vous créez un tileset à partir d’un jeu de données, puis mettez à jour ce dernier, le tileset n’est pas mis à jour. Pour refléter les modifications apportées à un jeu de données, vous devez créer un nouveau tileset. De même, si vous supprimez un tileset, le jeu de données n’est pas affecté.

### <a name="feature-statesets"></a>Stateset de caractéristique

Un stateset de caractéristique est une collections de propriétés dynamiques (états ou *states* en anglais) affectées à des caractéristiques de jeu de données, telles que des salles ou des équipements. Un exemple d’état (*state*) peut être une température ou une occupation. Chaque *état* est une paire clé/valeur contenant le nom de la propriété, la valeur et l’horodateur de la dernière mise à jour.

Le [service État de caractéristique](https://docs.microsoft.com/rest/api/maps/featurestate/createstatesetpreview) vous permet de créer et gérer un stateset de caractéristique pour un jeu de données. Le stateset est défini par un ou plusieurs *états*. Chaque caractéristique, telle une salle, peut avoir un *état* associé.

La valeur de chaque *état* dans un stateset peut être mise à jour ou récupérée par des appareils IoT ou d’autres applications.  Par exemple, à l’aide de l’[API de mise à jour d’état de caractéristique](https://docs.microsoft.com/rest/api/maps/featurestate/updatestatespreview), des appareils mesurant l’occupation de l’espace peuvent publier systématiquement le changement d’état d’une salle.

Une application peut utiliser un stateset de caractéristique pour restituer de façon dynamique des caractéristiques dans un bâtiment en fonction de leur état et de leur style de carte respectif. Pour plus d’informations sur l’utilisation de statesets de caractéristiques pour appliquer un style à des caractéristiques dans une carte de rendu, consultez [Module du kit de développement logiciel (SDK) web Intérieur](#indoor-maps-module).

>[!NOTE]
>À l’instar des tilesets, la modification d’un jeu de données n’affecte pas le stateset de caractéristique existant, et la suppression d’un stateset de caractéristique n’a aucun effet sur le jeu de données auquel il est attaché.

## <a name="using-indoor-maps"></a>Utilisation des cartes d’intérieur

### <a name="render-v2-service"></a>Service Render v2

L’[API Get Map Tile du service Render v2](https://docs.microsoft.com/rest/api/maps/renderv2/getmaptilepreview) a été étendue pour prendre en charge les tilesets du Créateur.

L’[API Get Map State Tile du service Render v2](https://docs.microsoft.com/rest/api/maps/renderv2/getmaptilepreview) permet aux applications de demander des tilesets. Les tilesets peut ensuite être intégré dans un contrôle de carte ou un Kit de développement logiciel (SDK). Pour obtenir un exemple de contrôle de carte utilisant le service Render v2, consultez [Module Cartes d’intérieur](#indoor-maps-module).

### <a name="web-feature-service-api"></a>API de service de caractéristique web

Des jeux de données peuvent être interrogés à l’aide de l’[API de service de caractéristique web](https://docs.microsoft.com/rest/api/maps/wfs). L’API de service de caractéristique web suit les [caractéristiques de l’API Open Geospatial Consortium](http://docs.opengeospatial.org/DRAFTS/17-069r1.html). L’API de service de caractéristique web vous permet d’interroger des caractéristiques à l’intérieur du jeu de données. Par exemple, vous pouvez utiliser le service de caractéristique web pour rechercher toutes les salles de réunion de taille moyenne d’un bâtiment et d’un étage donnés.

### <a name="indoor-maps-module"></a>Module Cartes d’intérieur

Le [Kit de développement logiciel (SDK) web Azure Maps](https://docs.microsoft.com/azure/azure-maps/) comprend le module Cartes d’intérieur. Ce module offre des fonctionnalités étendues à la bibliothèque *Map Control* d’Azure Maps. Le module Cartes d’intérieur affiche des cartes d’intérieur créées dans le Créateur. Il intègre des widgets tels qu’un *sélecteur d’étage*, qui aide les utilisateurs à visualiser les différents étages.

Le module Cartes d’intérieur vous permet de créer des applications web qui intègrent des données cartographiques d’intérieur avec d’autres [services Azure Maps](https://docs.microsoft.com/azure/azure-maps/). Les configurations d’applications les plus courantes peuvent inclure l’ajout à des cartes d’intérieur de connaissances provenant d’autres cartes, telles que la route, l’imagerie, la météo et le transit.

Le module Cartes d’intérieur prend également en charge l’application de style de carte dynamique. Pour une procédure pas à pas sur la façon d’implémenter l’application de style dynamique de stateset de caractéristique dans une application, consultez [Comment utiliser le module Cartes d’intérieur](how-to-use-indoor-module.md)

### <a name="azure-maps-integration"></a>Intégration d’Azure Maps

Lorsque vous commencez à développer des solutions pour des cartes d’intérieur, vous pouvez découvrir des façons d’intégrer des fonctionnalités Azure Maps existantes. Par exemple, vous pourriez implémenter des scénarios de suivi de ressource ou de sécurité en utilisant l’[API Geofence d’Azure Maps](https://docs.microsoft.com/rest/api/maps/spatial/postgeofence) avec des cartes d’intérieur du Créateur. L’API Geofence permet, par exemple, de déterminer si un employé entre dans des zones intérieures spécifiques ou en sort. Pour plus d’informations sur la façon de connecter Azure Maps avec la télémétrie IoT, voir [ici](tutorial-iot-hub-maps.md).

### <a name="data-maintenance"></a>Maintenance des données

 Les API Liste, Mettre à jour et Supprimer du Créateur Azure Maps vous permettent respectivement de répertorier, mettre à jour et supprimer vos jeux de données, tilesets et statesets de caractéristiques.

>[!NOTE]
>Chaque fois que vous examinez une liste d’éléments et décidez de les supprimer, vous devez prendre en compte l’impact de cette suppression sur l’ensemble des applications ou API dépendantes. Par exemple, si vous deviez supprimer un tileset actuellement utilisé par une application au moyen de l’[API Get Map Tile de Render v2](https://docs.microsoft.com/rest/api/maps/renderv2/getmaptilepreview), la suppression de ce tileset aurait pour effet que l’application échouerait à rendre celui-ci.

### <a name="example-updating-a-dataset"></a>Exemple : Mise à jour d’un jeu de données

L’exemple suivant montre comment mettre à jour un jeu de données, créer un tileset et supprimer un tileset.

1. Pour charger et convertir le nouveau package de dessin, suivez les étapes des sections [Charger un package de dessin](#upload-a-drawing-package) et [Convertir un package de dessin](#convert-a-drawing-package).

2. Utilisez l’[API de création de jeu de données](https://docs.microsoft.com/rest/api/maps/dataset/createpreview) pour ajouter les données converties au jeu de données existant.

3. Utilisez l’[API de création de tileset](https://docs.microsoft.com/rest/api/maps/tileset/createpreview) pour générer un nouveau tileset à partir du jeu de données mis à jour. Enregistrez le nouveau tilesetId pour l’étape 4.

4. Mettez à jour l’identificateur de tileset (tilesetid) dans votre application pour activer la visualisation du jeu de données campus mis à jour. Si l’ancien tileset n’est plus utilisé, vous pouvez le supprimer.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Tutoriel : Création d’un carte d’intérieur du Créateur](tutorial-creator-indoor-maps.md)
