---
title: Rendu du débogage
description: Vue d’ensemble des effets du rendu du débogage côté serveur
author: jumeder
ms.author: jumeder
ms.date: 06/15/2020
ms.topic: article
ms.openlocfilehash: aa6e6dced3dfd32896489db2ed76704304dbc745
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85565442"
---
# <a name="debug-rendering"></a>Rendu du débogage

L’API de rendu du débogage fournit un large éventail d’options globales pour modifier le rendu côté serveur avec différents effets de débogage.

## <a name="available-debug-rendering-effects"></a>Effets du rendu du débogage disponibles

|Paramètre                          | Résultat                               |
|---------------------------------|:-------------------------------------|
|Compteur de cadres                    | Restitue une superposition de texte en haut à gauche du cadre. Le texte affiche l’ID de cadre côté serveur actuel, qui est en permanence incrémenté à mesure que le rendu se poursuit. |
|Nombre de polygones                    | Restitue une superposition de texte en haut à gauche du cadre. Le texte affiche la quantité de polygones actuellement restitués, qui est la même valeur que celle interrogée par les [Requêtes de performances côté serveur](performance-queries.md).| 
|Modèle filaire                        | Si ce paramètre est activé, toute la géométrie d’objet chargée sur le serveur est restituée en mode filaire. Seuls les bords des polygones sont rastérisés dans ce mode. |

Le code suivant active ces effets de débogage :

```cs
void EnableDebugRenderingEffects(AzureSession session, bool highlight)
{
    DebugRenderingSettings settings = session.Actions.DebugRenderingSettings;

    // Enable frame counter text overlay on the server side rendering
    settings.RenderFrameCount = true;

    // Enable polygon count text overlay on the server side rendering
    settings.RenderPolygonCount = true;

    // Enable wireframe rendering of object geometry on the server
    settings.RenderWireframe = true;
}
```

```cpp
void EnableDebugRenderingEffects(ApiHandle<AzureSession> session, bool highlight)
{
    ApiHandle<DebugRenderingSettings> settings = *session->Actions()->DebugRenderingSettings();

    // Enable frame counter text overlay on the server side rendering
    settings->RenderFrameCount(true);

    // Enable polygon count text overlay on the server side rendering
    settings->RenderPolygonCount(true);

    // Enable wireframe rendering of object geometry on the server
    settings->RenderWireframe(true);
}
```

![Rendu du débogage](./media/debug-rendering.png)

> [!NOTE]
> Tous les effets du rendu du débogage sont des paramètres globaux qui affectent l’ensemble du cadre.

## <a name="use-cases"></a>Cas d'utilisation

L’API de rendu du débogage est destinée aux tâches de débogage simples, comme vérifier que la connexion du service est actuellement active et qu’elle fonctionne correctement. Les options de rendu du texte affectent directement les trames vidéo transmises en aval. Si vous les activez, le système vérifie si les nouvelles trames sont correctement reçues et décodées sous forme de vidéo.

Toutefois, les effets fournis ne donnent aucune introspection détaillée de l’intégrité du service. Les [requêtes de performances côté serveur](performance-queries.md) sont recommandées pour ce cas d’usage.

## <a name="performance-considerations"></a>Considérations relatives aux performances

* L’activation des superpositions de texte entraîne peu, voire pas, de surcharge de performances.
* L’activation du mode filaire entraîne une surcharge de performances non négligeable, même si elle peut varier en fonction de la scène. Pour les scènes complexes, ce mode peut provoquer la chute de la fréquence d’images en dessous de la cible de 60 Hz.

## <a name="next-steps"></a>Étapes suivantes

* [Modes de rendu](../../concepts/rendering-modes.md)
* [Requêtes de performances côté serveur](performance-queries.md)
