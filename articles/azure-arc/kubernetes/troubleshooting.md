---
title: Résoudre les problèmes courants liés à Kubernetes avec Azure Arc (préversion)
services: azure-arc
ms.service: azure-arc
ms.date: 05/19/2020
ms.topic: article
author: mlearned
ms.author: mlearned
description: Résolution des problèmes courants liés aux clusters Kubernetes avec Arc.
keywords: Kubernetes, Arc, Azure, containers
ms.openlocfilehash: 1527f8d4ca06c2deaf4ce18b73bfdb515dcadc63
ms.sourcegitcommit: 6fd8dbeee587fd7633571dfea46424f3c7e65169
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83725582"
---
# <a name="azure-arc-enabled-kubernetes-troubleshooting-preview"></a>Résolution des problèmes Kubernetes avec Azure Arc (préversion)

Ce document fournit quelques scénarios de résolution de problèmes courants relatifs à la connectivité, aux autorisations et aux agents.

## <a name="general-troubleshooting"></a>Résolution générale des problèmes

### <a name="azure-cli-set-up"></a>Configuration d’Azure CLI
Avant d’utiliser les commandes CLI az connectedk8s ou az k8sconfiguration, assurez-vous qu’az est configuré pour fonctionner avec l’abonnement Azure approprié.

```console
az account set --subscription 'subscriptionId'
az account show
```

### <a name="azure-arc-agents"></a>Agents azure-arc
Tous les agents pour Kubernetes avec Azure Arc sont déployés en tant que pods dans l’espace de noms `azure-arc`. En temps normal, tous les pods doivent être en cours d’exécution et réussir leurs contrôles d’intégrité.

Tout d’abord, vérifiez la version de Helm pour Azure Arc :

```console
$ helm --namespace default status azure-arc
NAME: azure-arc
LAST DEPLOYED: Fri Apr  3 11:13:10 2020
NAMESPACE: default
STATUS: deployed
REVISION: 5
TEST SUITE: None
```

Si la version de Helm est introuvable ou manquante, réessayez d’intégrer le cluster.

Si la version de Helm est présente et indique `STATUS: deployed`, déterminez l’état des agents en utilisant `kubectl` :

```console
$ kubectl -n azure-arc get deployments,pods
NAME                                        READY   UP-TO-DATE AVAILABLE AGE
deployment.apps/cluster-metadata-operator   1/1     1           1        16h
deployment.apps/clusteridentityoperator     1/1     1           1        16h
deployment.apps/config-agent                1/1     1           1        16h
deployment.apps/controller-manager          1/1     1           1        16h
deployment.apps/flux-logs-agent             1/1     1           1        16h
deployment.apps/metrics-agent               1/1     1           1        16h
deployment.apps/resource-sync-agent         1/1     1           1        16h

NAME                                            READY   STATUS   RESTART AGE
pod/cluster-metadata-operator-7fb54d9986-g785b  2/2     Running  0       16h
pod/clusteridentityoperator-6d6678ffd4-tx8hr    3/3     Running  0       16h
pod/config-agent-544c4669f9-4th92               3/3     Running  0       16h
pod/controller-manager-fddf5c766-ftd96          3/3     Running  0       16h
pod/flux-logs-agent-7c489f57f4-mwqqv            2/2     Running  0       16h
pod/metrics-agent-58b765c8db-n5l7k              2/2     Running  0       16h
pod/resource-sync-agent-5cf85976c7-522p5        3/3     Running  0       16h
```

Tous les pods doivent indiquer la valeur `Running` pour `STATUS` et la valeur `3/3` ou `2/2` pour `READY`. Récupérez les journaux et décrivez les pods qui renvoient `Error` ou `CrashLoopBackOff`.

## <a name="unable-to-connect-my-kubernetes-cluster-to-azure"></a>Impossible de connecter mon cluster Kubernetes à Azure

La connexion de clusters à Azure nécessite l’accès à un abonnement Azure et l’accès de `cluster-admin` à un cluster cible. Si le cluster ne peut pas être atteint ou si les autorisations sont insuffisantes, l’intégration échoue.

