---
title: 'Tutoriel : Configurer Snowflake pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs'
description: Découvrez comment configurer Azure Active Directory pour approvisionner et retirer automatiquement des comptes utilisateur sur Snowflake.
services: active-directory
documentationcenter: ''
author: zchia
writer: zchia
manager: beatrizd
ms.assetid: f9ce85f4-0992-4bc6-8276-4b2efbce8dcb
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2019
ms.author: zhchia
ms.openlocfilehash: 46ebb122b0165d469b1c40871d5939e50a8595c9
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87016301"
---
# <a name="tutorial-configure-snowflake-for-automatic-user-provisioning"></a>Tutoriel : Configurer Snowflake pour l’approvisionnement automatique d’utilisateurs

L’objectif de ce didacticiel est de présenter les étapes à effectuer dans Snowflake et Azure Active Directory (Azure AD) afin de configurer Azure AD pour l’approvisionnement et le déprovisionnement automatiques d’utilisateurs et/ou de groupes sur [Snowflake](https://www.Snowflake.com/pricing/). Pour découvrir les informations importantes sur ce que fait ce service, comment il fonctionne et consulter le forum aux questions, reportez-vous à l’article [Automatiser l’attribution et l’annulation de l’attribution des utilisateurs dans les applications SaaS avec Azure Active Directory](../manage-apps/user-provisioning.md). 


> [!NOTE]
> Ce connecteur est actuellement en préversion publique. Pour plus d’informations sur les conditions d’utilisation Microsoft Azure générales relatives aux fonctionnalités d’évaluation, consultez [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="capabilities-supported"></a>Fonctionnalités prises en charge
> [!div class="checklist"]
> * Créer des utilisateurs dans Snowflake
> * Supprimer des utilisateurs dans Snowflake quand ils ne nécessitent plus d’accès
> * Maintenir la synchronisation des attributs utilisateur entre Azure AD et Snowflake
> * Provisionner des groupes et des appartenances aux groupes dans Snowflake
> * [Authentification unique](https://docs.microsoft.com/azure/active-directory/saas-apps/snowflake-tutorial) auprès de Snowflake (recommandé)

## <a name="prerequisites"></a>Prérequis

Le scénario décrit dans ce tutoriel part du principe que vous disposez des prérequis suivants :

* [Un locataire Azure AD](https://docs.microsoft.com/azure/active-directory/develop/quickstart-create-new-tenant).
* Un compte d’utilisateur dans Azure AD avec l’[autorisation](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) de configurer l’approvisionnement (par exemple, Administrateur d’application, Administrateur d’application cloud, Propriétaire d’application ou Administrateur général).
* [Un locataire Snowflake](https://www.Snowflake.com/pricing/).
* Un compte d’utilisateur dans Snowflake avec des autorisations d’administrateur.

## <a name="step-1-plan-your-provisioning-deployment"></a>Étape 1. Planifier votre déploiement de l’approvisionnement
1. En savoir plus sur le [fonctionnement du service d’approvisionnement](https://docs.microsoft.com/azure/active-directory/manage-apps/user-provisioning).
2. Déterminez qui sera dans l’[étendue pour l’approvisionnement](https://docs.microsoft.com/azure/active-directory/manage-apps/define-conditional-rules-for-provisioning-user-accounts).
3. Déterminez les données à [mapper entre Azure AD et Snowflake](https://docs.microsoft.com/azure/active-directory/manage-apps/customize-application-attributes). 

## <a name="step-2-configure-snowflake-to-support-provisioning-with-azure-ad"></a>Étape 2. Configurer Snowflake pour prendre en charge le provisionnement avec Azure AD

Avant de configurer Snowflake pour l’attribution automatique d’utilisateurs avec Azure AD, vous devez activer le provisionnement SCIM sur Snowflake.

1. Connectez-vous à votre Console d’administration Snowflake. Entrez la requête illustrée ci-dessous dans la feuille de calcul en surbrillance, puis cliquez sur **Exécuter**.

    ![Console d’administrateur Snowflake](media/Snowflake-provisioning-tutorial/image00.png)

2.  Un jeton d’accès SCIM sera généré pour votre locataire Snowflake. Pour le récupérer, cliquez sur le lien en surbrillance ci-dessous.

    ![Ajout SCIM Snowflake](media/Snowflake-provisioning-tutorial/image01.png)

3. Copiez la valeur du jeton généré, puis cliquez sur **Terminé**. Cette valeur devra être entrée dans le champ **Jeton secret** dans l’onglet Approvisionnement de votre application Snowflake dans le portail Azure.

    ![Ajout SCIM Snowflake](media/Snowflake-provisioning-tutorial/image02.png)

## <a name="step-3-add-snowflake-from-the-azure-ad-application-gallery"></a>Étape 3. Ajouter Snowflake à partir de la galerie d’applications Azure AD

Ajoutez Snowflake à partir de la galerie d’applications Azure AD pour gérer le provisionnement dans Snowflake. Si vous avez déjà configuré Snowflake pour l’authentification unique, vous pouvez utiliser la même application. Toutefois, il est recommandé de créer une application distincte lors du test initial de l’intégration. En savoir plus sur l’ajout d’une application à partir de la galerie [ici](https://docs.microsoft.com/azure/active-directory/manage-apps/add-gallery-app). 

## <a name="step-4-define-who-will-be-in-scope-for-provisioning"></a>Étape 4. Définir qui sera dans l’étendue pour l’approvisionnement 

Le service d’approvisionnement Azure AD vous permet de définir l’étendue des utilisateurs approvisionnés en fonction de l’affectation à l’application et/ou en fonction des attributs de l’utilisateur/groupe. Si vous choisissez de définir l’étendue de l’approvisionnement pour votre application en fonction de l’attribution, vous pouvez utiliser les étapes de [suivantes](../manage-apps/assign-user-or-group-access-portal.md) pour affecter des utilisateurs et des groupes à l’application. Si vous choisissez de définir l’étendue de l’approvisionnement en fonction uniquement des attributs de l’utilisateur ou du groupe, vous pouvez utiliser un filtre d’étendue comme décrit [ici](https://docs.microsoft.com/azure/active-directory/manage-apps/define-conditional-rules-for-provisioning-user-accounts). 

* Quand vous attribuez des utilisateurs et des groupes à Snowflake, vous devez sélectionner un rôle autre que le rôle **Accès par défaut**. Les utilisateurs disposant du rôle Accès par défaut sont exclus de l’approvisionnement et sont marqués comme non autorisés dans les journaux de configuration. Si le seul rôle disponible dans l’application est le rôle d’accès par défaut, vous pouvez [mettre à jour le manifeste de l’application](https://docs.microsoft.com/azure/active-directory/develop/howto-add-app-roles-in-azure-ad-apps) pour ajouter des rôles supplémentaires. 

* Commencez progressivement. Testez avec un petit ensemble d’utilisateurs et de groupes avant d’effectuer un déploiement général. Lorsque l’étendue de l’approvisionnement est définie sur les utilisateurs et les groupes attribués, vous pouvez contrôler cela en affectant un ou deux utilisateurs ou groupes à l’application. Lorsque l’étendue est définie sur tous les utilisateurs et groupes, vous pouvez spécifier un [filtre d’étendue basé sur l’attribut](https://docs.microsoft.com/azure/active-directory/manage-apps/define-conditional-rules-for-provisioning-user-accounts). 


## <a name="step-5-configure-automatic-user-provisioning-to-snowflake"></a>Étape 5. Configurer l’approvisionnement automatique d’utilisateurs sur Snowflake 

Cette section vous guide tout au long des étapes de configuration du service d’approvisionnement d’Azure AD pour créer, mettre à jour et désactiver des utilisateurs et/ou des groupes dans Snowflake en fonction des attributions d’utilisateurs et/ou de groupes dans Azure AD.

### <a name="to-configure-automatic-user-provisioning-for-snowflake-in-azure-ad"></a>Pour configurer l’approvisionnement automatique d’utilisateurs pour Snowflake dans Azure AD :

1. Connectez-vous au [portail Azure](https://portal.azure.com). Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.

    ![Panneau Applications d’entreprise](common/enterprise-applications.png)

2. Dans la liste des applications, sélectionnez **Snowflake**.

    ![Lien Snowflake dans la liste des applications](common/all-applications.png)

3. Sélectionnez l’onglet **Approvisionnement**.

    ![Onglet Approvisionnement](common/provisioning.png)

4. Définissez le **Mode d’approvisionnement** sur **Automatique**.

    ![Onglet Approvisionnement](common/provisioning-automatic.png)

5. Sous la section Informations d’identification de l’administrateur, entrez les valeurs d’**URL de base SCIM 2.0 et de Jeton d’authentification** récupérées précédemment respectivement dans les champs **URL de locataire** et **Jeton secret**. Cliquez sur **Tester la connexion** pour vérifier qu’Azure AD peut se connecter à Snowflake. Si la connexion échoue, vérifiez que votre compte Snowflake dispose d’autorisations d’administrateur et réessayez.

    ![URL de locataire + Jeton](common/provisioning-testconnection-tenanturltoken.png)

7. Dans le champ **E-mail de notification**, entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement, puis cochez la case **Envoyer une notification par e-mail en cas de défaillance**.

    ![E-mail de notification](common/provisioning-notification-email.png)

8. Cliquez sur **Enregistrer**.

9. Dans la section **Mappages**, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec Snowflake**.

10. Dans la section **Mappages des attributs**, passez en revue les attributs d’utilisateurs qui sont synchronisés entre Azure AD et Snowflake. Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour faire correspondre les comptes d’utilisateur dans Snowflake pour les opérations de mise à jour. Cliquez sur le bouton **Enregistrer** pour valider les modifications.

   |Attribut|Type|
   |---|---|
   |active|Boolean|
   |displayName|String|
   |emails[type eq "work"].value|String|
   |userName|String|
   |name.givenName|String|
   |name.familyName|String|
   |urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:defaultRole|String|
   |urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:defaultWarehouse|String|

11. Dans la section **Mappages**, sélectionnez **Synchroniser les groupes Azure Active Directory avec Snowflake**.

12. Dans la section **Mappages des attributs**, passez en revue les attributs de groupes qui sont synchronisés entre Azure AD et Snowflake. Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour faire correspondre les groupes dans Snowflake pour les opérations de mise à jour. Cliquez sur le bouton **Enregistrer** pour valider les modifications.

      |Attribut|Type|
      |---|---|
      |displayName|String|
      |membres|Informations de référence|

13. Pour configurer des filtres d’étendue, reportez-vous aux instructions suivantes fournies dans [Approvisionnement d’applications basé sur les attributs avec filtres d’étendue](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md).

14. Pour activer le service d’approvisionnement Azure AD pour Snowflake, modifiez le paramètre **État d’approvisionnement** sur **Activé** dans la section **Paramètres**.

    ![État d’approvisionnement activé](common/provisioning-toggle-on.png)

15. Définissez les utilisateurs et/ou groupes que vous aimeriez approvisionner sur Snowflake en choisissant les valeurs souhaitées dans **Étendue** dans la section **Paramètres**. Si cette option n’est pas disponible, configurez les champs nécessaires sous Informations d’identification de l’administrateur, cliquez sur **Enregistrer**, puis actualisez la page. 

    ![Étendue de l’approvisionnement](common/provisioning-scope.png)

16. Lorsque vous êtes prêt à effectuer l’approvisionnement, cliquez sur **Enregistrer**.

    ![Enregistrement de la configuration de l’approvisionnement](common/provisioning-configuration-save.png)

    Cette opération démarre la synchronisation initiale de tous les utilisateurs et/ou groupes définis dans **Étendue** dans la section **Paramètres**. La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent toutes les 40 minutes environ tant que le service de provisionnement Azure AD est en cours d’exécution.

## <a name="step-6-monitor-your-deployment"></a>Étape 6. Surveiller votre déploiement
Une fois que vous avez configuré l’approvisionnement, utilisez les ressources suivantes pour surveiller votre déploiement :

1. Utilisez les [journaux d’approvisionnement](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-provisioning-logs) pour déterminer quels utilisateurs ont été configurés avec succès ou échoué.
2. Consultez la [barre de progression](https://docs.microsoft.com/azure/active-directory/manage-apps/application-provisioning-when-will-provisioning-finish-specific-user) pour afficher l’état du cycle d’approvisionnement et quand il se termine
3. Si la configuration de l’approvisionnement semble se trouver dans un état non sain, l’application passe en quarantaine. Pour en savoir plus sur les états de quarantaine, cliquez [ici](https://docs.microsoft.com/azure/active-directory/manage-apps/application-provisioning-quarantine-status).  

## <a name="connector-limitations"></a>Limitations du connecteur

* Les jetons SCIM générés par Snowflake expirent dans 6 mois. N’oubliez pas que ces derniers doivent être actualisés avant leur expiration pour permettre aux synchronisations de provisionnement de continuer de fonctionner. 

## <a name="change-log"></a>Journal des modifications

* 21/07/2020 : activation de la suppression réversible pour tous les utilisateurs (via l’attribut actif).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](../app-provisioning/configure-automatic-user-provisioning-portal.md).
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a>Étapes suivantes
* [Découvrez comment consulter les journaux d’activité et obtenir des rapports sur l’activité d’approvisionnement](../app-provisioning/check-status-user-account-provisioning.md).
