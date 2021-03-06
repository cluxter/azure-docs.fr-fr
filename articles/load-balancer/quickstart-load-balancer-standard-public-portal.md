---
title: 'Démarrage rapide : Créer un équilibreur de charge public - Portail Azure'
titleSuffix: Azure Load Balancer
description: Ce guide de démarrage rapide montre comment créer un équilibreur de charge à l’aide du portail Azure.
services: load-balancer
documentationcenter: na
author: asudbring
manager: KumudD
Customer intent: I want to create a load balancer so that I can load balance internet traffic to VMs.
ms.service: load-balancer
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2020
ms.author: allensu
ms.custom: mvc
ms.openlocfilehash: f9d736098e42bf5ca07eca0cb952275c5e39c2a9
ms.sourcegitcommit: 0e8a4671aa3f5a9a54231fea48bcfb432a1e528c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2020
ms.locfileid: "87125188"
---
# <a name="quickstart-create-a-load-balancer-to-load-balance-vms-using-the-azure-portal"></a>Démarrage rapide : Créer un équilibreur de charge pour équilibrer la charge des machines virtuelles à l’aide du portail Azure

Découvrez comment bien démarrer avec Azure Load Balancer en utilisant le portail Azure pour créer un équilibreur de charge public et trois machines virtuelles.

## <a name="prerequisites"></a>Prérequis

