---
title: 'Évaluer les machines virtuelles VMware avec Azure Migrate : Évaluation du serveur'
description: Décrit comment évaluer des machines virtuelles VMware locales pour la migration vers Azure avec Azure Migrate Server Assessment.
ms.topic: tutorial
ms.date: 06/03/2020
ms.custom: mvc
ms.openlocfilehash: dd00f800003724b3a5c15d265a5428272e1762fb
ms.sourcegitcommit: dccb85aed33d9251048024faf7ef23c94d695145
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87290212"
---
# <a name="assess-vmware-vms-with-server-assessment"></a>Évaluer les machines virtuelles VMware avec Server Assessment

Cet article vous explique comment évaluer des machines virtuelles VMware locales à l’aide de l’outil [Azure Migrate Server Assessment](migrate-services-overview.md#azure-migrate-server-assessment-tool).


Ce tutoriel est le deuxième d’une série qui explique comment évaluer et migrer des machines virtuelles VMware vers Azure. Dans ce tutoriel, vous allez apprendre à :
> [!div class="checklist"]
> * Configurer un projet Azure Migrate.
> * Configurer une appliance Azure Migrate qui s’exécute localement pour évaluer les machines virtuelles.
> * Démarrer la découverte continue des machines virtuelles locales. L’appliance envoie les données de configuration et de performances des machines virtuelles découvertes à Azure.
> * Regrouper les machines virtuelles découvertes, et évaluer le groupe de machines virtuelles.
> * Passer en revue l’évaluation.

> [!NOTE]
> Les tutoriels vous montrent le chemin de déploiement le plus simple pour un scénario donné afin que vous puissiez configurer rapidement une preuve de concept. Ils utilisent des options par défaut, le cas échéant, et ne montrent pas tous les paramètres et chemins possibles. Pour obtenir des instructions détaillées, consultez les articles sur les procédures.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/) avant de commencer.

## <a name="prerequisites"></a>Prérequis

