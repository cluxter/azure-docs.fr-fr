---
title: Nouveautés dans la documentation Azure Monitor
description: Chaque mois, la documentation Azure Monitor fait l’objet de mises à jour importantes.
ms.subservice: ''
ms.topic: overview
author: bwren
ms.author: bwren
ms.date: 07/08/2020
ms.openlocfilehash: 192219a804365957e9eaa0577019ff18d75861bf
ms.sourcegitcommit: 3543d3b4f6c6f496d22ea5f97d8cd2700ac9a481
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86498506"
---
# <a name="whats-new-in-azure-monitor-documentation"></a>Nouveautés dans la documentation Azure Monitor

Cet article liste les nouveaux articles Azure Monitor et ceux qui ont fait l’objet d’une mise à jour importante. Il sera actualisé la première semaine de chaque mois pour inclure les mises à jour d’articles du mois précédent.

## <a name="june-2020"></a>Juin 2020

### <a name="general"></a>Général
- [Déployer Azure Monitor](platform/deploy-scale.md) - Nouvel article.
- [Clé gérée par le client dans Azure Monitor](platform/customer-managed-keys.md) - Mise à jour de la propriété billingtype. Ajout de commandes PowerShell.

### <a name="agents"></a>Agents
- [Présentation de l’agent Log Analytics](platform/log-analytics-agent.md) - Ajout de l’exigence relative à Python 2.

### <a name="alerts"></a>Alertes
- [Guide pratique pour mettre à jour des règles d’alerte ou des règles d’action quand la ressource cible est déplacée vers une autre région Azure](platform/alerts-resource-move.md) - Nouvel article.
- [Résolution des problèmes liés aux alertes de métrique Azure](platform/alerts-troubleshoot-metric.md) - Nouvel article.
- [Résolution des problèmes liés aux alertes de journal d’activité dans Azure Monitor](platform/alerts-troubleshoot-metric.md) - Nouvel article.
  
### <a name="application-insights"></a>Application Insights
- [Azure Application Insights pour les applications web JavaScript](app/javascript.md) - Mise à jour de la section sur le SDK JavaScript. Mise à jour de l’extrait de code pour signaler les échecs de chargement.
- [Configurer BYOS (Bring Your Own Storage) pour Profiler et le Débogueur de capture instantanée](app/profiler-bring-your-own-storage.md) - Nouvel article.
- [Suivi des requêtes entrantes dans Azure Application Insights avec OpenCensus Python](app/opencensus-python-request.md) - Mise à jour de la journalisation et de la configuration pour OpenCensus.
- [Superviser une application web ASP.NET dynamique avec Azure Application Insights](app/monitor-performance-live-website-now.md) - Mise à jour de la date de dépréciation pour Status Monitor v1.
- [Superviser les services Node.js avec Azure Application Insights](app/nodejs.md) - Plusieurs mises à jour, notamment la migration à partir de versions antérieures et la configuration du SDK.
- [Superviser les applications Python avec Azure Monitor (préversion)](app/opencensus-python.md) - Ajout d’une section sur la configuration des exportateurs Azure Monitor.
- [Superviser vos applications sans modification du code - Instrumentation automatique pour Azure Monitor Application Insights](app/codeless-overview.md) - Nouvel article.
- [Résolution des échecs de chargement du SDK pour les applications web JavaScript](app/javascript-sdk-load-failure.md) - Nouvel article.

### <a name="containers"></a>Conteneurs
- [Guide pratique pour arrêter la supervision de votre cluster Kubernetes hybride](insights/container-insights-optout-hybrid.md) - Ajout d’une section pour Kubernetes compatible avec Arc.
- [Configurer un cluster Kubernetes compatible Azure Arc avec Azure Monitor pour conteneurs](insights/container-insights-enable-arc-enabled-clusters.md) - Nouvel article.
- [Configurer Azure Red Hat OpenShift v4.x avec Azure Monitor pour conteneurs](insights/container-insights-azure-redhat4-setup.md) - Mise à jour des prérequis.
- [Configurer Azure Monitor pour conteneurs - Live Data (préversion)](insights/container-insights-livedata-setup.md) - Suppression de la remarque signalant que la fonctionnalité n’est pas disponible dans Azure US Government.

### <a name="insights"></a>Insights
- [FAQ - Solution Network Performance Monitor dans Azure](insights/network-performance-monitor-faq.md) - Ajout d’un FAQ pour ExpressRoute Monitor.

### <a name="logs"></a>Journaux
- [Supprimer et récupérer un espace de travail Azure Log Analytics](platform/delete-workspace.md) – Ajout d’une commande PowerShell. Mise à jour de la résolution des problèmes.
- [Gérer les espaces de travail Log Analytics dans Azure Monitor](platform/manage-access.md) - Ajout d’un exemple pour les tables non autorisées dans la section RBAC.
- [Gérer l’utilisation et les coûts à l’aide des journaux d’activité Azure Monitor](platform/manage-cost-storage.md) - Détails supplémentaires sur le calcul de la taille des données. Mise à jour des alertes de volume de données de configuration. Détails sur les données de sécurité collectées par Azure Sentinel. Clarification sur la limite de données.
- [Utiliser Azure Monitor Logs avec Azure Logic Apps et Power Automate](platform/logicapp-flow-connector.md) - Ajout de limites de connecteur.

### <a name="metrics"></a>Métriques
- [Métriques prises en charge par Azure Monitor par type de ressource](platform/metrics-supported.md) - Mise à jour des métriques SQL Server.


### <a name="platform-logs"></a>Journaux de plateforme

