---
title: Télécharger en bloc une liste d’appartenances à des groupes - portail Azure Active Directory | Microsoft Docs
description: Ajoutez en bloc des utilisateurs dans le centre d'administration Azure.
services: active-directory
author: curtand
ms.author: curtand
manager: mtillman
ms.date: 04/16/2020
ms.topic: how-to
ms.service: active-directory
ms.subservice: users-groups-roles
ms.workload: identity
ms.custom: it-pro
ms.reviewer: jeffsta
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65a6a622a0d3fac7b28cc699d860068f12b780fe
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2020
ms.locfileid: "84728603"
---
# <a name="bulk-download-members-of-a-group-in-azure-active-directory"></a>Télécharger en bloc les membres d’un groupe dans Azure Active Directory

À l’aide du portail Azure Active Directory (Azure AD), vous pouvez télécharger en bloc les membres d’un groupe de votre organisation dans un fichier de valeurs séparées par des virgules (CSV).

## <a name="to-bulk-download-group-membership"></a>Pour télécharger en bloc des appartenances de groupes

1. Connectez-vous [au portail Azure](https://portal.azure.com) avec un compte Utilisateur administrateur dans l’organisation. Les propriétaires de groupes peuvent également télécharger en bloc les membres de groupes qu'ils possèdent.
1. Dans Azure AD, sélectionnez **Groupes** > **Tous les groupes**.
1. Ouvrez le groupe dont vous souhaitez télécharger l’appartenance, puis sélectionnez **Membres.**
1. Sur la page **Membres**, sélectionnez **Télécharger les membres** pour télécharger un fichier CSV des membres du groupe.

   ![La commande Télécharger les membres se trouve sur la page de profil du groupe](./media/groups-bulk-download-members/download-panel.png)

## <a name="check-download-status"></a>Vérifier l’état du téléchargement

Vous pouvez voir l’état de toutes vos demandes d’opération en bloc en attente dans la page **Résultats de l’opération en bloc**.

[![](media/groups-bulk-download-members/bulk-center.png "Check status in the Bulk Operations Results page")](media/groups-bulk-download-members/bulk-center.png#lightbox)

## <a name="bulk-download-service-limits"></a>Limites du service de téléchargement en bloc

Chaque opération en bloc pour télécharger une liste des membres d’un groupe peut prendre jusqu’à une heure. Cela vous permet de télécharger une liste d’au moins 500 000 membres.

## <a name="next-steps"></a>Étapes suivantes

- [Importer en bloc les membres du groupe](groups-bulk-import-members.md)
- [Supprimer en bloc les membres d’un groupe](groups-bulk-download-members.md)