- [Suivez le premier tutoriel](tutorial-prepare-vmware.md) de cette série. Si vous ne le faites pas, les instructions de ce tutoriel ne fonctionneront pas.
- Voici ce que vous avez dû faire dans le premier tutoriel :
    - [Préparer Azure](tutorial-prepare-vmware.md#prepare-azure) pour qu’il fonctionne avec Azure Migrate.
    - [Préparer VMware](tutorial-prepare-vmware.md#prepare-for-assessment) à l’évaluation. Comprend la vérification des paramètres VMware et la configuration d’un compte pouvant être utilisé par Azure Migrate pour accéder à vCenter Server.
    - [Vérifier](tutorial-prepare-vmware.md#verify-appliance-settings-for-assessment) ce dont vous avez besoin pour déployer l’appliance Azure Migrate dans le cadre de l’évaluation de VMware.

## <a name="set-up-an-azure-migrate-project"></a>Configurer un projet Azure Migrate

Configurez un nouveau projet Azure Migrate comme suit :

1. Dans le portail Azure, sélectionnez **Tous les services**, puis recherchez **Azure Migrate**.
2. Sous **Services**, sélectionnez **Azure Migrate**.
3. Dans **Vue d’ensemble**, sous **Découvrir, évaluer et migrer des serveurs**, sélectionnez **Évaluer et migrer des serveurs**.

   ![Bouton pour évaluer et migrer des serveurs](./media/tutorial-assess-vmware/assess-migrate.png)

4. Dans **Mise en route**, sélectionnez **Ajouter des outils**.
5. Dans **Projet de migration**, sélectionnez votre abonnement Azure, puis créez un groupe de ressources si vous n’en avez pas.     
6. Dans **Détails du projet**, spécifiez le nom du projet ainsi que la zone géographique où vous souhaitez le créer. Passez en revue les zones géographiques prises en charge pour les clouds [publics](migrate-support-matrix.md#supported-geographies-public-cloud) et du [secteur public](migrate-support-matrix.md#supported-geographies-azure-government).

   ![Zones pour le nom et la région du projet](./media/tutorial-assess-vmware/migrate-project.png)

7. Sélectionnez **Suivant**.
8. Dans **Sélectionner un outil d’évaluation**, sélectionnez **Azure Migrate : Server Assessment** > **Suivant**.

   ![Sélection de l’outil Server Assessment](./media/tutorial-assess-vmware/assessment-tool.png)

9. Dans **Sélectionner un outil de migration**, sélectionnez **Ignorer l’ajout d’un outil de migration pour l’instant** > **Suivant**.
10. Dans **Vérifier + ajouter des outils**, passez en revue les paramètres, puis sélectionnez **Ajouter des outils**.
11. Attendez quelques minutes, le temps nécessaire au déploiement du projet Azure Migrate. Vous êtes dirigé vers la page du projet. Si vous ne voyez pas le projet, vous pouvez y accéder à partir de **Serveurs** dans le tableau de bord Azure Migrate.

## <a name="set-up-the-azure-migrate-appliance"></a>Configurer l’appliance Azure Migrate

Azure Migrate Server Assessment utilise une appliance Azure Migrate légère. L’appliance effectue la découverte des machines virtuelles, puis envoie les métadonnées et les données de performances des machines virtuelles à Azure Migrate. L’appliance peut être configurée de plusieurs façons.

- Configurez-la sur une machine virtuelle VMware au moyen d’un modèle OVA téléchargé. Il s’agit de la méthode utilisée dans ce tutoriel.
- Configurez-la sur une machine virtuelle VMware ou machine physique avec un script d’installation PowerShell. [Cette méthode](deploy-appliance-script.md) doit être utilisée si vous ne pouvez pas configurer une machine virtuelle à l’aide d’un modèle OVA, ou si vous êtes dans Azure Government.

Après avoir créé l’appliance, vérifiez qu’elle peut se connecter à Azure Migrate Server Assessment, configurez-la pour la première fois, puis inscrivez-la auprès du projet Azure Migrate.


### <a name="download-the-ova-template"></a>Télécharger le modèle OVA

1. Dans **Objectifs de migration** > **Serveurs** > **Azure Migrate : Server Assessment**, sélectionnez **Découvrir**.
2. Dans **Découvrir des machines** > **Vos machines sont-elles virtualisées ?** , sélectionnez **Oui, avec l’hyperviseur vSphere VMware**.
3. Sélectionnez **Télécharger** pour télécharger le fichier de modèle OVA.

   ![Sélections pour le téléchargement d’un fichier OVA](./media/tutorial-assess-vmware/download-ova.png)

### <a name="verify-security"></a>Vérifier la sécurité

Vérifiez que le fichier OVA est sécurisé avant de le déployer :

1. Sur l’ordinateur où vous avez téléchargé le fichier, ouvrez une fenêtre de commande d’administrateur.
2. Exécutez la commande suivante pour générer le code de hachage du fichier OVA :
  
   ```C:\>CertUtil -HashFile <file_location> [Hashing Algorithm]```
   
   Exemple d’utilisation : ```C:\>CertUtil -HashFile C:\AzureMigrate\AzureMigrate.ova SHA256```

3. Vérifiez les toutes dernières versions de l’appliance et les valeurs de hachage :

    - Pour le cloud public Azure :
    
        **Algorithme** | **Télécharger** | **SHA256**
        --- | --- | ---
        VMware (10,9 Go) | [Version la plus récente](https://aka.ms/migrate/appliance/vmware) | cacbdaef927fe5477fa4e1f494fcb7203cbd6b6ce7402b79f234bc0fe69663dd

    - Pour Azure Government :
    
        **Algorithme** | **Télécharger** | **SHA256**
        --- | --- | ---
        VMware (63,1 Mo) | [Version la plus récente](https://go.microsoft.com/fwlink/?linkid=2120300&clcid=0x409 ) | 3d5822038646b81f458d89d706832c0a2c0e827bfa9b0a55cc478eaf2757a4de


### <a name="create-the-appliance-vm"></a>Créer la machine virtuelle de l’appliance

Importez le fichier téléchargé, puis créez une machine virtuelle :

1. Dans la console du client vSphere, sélectionnez **File** (Fichier) > **Deploy OVF Template** (Déployer le modèle OVF).

   ![Commande de menu pour le déploiement d’un modèle OVF](./media/tutorial-assess-vmware/deploy-ovf.png)

2. Dans l’Assistant de déploiement du modèle OVF > **Source**, spécifiez l’emplacement du fichier .OVA.
3. Dans **Name** (Nom) et **Location** (Emplacement), spécifiez un nom convivial pour la machine virtuelle. Sélectionnez l’objet d’inventaire dans lequel la machine virtuelle doit être hébergée.
4. Dans **Host/Cluster** (Hôte/Cluster), spécifiez l’hôte ou le cluster sur lequel s’exécute la machine virtuelle.
5. Dans **Storage** (Stockage), spécifiez la destination du stockage de la machine virtuelle.
6. Dans **Disk Format** (Format de disque), spécifiez le type de disque et la taille.
7. Dans **Network Mapping** (Mappage réseau), spécifiez le réseau auquel se connectera la machine virtuelle. Le réseau a besoin d’une connexion à Internet pour envoyer des métadonnées à Azure Migrate Server Assessment.
8. Validez les paramètres, puis sélectionnez **Finish (Terminer)** .

## <a name="verify-appliance-access-to-azure"></a>Vérifier l’accès de l’appliance à Azure

Vérifiez que la machine virtuelle de l’appliance peut se connecter aux URL Azure pour les clouds [publics](migrate-appliance.md#public-cloud-urls) et du [secteur public](migrate-appliance.md#government-cloud-urls).

### <a name="configure-the-appliance"></a>Configurer l’appliance

Configurez l’appliance pour la première fois.

> [!NOTE]
> Si vous configurez l’appliance à l’aide d’un [script PowerShell](deploy-appliance-script.md) au lieu du modèle OVA téléchargé, ne tenez pas compte des deux premières étapes de cette procédure.

1. Dans la console du client vSphere, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Open Console** (Ouvrir la console).
2. Spécifiez la langue, le fuseau horaire et le mot de passe pour l’appliance.
3. Ouvrez un navigateur sur une machine qui peut se connecter à la machine virtuelle, puis ouvrez l’URL de l’application web de l’appliance : **https://*nom ou adresse IP de l’appliance* : 44368**.

   Vous pouvez aussi ouvrir l’application à partir du Bureau de l’appliance en sélectionnant le raccourci de l’application.
1. Dans l’application web > **Configurer les prérequis**, procédez comme suit :
   - **Licence** : Acceptez les termes de licence et lisez les informations relatives aux tiers.
   - **Connectivité** : L’application vérifie que la machine virtuelle a accès à Internet. Si la machine virtuelle utilise un proxy :
     - Sélectionnez **Paramètres du proxy** et spécifiez l’adresse du proxy et le port d’écoute sous la forme http://ProxyIPAddress ou http://ProxyFQDN.
     - Spécifiez les informations d’identification si le proxy nécessite une authentification.
     - Seuls les proxys HTTP sont pris en charge.
   - **Synchronisation de l’heure** : L’heure de l’appliance doit être synchronisée avec l’heure Internet pour que la découverte fonctionne correctement.
   - **Installer les mises à jour** : L’appliance vérifie que les dernières mises à jour sont installées.
   - **Installer VDDK** : L’appliance vérifie que VDDK (VMware vSphere Virtual Disk Development Kit) est installé. S’il n’est pas installé, téléchargez VDDK 6.7 à partir de VMware, puis extrayez le contenu du fichier zip téléchargé à l’emplacement spécifié sur l’appliance.

     Azure Migrate Server Migration utilise VDDK pour répliquer les machines durant la migration vers Azure.       

### <a name="register-the-appliance-with-azure-migrate"></a>Inscrire l’appliance auprès d’Azure Migrate

1. Sélectionnez **Connexion**. S’il n’apparaît pas, vérifiez que vous avez désactivé le bloqueur de fenêtres publicitaires dans le navigateur.
2. Sous le nouvel onglet, connectez-vous avec votre nom d’utilisateur et votre mot de passe Azure.
   
   La connexion avec un code PIN n’est pas prise en charge.
3. Une fois la connexion réussie, revenez à l’application web.
4. Sélectionnez l’abonnement dans lequel le projet Azure Migrate a été créé, puis sélectionnez le projet.
5. Spécifiez un nom pour l’appliance. Le nom doit être alphanumérique et comporter 14 caractères au maximum.
6. Sélectionnez **Inscription**.


## <a name="start-continuous-discovery"></a>Démarrer la découverte en continu

L’appliance doit se connecter à vCenter Server pour découvrir les données de configuration et de performances des machines virtuelles.

### <a name="specify-vcenter-server-details"></a>Spécifier les détails vCenter Server
1. Dans **Spécifier les détails vCenter Server**, spécifiez le nom (FQDN) ou l’adresse IP de l’instance du serveur vCenter Server. Vous pouvez laisser le port par défaut ou spécifier un port personnalisé sur lequel votre serveur vCenter Server est à l’écoute.
2. Dans **Nom d’utilisateur** et **Mot de passe**, spécifiez les informations d’identification du compte vCenter Server que l’appliance doit utiliser pour découvrir les machines virtuelles sur l’instance vCenter Server. 

    - Vous devez avoir configuré un compte avec les autorisations nécessaires dans le [tutoriel précédent](tutorial-prepare-vmware.md#set-up-permissions-for-assessment).
    - Si vous souhaitez étendre la découverte à des objets VMware spécifiques (centres de données vCenter Server, clusters, dossier de clusters, hôtes, dossier d’hôtes ou machines virtuelles individuelles), passez en revue les instructions contenues dans [cet article](set-discovery-scope.md) pour restreindre le compte utilisé par Azure Migrate.

3. Sélectionnez **Valider la connexion** pour vérifier que l’appliance peut se connecter à vCenter Server.
4. Dans **Découvrir les applications et les dépendances sur les machines virtuelles**, vous pouvez cliquer sur **Ajouter des informations d’identification** et spécifier le système d’exploitation pour lequel les informations d’identification sont pertinentes, ainsi que le nom d’utilisateur et le mot de passe des informations d’identification. Cliquez ensuite sur **Ajouter**.

    - Vous pouvez ajouter des informations d’identification ici si vous avez créé un compte à utiliser pour la [fonctionnalité de découverte d’applications](how-to-discover-applications.md) ou la [fonctionnalité d’analyse de dépendances sans agent](how-to-create-group-machine-dependencies-agentless.md).
    - Si vous n’utilisez pas ces fonctionnalités, vous pouvez ignorer ce paramètre.
    - Passez en revue les informations d’identification nécessaires pour la [découverte d’applications](migrate-support-matrix-vmware.md#application-discovery-requirements) ou l’[analyse sans agent](migrate-support-matrix-vmware.md#dependency-analysis-requirements-agentless).

5. **Enregistrez et démarrez la découverte** pour lancer la découverte de machines virtuelles.

La découverte fonctionne comme ceci :
- Environ 15 minutes sont nécessaires pour que les métadonnées des machines virtuelles découvertes apparaissent dans le portail.
- La découverte des applications, rôles et fonctionnalités installés prend un certain temps. Sa durée dépend du nombre de machines virtuelles découvertes. Pour 500 machines virtuelles, il faut environ une heure pour que l’inventaire des applications s’affiche dans le portail Azure Migrate.

### <a name="verify-vms-in-the-portal"></a>Vérifier les machines virtuelles dans le portail

Une fois la découverte effectuée, vous pouvez vérifier que les machines virtuelles apparaissent dans le portail Azure :

1. Ouvrez le tableau de bord Azure Migrate.
2. Dans la page **Azure Migrate - Serveurs** > **Azure Migrate : Server Assessment**, sélectionnez l’icône qui affiche le nombre de **serveurs découverts**.

## <a name="set-up-an-assessment"></a>Configurer une évaluation

Vous pouvez créer deux types d’évaluations avec Azure Migrate Server Assessment :

**Type d’évaluation** | **Détails**
--- | --- 
**Microsoft Azure** | Évaluations pour migrer vos serveurs locaux vers des machines virtuelles Azure. <br/><br/> Vous pouvez évaluer vos [machines virtuelles VMware](how-to-set-up-appliance-vmware.md), [machines virtuelles Hyper-V](how-to-set-up-appliance-hyper-v.md) et [serveurs physiques](how-to-set-up-appliance-physical.md) locaux pour la migration vers Azure à l’aide de ce type d’évaluation. [En savoir plus](concepts-assessment-calculation.md)
**Azure VMware Solution (AVS)** | Évaluations pour migrer vos serveurs locaux vers [Azure VMware Solution (AVS)](../azure-vmware/introduction.md). <br/><br/> Vous pouvez évaluer vos [machines virtuelles VMware](how-to-set-up-appliance-vmware.md) locales pour la migration vers Azure VMware Solution (AVS) avec ce type d’évaluation. [En savoir plus](concepts-azure-vmware-solution-assessment-calculation.md)

L’évaluation de serveur fournit deux options de critères de dimensionnement :

**Critère de dimensionnement** | **Détails** | **Données**
--- | --- | ---
**Basée sur les performances** | Évaluations qui donnent des recommandations en fonction des données de performances collectées | **Évaluation des machines virtuelles Azure** : Les recommandations concernant les machines virtuelles sont fonction des données d’utilisation du processeur et de la mémoire.<br/><br/> Les recommandations concernant le type de disque (HDD/SSD ou disque managé premium) sont fonction de l’IOPS et du débit des disques locaux.<br/><br/> **Évaluation d’Azure VMware Solution (AVS)**  : Les suggestions concernant les nœuds AVS sont basées sur les données d’utilisation du processeur et de la mémoire.
**Telle quelle locale** | Évaluations qui n’utilisent pas de données de performances pour formuler des recommandations. | **Évaluation des machines virtuelles Azure** : Les recommandations concernant la taille des machines virtuelles sont basées sur la taille de la machines virtuelle locale.<br/><br> Le type de disque recommandé est basé sur ce que vous sélectionnez dans le paramètre type de stockage pour l’évaluation.<br/><br/> **Évaluation d’Azure VMware Solution (AVS)**  : Les suggestions concernant les nœuds AVS sont basées sur la taille des machines virtuelles locales.

## <a name="run-an-assessment"></a>Exécuter une évaluation

Exécutez une *évaluation des machines virtuelles Azure* comme suit :

1. Passez en revue les [meilleures pratiques](best-practices-assessment.md) liées à la création d’évaluations.
2. Sous l’onglet **Serveurs**, dans la vignette **Azure Migrate : Server Assessment**, sélectionnez **Évaluer**.

   ![Emplacement du bouton Évaluer](./media/tutorial-assess-vmware/assess.png)

3. Dans **Évaluer les serveurs**, sélectionnez le type d’évaluation « Machine virtuelle Azure », sélectionnez la source de détection et spécifiez le nom de l’évaluation.

    ![Notions de base d’évaluation](./media/tutorial-assess-vmware/assess-servers-azurevm.png)
 
4. Sélectionnez **Afficher tout**, puis passez en revue les propriétés d’évaluation.

   ![Propriétés de l’évaluation](./media/tutorial-assess-vmware/view-all.png)

5. Cliquez sur **Suivant** pour **sélectionner les machines à évaluer**. Dans **Sélectionner ou créer un groupe**, sélectionnez **Créer**, puis spécifiez un nom de groupe. Un groupe rassemble une ou plusieurs machines virtuelles à évaluer.
6. Dans **Ajouter des machines au groupe**, sélectionnez les machines virtuelles à ajouter au groupe.
7. Cliquez sur **Suivant** pour **vérifier + créer une évaluation** afin de passer en revue les détails de l’évaluation.
8. Sélectionnez **Créer une évaluation** pour créer le groupe, puis exécutez l’évaluation.

   ![Évaluer des serveurs](./media/tutorial-assess-vmware/assessment-create.png)

8. Une fois l’évaluation créée, vous pouvez la voir dans **Serveurs** > **Azure Migrate : Server Assessment** > **Évaluations**.
9. Sélectionnez **Exporter l’évaluation** pour la télécharger sous la forme d’un fichier Excel.

Si vous souhaitez exécuter une **évaluation Azure VMware Solution (AVS)** , suivez les étapes mentionnées [ici](how-to-create-azure-vmware-solution-assessment.md).


## <a name="review-an-assessment"></a>Réviser une évaluation

Une évaluation décrit les éléments suivants :

- **Préparé pour Azure** : Indique si les machines virtuelles peuvent faire l’objet d’une migration vers Azure.
- **Estimation des coûts mensuels** : Coûts mensuels de calcul et de stockage estimés pour l’exécution des machines virtuelles dans Azure.
- **Estimation des coûts de stockage mensuels** : Coûts estimés pour le stockage sur disque après la migration.

Pour voir une évaluation :

1. Dans **Objectifs de migration** > **Serveurs**, sélectionnez **Évaluations** dans **Azure Migrate : Évaluation de serveur**.
2. Dans **Évaluations**, sélectionnez une évaluation pour l’ouvrir.

   ![Récapitulatif de l’évaluation](./media/tutorial-assess-vmware/assessment-summary.png)

### <a name="review-azure-readiness"></a>Examiner la préparation pour Azure

1. Dans **Préparé pour Azure**, vérifiez si les machines virtuelles sont prêtes pour la migration vers Azure.
2. Passez en revue l’état des machines virtuelles :
    - **Disponible pour Azure** : Utilisé quand Azure Migrate recommande une taille de machine virtuelle et donne des estimations de coût pour les machines virtuelles de l’évaluation.
    - **Disponible sous conditions** : Montre des problèmes et leur correction suggérée.
    - **Non disponible pour Azure** : Montre des problèmes et leur correction suggérée.
    - **État de la préparation inconnu** : Utilisé quand Azure Migrate ne peut pas évaluer la préparation en raison de problèmes de disponibilité des données.

3. Sélectionnez un état **Préparé pour Azure**. Vous pouvez voir les détails de la préparation de la machine virtuelle. Vous pouvez également consulter les détails de la machine virtuelle, notamment les paramètres de calcul, de stockage et de réseau.

### <a name="review-cost-details"></a>Passer en revue les détails des coûts

Ce résumé d’évaluation montre une estimation des coûts de calcul et de stockage liés à l’exécution des machines virtuelles dans Azure. Les coûts sont agrégés pour toutes les machines virtuelles du groupe évalué. Vous pouvez consulter le détail des coûts de machines virtuelles spécifiques.

> [!NOTE]
> Les estimations des coûts sont basées sur les suggestions de taille d’une machine, ses disques et ses propriétés. Les estimations concernent l’exécution des machines virtuelles locales en tant que machines virtuelles IaaS. Azure Migrate Server Assessment ne prend pas en compte les coûts PaaS ou SaaS.

Les coûts de stockage agrégés pour le groupe évalué sont répartis selon différents types de disque de stockage. 

### <a name="review-confidence-rating"></a>Examiner le niveau de confiance

Azure Migrate : Évaluation du serveur attribue un niveau de confiance à une évaluation basée sur les performances, qui va de une étoile (le plus faible) à cinq étoiles (le plus élevé).

![Niveau de confiance](./media/tutorial-assess-vmware/confidence-rating.png)

Le niveau de confiance vous aide à estimer la fiabilité des suggestions de taille fournies par l’évaluation. Le niveau de confiance est basé sur la disponibilité des points de données nécessaires pour calculer l’évaluation :

**Disponibilité des points de données** | **Niveau de confiance**
--- | ---
0 %-20 % | 1 étoile
21 %-40 % | 2 étoiles
41 %-60 % | 3 étoiles
61 %-80 % | 4 étoiles
81 %-100 % | 5 étoiles

[Découvrez les bonnes pratiques](best-practices-assessment.md#best-practices-for-confidence-ratings) relatives aux niveaux de confiance.

## <a name="next-steps"></a>Étapes suivantes

Dans ce tutoriel, vous avez configuré une appliance Azure Migrate. Vous avez aussi créé et passé en revue une évaluation.

Pour apprendre à migrer des machines virtuelles VMware vers Azure avec Azure Migrate Server Migration, passez au troisième tutoriel de la série :

> [!div class="nextstepaction"]
> [Migrer des machines virtuelles VMware](./tutorial-migrate-vmware.md)