- Compte Azure avec un abonnement actif. [Créez un compte gratuitement](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="sign-in-to-azure"></a>Connexion à Azure

Connectez-vous au portail Azure sur [https://portal.azure.com](https://portal.azure.com).

---

# <a name="option-1-default-create-a-load-balancer-standard-sku"></a>[Option 1 (par défaut) : Créer un équilibreur de charge (référence SKU Standard)](#tab/option-1-create-load-balancer-standard)

>[!NOTE]
>Il est recommandé de disposer d’un équilibreur de charge de référence SKU Standard pour les charges de travail de production.  Pour plus d’informations sur les références SKU, consultez **[Références SKU Azure Load Balancer](skus.md)** .

Dans cette section, vous créez un équilibreur de charge qui équilibre la charge des machines virtuelles. 

Vous pouvez créer un équilibreur de charge public ou un équilibreur de charge interne. 

Quand vous créez un équilibreur de charge public, vous créez une adresse IP publique configurée en tant que front-end (nommée **LoadBalancerFrontend** par défaut) pour l’équilibreur de charge.

1. Dans l’angle supérieur gauche de l’écran, cliquez sur **Créer une ressource** > **Mise en réseau** > **Load Balancer**.

2. Dans l’onglet **Fonctions de base** de la page **Créer un équilibreur de charge**, entrez ou sélectionnez les informations suivantes : 

    | Paramètre                 | Valeur                                              |
    | ---                     | ---                                                |
    | Abonnement               | Sélectionnez votre abonnement.    |    
    | Resource group         | Sélectionnez **Créer**, puis entrez **myResourceGroupLB** dans la zone de texte.|
    | Nom                   | Entrez **myLoadBalancer**                                   |
    | Région         | Sélectionnez **Europe Ouest**.                                        |
    | Type          | Sélectionnez **Public**.                                        |
    | SKU           | sélectionnez **Standard**. |
    | Adresse IP publique | Sélectionnez **Créer nouveau**. Si vous avez une adresse IP publique existante que vous souhaitez utiliser, sélectionnez **Utiliser l’existant**. |
    | Nom de l’adresse IP publique | Tapez **myPublicIP** dans la zone de texte.|
    | Zone de disponibilité | Sélectionnez **Redondant interzone** pour créer un équilibreur de charge résilient. Pour créer un équilibreur de charge zonal, sélectionnez une zone spécifique parmi 1, 2 ou 3 |
    | Ajouter une adresse IPv6 publique | Sélectionnez **Non**. </br> Pour plus d’informations sur les adresses IPv6 et l’équilibreur de charge, consultez [Qu’est-ce que le protocole IPv6 pour réseau virtuel Azure ?](https://docs.microsoft.com/azure/virtual-network/ipv6-overview)  |

3. Acceptez les valeurs par défaut pour les paramètres restants, puis sélectionnez **Vérifier + créer**.

4. Sous l’onglet **Review + create (Vérifier + créer)** , sélectionnez **Créer**.   
    
    :::image type="content" source="./media/quickstart-load-balancer-standard-public-portal/create-standard-load-balancer.png" alt-text="Créer un équilibreur de charge standard" border="true":::
 
## <a name="create-load-balancer-resources"></a>Créer les ressources d’équilibreur de charge

Dans cette section, vous configurez :

* Les paramètres d’équilibreur de charge d’un pool d’adresses de back-ends
* Une sonde d’intégrité
* Une règle d’équilibreur de charge et une règle de trafic sortant automatique

### <a name="create-a-backend-pool"></a>Créer un pool principal

Un pool d’adresses de back-ends contient les adresses IP des cartes d’interface réseau virtuelles connectées à l’équilibreur de charge. 

Créez le pool d’adresses principal **myBackendPool** afin d’inclure des machines virtuelles pour l’équilibrage de charge du trafic Internet.

1. Sélectionnez **Tous les services** dans le menu de gauche, **Toutes les ressources**, puis **myLoadBalancer** dans la liste des ressources.

2. Sous **Paramètres**, sélectionnez **Pools principaux**, puis **Ajouter**.

3. Dans la page **Ajouter un pool de backends**, entrez **myBackendPool** comme nom de votre pool principal, puis sélectionnez **Ajouter**.

### <a name="create-a-health-probe"></a>Créer une sonde d’intégrité

L’équilibreur de charge supervise l’état de votre application avec une sonde d’intégrité. 

La sonde d’intégrité ajoute ou supprime des machines virtuelles dans l’équilibreur de charge en fonction de leur réponse aux contrôles d’intégrité. 

Créez une sonde d’intégrité nommée **myHealthProbe** pour surveiller l’intégrité des machines virtuelles.

1. Sélectionnez **Tous les services** dans le menu de gauche, **Toutes les ressources**, puis **myLoadBalancer** dans la liste des ressources.

2. Sous **Paramètres**, sélectionnez **Sondes d’intégrité**, puis **Ajouter**.
    
    | Paramètre | Valeur |
    | ------- | ----- |
    | Nom | Entrez **MyHealthProbe**. |
    | Protocol | Sélectionnez **HTTP**. |
    | Port | Entrez **80**.|
    | Intervalle | Entrez **15** pour **l’intervalle** en secondes entre les tentatives de la sonde. |
    | Seuil de défaillance sur le plan de l’intégrité | Sélectionnez **2** pour le **Seuil de défaillance sur le plan de l’intégrité**, soit le nombre d’échecs de sonde consécutifs qui peuvent se produire avant qu’une machine virtuelle soit considérée comme non saine.|
    | | |

3. Laissez les autres valeurs par défaut et sélectionnez **OK**.

### <a name="create-a-load-balancer-rule"></a>Créer une règle d’équilibreur de charge

Une règle d’équilibrage de charge est utilisée pour définir la distribution du trafic vers les machines virtuelles. Vous définissez la configuration IP front-end pour le trafic entrant et le pool d’adresses IP de back-ends pour la réception du trafic. Les ports source et de destination sont définis dans la règle. 

Dans cette section, vous allez créer une règle d’équilibreur de charge :

* A pour nom **myHTTPRule**.
* Se trouve dans le front-end nommé **LoadBalancerFrontEnd**.
* Écoute sur le **Port 80**.
* Dirige le trafic à charge équilibrée vers le back-end nommé **myBackendPool** sur le **Port 80**.

1. Sélectionnez **Tous les services** dans le menu de gauche, **Toutes les ressources**, puis **myLoadBalancer** dans la liste des ressources.

2. Sous **Paramètres**, sélectionnez **Règles d’équilibrage de charge**, puis **Ajouter**.

3. Pour configurer la règle d’équilibrage de charge, utilisez les valeurs suivantes :
    
    | Paramètre | Valeur |
    | ------- | ----- |
    | Nom | Entrez **MyHTTPRule**. |
    | Version de l’adresse IP | Sélectionnez **IPv4** |
    | Adresse IP du serveur frontal | Sélectionnez **LoadBalancerFrontEnd** |
    | Protocol | Sélectionnez **TCP**. |
    | Port | Entrez **80**.|
    | Port principal | Entrez **80**. |
    | Pool principal | Sélectionnez **MyBackendPool**.|
    | Sonde d’intégrité | Sélectionnez **myHealthProbe**. |
    | Créer des règles de trafic sortant implicites | Sélectionnez **Non**.

4. Laissez les autres valeurs par défaut, puis sélectionnez **OK**.

## <a name="create-backend-servers"></a>Créer des serveurs principaux

Dans cette section, vous allez :

* Créez un réseau virtuel.
* Créez trois machines virtuelles pour le pool de back-ends de l’équilibreur de charge.
* Installez IIS sur les machines virtuelles pour tester l’équilibreur de charge.

## <a name="virtual-network-and-parameters"></a>Réseau virtuel et paramètres

Dans cette section, vous allez remplacer les paramètres des étapes par les informations ci-dessous :

| Paramètre                   | Valeur                |
|-----------------------------|----------------------|
| **\<resource-group-name>**  | myResourceGroupLB |
| **\<virtual-network-name>** | myVNet          |
| **\<region-name>**          | Europe Ouest      |
| **\<IPv4-address-space>**   | 10.1.0.0\16          |
| **\<subnet-name>**          | myBackendSubnet        |
| **\<subnet-address-range>** | 10.1.0.0\24          |

[!INCLUDE [virtual-networks-create-new](../../includes/virtual-networks-create-new.md)]

### <a name="create-virtual-machines"></a>Créer des machines virtuelles

Les références SKU d’adresse IP publique et d’équilibreur de charge doivent correspondre. Pour un équilibreur de charge standard, utilisez des machines virtuelles auxquelles sont associées des adresses IP standard dans le pool de back-ends. 

Dans cette section, vous allez créer trois machines virtuelles (**myVM1**, **myVM2** et **myVM3**) avec une adresse IP publique standard dans trois zones différentes (**Zone 1**, **Zone 2** et **Zone 3**). 

Ces machines virtuelles sont ajoutées au pool de back-ends de l’équilibreur de charge créé auparavant.

1. En haut à gauche du portail, sélectionnez **Créer une ressource** > **Calcul** > **Machine virtuelle**. 
   
2. Dans **Créer une machine virtuelle**, tapez ou sélectionnez les valeurs sous l’onglet **De base** :

    | Paramètre | Value                                          |
    |-----------------------|----------------------------------|
    | **Détails du projet** |  |
    | Abonnement | Sélectionner votre abonnement Azure |
    | Groupe de ressources | Sélectionnez **myResourceGroupLB** |
    | **Détails de l’instance** |  |
    | Nom de la machine virtuelle | Entrez **myVM1** |
    | Région | Sélectionnez **Europe Ouest** |
    | Options de disponibilité | Sélectionnez **Zones de disponibilité** |
    | Zone de disponibilité | Sélectionnez **1** |
    | Image | Sélectionnez **Windows Server 2019 Datacenter** |
    | Instance Azure Spot | Sélectionnez **Non** |
    | Taille | Choisissez la taille de la machine virtuelle ou acceptez le paramètre par défaut |
    | **Compte administrateur** |  |
    | Nom d’utilisateur | Entrez un nom d’utilisateur |
    | Mot de passe | Entrez un mot de passe |
    | Confirmer le mot de passe | Entrez à nouveau le mot de passe |

3. Sélectionnez l'onglet **Mise en réseau** ou choisissez **Suivant : Disques**, puis **Suivant : Mise en réseau**.
  
4. Sous l’onglet Réseau, sélectionnez ou entrez :

    | Paramètre | Value |
    |-|-|
    | **Interface réseau** |  |
    | Réseau virtuel | **myVNet** |
    | Subnet | **myBackendSubnet** |
    | Adresse IP publique | Acceptez la valeur par défaut **myVM-ip**. </br> L’adresse IP est automatiquement une adresse IP de référence SKU Standard dans la Zone 1. |
    | Groupe de sécurité réseau de la carte réseau | Sélectionnez **Avancé**|
    | Configurer un groupe de sécurité réseau | Sélectionnez **Créer nouveau**. </br> Dans **Créer un groupe de sécurité réseau**, entrez **myNSG** dans **Nom**. </br> Sous **Règles de trafic entrant**, sélectionnez **+Ajouter une règle de trafic entrant**. </br> Sous **Plages de ports de destination**, entrez **80**. </br> Sous **Priorité**, entrez **100**. </br> Dans **Nom**, entrez **myHTTPRule** </br> Sélectionnez **Ajouter** </br> Sélectionnez **OK**. |
    | **Équilibrage de charge**  |
    | Placer cette machine virtuelle derrière une solution d’équilibrage de charge existante ? | Sélectionnez **Oui**. |
    | **Paramètres d’équilibrage de charge** |
    | Options d’équilibrage de charge | Sélectionnez **Équilibrage de charge Azure** |
    | Sélectionnez un équilibreur de charge | Sélectionnez **myLoadBalancer**  |
    | Sélectionnez un pool principal | Sélectionnez **myBackendPool** |

5. Sélectionnez l’onglet **Gestion** ou sélectionnez **Suivant** > **Gestion**.

6. Sous l’onglet **Gestion**, sélectionnez ou entrez :
    
    | Paramètre | Value |
    |-|-|
    | **Surveillance** |  |
    | Diagnostics de démarrage | Sélectionnez **Désactivé** |
   
7. Sélectionnez **Revoir + créer**. 
  
8. Passez en revue les paramètres, puis sélectionnez **Créer**.

9. Suivez les étapes 1 à 8 pour créer deux machines virtuelles supplémentaires avec les valeurs suivantes et tous les autres paramètres identiques à ceux de **myVM1** :

    | Paramètre | Machine virtuelle 2| Machine virtuelle 3|
    | ------- | ----- |---|
    | Nom |  **myVM2** |**myVM3**|
    | Zone de disponibilité | **2** |**3**|
    | Groupe de sécurité réseau | Sélectionnez le groupe **myNSG** existant| Sélectionnez le groupe **myNSG** existant|

## <a name="create-outbound-rule-configuration"></a>Créer une configuration de règle de trafic sortant
Les règles de trafic sortant de l’équilibreur de charge configurent la SNAT sortante pour les machines virtuelles dans le pool principal. 

Pour plus d’informations sur les connexions sortantes, consultez [Connexions sortantes dans Azure](load-balancer-outbound-connections.md).

### <a name="create-outbound-rule"></a>Créer une règle de trafic sortant

1. Sélectionnez **Tous les services** dans le menu de gauche, **Toutes les ressources**, puis **myLoadBalancer** dans la liste des ressources.

2. Sous **Paramètres**, sélectionnez **Règles de trafic sortant**, puis **Ajouter**.

3. Pour configurer les règles de trafic sortant, utilisez les valeurs suivantes :

    | Paramètre | Value |
    | ------- | ----- |
    | Name (Name) | Entrez **myOutboundRule**. |
    | Adresse IP du serveur frontal | Sélectionnez **Créer nouveau**. </br> Dans **Nom**, entrez **LoadBalancerFrontEndOutbound**. </br> Sélectionnez **Adresse IP** ou **Préfixe d’adresse IP**. </br> Sélectionnez **Créer** sous **Adresse IP publique** ou **Préfixe d’adresse IP publique**. </br> Pour Nom, entrez **myPublicIPOutbound** ou **myPublicIPPrefixOutbound**. </br> Sélectionnez **OK**. </br> Sélectionnez **Ajouter**.|
    | Délai d’inactivité (minutes) | Déplacez le curseur sur **15 minutes**.|
    | Réinitialisation du protocole TCP | Sélectionnez **Enabled**.|
    | Pool principal | Sélectionnez **Créer nouveau**. </br> Entrez **myBackendPoolOutbound** dans **Name**. </br> Sélectionnez **Ajouter**. |
    | Allocation de port -> Allocation de port | Sélectionnez **Choisir manuellement le nombre de ports de sortie** |
    | Ports de sortie -> Choisir par | Sélectionnez **Ports par instance** |
    | Ports de sortie -> Ports par instance | Entrez **10000**. |

4. Sélectionnez **Ajouter**.

### <a name="add-virtual-machines-to-outbound-pool"></a>Ajouter des machines virtuelles au pool sortant

1. Sélectionnez **Tous les services** dans le menu de gauche, **Toutes les ressources**, puis **myLoadBalancer** dans la liste des ressources.

2. Sous **Paramètres**, sélectionnez **Backend Pools (Pools principaux)** .

3. Sélectionnez **myBackendPoolOutbound**.

4. Dans **Réseau virtuel**, sélectionnez **myVNet**.

5. Dans **Machines virtuelles**, sélectionnez **+ Ajouter**.

6. Cochez les cases en regard de **myVM1**, **myVM2** et **myVM3**. 

7. Sélectionnez **Ajouter**.

8. Sélectionnez **Enregistrer**.

# <a name="option-2-create-a-load-balancer-basic-sku"></a>[Option n°2 : Créer un équilibreur de charge (référence SKU De base)](#tab/option-1-create-load-balancer-basic)

>[!NOTE]
>Il est recommandé de disposer d’un équilibreur de charge de référence SKU Standard pour les charges de travail de production.  Pour plus d’informations sur les références SKU, consultez **[Références SKU Azure Load Balancer](skus.md)** .

Dans cette section, vous créez un équilibreur de charge qui équilibre la charge des machines virtuelles. 

Vous pouvez créer un équilibreur de charge public ou un équilibreur de charge interne. 

Quand vous créez un équilibreur de charge public, vous créez une adresse IP publique configurée en tant que front-end (nommée **LoadBalancerFrontend** par défaut) pour l’équilibreur de charge.

1. Dans l’angle supérieur gauche de l’écran, cliquez sur **Créer une ressource** > **Mise en réseau** > **Load Balancer**.

2. Dans l’onglet **Fonctions de base** de la page **Créer un équilibreur de charge**, entrez ou sélectionnez les informations suivantes : 

    | Paramètre                 | Value                                              |
    | ---                     | ---                                                |
    | Abonnement               | Sélectionnez votre abonnement.    |    
    | Resource group         | Sélectionnez **Créer**, puis tapez **myResourceGroupLB** dans la zone de texte.|
    | Nom                   | Entrez **myLoadBalancer**                                   |
    | Région         | Sélectionnez **Europe Ouest**.                                        |
    | Type          | Sélectionnez **Public**.                                        |
    | SKU           | Sélectionnez **De base** |
    | Adresse IP publique | Sélectionnez **Créer nouveau**. Si vous avez une adresse IP publique existante que vous souhaitez utiliser, sélectionnez **Utiliser l’existant**. |
    | Nom de l’adresse IP publique | Tapez **myPublicIP** dans la zone de texte.|
    | Affectation | Sélectionnez **Dynamique** |
    | Ajouter une adresse IPv6 publique | Sélectionnez **Non**. </br> Pour plus d’informations sur les adresses IPv6 et l’équilibreur de charge, consultez [Qu’est-ce que le protocole IPv6 pour réseau virtuel Azure ?](https://docs.microsoft.com/azure/virtual-network/ipv6-overview)  |

3. Acceptez les valeurs par défaut pour les paramètres restants, puis sélectionnez **Vérifier + créer**.

4. Sous l’onglet **Review + create (Vérifier + créer)** , sélectionnez **Créer**.   

    :::image type="content" source="./media/quickstart-load-balancer-standard-public-portal/create-basic-load-balancer.png" alt-text="Créer un équilibreur de charge de base" border="true":::

## <a name="create-load-balancer-resources"></a>Créer les ressources d’équilibreur de charge

Dans cette section, vous configurez :

* Créez un réseau virtuel.
* Les paramètres d’équilibreur de charge d’un pool d’adresses de back-ends
* Une sonde d’intégrité
* Une règle d’équilibreur de charge

## <a name="virtual-network-and-parameters"></a>Réseau virtuel et paramètres

Dans cette section, vous allez remplacer les paramètres des étapes par les informations ci-dessous :

| Paramètre                   | Valeur                |
|-----------------------------|----------------------|
| **\<resource-group-name>**  | myResourceGroupLB |
| **\<virtual-network-name>** | myVNet          |
| **\<region-name>**          | Europe Ouest      |
| **\<IPv4-address-space>**   | 10.1.0.0\16          |
| **\<subnet-name>**          | myBackendSubnet        |
| **\<subnet-address-range>** | 10.1.0.0\24          |

[!INCLUDE [virtual-networks-create-new](../../includes/virtual-networks-create-new.md)]

### <a name="create-a-backend-pool"></a>Créer un pool principal

Un pool d’adresses de back-ends contient les adresses IP des cartes d’interface réseau virtuelles connectées à l’équilibreur de charge. 

Créez le pool d’adresses principal **myBackendPool** afin d’inclure des machines virtuelles pour l’équilibrage de charge du trafic Internet.

1. Sélectionnez **Tous les services** dans le menu de gauche, **Toutes les ressources**, puis **myLoadBalancer** dans la liste des ressources.

2. Sous **Paramètres**, sélectionnez **Pools principaux**, puis **Ajouter**.

3. Dans la page **Ajouter un pool de back-ends**, entrez ou sélectionnez :
    
    | Paramètre | Valeur |
    | ------- | ----- |
    | Nom | Entrez **myBackendPool**. |
    | Réseau virtuel | Sélectionnez **myVNet**. |
    | Associé à | Sélectionnez **Machines virtuelles** |

### <a name="create-a-health-probe"></a>Créer une sonde d’intégrité

L’équilibreur de charge supervise l’état de votre application avec une sonde d’intégrité. 

La sonde d’intégrité ajoute ou supprime des machines virtuelles dans l’équilibreur de charge en fonction de leur réponse aux contrôles d’intégrité. 

Créez une sonde d’intégrité nommée **myHealthProbe** pour surveiller l’intégrité des machines virtuelles.

1. Sélectionnez **Tous les services** dans le menu de gauche, **Toutes les ressources**, puis **myLoadBalancer** dans la liste des ressources.

2. Sous **Paramètres**, sélectionnez **Sondes d’intégrité**, puis **Ajouter**.
    
    | Paramètre | Valeur |
    | ------- | ----- |
    | Name (Name) | Entrez **MyHealthProbe**. |
    | Protocol | Sélectionnez **HTTP**. |
    | Port | Entrez **80**.|
    | Path | Entrez **/** |
    | Intervalle | Entrez **15** pour **l’intervalle** en secondes entre les tentatives de la sonde. |
    | Seuil de défaillance sur le plan de l’intégrité | Sélectionnez **2** pour le **Seuil de défaillance sur le plan de l’intégrité**, soit le nombre d’échecs de sonde consécutifs qui peuvent se produire avant qu’une machine virtuelle soit considérée comme non saine.|

3. Sélectionnez **OK**.

### <a name="create-a-load-balancer-rule"></a>Créer une règle d’équilibreur de charge

Une règle d’équilibrage de charge est utilisée pour définir la distribution du trafic vers les machines virtuelles. Vous définissez la configuration IP front-end pour le trafic entrant et le pool d’adresses IP de back-ends pour la réception du trafic. Les ports source et de destination sont définis dans la règle. 

Dans cette section, vous allez créer une règle d’équilibreur de charge :

* A pour nom **myHTTPRule**.
* Se trouve dans le front-end nommé **LoadBalancerFrontEnd**.
* Écoute sur le **Port 80**.
* Dirige le trafic à charge équilibrée vers le back-end nommé **myBackendPool** sur le **Port 80**.

1. Sélectionnez **Tous les services** dans le menu de gauche, **Toutes les ressources**, puis **myLoadBalancer** dans la liste des ressources.

2. Sous **Paramètres**, sélectionnez **Règles d’équilibrage de charge**, puis **Ajouter**.

3. Pour configurer la règle d’équilibrage de charge, utilisez les valeurs suivantes :
    
    | Paramètre | Valeur |
    | ------- | ----- |
    | Nom | Entrez **MyHTTPRule**. |
    | Version de l’adresse IP | Sélectionnez **IPv4** |
    | Adresse IP du serveur frontal | Sélectionnez **LoadBalancerFrontEnd** |
    | Protocol | Sélectionnez **TCP**. |
    | Port | Entrez **80**.|
    | Port principal | Entrez **80**. |
    | Pool principal | Sélectionnez **MyBackendPool**.|
    | Sonde d’intégrité | Sélectionnez **myHealthProbe**. |
 
4. Laissez les autres valeurs par défaut, puis sélectionnez **OK**.

## <a name="create-backend-servers"></a>Créer des serveurs principaux

Dans cette section, vous allez :

* Créez trois machines virtuelles pour le pool de back-ends de l’équilibreur de charge.
* Créez un groupe à haute disponibilité pour les machines virtuelles.
* Installez IIS sur les machines virtuelles pour tester l’équilibreur de charge.

### <a name="create-virtual-machines"></a>Créer des machines virtuelles

Les références SKU d’adresse IP publique et d’équilibreur de charge doivent correspondre. Pour un équilibreur de charge de base, utilisez des machines virtuelles auxquelles sont associées des adresses IP de base dans le pool de back-ends. 

Dans cette section, vous allez créer trois machines virtuelles (**myVM1**, **myVM2** et **myVM3**) avec une adresse IP publique de base.  

Les trois machines virtuelles vont être ajoutées à un groupe à haute disponibilité nommé **myAvailabilitySet**.

Ces machines virtuelles sont ajoutées au pool de back-ends de l’équilibreur de charge créé auparavant.

1. En haut à gauche du portail, sélectionnez **Créer une ressource** > **Calcul** > **Machine virtuelle**. 
   
2. Dans **Créer une machine virtuelle**, tapez ou sélectionnez les valeurs sous l’onglet **De base** :

    | Paramètre | Valeur                                          |
    |-----------------------|----------------------------------|
    | **Détails du projet** |  |
    | Abonnement | Sélectionner votre abonnement Azure |
    | Groupe de ressources | Sélectionnez **myResourceGroupLB** |
    | **Détails de l’instance** |  |
    | Nom de la machine virtuelle | Entrez **myVM1** |
    | Région | Sélectionnez **Europe Ouest** |
    | Options de disponibilité | Sélectionnez **Groupe à haute disponibilité** |
    | Groupe à haute disponibilité | Sélectionnez **Créer nouveau**. </br> Entrez **myAvailabilitySet** dans **Nom**. </br> Sélectionnez **OK**. |
    | Image | **Windows Server 2019 Datacenter** |
    | Instance Azure Spot | Sélectionnez **Non** |
    | Taille | Choisissez la taille de la machine virtuelle ou acceptez le paramètre par défaut |
    | **Compte administrateur** |  |
    | Nom d’utilisateur | Entrez un nom d’utilisateur |
    | Mot de passe | Entrez un mot de passe |
    | Confirmer le mot de passe | Entrez à nouveau le mot de passe |

3. Sélectionnez l'onglet **Mise en réseau** ou choisissez **Suivant : Disques**, puis **Suivant : Mise en réseau**.
  
4. Sous l’onglet Réseau, sélectionnez ou entrez :

    | Paramètre | Valeur |
    |-|-|
    | **Interface réseau** |  |
    | Réseau virtuel | Sélectionnez **myVNet** |
    | Subnet | Sélectionnez **myBackendSubnet** |
    | Adresse IP publique | Sélectionnez **Créer** </br> Entrez le nom **myVM-ip**. </br> Sélectionnez **OK**. |
    | Groupe de sécurité réseau de la carte réseau | Sélectionnez **Avancé**|
    | Configurer un groupe de sécurité réseau | Sélectionnez **Créer nouveau**. </br> Dans **Créer un groupe de sécurité réseau**, entrez **myNSG** dans **Nom**. </br> Sous **Règles de trafic entrant**, sélectionnez **+Ajouter une règle de trafic entrant**. </br> Sous **Plages de ports de destination**, entrez **80**. </br> Sous **Priorité**, entrez **100**. </br> Dans **Nom**, entrez **myHTTPRule** </br> Sélectionnez **Ajouter** </br> Sélectionnez **OK**. |
    | **Équilibrage de charge**  |
    | Placer cette machine virtuelle derrière une solution d’équilibrage de charge existante ? | Sélectionnez **Non** |
 
5. Sélectionnez l’onglet **Gestion** ou sélectionnez **Suivant** > **Gestion**.

6. Sous l’onglet **Gestion**, sélectionnez ou entrez :
    | Paramètre | Valeur |
    |-|-|
    | **Surveillance** | |
    | Diagnostics de démarrage | Sélectionnez **Désactivé** |

7. Sélectionnez **Revoir + créer**. 
  
8. Passez en revue les paramètres, puis sélectionnez **Créer**.

9. Suivez les étapes 1 à 8 pour créer deux machines virtuelles supplémentaires avec les valeurs suivantes et tous les autres paramètres identiques à ceux de **myVM1** :

    | Paramètre | Machine virtuelle 2| Machine virtuelle 3|
    | ------- | ----- |---|
    | Nom |  **myVM2** |**myVM3**|
    | Groupe à haute disponibilité| Sélectionnez **myAvailabilitySet** | Sélectionnez **myAvailabilitySet**|
    | Groupe de sécurité réseau | Sélectionnez le groupe **myNSG** existant| Sélectionnez le groupe **myNSG** existant|

---

## <a name="install-iis"></a>Installer IIS

1. Sélectionnez **Tous les services** dans le menu de gauche, sélectionnez **Toutes les ressources**, puis dans la liste de ressources, sélectionnez **myVM1** qui se trouve dans le groupe de ressources **myResourceGroupLB**.

2. Dans la page **Vue d’ensemble**, sélectionnez **Se connecter** pour télécharger le fichier RDP de la machine virtuelle.

3. Ouvrez le fichier RDP.

4. Connectez-vous à la machine virtuelle avec les informations d’identification fournies lors de sa création.

5. Sur le bureau du serveur, accédez à **Outils d’administration Windows**>**Windows PowerShell**.

6. Dans la fenêtre PowerShell, exécutez les commandes suivantes pour :

    * Installer le serveur IIS
    * Supprimer le fichier iisstart.htm par défaut
    * Ajoutez un nouveau fichier iisstart.htm qui affiche le nom de la machine virtuelle :

   ```powershell
    
    # install IIS server role
    Install-WindowsFeature -name Web-Server -IncludeManagementTools
    
    # remove default htm file
     remove-item  C:\inetpub\wwwroot\iisstart.htm
    
    # Add a new htm file that displays server name
     Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)
   ```
7. Fermez la session RDP avec **myVM1**.

8. Répétez les étapes 1 à 6 pour installer IIS et le fichier iisstart.htm mis à jour sur **myVM2** et **myVM3**.

## <a name="test-the-load-balancer"></a>Tester l’équilibreur de charge

1. Recherchez l’adresse IP publique de l’équilibreur de charge sur l’écran **Vue d’ensemble**. Sélectionnez **Tous les services** dans le menu de gauche, sélectionnez **Toutes les ressources**, puis sélectionnez **myPublicIP**.

2. Copiez l’adresse IP publique, puis collez-la dans la barre d’adresses de votre navigateur. La page par défaut du serveur Web IIS s’affiche sur le navigateur.

   ![Serveur Web IIS](./media/tutorial-load-balancer-standard-zonal-portal/load-balancer-test.png)

Pour voir l’équilibreur de charge répartir le trafic entre les trois machines virtuelles, vous pouvez personnaliser la page par défaut du serveur web IIS de chaque machine virtuelle, puis forcer votre navigateur à s’actualiser à partir de la machine cliente.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Quand vous n’en avez plus besoin, supprimez le groupe de ressources, l’équilibreur de charge et toutes les ressources associées. Pour ce faire, sélectionnez le groupe de ressources **myResourceGroupLB** qui contient les ressources, puis sélectionnez **Supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous :

* Avez créé un équilibreur de charge Azure Standard ou De base
* Avez attaché 3 machines virtuelles à l’équilibreur de charge
* Avez configuré la règle de trafic de l’équilibreur de charge, configuré la sonde d’intégrité, puis testé l’équilibreur de charge 

Pour en savoir plus sur Azure Load Balancer, consultez [Qu’est-ce qu’Azure Load Balancer ?](load-balancer-overview.md) et [Questions fréquentes sur Load Balancer](load-balancer-faqs.md).

Découvrez-en plus sur les [équilibreurs de charge et les zones de disponibilité](load-balancer-standard-availability-zones.md).
