---
title: 'Application Insights : langages, plateformes et intégrations | Microsoft Docs'
description: Langages, plateformes et intégrations disponibles pour Application Insights
ms.topic: conceptual
ms.date: 07/18/2019
ms.reviewer: olegan
ms.openlocfilehash: 35dc6c5146edd13309a42702d1bc247333ff0fd7
ms.sourcegitcommit: a76ff927bd57d2fcc122fa36f7cb21eb22154cfa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87322446"
---
# <a name="supported-languages"></a>Langues prises en charge

* [C#|VB (.NET)](./asp-net.md)
* [Java](./java-get-started.md)
* [JavaScript](./javascript.md)
* [Node.JS](./nodejs.md)
* [Python](./opencensus-python.md)

## <a name="supported-platforms-and-frameworks"></a>Plateformes et infrastructures prises en charge

### <a name="instrumentation-for-already-deployed-applications-codeless-agent-based"></a>Instrumentation pour les applications déjà déployées (sans codes, basées sur un agent)
* [Machines virtuelles et groupes de machines virtuelles identiques Azure](./azure-vm-vmss-apps.md)
* [Azure App Service](./azure-web-apps.md)
* [ASP.NET : pour les applications déjà actives](./monitor-performance-live-website-now.md)
* [Azure Cloud Services](./cloudservices.md) incluant les rôles web et de travail
* [Azure Functions](../../azure-functions/functions-monitoring.md)
### <a name="instrumentation-through-code-sdks"></a>Instrumentation par le biais du code (SDK)
* [ASP.NET](./asp-net.md)
* [ASP.NET Core](./asp-net-core.md)
* [Android](../learn/mobile-center-quickstart.md) (App Center)
* [iOS](../learn/mobile-center-quickstart.md) (App Center)
* [Java EE](./java-get-started.md)
* [Node.JS](https://www.npmjs.com/package/applicationinsights)
* [Python](./opencensus-python.md)
* [Application Windows universelle](../learn/mobile-center-quickstart.md) (App Center)
* [Rôles de travail, services et applications de bureau Windows](./windows-desktop.md)

## <a name="logging-frameworks"></a>Frameworks de journalisation
* [ILogger](./ilogger.md)
* [Log4Net, NLog ou System.Diagnostics.Trace](./asp-net-trace-logs.md)
* [Java, Log4J ou Logback](./java-trace-logs.md)
* [Plug-in LogStash](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-output-applicationinsights)
* [Azure Monitor](/archive/blogs/msoms/application-insights-connector-in-oms)

## <a name="export-and-data-analysis"></a>Exportation et analyse de données
* [Power BI](https://powerbi.microsoft.com/blog/explore-your-application-insights-data-with-power-bi/)
* [Stream Analytics](./export-power-bi.md)

## <a name="unsupported-sdks"></a>Kits de développement logiciel (SDK) non pris en charge
Nous sommes conscients qu’il existe plusieurs autres SDK pris en charge par la communauté. Toutefois, Azure Monitor assure uniquement la prise en charge lors de l’utilisation des kits de développement logiciel pris en charge figurant sur cette page. Nous évaluons constamment les opportunités de développer notre prise en charge d’autres langues. Suivez notre page d’[annonces GitHub](https://github.com/microsoft/ApplicationInsights-Announcements/issues) pour recevoir les dernières informations concernant les kits de développement (SDK). 

