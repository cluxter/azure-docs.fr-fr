---
title: Langage de requête
titleSuffix: Azure Digital Twins
description: Découvrez les principes de base du langage de magasin de données des requêtes Azure Digital Twins.
author: baanders
ms.author: baanders
ms.date: 3/26/2020
ms.topic: conceptual
ms.service: digital-twins
ms.openlocfilehash: f7e9a76309b4d9dcd010b85d1b55f340374be5c4
ms.sourcegitcommit: 46f8457ccb224eb000799ec81ed5b3ea93a6f06f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87337923"
---
# <a name="about-the-query-language-for-azure-digital-twins"></a>À propos du langage de requête pour Azure Digital Twins

N’oubliez pas que le centre d’Azure Digital Twins est le [**graphique de jumeaux**](concepts-twins-graph.md) construit à partir des  **jumeaux numériques** et des **relations**. Ce graphique peut être interrogé pour obtenir des informations sur les jumeaux numériques et les relations qu’il contient. Ces requêtes sont écrites dans un langage de requête de type SQL personnalisé, appelé **langage de magasin de données des requêtes Azure Digital Twins**.

Pour soumettre une requête au service à partir d’une application cliente, vous allez utiliser l’[**API de requête**](https://docs.microsoft.com/dotnet/api/azure.digitaltwins.core.digitaltwinsclient.query?view=azure-dotnet-preview) Azure Digital Twins. Ceci permet aux développeurs d’écrire des requêtes et d’appliquer des filtres pour rechercher des ensembles de jumeaux numériques dans le graphique des jumeaux, ainsi que d’autres informations sur le scénario Azure Digital Twins.

## <a name="query-language-features"></a>Fonctionnalités du langage de requête

Azure Digital Twins fournit des fonctionnalités de requête étendues par rapport au graphique de jumeaux. Les requêtes sont décrites à l’aide de la syntaxe de type SQL, dans un langage de requête similaire au [langage de requête IoT Hub](../iot-hub/iot-hub-devguide-query-language.md) avec de nombreuses fonctionnalités comparables.

> [!NOTE]
> Toutes les opérations de requête Azure Digital Twins respectent la casse.

Voici les opérations disponibles dans langage de magasin de données des requêtes Azure Digital Twins :
* Obtenir des jumeaux par propriétés de jumeaux numériques (y compris des [balises](how-to-use-tags.md)).
* Obtenir des jumeaux par interfaces des jumeaux numériques.
* Obtenir des jumeaux par propriétés des relations.
* Obtenir des jumeaux via des types de relations multiples (requêtes`JOIN`). Le nombre de `JOIN`s autorisées (un niveau pour la préversion publique) est limité.
* Utilisez la fonction personnalisée `IS_OF_MODEL(twinCollection, twinTypeName)`, qui permet de filtrer en fonction du [modèle](concepts-models.md) de jumeau. Elle prend en charge l’héritage.
* Utilisez des fonctions scalaires : `IS_BOOL`, `IS_DEFINED`, `IS_NULL`, `IS_NUMBER`, `IS_OBJECT`, `IS_PRIMITIVE`, `IS_STRING`, `STARTS_WITH`, `ENDS_WITH`.
* Utilisez des opérateurs de comparaison de requêtes : `IN`/`NIN`, `=`, `!=`, `<`, `>`, `<=`, `>=`.
* Utilisez n’importe laquelle des combinaisons (opérateur `AND`, `OR`, `NOT`) ci-dessus.
* Utilisez la continuation : L’objet query est instancié avec une taille de page (jusqu’à 100). Vous pouvez récupérer les jumeaux numériques une page à la fois en fournissant le jeton de continuation dans les appels suivants à l’API.

## <a name="next-steps"></a>Étapes suivantes

Apprenez à écrire des requêtes et consultez des exemples de codes clients dans [*Guide pratique : Interroger le graphique de jumeaux*](how-to-query-graph.md).
