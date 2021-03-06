---
title: Créer votre première fonction à l’aide du Portail Azure
description: Apprenez à créer votre première fonction Azure pour une exécution sans serveur à l’aide du portail Azure.
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.topic: how-to
ms.date: 03/26/2020
ms.custom: mvc, devcenter, cc996988-fb4f-47
ms.openlocfilehash: 030af8a289daaf03d17f8402e8d603e893657853
ms.sourcegitcommit: a8ee9717531050115916dfe427f84bd531a92341
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83123608"
---
# <a name="create-your-first-function-in-the-azure-portal"></a>Créer votre première fonction à l’aide du Portail Azure

Azure Functions vous permet d’exécuter votre code dans un environnement serverless, et sans avoir à créer une machine virtuelle ou à publier une application web au préalable. Dans cet article, vous allez découvrir comment utiliser Azure Functions pour créer une fonction de déclencheur via HTTP, « Hello world », dans le Portail Azure.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

Si vous êtes développeur C#, envisagez de [créer votre première fonction dans Visual Studio 2019](functions-create-your-first-function-visual-studio.md) plutôt que dans le portail. 

## <a name="sign-in-to-azure"></a>Connexion à Azure

Connectez-vous au [portail Azure](https://portal.azure.com) avec votre compte Azure.

## <a name="create-a-function-app"></a>Créer une application de fonction

Vous devez disposer d’une Function App pour héberger l’exécution de vos fonctions. Une application de fonctions vous permet de regrouper des fonctions en une unité logique pour faciliter la gestion, le déploiement et le partage des ressources.

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

Créez ensuite une fonction dans la nouvelle application de fonction.

## <a name="create-an-http-trigger-function"></a><a name="create-function"></a>Créer une fonction de déclencheur HTTP

1. Dans le menu de gauche de la fenêtre **Fonctions**, sélectionnez **Fonctions**, puis **Ajouter** dans le menu supérieur. 
 
1. Dans la fenêtre **Nouvelle fonction**, sélectionnez **Déclencheur http**.

    ![Choisir une fonction de déclencheur HTTP](./media/functions-create-first-azure-function/function-app-select-http-trigger.png)

1. Dans la fenêtre **Nouvelle fonction**, acceptez le nom par défaut pour la **Nouvelle fonction** ou entrez un nouveau nom. 

1. Choisissez **Anonyme** dans la liste déroulante **Niveau d’autorisation**, puis sélectionnez **Créer une fonction**.

    Azure crée la fonction de déclencheur HTTP. Vous pouvez maintenant exécuter la nouvelle fonction en envoyant une requête HTTP.

## <a name="test-the-function"></a>Tester la fonction

1. Dans votre nouvelle fonction de déclencheur HTTP, sélectionnez **Code + test** dans le menu de gauche, puis sélectionnez **Obtenir l’URL de la fonction** dans le menu supérieur.

    ![Sélectionner Obtenir l’URL de la fonction](./media/functions-create-first-azure-function/function-app-select-get-function-url.png)

1. Dans la boîte de dialogue **Obtenir l’URL de la fonction**, sélectionnez **Par défaut** dans la liste déroulante, puis choisissez l’icône **Copier dans le Presse-papiers.** . 

    ![Copier l’URL de fonction à partir du portail Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

1. Collez l’URL de fonction dans la barre d’adresse de votre navigateur. Ajoutez la valeur de la chaîne de requête `?name=<your_name>` à la fin de cette URL, puis appuyez sur la touche Entrée pour exécuter la requête. 

    L’exemple suivant montre la réponse dans le navigateur :

    ![Réponse de la fonction dans le navigateur.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    L’URL de demande inclut une clé qui est requise, par défaut, pour accéder à votre fonction sur HTTP.

1. Lorsque votre fonction s’exécute, des informations de suivi sont écrites dans les journaux d’activité. Pour afficher la sortie de suivi, revenez à la page **Code + test** dans le portail, puis développez la flèche **Journaux** en bas de la page.

   ![Affichage des journaux de fonction dans le portail Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Nettoyer les ressources

[!INCLUDE [Clean-up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

