---
title: Méthodes d’authentification
titleSuffix: Azure Maps
description: Dans cet article, vous allez découvrir l’authentification Azure Active Directory et l’authentification par clé partagée. Les deux sont utilisées pour les services Microsoft Azure Maps. Découvrez comment obtenir une clé d’abonnement Azure Maps.
author: philmea
ms.author: philmea
ms.date: 06/12/2020
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: philmea
ms.custom: mvc
ms.openlocfilehash: fe79b630291959ce4dc8b4743127986088a876ae
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2020
ms.locfileid: "84987546"
---
# <a name="authentication-with-azure-maps"></a>Authentification avec Azure Maps

Azure Maps prend en charge deux méthodes pour authentifier les requêtes : Authentification par clé partagée et authentification [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis). Cet article explique ces méthodes d’authentification pour vous guider dans votre implémentation des services Azure Maps.

> [!NOTE]
> Pour sécuriser davantage la communication avec Azure Maps, nous prenons désormais en charge le protocole TLS 1.2 et ne prenons plus en charge les versions 1.0 et 1.1 de ce protocole. Pour éviter toute interruption de service, **mettez à jour vos serveurs et vos applications pour qu’ils utilisent TLS 1.2 avant le 2 avril 2020**.  Si vous utilisez actuellement TLS 1.x, découvrez si vous êtes prêt à passer à TLS 1.2 et créez un plan de migration avec les tests décrits dans [Résoudre les problèmes de dépendances TLS 1.0](https://docs.microsoft.com/security/solving-tls1-problem).

## <a name="shared-key-authentication"></a>Authentification par clé partagée

 Les clés primaires et secondaires sont générées après la création du compte Azure Maps. Nous vous encourageons à utiliser la clé primaire comme clé d’abonnement lors de l’appel d’Azure Maps à l’aide de l’authentification par clé partagée. L’authentification par clé partagée transmet une clé générée par un compte Azure Maps à un service Azure Maps. Pour chaque requête envoyée aux services Azure Maps, ajoutez la *clé d’abonnement* à l’URL en tant que paramètre. La clé secondaire peut être utilisée dans des scénarios tels que le roulement des changements de clés.  

Pour plus d’informations sur l’affichage de vos clés dans le portail Azure, consultez [Gérer l’authentification](https://aka.ms/amauthdetails).

> [!Tip]
> Nous vous recommandons de regénérer régulièrement vos clés. Vous disposez de deux clés, ce qui signifie que vous pouvez maintenir les connexions à l’aide d’une clé pendant que vous regénérez l’autre clé. Lorsque vous régénérez vos clés, vous devez mettre à jour toutes les applications qui accèdent à votre compte pour qu’elles utilisent les nouvelles clés.

## <a name="azure-ad-authentication"></a>Authentification Azure AD

Les abonnements Azure sont fournis avec un locataire Azure AD afin de permettre un contrôle d’accès affiné. Azure Maps offre une authentification pour les services Azure Maps à l’aide d’Azure AD. Azure AD fournit une authentification basée sur les identités pour les utilisateurs et les applications inscrits dans le locataire Azure AD.

Azure Maps accepte les jetons d’accès **OAuth 2.0** pour les locataires Azure AD associés à un abonnement Azure comprenant un compte Azure Maps. Azure Maps accepte également les jetons pour :

* Utilisateurs Azure AD
* Applications partenaires qui utilisent des autorisations déléguées par des utilisateurs
* Identités gérées pour les ressources Azure

Azure Maps génère un *identificateur unique (ID client)* pour chaque compte Azure Maps. Vous pouvez demander des jetons à Azure AD lorsque vous combinez cet ID client avec des paramètres supplémentaires.

Si vous souhaitez obtenir plus d’informations sur la configuration d’Azure AD et sur les requêtes de jetons pour Azure Maps, consultez [Gérer l’authentification dans Azure Maps](https://docs.microsoft.com/azure/azure-maps/how-to-manage-authentication).

Pour obtenir des informations générales sur l’authentification auprès d’Azure AD, consultez [Qu’est-ce que l’authentification ?](https://docs.microsoft.com/azure/active-directory/develop/authentication-scenarios).

### <a name="managed-identities-for-azure-resources-and-azure-maps"></a>Identités managées pour les ressources Azure et Azure Maps

Les [identités managées pour les ressources Azure](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) fournissent aux services Azure un principal de sécurité basé sur l’application et managé automatiquement qui peut s’authentifier auprès d’Azure AD. Avec le contrôle d’accès en fonction du rôle (RBAC), le principal de sécurité d’identités managées peut être autorisé à accéder aux services Azure Maps. Voici quelques exemples d’identités managées : Azure App Service, Azure Functions et Machines virtuelles Azure. Pour obtenir une liste d’identités managées, consultez [Identités managées pour les ressources Azure](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/services-support-managed-identities).

### <a name="configuring-application-azure-ad-authentication"></a>Configuration de l’authentification Azure AD des applications

Les applications s’authentifient auprès du locataire Azure AD par le biais d’un ou plusieurs scénarios pris en charge fournis par Azure AD. Chaque scénario d’application Azure AD représente des exigences différentes en fonction des besoins de l’entreprise. Certaines applications peuvent nécessiter des expériences de connexion utilisateur, tandis que d’autres peuvent nécessiter une expérience de connexion d’application. Pour plus d’informations, consultez [Flux d’authentification et scénarios d’applications](https://docs.microsoft.com/azure/active-directory/develop/authentication-flows-app-scenarios).

Une fois que l’application a reçu un jeton d’accès, le SDK et/ou l’application envoie une requête HTTPS avec l’ensemble suivant d’en-têtes HTTP requis en plus des autres en-têtes HTTP de l’API REST :

| Nom de l’en-tête    | Valeur               |
| :------------- | :------------------ |
| x-ms-client-id | 30d7cc….9f55        |
| Autorisation  | Bearer eyJ0e….HNIVN |

> [!Note]
> `x-ms-client-id` est le compte Azure Maps basé sur le GUID, qui apparaît dans la page d’authentification Azure Maps.

Voici un exemple de requête de routage Azure Maps qui utilise un jeton du porteur OAuth Azure AD :

```http
GET /route/directions/json?api-version=1.0&query=52.50931,13.42936:52.50274,13.43872
Host: atlas.microsoft.com
x-ms-client-id: 30d7cc….9f55
Authorization: Bearer eyJ0e….HNIVN
```

Pour plus d’informations sur l’affichage de votre ID client, consultez [Voir les détails de l’authentification](https://aka.ms/amauthdetails).

## <a name="authorization-with-role-based-access-control"></a>Autorisation avec contrôle d’accès en fonction du rôle

Azure Maps prend en charge l’accès à tous les types de principaux pour le [contrôle d’accès en fonction du rôle Azure](https://docs.microsoft.com/azure/role-based-access-control/overview), notamment les utilisateurs Azure AD, les groupes, les applications, les ressources Azure et les identités managées Azure. Un jeu d’autorisations, également appelé définition de rôle, est accordé aux types de principaux. Une définition de rôle fournit des autorisations pour les actions de l’API REST. L’application de l’accès à un ou plusieurs comptes Azure Maps est appelée « étendue ». Lors de l’application d’un principal, d’une définition de rôle et d’une étendue, une attribution de rôle est créée. 

Les sections ci-après traitent des concepts et des composants de l’intégration d’Azure Maps au contrôle d’accès en fonction du rôle Azure AD. Dans le cadre du processus de configuration de votre compte Azure Maps, un annuaire Azure AD est associé à l’abonnement Azure dans lequel réside le compte Azure Maps. 

Quand vous configurez Azure RBAC, vous choisissez un principal de sécurité et l’appliquez à une attribution de rôle. Pour découvrir comment ajouter des attributions de rôles dans le portail Azure, consultez [Ajouter ou supprimer des attributions de rôles Azure](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).

### <a name="picking-a-role-definition"></a>Sélection d’une définition de rôle

Les types de définitions de rôles suivants sont disponibles pour prendre en charge les scénarios d’application.

| Définition de rôle Azure       | Description                                                                                              |
| :-------------------------- | :------------------------------------------------------------------------------------------------------- |
| Lecteur de données Azure Maps      | Fournit l’accès aux API REST Azure Maps immuables.                                                       |
| Contributeur aux données Azure Maps | Fournit l’accès aux API REST Azure Maps mutables. La mutabilité est définie par les actions Écrire et Supprimer. |
| Définition de rôle personnalisée      | Créez un rôle conçu pour permettre un accès limité flexible aux API REST Azure Maps.                      |

Certains services Azure Maps peuvent nécessiter des privilèges élevés pour effectuer des actions d’écriture ou de suppression sur les API REST Azure Maps. Le rôle Contributeur aux données Azure Maps est obligatoire pour les services qui fournissent des actions d’écriture ou de suppression. Le tableau suivant décrit les services auxquels s’applique le rôle Contributeur aux données Azure Maps lors de l’utilisation d’actions d’écriture ou de suppression sur le service donné. Si seules des actions de lecture sont utilisées sur le service, vous pouvez utiliser le rôle Lecteur de données Azure Maps plutôt que Contributeur aux données Azure Maps.

| Service Azure Maps | Définition de rôle Azure Maps  |
| :----------------- | :-------------------------- |
| Données               | Contributeur aux données Azure Maps |
| Creator            | Contributeur aux données Azure Maps |
| Spatial            | Contributeur aux données Azure Maps |

Pour plus d’informations sur la consultation de vos paramètres RBAC, consultez [Comment configurer le contrôle RBAC pour Azure Maps](https://aka.ms/amrbac).

#### <a name="custom-role-definitions"></a>Définitions de rôles personnalisées

L’un des aspects de la sécurité des applications concerne l’application du principe du privilèges minimum. Ce principe implique qu’il ne faut accorder au principal de sécurité que l’accès nécessaire, et aucun accès supplémentaire. La création de définitions de rôles personnalisées peut prendre en charge des cas d’usage qui nécessitent une granularité supplémentaire du contrôle d’accès. Pour créer une définition de rôle personnalisée, vous pouvez sélectionner des actions de données spécifiques à inclure ou exclure pour la définition. 

La définition de rôle personnalisée peut ensuite être utilisée dans une attribution de rôle pour n’importe quel principal de sécurité. Pour en savoir plus sur les définitions de rôles personnalisées Azure, consultez [Rôles personnalisés Azure](https://docs.microsoft.com/azure/role-based-access-control/custom-roles).

Voici quelques exemples de scénarios dans lesquels des rôles personnalisés peuvent améliorer la sécurité de l’application.

| Scénario                                                                                                                                                                                                                 | Action(s) de données de rôles personnalisés                                                                                                                  |
| :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------ |
| Une page web de connexion interactive ou publique avec des mosaïques de base et aucune autre API REST.                                                                                                                              | `Microsoft.Maps/accounts/services/render/read`                                                                                              |
| Une application qui nécessite uniquement le géocodage inversé et aucune autre API REST.                                                                                                                                             | `Microsoft.Maps/accounts/services/search/read`                                                                                              |
| Un rôle pour un principal de sécurité qui demande la lecture de données cartographiques basées sur Azure Maps Creator et des API REST de mosaïques de base.                                                                                                 | `Microsoft.Maps/accounts/services/data/read`, `Microsoft.Maps/accounts/services/render/read`                                                |
| Un rôle pour un principal de sécurité qui nécessite la lecture, l’écriture et la suppression de données cartographiques basées sur Creator. Cela peut être défini en tant que rôle d’éditeur de données de carte, mais n’autorise pas l’accès à d’autres API REST comme les mosaïques de base. | `Microsoft.Maps/accounts/services/data/read`, `Microsoft.Maps/accounts/services/data/write`, `Microsoft.Maps/accounts/services/data/delete` |

### <a name="understanding-scope"></a>Présentation de l’étendue

Quand vous créez une attribution de rôle, elle est définie dans la hiérarchie de ressources Azure. En haut de la hiérarchie figure un [groupe d’administration](https://docs.microsoft.com/azure/governance/management-groups/overview), et tout en bas se trouvent les ressources Azure comme les comptes Azure Maps.
L’attribution d’une attribution de rôle à un groupe de ressources peut permettre l’accès à plusieurs comptes Azure Maps ou à plusieurs ressources du groupe.

> [!Tip]
> La recommandation générale de Microsoft consiste à attribuer l’accès à l’étendue de compte Azure Maps, car cela empêche tout **accès involontaire à d’autres comptes Azure Maps** existants dans le même abonnement Azure.

## <a name="next-steps"></a>Étapes suivantes

* Pour en savoir plus sur RBAC, consultez [Vue d’ensemble du contrôle d’accès en fonction du rôle](https://docs.microsoft.com/azure/role-based-access-control/overview).

* Pour plus d’informations sur l’authentification d’une application avec Azure AD et Azure Maps, consultez [Gérer l’authentification dans Azure Maps](https://docs.microsoft.com/azure/azure-maps/how-to-manage-authentication).

* Pour plus d’informations sur l’authentification d’Azure Maps, de Map Control et d’Azure AD, consultez [Utiliser Azure AD et Azure Maps Map Control](https://aka.ms/amaadmc).
