---
title: Gérer l’authentification
titleSuffix: Azure Maps
description: Utilisez le portail Azure pour gérer l’authentification dans Microsoft Azure Maps.
author: philmea
ms.author: philmea
ms.date: 06/12/2020
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: 174606b4b070b69aba94f438a3f7177f0d5897f8
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2020
ms.locfileid: "84981713"
---
# <a name="manage-authentication-in-azure-maps"></a>Gérer l’authentification dans Azure Maps

Suite à la création d’un compte Azure Maps, un ID client et des clés sont créés pour prendre en charge l’authentification Azure Active Directory (Azure AD) et l’authentification par clé partagée.

## <a name="view-authentication-details"></a>Afficher les détails de l’authentification

Après la création du compte Azure Maps, les clés principales et secondaires sont générées. Nous vous recommandons d’utiliser la clé principale comme clé d’abonnement quand vous [utilisez l’authentification par clé partagée pour appeler Azure Maps](https://docs.microsoft.com/azure/azure-maps/azure-maps-authentication#shared-key-authentication). Vous pouvez utiliser une clé secondaire dans des scénarios comme des changements dans la permutation des clés. Pour plus d’informations, consultez [Authentification dans Azure Maps](https://aka.ms/amauth).

Vous pouvez voir les détails de votre authentification dans le portail Azure. Dans votre compte, dans le menu **Paramètres**, sélectionnez **Authentification**.

> [!div class="mx-imgBorder"]
> ![Informations sur l’authentification](./media/how-to-manage-authentication/how-to-view-auth.png)

## <a name="discover-category-and-scenario"></a>Catégorie et scénario de découverte

En fonction des besoins de l’application, il existe des chemins spécifiques pour sécuriser l’application. Azure AD définit des catégories pour prendre en charge un large éventail de flux d’authentification. Consultez [les catégories d’applications](https://docs.microsoft.com/azure/active-directory/develop/authentication-flows-app-scenarios#application-categories) pour comprendre quelle catégorie est adaptée à l’application.

> [!NOTE]
> Même si vous utilisez l’authentification par clé partagée, comprendre les catégories et les scénarios vous aide à sécuriser l’application.

## <a name="determine-authentication-and-authorization"></a>Déterminer l’authentification et l’autorisation

Le tableau suivant présente les scénarios d’authentification et d’autorisation courants dans Azure Maps. Le tableau fournit une comparaison des types de protection proposés par chaque scénario.

> [!IMPORTANT]
> Microsoft recommande d’implémenter Azure Active Directory (Azure AD) et le contrôle d’accès en fonction du rôle (RBAC) pour les applications de production.

| Scénario                                                                                    | Authentification | Autorisation | Effort de développement | Effort opérationnel |
| ------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------------ | ------------------ |
| [Démon approuvé/application cliente non interactive](./how-to-secure-daemon-app.md)        | Clé partagée     | N/A           | Moyenne             | Élevé               |
| [Démon approuvé/application cliente non interactive](./how-to-secure-daemon-app.md)        | Azure AD       | Élevé          | Faible                | Moyenne             |
| [Application web à page unique avec authentification unique interactive](./how-to-secure-spa-users.md) | Azure AD       | Élevé          | Moyenne             | Moyenne             |
| [Application web à page unique avec authentification non interactive](./how-to-secure-spa-app.md)      | Azure AD       | Élevé          | Moyenne             | Moyenne             |
| [Application web avec authentification unique interactive](./how-to-secure-webapp-users.md)          | Azure AD       | Élevé          | Élevé               | Moyenne             |
| [Appareil IoT/appareil avec restriction d’entrée](./how-to-secure-device-code.md)                     | Azure AD       | Élevé          | Moyenne             | Moyenne             |

Les liens du tableau vous conduisent à des informations détaillées sur la configuration de chaque scénario.

## <a name="view-role-definitions"></a>Afficher les définitions de rôles

Pour voir les rôles RBAC disponibles pour Azure Maps, accédez à **Contrôle d’accès (IAM)** . Sélectionnez **Rôles**, puis recherchez les rôles qui commencent par *Azure Maps*. Ces rôles Azure Maps sont les rôles auxquels vous pouvez accorder un accès.

> [!div class="mx-imgBorder"]
> ![View available roles](./media/how-to-manage-authentication/how-to-view-avail-roles.png)

## <a name="view-role-assignments"></a>Voir les attributions de rôles

Pour voir les applications et les utilisateurs auxquels le contrôle d’accès en fonction du rôle (RBAC) pour Azure Maps a été accordé, accédez à l’option **Contrôle d’accès (IAM)** . Ensuite, sélectionnez **Attributions de rôles**, puis filtrez sur **Azure Maps**.

> [!div class="mx-imgBorder"]
> ![View users and apps that have been granted RBAC](./media/how-to-manage-authentication/how-to-view-amrbac.png)

## <a name="request-tokens-for-azure-maps"></a>Demander des jetons pour Azure Maps

Demandez un jeton auprès du point de terminaison de jeton Azure AD. Dans votre demande Azure AD, utilisez les informations suivantes :

| Environnement Azure      | Point de terminaison de jeton Azure AD             | ID de ressource Azure              |
| ---------------------- | ----------------------------------- | ------------------------------ |
| Cloud public Azure     | `https://login.microsoftonline.com` | `https://atlas.microsoft.com/` |
| Cloud Azure Government | `https://login.microsoftonline.us`  | `https://atlas.microsoft.com/` |

Pour en savoir plus sur les demandes de jetons d’accès auprès d’Azure AD pour des utilisateurs et principaux de service, consultez [Scénarios d’authentification pour Azure AD](https://docs.microsoft.com/azure/active-directory/develop/authentication-scenarios) et des scénarios spécifiques du tableau [Scénarios](./how-to-manage-authentication.md#determine-authentication-and-authorization).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez [Azure AD et SDK web Azure Maps](https://docs.microsoft.com/azure/azure-maps/how-to-use-map-control).

Recherchez les métriques d’utilisation de l’API pour votre compte Azure Maps :
> [!div class="nextstepaction"]
> [Afficher les métriques d’utilisation](how-to-view-api-usage.md)

Explorez des exemples qui montrent comment intégrer Azure AD à Azure Maps :

> [!div class="nextstepaction"]
> [Exemples d’authentification Azure AD](https://github.com/Azure-Samples/Azure-Maps-AzureAD-Samples)