### <a name="insufficient-cluster-permissions"></a>Autorisations du cluster insuffisantes

Si le fichier kubeconfig fourni ne dispose pas d’autorisations suffisantes pour installer les agents Azure Arc, la commande Azure CLI retourne une erreur lors de la tentative d’appel de l’API Kubernetes.

```console
$ az connectedk8s connect --resource-group AzureArc --name AzureArcCluster
Command group 'connectedk8s' is in preview. It may be changed/removed in a future release.
Ensure that you have the latest helm version installed before proceeding to avoid unexpected errors.
This operation might take a while...

Error: list: failed to list: secrets is forbidden: User "myuser" cannot list resource "secrets" in API group "" at the cluster scope
```

Le propriétaire du cluster doit utiliser un utilisateur Kubernetes avec des autorisations d’administrateur du cluster.

### <a name="installation-timeouts"></a>Délai d’installation

L’installation de l’agent Azure Arc nécessite l’exécution d’un ensemble de conteneurs sur le cluster cible. Si le cluster s’exécute sur une connexion Internet lente, l’extraction de l’image conteneur peut prendre plus de temps que le délai accordé par Azure CLI.

```console
$ az connectedk8s connect --resource-group AzureArc --name AzureArcCluster
Command group 'connectedk8s' is in preview. It may be changed/removed in a future release.
Ensure that you have the latest helm version installed before proceeding to avoid unexpected errors.
This operation might take a while...

There was a problem with connect-agent deployment. Please run 'kubectl -n azure-arc logs -l app.kubernetes.io/component=connect-agent -c connect-agent' to debug the error.
```

## <a name="configuration-management"></a>Gestion des configurations

### <a name="general"></a>Général
Pour aider à résoudre les problèmes liés à la configuration du contrôle de code source, exécutez les commandes az avec le commutateur --debug.

```console
az provider show -n Microsoft.KubernetesConfiguration --debug
az k8sconfiguration create <parameters> --debug
```

### <a name="create-source-control-configuration"></a>Créer une configuration du contrôle de code source
Le rôle Contributeur sur la ressource Microsoft.Kubernetes/connectedCluster est nécessaire et suffisant pour créer la ressource Microsoft.KubernetesConfiguration/sourceControlConfiguration.

### <a name="configuration-remains-pending"></a>La configuration reste à l’état `Pending`

```console
kubectl -n azure-arc logs -l app.kubernetes.io/component=config-agent -c config-agent
$ k -n pending get gitconfigs.clusterconfig.azure.com  -o yaml
apiVersion: v1
items:
- apiVersion: clusterconfig.azure.com/v1beta1
  kind: GitConfig
  metadata:
    creationTimestamp: "2020-04-13T20:37:25Z"
    generation: 1
    name: pending
    namespace: pending
    resourceVersion: "10088301"
    selfLink: /apis/clusterconfig.azure.com/v1beta1/namespaces/pending/gitconfigs/pending
    uid: d9452407-ff53-4c02-9b5a-51d55e62f704
  spec:
    correlationId: ""
    deleteOperator: false
    enableHelmOperator: false
    giturl: git@github.com:slack/cluster-config.git
    helmOperatorProperties: null
    operatorClientLocation: azurearcfork8s.azurecr.io/arc-preview/fluxctl:0.1.3
    operatorInstanceName: pending
    operatorParams: '"--disable-registry-scanning"'
    operatorScope: cluster
    operatorType: flux
  status:
    configAppliedTime: "2020-04-13T20:38:43.081Z"
    isSyncedWithAzure: true
    lastPolledStatusTime: ""
    message: 'Error: {exit status 1} occurred while doing the operation : {Installing
      the operator} on the config'
    operatorPropertiesHashed: ""
    publicKey: ""
    retryCountPublicKey: 0
    status: Installing the operator
kind: List
metadata:
  resourceVersion: ""
  selfLink: ""
```
