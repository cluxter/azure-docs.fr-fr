---
title: ALTER EXTERNAL STREAM (Transact-SQL) - Azure SQL Edge (préversion)
description: En savoir plus sur l'instruction ALTER EXTERNAL STREAM d'Azure SQL Edge (préversion)
keywords: ''
services: sql-edge
ms.service: sql-edge
ms.topic: conceptual
author: SQLSourabh
ms.author: sourabha
ms.reviewer: sstein
ms.date: 05/19/2020
ms.openlocfilehash: 2559c4b4b875403b7c70671e27cb6222a3f1103a
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2020
ms.locfileid: "84235194"
---
# <a name="alter-external-stream-transact-sql"></a>ALTER EXTERNAL STREAM (Transact-SQL)

Modifie la définition d’un flux externe. La modification d’un flux externe utilisé par une tâche de streaming dans un état *En cours d'exécution* n’est pas autorisée. 



## <a name="syntax"></a>Syntaxe

```sql
  ALTER EXTERNAL STREAM external_stream_name 
  SET 
    [DATA_SOURCE] = <data_source_name> 
    , LOCATION = <location_name> 
    , EXTERNAL_FILE_FORMAT = <external_file_format_name> 
    , INPUT_OPTIONS = <input_options> 
    , OUTPUT_OPTIONS = <output_options> 
```

## <a name="arguments"></a>Arguments

Pour plus d’informations sur les arguments de la commande Alter External Stream, consultez [CREATE EXTERNAL STREAM (Transact-SQL)](create-external-stream-transact-sql.md).

## <a name="return-code-values"></a>Valeurs des codes de retour

ALTER EXTERNAL STREAM retourne 0 en cas de réussite. Toute valeur autre que 0 indique un échec.


## <a name="see-also"></a>Voir aussi

- [CREATE EXTERNAL STREAM (Transact-SQL)](create-external-stream-transact-sql.md) 
- [DROP EXTERNAL STREAM (Transact-SQL)](drop-external-stream-transact-sql.md) 
