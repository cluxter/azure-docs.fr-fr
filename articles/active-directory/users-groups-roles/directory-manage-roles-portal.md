---
title: Afficher et affecter des autorisations de rôles d’administrateur - Azure AD | Microsoft Docs
description: Vous pouvez maintenant consulter et gérer les membres d’un rôle d’administrateur Azure AD dans le portail. Pour les personnes qui gèrent fréquemment les attributions de rôles.
services: active-directory
author: curtand
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.subservice: users-groups-roles
ms.topic: how-to
ms.date: 06/15/2020
ms.author: curtand
ms.reviewer: vincesm
ms.custom: it-pro
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e067e8d56f8a928f952648fc76cd5d6b7a1afe7
ms.sourcegitcommit: f844603f2f7900a64291c2253f79b6d65fcbbb0c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86221261"
---
# <a name="view-and-assign-administrator-roles-in-azure-active-directory"></a>Afficher et assigner des rôles d’administrateur dans Azure Active Directory

Vous pouvez maintenant consulter et gérer tous les membres des rôles d’administrateur dans le portail Azure Active Directory. Si vous gérez fréquemment des attributions de rôles, vous préférerez probablement cette expérience. Et si vous vous êtes déjà demandé « À quoi ces rôles servent-ils vraiment ? », vous pouvez voir une liste détaillée des autorisations pour chacun des rôles d’administrateur Azure AD.

## <a name="view-all-roles"></a>Afficher tous les rôles

1. Connectez-vous au [portail Azure](https://portal.azure.com) et sélectionnez **Azure Active Directory**.

1. Sélectionnez **Rôles et administrateurs** pour voir la liste de tous les rôles disponibles.

1. Sélectionnez les points de suspension à droite de chaque ligne pour afficher les autorisations pour le rôle. Sélectionnez un rôle pour afficher les utilisateurs assignés au rôle. Si vous voyez un nom différent de l’image suivante, lisez la Note dans [Afficher les affectations de rôles privilégiés](#view-assignments-for-privileged-roles) pour vérifier si vous êtes dans Privileged Identity Management (PIM).

    ![liste des rôles dans le portail Azure AD](./media/directory-manage-roles-portal/view-roles-in-azure-active-directory.png)

## <a name="view-my-roles"></a>Afficher mes rôles

Il est également facile d’afficher vos propres autorisations. Sélectionnez **Votre rôle** dans la page **Rôles et administrateurs** pour afficher les rôles qui sont actuellement attribués.

## <a name="view-assignments-for-privileged-roles"></a>Afficher les affectations pour les rôles privilégiés

Vous pouvez sélectionner **Gérer dans PIM** pour disposer de davantage de fonctionnalités de gestion. Les administrateurs de rôle privilégié peuvent modifier les affectations « permanentes » (toujours actives dans le rôle) en affectations « éligibles » (dans le rôle uniquement en cas d’élévation). Si vous n’avez pas Privileged Identity Management, vous pouvez toujours sélectionner **Gérer dans PIM** pour vous inscrire à un essai. Privileged Identity Management nécessite un [plan de licences Azure AD Premium P2](../privileged-identity-management/subscription-requirements.md).

![liste des membres d’un rôle d’administrateur](./media/directory-manage-roles-portal/member-list.png)

Si vous êtes un administrateur global ou un administrateur de rôle privilégié, vous pouvez facilement ajouter ou supprimer des membres, filtrer la liste ou sélectionner un membre pour voir ses rôles assignés actifs.

> [!Note]
> Si vous disposez d’une licence Azure AD Premium P2 et que vous utilisez déjà Privileged Identity Management, toutes les tâches de gestion des rôles sont effectuées dans Privilege Identity Management et non dans Azure AD.
>
> ![Rôles Azure AD gérés dans PIM pour les utilisateurs qui utilisent déjà PIM et qui disposent d’une licence Premium P2](./media/directory-manage-roles-portal/pim-manages-roles-for-p2.png)

## <a name="view-a-users-role-permissions"></a>Afficher les autorisations de rôles d’un utilisateur

Lorsque vous affichez les membres d’un rôle, sélectionnez **Description** pour afficher la liste complète des autorisations accordées par l’attribution de rôle. Cette page inclut des liens vers la documentation correspondante pour vous guider tout au long de la gestion des rôles d’annuaire.

![liste des autorisations pour un rôle d’administrateur](./media/directory-manage-roles-portal/role-description.png)

## <a name="assign-a-role"></a>Attribuer un rôle

1. Connectez-vous au [Portail Azure](https://portal.azure.com) avec les autorisations d’administrateur général ou d’administrateur de rôle privilégié, puis sélectionnez **Azure Active Directory**.

1. Sélectionnez **Rôles et administrateurs** pour voir la liste de tous les rôles disponibles.

1. Sélectionnez un rôle pour afficher ses attributions.

    ![liste des autorisations pour un rôle d’administrateur](./media/directory-manage-roles-portal/member-list.png)

1. Sélectionnez **Ajouter des attributions** et sélectionnez les rôles que vous souhaitez attribuer. Vous pouvez sélectionner **Gérer dans PIM** pour disposer de davantage de fonctionnalités de gestion. Si vous voyez un nom différent de l’image suivante, lisez la Note dans [Afficher les affectations de rôles privilégiés](#view-assignments-for-privileged-roles) pour vérifier si vous êtes dans PIM.

    ![liste des autorisations pour un rôle d’administrateur](./media/directory-manage-roles-portal/directory-role-select-role.png)

## <a name="next-steps"></a>Étapes suivantes

* N’hésitez pas à nous donner votre avis sur le [forum des rôles d’administrateur Azure AD](https://feedback.azure.com/forums/169401-azure-active-directory?category_id=166032).
* Pour plus d’informations sur les rôles et l’attribution de rôle d’administrateur, consultez [Attribuer des rôles d’administrateur](directory-assign-admin-roles.md).
* Pour les autorisations d’utilisateur par défaut, consultez une [comparaison des autorisations par défaut d’un utilisateur invité et d’un membre](../fundamentals/users-default-permissions.md).
