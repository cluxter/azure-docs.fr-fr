---
title: Migrer des machines locales à l’aide d’Azure Site Recovery
description: Cet article explique comment migrer des machines sur site vers Azure à l’aide d’Azure Site Recovery.
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.topic: tutorial
ms.date: 07/27/2020
ms.author: raynew
ms.openlocfilehash: 3c421845d4e15ef13ce98d0de111270159f564fe
ms.sourcegitcommit: dccb85aed33d9251048024faf7ef23c94d695145
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87285354"
---
# <a name="migrate-on-premises-machines-to-azure"></a>Migrer des machines sur site vers Azure

Cet article décrit les options de migration des machines locales vers Azure. 

## <a name="migrate-with-azure-migrate"></a>Migrer avec Azure Migrate

Nous vous recommandons de migrer des machines vers Azure à l’aide du service [Azure Migrate](../migrate/migrate-services-overview.md). Azure Migrate fournit un hub centralisé pour l’évaluation et la migration de machines locales vers Azure, à l’aide d’Azure Migrate, d’autres services Azure et d’outils tiers.

Pour migrer avec Azure Migrate, cliquez sur les liens suivants :

- [En savoir plus sur](../migrate/server-migrate-overview.md) les options de migration pour les machines virtuelles VMware, puis la migration des machines virtuelles vers Azure à l’aide d’une migration [sans agent](../migrate/tutorial-migrate-vmware.md) ou [avec agent](../migrate/tutorial-migrate-vmware-agent.md).
- [Migrer des machines virtuelles Hyper-V](../migrate/tutorial-migrate-hyper-v.md) vers Azure.
- Migrez des [serveurs physiques ou d’autres machines virtuelles](../migrate/tutorial-migrate-physical-virtual-machines.md), notamment des instances [AWS](../migrate/tutorial-migrate-aws-virtual-machines.md) vers Azure.

## <a name="migrate-with-site-recovery"></a>Migrer avec Site Recovery
Site Recovery ne doit être utilisé que pour la récupération d’urgence, pas pour la migration.

Si vous utilisez déjà Azure Site Recovery et souhaitez continuer à l’utiliser pour la migration, procédez comme pour configurer la récupération d’urgence.

- Machines virtuelles VMware : [Préparez Azure](tutorial-prepare-azure.md) et [VMware](vmware-azure-tutorial-prepare-on-premises.md), commencez la [réplication des machines](vmware-azure-tutorial.md), [vérifiez](tutorial-dr-drill-azure.md) que tout fonctionne et [exécutez un basculement](vmware-azure-tutorial-failover-failback.md).
- Machines virtuelles Hyper-V : [Préparez Azure](tutorial-prepare-azure-for-hyperv.md) et [Hyper-V](hyper-v-prepare-on-premises-tutorial.md), commencez la [réplication des machines](hyper-v-azure-tutorial.md), [vérifiez](tutorial-dr-drill-azure.md) que tout fonctionne et [exécutez un basculement](hyper-v-azure-failover-failback-tutorial.md).
- Serveurs physiques : [Suivez la procédure pas à pas](physical-azure-disaster-recovery.md) pour préparer Azure, préparer des machines pour la récupération d’urgence et configurer la réplication.

> [!NOTE]
> Lorsque vous opérez un basculement à des fins de récupération d’urgence, lors de la dernière étape, vous validez le basculement. Lorsque vous migrez des machines locales, l’option **Valider** n’est pas pertinente. Sélectionnez à la place l’option **Terminer la migration**. 

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Passez en revue les questions courantes](../migrate/resources-faq.md) sur Azure Migrate.

  
