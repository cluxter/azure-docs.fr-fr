---
title: Configurer des données basées sur STIG pour Azure Automation State Configuration
description: Cet article explique comment configurer des données basées sur STIG pour Azure Automation State Configuration.
keywords: dsc,powershell,configuration,installation
services: automation
ms.service: automation
ms.subservice: dsc
author: mgreenegit
ms.author: migreene
ms.date: 08/08/2019
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 113a6a259f0c69bdcc3b1684803af54ed7ecbddf
ms.sourcegitcommit: ec682dcc0a67eabe4bfe242fce4a7019f0a8c405
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86186484"
---
# <a name="configure-data-based-on-stig"></a>Configurer des données basées sur STIG

> S’applique à : Windows PowerShell 5.1

Créer du contenu de configuration pour la première fois peut s’avérer délicat.
Dans bien des cas, l’objectif est d’automatiser la configuration des serveurs selon une « ligne de base » qui, de préférence, est conforme aux recommandations du secteur.

> [!NOTE]
> Cet article fait référence à une solution tenue à jour par la communauté Open Source.
> La prise en charge est disponible uniquement sous forme de collaboration GitHub, et non auprès de Microsoft.

## <a name="community-project-powerstig"></a>Projet communautaire : PowerSTIG

Un projet communautaire nommé [PowerSTIG](https://github.com/microsoft/powerstig) a pour but de résoudre ce problème en générant du contenu DSC basé sur des [informations publiques](https://public.cyber.mil/stigs/) sur STIG (Security Technical Implementation Guide).

Utiliser des lignes de base est plus compliqué qu’il n’y paraît.
Nombreuses sont les organisations à devoir [documenter les exceptions](https://github.com/microsoft/powerstig#powerstigdata) aux règles et à gérer ces données à la bonne échelle.
PowerSTIG résout le problème en fournissant des [ressources composites](https://github.com/microsoft/powerstig#powerstigdsc) destinées à gérer chaque partie de la configuration au lieu de tenter de gérer l’ensemble des paramètres dans un même fichier volumineux.

Une fois que les configurations ont été générées, vous pouvez utiliser les [scripts de configuration DSC](/powershell/scripting/dsc/configurations/configurations) pour générer des fichiers MOF et [charger ces mêmes fichiers MOF dans Azure Automation](./tutorial-configure-servers-desired-state.md#create-and-upload-a-configuration-to-azure-automation).
Inscrivez ensuite vos serveurs [localement](./automation-dsc-onboarding.md#enable-physicalvirtual-linux-machines) ou [dans Azure](./automation-dsc-onboarding.md#enable-azure-vms) pour extraire les configurations.

Pour tester PowerSTIG, accédez à [PowerShell Gallery](https://www.powershellgallery.com) et téléchargez la solution ou cliquez sur « Project Site » pour afficher la [documentation](https://github.com/microsoft/powerstig).

## <a name="next-steps"></a>Étapes suivantes

- Pour comprendre DSC PowerShell, consultez [Vue d’ensemble de la fonctionnalité Desired State Configuration de Windows PowerShell](/powershell/scripting/dsc/overview/overview).
- Découvrez les ressources DSC PowerShell dans [Ressources DSC](/powershell/scripting/dsc/resources/resources).
- Pour plus d’informations sur la configuration du Configuration Manager local, consultez [configuration du Configuration Manager local](/powershell/scripting/dsc/managing-nodes/metaconfig).