- [Exemples de modèle Resource Manager pour les paramètres de diagnostic](samples/resource-manager-diagnostic-settings.md) - Correctif pour le paramètre de diagnostic du journal d’activité.
- [Envoyer le journal d’activité Azure à un espace de travail Log Analytics à l’aide du portail Azure](learn/quick-collect-activity-log-portal.md) - Nouvel article.
- [Envoyer le journal d’activité Azure à un espace de travail Log Analytics à l’aide d’un modèle Azure Resource Manager](learn/quick-collect-activity-log-arm.md) - Nouvel article.

#### <a name="new-and-updated-articles-from-restructure-and-consolidation-of-platform-log-content"></a>Articles nouveaux et mis à jour suite à la restructuration et au regroupement du contenu sur les journaux de plateforme
- [Archiver des journaux de ressources Azure sur un compte de stockage](./platform/resource-logs.md#send-to-azure-storage)
- [Schéma d’événement du journal d’activité Azure](platform/activity-log-schema.md)
- [Journal d’activité Azure](platform/activity-log.md)
- [Exemples d’interface CLI Azure Monitor](samples/cli-samples.md)
- [Exemples PowerShell Azure Monitor](samples/powershell-samples.md)
- [Procédure pas à pas d’utilisation de l’API REST d’Azure Monitor](platform/rest-api-walkthrough.md)
- [Services et schémas pris en charge pour les journaux de ressource Azure](./platform/resource-logs-schema.md)
- [Journaux de ressources Azure](platform/resource-logs.md)
- [Collecter et analyser les journaux d’activités Azure dans Azure Monitor](./platform/activity-log.md)
- [Collecter les journaux de ressources Azure dans l’espace de travail Log Analytics](./platform/resource-logs.md#send-to-log-analytics-workspace)
- [Créer des paramètres de diagnostic pour envoyer des journaux et des métriques de plateforme à différentes destinations](platform/diagnostic-settings.md)
- [Exporter le journal d’activité Azure](./platform/activity-log.md#legacy-collection-methods)
- [Vue d’ensemble des journaux de plateforme Azure](platform/platform-logs-overview.md)
- [Diffuser en continu les journaux de plateforme Azure vers un Event Hub](./platform/resource-logs.md#send-to-azure-event-hubs)
- [Afficher les événements du journal d’activité Azure dans Azure Monitor](./platform/activity-log.md#view-the-activity-log)

### <a name="virtual-machines"></a>Machines virtuelles
- [Activer Azure Monitor pour machines virtuelles sur le portail Azure](insights/vminsights-enable-single-vm.md) - Mise à jour de façon à inclure Azure Arc.
- [Vue d’ensemble de l’activation d’Azure Monitor pour machines virtuelles](insights/vminsights-enable-overview.md) - Mise à jour de façon à inclure Azure Arc.
- [Qu’est-ce qu’Azure Monitor pour machines virtuelles ?](insights/vminsights-overview.md) - Mise à jour de façon à inclure Azure Arc.


### <a name="visualizations"></a>Visualisations
- [Sources de données des classeurs Azure Monitor](platform/workbooks-data-sources.md) - Ajout d’une section sur les alertes et les points de terminaison personnalisés.
- [Résolution des problèmes liés aux insights basés sur des classeurs Azure Monitor](insights/troubleshoot-workbooks.md) - Nouvel article.
- [Mise à niveau de vos visualisations de tableau de bord Log Analytics](log-query/dashboard-upgrade.md) - Nouvel article.



## <a name="may-2020"></a>Mai 2020

### <a name="general"></a>Général

- [FAQ Azure Monitor](faq.md) - Ajout de la section sur les métriques.
- [Clé gérée par le client Azure Monitor](platform/customer-managed-keys.md) - Diverses modifications en vue de la disponibilité générale.
- [Définitions de stratégie intégrées pour Azure Monitor](samples/policy-samples.md) - Nouvel article.
- [Comptes de stockage appartenant au client pour l’ingestion des journaux](platform/private-storage.md) - Nouvel article.
- [Gérer l’utilisation et les coûts à l’aide des journaux Azure Monitor](platform/manage-cost-storage.md) - Ajout de la facturation proportionnelle pour les clusters.
- [Utiliser Azure Private Link pour connecter en toute sécurité des réseaux à Azure Monitor](platform/private-link-security.md) - Nouvel article.


#### <a name="new-resource-manager-template-samples"></a>Nouveaux exemples de modèles Resource Manager 
- [Exemples de modèle Resource Manager pour Azure Monitor](samples/resource-manager-samples.md)
- [Exemples de modèle Resource Manager pour les groupes d’actions](samples/resource-manager-action-groups.md)
- [Exemples de modèle Azure Resource Manager pour les agents](samples/resource-manager-agent.md)
- [Exemples de modèle Resource Manager destinés à Azure Monitor pour conteneurs](samples/resource-manager-container-insights.md)
- [Exemples de modèle Resource Manager destinés à Azure Monitor pour machines virtuelles](samples/resource-manager-vminsights.md)
- [Exemples de modèle Resource Manager pour les paramètres de diagnostic](samples/resource-manager-diagnostic-settings.md)
- [Exemples de modèle Resource Manager pour les espaces de travail Log Analytics](samples/resource-manager-workspace.md)
- [Exemples de modèle Resource Manager pour les requêtes de journal](samples/resource-manager-log-queries.md)
- [Exemples de modèle Resource Manager pour les règles d’alerte de requête de journal](samples/resource-manager-alerts-log.md)
- [Exemples de modèle Resource Manager pour les règles d’alerte de métrique](samples/resource-manager-alerts-metric.md)
- [Exemples de modèle Resource Manager pour les classeurs](samples/resource-manager-workbooks.md)

### <a name="agents"></a>Agents
- [Installer et configurer l’extension Diagnostics Azure pour Windows (WAD)](platform/diagnostics-extension-windows-install.md) - Ajout d’informations sur la configuration de diagnostics.
- [Vue d’ensemble de l’agent Log Analytics](platform/log-analytics-agent.md) - Ajout de versions Linux prises en charge.

### <a name="application-insights"></a>Application Insights

- [Surveiller les applications qui s’exécutent sur Azure Functions avec Application Insights - Azure Monitor](app/monitor-functions.md) - Nouvel article.
- [Surveiller les services Node.js avec Azure Application Insights](app/nodejs.md) - Mises à jour générales, notamment nouvelle section sur la migration à partir de versions antérieures.
- [Adresses IP utilisées par Application Insights et Log Analytics](app/ip-addresses.md) - Ajout d’adresses IP pour les webhooks et US Government.
- [Surveiller des applications sur Azure Kubernetes Service (AKS) avec Application Insights - Azure Monitor](app/kubernetes-codeless.md) - Nouvel article.
- [Résolution des problèmes liés à l’absence de données pour .NET](app/asp-net-troubleshoot-no-data.md) - Ajout de la section sur la collecte de journaux avec dotnet-trace.
- [Utiliser l’analyse des changements d’application dans Azure Monitor pour rechercher les problèmes liés aux applications web](app/change-analysis.md) - Plusieurs mises à jour dans la fonctionnalité Analyse des changements.

#### <a name="new-and-updated-articles-for-preview-of-workspace-based-applications"></a>Articles nouveaux et mis à jour pour la préversion des applications basées sur un espace de travail
- [Schéma de ressource Azure Monitor Application Insights basé sur un espace de travail](app/apm-tables.md)
- [Créer une ressource Azure Monitor Application Insights basée sur un espace de travail](app/create-workspace-resource.md)
- [Expression app() dans les requêtes de journal Azure Monitor](log-query/app-expression.md)
- [Étendue de requête de journal dans la fonctionnalité Log Analytics d’Azure Monitor](log-query/scope.md)
- [Interroger des ressources avec Azure Monitor](log-query/cross-workspace-query.md)
- [Propriétés standard dans les enregistrements de journaux Azure Monitor](platform/log-standard-properties.md)
- [Structure des journaux Azure Monitor](log-query/logs-structure.md)





### <a name="containers"></a>Containers
- [Procédure d’activation d’Azure Monitor pour conteneurs](insights/container-insights-onboard.md) - Mise à jour de la table de configuration du pare-feu.
- [Mise à jour d’Azure Monitor pour conteneurs afin d’activer les métriques](insights/container-insights-update-metrics.md) - Mise à jour relative à l’utilisation d’identités managées pour la collecte des métriques.
- [Coût de supervision pour Azure Monitor pour conteneurs](insights/container-insights-cost.md) - Nouvel article.
- [Configurer Live Data avec Azure Monitor pour conteneurs (préversion)](insights/container-insights-livedata-setup.md) - Prise en charge de la nouvelle liaison de rôle de cluster.

### <a name="insights"></a>Insights
- [Azure Monitor pour Azure Cache pour Redis (préversion)](insights/redis-cache-insights-overview.md) - Nouvel article.
- [Surveiller Key Vault avec Azure Monitor pour Key Vault (préversion)](./insights/key-vault-insights-overview.md) - Nouvel article.

### <a name="logs"></a>Journaux d’activité
- [Créer et configurer Log Analytics avec PowerShell](platform/powershell-workspace-configuration.md) - Ajout de la section Résolution des problèmes.
- [Créer un espace de travail Log Analytics dans le portail Azure](learn/quick-create-workspace.md) - Ajout de la section Résolution des problèmes.
- [Créer un espace de travail Log Analytics à l’aide d’Azure CLI](learn/quick-create-workspace-cli.md) - Ajout de la section Résolution des problèmes.
- [Supprimer et récupérer l’espace de travail Azure Log Analytics](platform/delete-workspace.md) -Mise à jour des informations sur la récupération d’un espace de travail supprimé.
- [Fonctions dans les requêtes de journal Azure Monitor](log-query/functions.md) - Suppression d’une note sur les fonctions qui ne contiennent pas d’autres fonctions.
- [Structure des journaux Azure Monitor](log-query/logs-structure.md) - Clarification des descriptions de propriétés pour la table Application Insights.
- [Utiliser Azure Monitor Logs avec Azure Logic Apps et Power Automate](platform/logicapp-flow-connector.md) - Ajout de la section Limites.
- [Utiliser PowerShell pour créer et configurer un espace de travail Log Analytics](platform/powershell-workspace-configuration.md) - Ajout de la section Résolution des problèmes.


### <a name="metrics"></a>Mesures
- [Métriques prises en charge par Azure Monitor par type de ressource](platform/metrics-supported.md) - Clarification des métriques invitées et du routage de métriques. 

### <a name="solutions"></a>Solutions
- [Optimiser son environnement Active Directory avec Azure Monitor](insights/ad-assessment.md) - Ajout de Windows Server 2019 aux versions prises en charge.
- [Optimiser son environnement SQL Server avec Azure Monitor](insights/sql-assessment.md) – Ajout des versions prises en charge de SQL Server.


### <a name="virtual-machines"></a>Machines virtuelles
- [Vue d’ensemble de l’activation d’Azure Monitor pour machines virtuelles](insights/vminsights-enable-overview.md) - Ajout des versions prises en charge d’Ubuntu Server. Ajout de régions prises en charge pour l’espace de travail Log Analytics.
- [Comment créer des graphiques de performances avec Azure Monitor pour machines virtuelles](insights/vminsights-performance.md) - Ajout de la section Limitations pour les métriques non disponibles.

### <a name="visualizations"></a>Visualisations
- [Classeurs Azure Monitor et modèles Azure Resource Manager](platform/workbooks-automate.md) - Ajout de la mise à jour Resource Manager pour le déploiement d’un modèle de classeur.
- [Groupes dans des classeurs Azure Monitor](platform/workbooks-groups.md) - Nouvel article.
- [Classeurs Azure Monitor - Transformer des données JSON avec JSONPath](platform/workbooks-jsonpath.md) - Nouvel article.


## <a name="april-2020"></a>Avril 2020

### <a name="general"></a>Général

- [Clé gérée par le client dans Azure Monitor](platform/customer-managed-keys.md) - Ajout d’une section sur les opérations asynchrones
- [Gérer les espaces de travail Log Analytics dans Azure Monitor](platform/manage-access.md) – Mises à jour apportées aux sections sur les journaux personnalisés.

### <a name="alerts"></a>Alertes

- [Règles d’action pour les alertes Azure Monitor](platform/alerts-action-rules.md) - Ajout d’une vidéo.
- [Vue d’ensemble des alertes et de la supervision des notifications dans Azure](platform/alerts-overview.md) - Ajout d’une vidéo.

### <a name="application-insights"></a>Application Insights

- [Cartographie d’application dans Azure Application Insights](app/app-map.md) - Ajout de la configuration des noms de rôles de cloud pour l’agent Java.
- [Informations de référence sur l’API de l’agent .NET d’Azure Application Insights](app/status-monitor-v2-api-reference.md) - Regroupement des informations de référence sur l’API.
- [Adresses IP utilisées par Application Insights et Log Analytics](app/ip-addresses.md) - Mise à jour des adresses IP pour les API App Insights et Log Analytics, les webhooks de groupes d’actions, Azure US Government.
- [Superviser les applications Java en tout lieu](app/java-standalone-config.md) - Nouvel article.
- [Superviser les applications Java sur n’importe quel environnement](app/java-in-process-agent.md) - Nouvel article.
- [Superviser les applications Java qui s’exécutent dans n’importe quel environnement](app/java-standalone-arguments.md) - Nouvel article.
- [Superviser les applications Java s’exécutant localement](app/java-on-premises.md) - Nouvel article.
- [Supprimer Application Insights dans Visual Studio](app/remove-application-insights.md) - Nouvel article.
- [Échantillonnage de télémétrie dans Azure Application Insights](app/sampling.md) - Correction de l’échantillonnage à débit fixe en Python.

### <a name="containers"></a>Containers

- [Configurer Azure Red Hat OpenShift v4.x avec Azure Monitor pour conteneurs](insights/container-insights-azure-redhat4-setup.md) - Nouvel article.
- [Guide pratique pour corriger manuellement les problèmes de synchronisation de ServiceNow](platform/itsmc-resync-servicenow.md) - Nouvel article.
- [Guide pratique pour arrêter la supervision de votre cluster Azure et Red Hat OpenShift v4](insights/container-insights-optout-openshift-v4.md) - Nouvel article.
- [Guide pratique pour arrêter la supervision de votre cluster Azure Red Hat OpenShift v3](insights/container-insights-optout-openshift-v3.md) - Nouvel article.
- [Guide pratique pour arrêter la supervision de votre cluster Kubernetes hybride](insights/container-insights-optout-hybrid.md) - Nouvel article.

### <a name="insights"></a>Insights

- [Superviser les coffres de clés Azure avec Azure Monitor pour les coffres de clés (préversion)](insights/key-vault-insights-overview.md) - Nouvel article.

### <a name="logs"></a>Journaux d’activité

- [Limites du service Azure Monitor](service-limits.md) - Ajout de la limitation des requêtes utilisateur.
- [Gérer l’utilisation et les coûts à l’aide des journaux Azure Monitor](platform/manage-cost-storage.md) - Ajout de la facturation pour les clusters de journaux. Ajout d’une requête Kusto pour permettre aux clients ayant un niveau tarifaire hérité Par nœud de déterminer s’ils doivent passer à un niveau de Réservation par capacité ou Par Go.

### <a name="metrics"></a>Mesures

- [Fonctionnalités avancées d’Azure Metrics Explorer](platform/metrics-charts.md) - Ajout de la section sur l’agrégation.

### <a name="workbooks"></a>Workbooks

- [Classeurs Azure Monitor et modèles Azure Resource Manager](platform/workbooks-automate.md) - Ajout du modèle Resource Manager ajouté pour le déploiement d’un modèle de classeur.

## <a name="march-2020"></a>Mars 2020

### <a name="general"></a>Général

- [Vue d’ensemble d’Azure Monitor](overview.md) - Ajout de la vidéo de présentation d’Azure Monitor.
- [Configuration de clés gérées par le client dans Azure Monitor](platform/customer-managed-keys.md) – Mises à jour générales.
- [Référence de données Azure Monitor](/azure/azure-monitor/reference/) - Nouveau site.

### <a name="alerts"></a>Alertes

- [Créer, afficher et gérer des alertes de journal d’activité dans Azure Monitor](platform/alerts-activity-log.md) - Explication supplémentaire du modèle Resource Manager.
- [Comprendre le fonctionnement des alertes de métrique dans Azure Monitor.](platform/alerts-metric-overview.md) Mise à jour pour la prise en charge de Government.
- [Résolution des problèmes liés aux alertes et notifications Azure Monitor](platform/alerts-troubleshoot.md) - Nouvel article.

### <a name="application-insights"></a>Application Insights

- [Automatiser Azure Application Insights avec PowerShell](app/powershell.md) | Ajout d’exemples ARMClient.
- [Exportation continue de télémétrie depuis Application Insights](app/export-telemetry.md) - Ajout d’une table avec les détails de la structure d’exportation.
- [Activer le Débogueur de capture instantanée pour les applications .NET dans Azure App Service](app/snapshot-debugger-appservice.md) - Ajout d’un exemple de modèle Resource Manager.
- [Gérer l’utilisation et les coûts pour Azure Application Insights](app/pricing.md)| Ajout d’informations sur l’alerte du plafond de données.
- [Superviser les applications Python avec Azure Monitor (préversion)](app/opencensus-python.md) - Ajout de métriques standard.
- [Prise en charge du mappage de source pour les applications JavaScript – Azure Monitor Application Insights](app/source-map-support.md) - Nouvel article.

### <a name="containers"></a>Conteneurs

- [Questions fréquentes (FAQ) Azure Monitor](faq.md) - Mise à jour relative à Azure Monitor pour conteneurs.
- [Configurer la supervision de GPU avec Azure Monitor pour conteneurs](insights/container-insights-gpu-monitoring.md) - Nouvel article.

### <a name="insights"></a>Insights

- [Solution de gestion Office 365 dans Azure](insights/solution-office-365.md) - Mise à jour de la date de dépréciation.

### <a name="logs"></a>Journaux d’activité

- [Optimiser les requêtes de journal dans Azure Monitor](log-query/query-optimization.md) - Ajout d’une condition d’UC pour l’analyse XML et JSON.
- [Supprimer et récupérer un espace de travail Azure Log Analytics](platform/delete-workspace.md) – Ajout de la résolution des problèmes.
- [Utiliser les journaux Azure Monitor avec Azure Logic Apps et Power Automate](platform/logicapp-flow-connector.md) - Mise à jour pour le nouveau connecteur Azure Monitor.

### <a name="metrics"></a>Mesures

- [Dépréciation des métriques de disque dans le portail Azure](platform/portal-disk-metrics-deprecation.md) - Nouvel article.
- [Tutoriel - Créer un graphique de métriques dans Azure Monitor](learn/tutorial-metrics-explorer.md) - Ajout d’une vidéo.

### <a name="platform-logs"></a>Journaux de plateforme

- [Collecter et analyser le journal d’activité Azure dans Azure Monitor](./platform/activity-log.md) - Réécriture pour une meilleure explication de la collecte du journal d’activité avec des paramètres de diagnostic.

### <a name="virtual-machines"></a>Machines virtuelles

- [Superviser des machines virtuelles Azure avec Azure Monitor](insights/monitor-vm-azure.md) - Nouvel article.
- [Démarrage rapide : Superviser des machines virtuelles Azure avec Azure Monitor](learn/quick-monitor-azure-vm.md) - Mise à jour permettant d’ajouter Azure Monitor pour machines virtuelles.
- [Alertes Azure Monitor pour machines virtuelles](insights/vminsights-alerts.md) - Nouvel article.
- [Vue d’ensemble Activer Azure Monitor pour machines virtuelles](insights/vminsights-enable-overview.md) - Mise à jour des liens de téléchargement d’agent.

Mises à jour générales relatives à la disponibilité générale d’Azure Monitor pour machines virtuelles

- [Qu’est-ce qu’Azure Monitor pour machines virtuelles ?](insights/vminsights-overview.md)
- [Questions fréquentes sur Azure Monitor pour machines virtuelles (GA)](insights/vminsights-ga-release-faq.md) 
- [Activer Azure Monitor pour machines virtuelles à l’aide d’Azure Policy](insights/vminsights-enable-at-scale-policy.md) 
- [Créer des graphiques de performances avec Azure Monitor pour machines virtuelles](insights/vminsights-performance.md)
- [Interroger les journaux des requêtes à partir d’Azure Monitor pour machines virtuelles](insights/vminsights-log-search.md)
- [Visualiser les dépendances d’applications avec Azure Monitor pour machines virtuelles](insights/vminsights-maps.md) 

### <a name="visualizations"></a>Visualisations

- [Visualisation des données à partir d’Azure Monitor](visualizations.md) - Mise à jour permettant de noter la dépréciation planifiée du concepteur de vues.

## <a name="february-2020"></a>Février 2020

### <a name="agents"></a>Agents

Plusieurs mises à jour effectuées dans le cadre de la réécriture du contenu sur l’extension Diagnostics.

- [Vue d’ensemble des agents de surveillance Azure](platform/agents-overview.md) - Restructuration des tables pour clarifier les fonctionnalités spécifiques à chaque agent.
- [Vue d’ensemble de l’extension Diagnostics Azure](platform/diagnostics-extension-overview.md) - Réécriture complète.
- [Utilisation d’un Stockage Blob pour IIS et d’un Stockage Table pour les événements dans Azure Monitor](platform/diagnostics-extension-logs.md) - Réécriture générale à des fins de mise à jour et de clarification.
- [Installer et configurer l’extension Diagnostics Azure pour Windows (WAD)](platform/diagnostics-extension-windows-install.md) - Nouvel article. 
- [Schéma d’extension de diagnostic Windows](platform/diagnostics-extension-schema-windows.md) - Réorganisation.
- [Envoyer des données provenant de l’extension Diagnostics Azure pour Windows à Azure Event Hubs](platform/diagnostics-extension-stream-event-hubs.md) - Réécriture et mise à jour complètes.
- [Stocker et afficher des données de diagnostic dans le stockage Azure](../cloud-services/diagnostics-extension-to-storage.md) - Réécriture et mise à jour complètes.
- [Extension de machine virtuelle Log Analytics pour Windows](../virtual-machines/extensions/oms-windows.md) - Clarification de la relation avec l’agent Log Analytics.
- [Extension de machine virtuelle Azure Monitor pour Linux](../virtual-machines/extensions/oms-linux.md) - Clarification de la relation avec l’agent Log Analytics.

### <a name="application-insights"></a>Application Insights

- [Chaînes de connexion dans Azure Application Insights](app/sdk-connection-string.md) - Nouvel article.

### <a name="insights-and-solutions"></a>Insights et solutions

#### <a name="azure-monitor-for-containers"></a>Azure Monitor pour conteneurs

- [Intégrer Azure Active Directory dans Azure Kubernetes Service](../aks/azure-ad-integration-cli.md) - Ajout d’une note concernant la création d’une application cliente pour prendre en charge le cluster RBAC afin de prendre en charge Azure Monitor pour les conteneurs.

#### <a name="azure-monitor-for-vms"></a>Azure Monitor pour machines virtuelles

- [Questions fréquentes sur Azure Monitor pour machines virtuelles (version en disponibilité générale)](insights/vminsights-ga-release-faq.md) - Modification concernant le mode de stockage des données de performance.

#### <a name="office-365"></a>Office 365

- [Solution de gestion Office 365 dans Azure](insights/solution-office-365.md) - Mise à jour de la date de dépréciation.


### <a name="logs"></a>Journaux d’activité

- [Optimiser les requêtes de journal dans Azure Monitor](log-query/query-optimization.md) - Nouvel article.
- [Gérer l’utilisation et les coûts pour les journaux Azure Monitor](platform/manage-cost-storage.md) - Amélioration des exemples de requête pour une meilleure compréhension de l’utilisation.

### <a name="metrics"></a>Mesures

- [Métriques de plateforme Azure Monitor exportables par le biais des paramètres de diagnostic](platform/metrics-supported-export-diagnostic-settings.md) - Ajout d’une section portant sur la modification du comportement pour les valeurs Null et zéro.

### <a name="visualizations"></a>Visualisations

Plusieurs nouveaux articles d’aide sur le concepteur de vues, concernant les conversions en classeurs.

- [Guide de transition : du concepteur de vues Azure Monitor aux classeurs](platform/view-designer-conversion-overview.md) - Nouvel article.
- [Concepteur de vues Azure Monitor - Options de conversion en classeurs](platform/view-designer-conversion-options.md) - Nouvel article.
- [Concepteur de vues Azure Monitor pour les conversions de vignettes de classeurs](platform/view-designer-conversion-tiles.md) - Nouvel article.
- [Récapitulatif et accès pour la conversion du Concepteur de vues Azure Monitor en classeurs](platform/view-designer-conversion-access.md) - Nouvel article.
- [Concepteur de vues Azure Monitor - Tâches courantes liées à la conversion de vues en classeurs](platform/view-designer-conversion-tasks.md) - Nouvel article.
- [Concepteur de vues Azure Monitor - Exemples de conversions en classeurs](platform/view-designer-conversion-examples.md) - Nouvel article.

## <a name="january-2020"></a>Janvier 2020

### <a name="general"></a>Général

- [Quels sont les éléments supervisés par Azure Monitor ?](monitor-reference.md) – Nouvel article.

### <a name="agents"></a>Agents

- [Collecter des données de journal avec l’agent Log Analytics](platform/log-analytics-agent.md) – Mise à jour du tableau de la section Configuration requise du pare-feu réseau.

### <a name="alerts"></a>Alertes

- [Créer et gérer des groupes d’actions sur le Portail Azure](platform/action-groups.md) – Suppression d’un paramètre qui n’est plus obligatoire pour les fonctions v2.
- [Créer une alerte de métrique avec un modèle Resource Manager](platform/alerts-metric-create-templates.md) – Ajout d’un exemple pour le paramètre *ignoreDataBefore*.  Ajout de contraintes concernant les règles multicritères.
- [Utilisation de l’API REST d’alerte Log Analytics](platform/api-alerts.md) – Exemple JSON corrigé.

### <a name="application-insights"></a>Application Insights

- [Adresses IP utilisées par Application Insights et Log Analytics](app/ip-addresses.md) – Mise à jour de la section Tests de disponibilité concernant la manière d’ajouter une règle de port d’entrée pour autoriser le trafic en utilisant des groupes de sécurité réseau Azure.
- [Résoudre les problèmes liés à Azure Application Insights Profiler](app/profiler-troubleshooting.md) – Mise à jour générale des solutions de dépannage.
- [Échantillonnage de la télémétrie dans Azure Application Insights](app/sampling.md) – Article mis à jour et restructuré sur la base des commentaires de clients de façon à améliorer la lisibilité.

### <a name="data-security"></a>Sécurité des données

- [Configuration de clés gérées par le client dans Azure Monitor](platform/customer-managed-keys.md) – Nouvel article.

### <a name="insights-and-solutions"></a>Insights et solutions

#### <a name="azure-monitor-for-containers"></a>Azure Monitor pour conteneurs

- [Configurer la collecte de données de l’agent pour Azure Monitor pour les conteneurs](insights/container-insights-agent-config.md) – Ajout de détails concernant la mise à niveau de l’agent dans Azure Red Hat OpenShift et ajout d’informations supplémentaires pour distinguer les méthodes de mise à niveau de l’agent.
- [Créer des alertes pour des problèmes de performances dans Azure Monitor pour les conteneurs](insights/container-insights-alerts.md) – Révision des informations et mise à jour de la procédure de création d’une alerte sur les données de performances stockées dans un espace de travail qui se déclenche en fonction du contexte de l’espace de travail.
- [Supervision Kubernetes avec Azure Monitor pour les conteneurs](insights/container-insights-analyze.md) – Mise à jour de l’article de présentation et de l’article d’analyse concernant la prise en charge des clusters Windows Kubernetes.
- [Configurer des clusters Azure Red Hat OpenShift avec Azure Monitor pour les conteneurs](insights/container-insights-azure-redhat-setup.md) – Ajout de détails concernant la mise à niveau de l’agent dans Azure Red Hat OpenShift et ajout d’informations supplémentaires pour distinguer les méthodes de mise à niveau de l’agent.
- [Configurer des clusters Kubernetes hybrides avec Azure Monitor pour les conteneurs](insights/container-insights-hybrid-setup.md) – Mise à jour pour prendre en compte l’ajout de la prise en charge de secure port:10250 avec cAdvisor de Kubelet.
- [Guide pratique pour la gestion de l’agent Azure Monitor pour les conteneurs](insights/container-insights-manage-agent.md) – Mise à jour des détails concernant le comportement et la configuration de l’extraction avec Azure Red Hat OpenShift par rapport à d’autres types de clusters Kubernetes.
- [Configurer la capture des métriques Prometheus avec Azure Monitor pour les conteneurs](insights/container-insights-prometheus-integration.md) – Mise à jour des détails concernant le comportement et la configuration de l’extraction des métriques avec Azure Red Hat OpenShift par rapport à d’autres types de clusters Kubernetes.
- [Mise à jour d’Azure Monitor pour les conteneurs afin d’activer les métriques](insights/container-insights-update-metrics.md) – Mise à jour des détails concernant le comportement et la configuration de l’extraction des métriques avec Azure Red Hat OpenShift par rapport à d’autres types de clusters Kubernetes.

#### <a name="azure-monitor-for-vms"></a>Azure Monitor pour machines virtuelles

- [Questions fréquentes sur Azure Monitor pour machines virtuelles (version en disponibilité générale)](insights/vminsights-ga-release-faq.md) – Ajout d’informations concernant la mise à niveau de l’espace de travail et des agents vers une nouvelle version.

#### <a name="office-365"></a>Office 365

- [Solution de gestion Office 365 dans Azure (préversion)](insights/solution-office-365.md) – Ajout de détails et des questions fréquentes (FAQ) sur la migration vers la solution Office 365 dans Azure Sentinel. Suppression de la section relative à l’intégration.

### <a name="logs"></a>Journaux d’activité

- [Gérer les espaces de travail Log Analytics dans Azure Monitor](platform/manage-access.md) – Mises à jour apportées aux non-actions.
- [Gérer l’utilisation et les coûts des journaux Azure Monitor](platform/manage-cost-storage.md) – Ajout de précisions concernant le calcul du volume de données dans la section Modèle de tarification.
- [Utiliser des modèles Azure Resource Manager pour créer et configurer un espace de travail Log Analytics](platform/template-workspace-configuration.md) – Modèle mis à jour avec les nouveaux niveaux tarifaires.

### <a name="platform-logs"></a>Journaux de plateforme

- [Collecter le journal d’activité Azure avec des paramètres de diagnostic – Azure Monitor](./platform/activity-log.md) – Informations supplémentaires concernant les propriétés modifiées.
- [Exporter le journal d’activité Azure](./platform/activity-log.md#legacy-collection-methods) – Mis à jour par rapport aux modifications apportées à l’interface utilisateur. 

## <a name="december-2019"></a>Décembre 2019

### <a name="agents"></a>Agents

- [Connecter des ordinateurs Linux à Azure Monitor](platform/agent-linux.md) – Nouvel article.

### <a name="alerts"></a>Alertes

- [Créer une alerte de métrique avec un modèle Resource Manager](platform/alerts-metric-create-templates.md) – Ajout d’un exemple pour le métrique personnalisée.
- [Création d’alertes avec des seuils dynamiques dans Azure Monitor](platform/alerts-dynamic-thresholds.md) – Ajout d’une section relative à l’interprétation des graphiques de seuils dynamiques.
- [Vue d’ensemble des alertes et de la supervision des notifications dans Azure](platform/alerts-overview.md) – Mise à jour concernant la requête Resource Graph.
- [Ressources prises en charge pour les alertes de métrique dans Azure Monitor](platform/alerts-metric-near-real-time.md) – Mise à jour concernant les métriques et les dimensions prises en charge.
- [Passer de l’API Alerte héritée de Log Analytics à la nouvelle API Alertes Azure](platform/alerts-log-api-switch.md) – Ajout d’une remarque concernant la modification du nom de l’alerte.
- [Comprendre le fonctionnement des alertes de métrique dans Azure Monitor.](platform/alerts-metric-overview.md) – Ajout de types de ressources pris en charge pour une supervision à la bonne échelle.

### <a name="application-insights"></a>Application Insights

- [Application Insights pour les applications Service Worker (applications non HTTP)](app/worker-service.md) – Ajout du niveau de journalisation par défaut au code C#. Mise à jour de la version de référence du package.
- [Référence sur ApplicationInsights.config – Azure](app/configuration-with-applicationinsights-config.md) – Mise à jour de l’exemple de code.
- [Automatiser Azure Application Insights avec PowerShell](app/powershell.md) – Mise à jour du modèle Resource Manager.
- [Packages NuGet Application Insights Azure Monitor](app/nuget.md) – Mise à jour des versions de packages.
- [Créer une ressource Azure Application Insights](app/create-new-resource.md) – Ajout d’une remarque concernant le nom global unique.
- [Diagnostiquer avec les flux de métriques temps réel – Azure Application Insights](app/live-stream.md) – Mise à concernant la version exigée du SDK ASP.NET Core .
- [Compteurs d’événements dans Application Insights](app/eventcounters.md) – Catégorie et tableau mis à jour pour customMetrics.
- [Explorer les journaux de suivi Java dans Azure Application Insights](app/java-trace-logs.md) – Ajout de la configuration du seuil de journalisation de l’agent.
- [Adresses IP utilisées par Application Insights et Log Analytics](app/ip-addresses.md) – Mise à jour des adresses IP pour les flux de métriques temps réel.
- [Superviser les performances d’Azure App Service](app/azure-web-apps.md) – Ajout de la prise en charge d’ASP.NET Core 3.0. 
- [Superviser les applications avec Azure Monitor (préversion)](app/opencensus-python.md) – Ajout de précisions concernant le mappage du schéma Python OpenCensus au schéma Azure Monitor
- [Notes de publication d’Azure Application Insights](app/release-notes.md) – Ajout de remarques concernant les anciennes versions.
- [Canaux de télémétrie dans Azure Application Insights](app/telemetry-channels.md) – Mise à jour concernant l’abandon des données à la suite d’une perte de connexion prolongée.
- [Échantillonnage de la télémétrie dans Azure Application Insights](app/sampling.md) – Correction de l’extrait de code pour l’élément TelemetryInitializer personnalisé.
- [Résoudre les problèmes liés à Application Insights dans un projet web Java](app/java-troubleshoot.md) – Suppression de l’information concernant la non prise en charge de la collecte de dépendances dans JDK 9.

### <a name="insights-and-solutions"></a>Insights et solutions

- [Questions fréquentes sur Azure Monitor pour les conteneurs](./faq.md) – Ajout d’une question concernant les champs Image et Name.
- [Solution Azure SQL Analytics dans Azure Monitor](insights/azure-sql.md) – Mise à jour concernant la prise en charge de Attente de la base de données pour les instances Managed Instance.
- [Configurer Azure Monitor pour la collecte de données de l’agent de conteneurs](insights/container-insights-agent-config.md) – Ajout du paramètre pour enrich_container_logs.
- [Configurer des clusters Kubernetes hybrides avec Azure Monitor pour les conteneurs](insights/container-insights-hybrid-setup.md) – Ajout d’une section Résolution des problèmes.
- [Superviser l’état de la réplication Active Directory avec Azure Monitor](insights/ad-replication-status.md) – Mise à jour des prérequis .NET Microsoft.
- [Solution Network Performance Monitor dans Azure](insights/network-performance-monitor.md) – Ajout des régions prises en charge.
- [Optimiser son environnement Active Directory avec Azure Monitor](insights/ad-assessment.md) – Mise à jour des prérequis .NET Framework.
- [Optimiser son environnement SQL Server avec Azure Monitor](insights/sql-assessment.md) – Mise à jour des prérequis .NET Framework.
- [Optimiser son environnement System Center Operations Manager avec Azure Log Analytics](insights/scom-assessment.md) – Mise à jour des prérequis .NET Framework.
- [Connexions prises en charge avec le connecteur de gestion des services informatiques dans Azure Log Analytics](platform/itsmc-connections.md) – Ajout de New York à l’ID client et à la clé secrète client prérequis.

### <a name="logs"></a>Journaux d’activité

- [Supprimer et récupérer un espace de travail Azure Log Analytics](platform/delete-workspace.md) – Ajout de la méthode PowerShell.
- [Conception de votre déploiement de journaux Azure Monitor](platform/design-logs-deployment.md) – Augmentation du débit d’ingestion des données pour un espace de travail.

### <a name="metrics"></a>Mesures

- [Métriques de plateforme Azure Monitor exportables par le biais des paramètres de diagnostic](platform/metrics-supported-export-diagnostic-settings.md) – Nouvel article.

### <a name="platform-logs"></a>Journaux de plateforme

Plusieurs articles ont été mis à jour après la restructuration du contenu relatif aux journaux de plateforme du fait de la nouvelle fonctionnalité de configuration du journal d’activité à l’aide des paramètres de diagnostic.

- [Archiver des journaux de ressources Azure sur un compte de stockage](./platform/resource-logs.md#send-to-azure-storage)
- [Schéma d’événement du journal d’activité Azure](platform/activity-log-schema.md)
- [Limites du service Azure Monitor](service-limits.md)
- [Collecter et analyser les journaux d’activité Azure dans l’espace de travail Log Analytics](./platform/activity-log.md)
- [Collecter le journal d’activité Azure avec les paramètres de diagnostic (préversion) – Azure Monitor](./platform/activity-log.md)
- [Collecter les journaux d’activité Azure dans un espace de travail Log Analytics auprès de locataire Azure](platform/activity-log-collect-tenants.md)
- [Collecter les journaux de ressources Azure dans l’espace de travail Log Analytics](./platform/resource-logs.md#send-to-log-analytics-workspace)
- [Créer un paramètre de diagnostic dans Azure à l’aide d’un modèle Resource Manager](platform/diagnostic-settings-template.md)
- [Créer un paramètre de diagnostic pour collecter les journaux et les métriques dans Azure](platform/diagnostic-settings.md)
- [Exporter le journal d’activité Azure](./platform/activity-log.md#legacy-collection-methods)
- [Vue d’ensemble des journaux de plateforme Azure](platform/platform-logs-overview.md)
- [Envoyer en streaming des données de supervision Azure vers un hub d’événements](platform/stream-monitoring-data-event-hubs.md)
- [Diffuser en continu les journaux de plateforme Azure vers un Event Hub](./platform/resource-logs.md#send-to-azure-event-hubs)

### <a name="quickstarts-and-tutorials"></a>Guides de démarrages rapides et tutoriels

- [Créer un graphique de métriques dans Azure Monitor](learn/tutorial-metrics-explorer.md) – Nouvel article.
- [Collecter des journaux de ressources à partir d’une ressource Azure et les analyser avec Azure Monitor](learn/tutorial-resource-logs.md) – Nouvel article.
- [Superviser une ressource Azure avec Azure Monitor](learn/quick-monitor-azure-resource.md) – Nouvel article.
   
## <a name="next-steps"></a>Étapes suivantes

- Pour contribuer à la documentation Azure Monitor, consultez le [guide du contributeur de documents](/contribute/).
