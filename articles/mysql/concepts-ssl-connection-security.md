---
title: Connectivité SSL/TLS – Azure Database pour MySQL
description: Informations de configuration de la base de données Azure pour MySQL et des applications associées afin d’utiliser correctement les connexions SSL.
author: kummanish
ms.author: manishku
ms.service: mysql
ms.topic: conceptual
ms.date: 07/09/2020
ms.openlocfilehash: 0956a38349ef7bc7571dfac2f3722dd9fea425a3
ms.sourcegitcommit: 3541c9cae8a12bdf457f1383e3557eb85a9b3187
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86201642"
---
# <a name="ssltls-connectivity-in-azure-database-for-mysql"></a>Connectivité SSL/TLS dans Azure Database pour MySQL

La base de données Azure pour MySQL prend en charge la connexion de votre serveur de base de données aux applications clientes via SSL (Secure Sockets Layer). L’application de connexions SSL entre votre serveur de base de données et vos applications clientes vous protège contre les « attaques de l’intercepteur » en chiffrant le flux de données entre le serveur et votre application.

> [!NOTE]
> La mise à jour de la valeur du paramètre de serveur `require_secure_transport` n’affecte pas le comportement du service MySQL. Utilisez les fonctionnalités d’application SSL et TLS décrites dans cet article pour sécuriser les connexions.

## <a name="ssl-default-settings"></a>Paramètres SSL par défaut

Par défaut, le service de base de données doit être configuré pour exiger des connexions SSL lors de la connexion à MySQL.  Nous vous recommandons d’éviter de désactiver l’option SSL dans la mesure du possible.

Lorsque vous approvisionnez un nouveau serveur de base de données Azure pour MySQL par le biais du Portail Azure et d’Azure CLI, l’application de connexions SSL est activée par défaut. 

Les chaînes de connexion pour les différents langages de programmation sont affichées dans le portail Azure. Ces chaînes de connexion incluent les paramètres SSL requis pour se connecter à votre base de données. Dans le portail Azure, sélectionnez votre serveur. Sous l’en-tête **Paramètres**, sélectionnez les **Chaînes de connexion**. Le paramètre SSL varie en fonction du connecteur, par exemple « ssl=true », « sslmode=require » ou « sslmode=require » et d’autres variations.

Dans certains cas, les applications nécessitent un fichier de certificat local généré à partir du fichier de certificat d’une autorité de certification (AC) approuvée pour se connecter en toute sécurité. Vous trouverez le certificat permettant la connexion à un serveur Azure Database pour MySQL ici : https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem. 

Consultez les liens suivants afin d’obtenir des certificats pour les serveurs de clouds souverains : [Azure Government](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem), [Azure Chine](https://dl.cacerts.digicert.com/DigiCertGlobalRootCA.crt.pem) et [Azure Allemagne](https://www.d-trust.net/cgi-bin/D-TRUST_Root_Class_3_CA_2_2009.crt).

Pour découvrir comment activer ou désactiver la connexion SSL pour le développement d’applications, consultez la page [Guide pratique : configurer SSL](howto-configure-ssl.md).

## <a name="tls-enforcement-in-azure-database-for-mysql"></a>Imposition du protocole TLS dans Azure Database pour MySQL

Azure Database pour MySQL prend en charge le chiffrement pour les clients qui se connectent à votre serveur de base de données à l’aide du protocole TLS (Transport Layer Security). TLS est un protocole standard qui garantit la sécurité des connexions réseau entre votre serveur de base de données et vos applications clientes, ce qui vous permet de respecter les exigences de conformité.

### <a name="tls-settings"></a>Paramètres TLS

Azure Database pour MySQL offre la possibilité d’imposer la version du protocole TLS pour les connexions clientes. Pour imposer la version du protocole TLS, utilisez le paramètre d’option **Version TLS minimale**. Les valeurs suivantes sont autorisées pour ce paramètre d’option :

|  Paramètre TLS minimal             | Version TLS du client prise en charge                |
|:---------------------------------|-------------------------------------:|
| TLSEnforcementDisabled (par défaut) | Aucun protocole TLS requis                      |
| TLS1_0                           | TLS 1.0, TLS 1.1, TLS 1.2 et versions ultérieures           |
| TLS1_1                           | TLS 1.1, TLS 1.2 et versions ultérieures                   |
| TLS1_2                           | TLS versions 1.2 et ultérieures                     |


Par exemple, la définition de la valeur du paramètre de version minimale du protocole TLS sur TLS 1.0 signifie que votre serveur autorise les connexions en provenance des clients utilisant les protocoles TLS 1.0, 1.1 et 1.2+. Si vous choisissez la valeur 1.2, en revanche, cela signifie que vous autorisez uniquement les connexions en provenance des clients utilisant TLS 1.2+ et que toutes les connexions à l’aide des protocoles TLS 1.0 et TLS 1.1 sont rejetées.

> [!Note] 
> Par défaut, Azure Database pour MySQL n’applique aucune version TLS minimale (le paramètre `TLSEnforcementDisabled`).
>
> Une fois que vous avez appliqué une version TLS minimale, vous ne pourrez plus la désactiver.

Pour découvrir comment définir le paramètre TLS pour Azure Database pour MySQL, consultez le [Guide pratique pour configurer le paramètre TLS](howto-tls-configurations.md).

## <a name="next-steps"></a>Étapes suivantes

- [Bibliothèques de connexions de la base de données Azure pour MySQL](concepts-connection-libraries.md)
- Découvrez comment [configurer le protocole SSL](howto-configure-ssl.md)
- Découvrez comment [configurer le protocole TLS](howto-tls-configurations.md)
