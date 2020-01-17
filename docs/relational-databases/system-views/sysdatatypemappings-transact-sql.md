---
title: sysdatatypemappings (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3d58525ec4bcedc4249466be93628a7c1baa21bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910146"
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysdatatypemappings**ビューを使用して、SQL Server データ型と SQL Server 以外のデータベース管理システム (DBMS) のデータ型間のマッピングを表示します。 このビューは、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**int**|データ型のマッピングの ID。|  
|**source_dbms**|**sysname**|元のデータ型がマップされ、次の値のいずれかの DBMS の名前を示します。<br /><br /> **MSSQLSERVER** =、ソースが SQL Server データベース。<br /><br /> **ORACLE** = ソースには、Oracle データベース。|  
|**source_version**|**sysname**|マップ元 DBMS の製品バージョンを示します。|  
|**source_type**|**sysname**|マップ元 DBMS でのデータ型を示します。|  
|**source_length_min**|**bigint**|マップ元 DBMS におけるデータ型の最小の長さ。値 NULL は長さが使用されないことを示します。|  
|**source_length_max**|**bigint**|マップ元 DBMS で NULL 値が長さが使用されないことを示すにおけるデータ型の最大長。|  
|**source_precision_min**|**bigint**|マップ元 DBMS で NULL 値が有効桁数が使用されないことを示すにおけるデータ型の最小有効桁数。|  
|**source_precision_max**|**bigint**|マップ元 DBMS で NULL 値が有効桁数が使用されないことを示すにおけるデータ型の最大有効桁数。|  
|**source_scale_min**|**int**|マップ元 DBMS で NULL 値がスケールが使用されないことを示すにおけるデータ型の最小のスケール。|  
|**source_scale_max**|**int**|マップ元 DBMS におけるデータ型の最大小数点以下桁数。値 NULL は小数点以下桁数が使用されないことを示します。|  
|**source_nullable**|**bit**|変換先のデータ型が null 値をサポートしているかが示されます。|  
|**source_createparams**|**int**|内部使用のみです。|  
|**destination_dbms**|**sysname**|マップ先 DBMS の名前を示します。次の値のいずれかになります。<br /><br /> **MSSQLSERVER** =、変換先は、SQL Server データベース。<br /><br /> **ORACLE** =、変換先は Oracle データベース。<br /><br /> **DB2** =、変換先は、IBM DB2 データベース。<br /><br /> **SYBASE** =、変換先は Sybase データベース。|  
|**destination_version**|**sysname**|マップ先 DBMS の製品バージョンです。|  
|**destination_type**|**sysname**|マップ先 DBMS でのデータ型。|  
|**destination_length**|**bigint**|マップ先 DBMS のデータ型の長さです。|  
|**destination_precision**|**bigint**|マップ先 DBMS でのデータ型の有効桁数。|  
|**destination_scale**|**int**|マップ先 DBMS のデータ型の小数点以下桁数です。|  
|**destination_nullable**|**bit**|マップ先 DBMS でのデータ型が null 値をサポートしているかを示します。|  
|**destination_createparams**|**int**|内部使用のみです。|  
|**dataloss**|**bit**|かどうか、ソースとマップ先 DBMS でのデータ型間のマッピングとデータの損失が発生することを示します。|  
|**is_default**|**bit**|データ型マッピングが既定で使用されるかどうかを示します。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpdatatypemap &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
