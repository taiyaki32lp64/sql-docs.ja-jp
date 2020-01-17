---
title: MSdbms_datatype (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
author: stevestein
ms.author: sstein
ms.openlocfilehash: 301aa5af9aa34031f381235341f1e7d461675432
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907510"
---
# <a name="msdbms_datatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype**テーブルには、異種データベース レプリケーションでパブリッシャーまたはサブスクライバーとして使用される各サポートされているデータベース管理システム (DBMS) でのネイティブ データ型の完全な一覧が含まれています。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|各一意のデータ型を識別します。|  
|**dbms_id**|**int**|型が属する DBMS を識別します。|  
|**type**|**sysname**|データ型の名前 (ネイティブ)。|  
|**createparams**|**int**|各データ型に適用できる長さ、有効桁数、および小数点以下桁数の組み合わせを表すビットマップです。以下の要素が含まれます。<br /><br /> **0x1** = 有効桁数。<br /><br /> **0x2**スケールを = です。<br /><br /> **0x4**長さを = です。|  
  
## <a name="remarks"></a>コメント  
 このテーブルには、SQL Server のインスタンスことができるため両方非 SQL Server データベースにサブスクライブする - SQL Server 以外のサブスクライバーの発行の SQL Server データ型のエントリが含まれています。  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle パブリッシャーのデータ型マッピングの指定](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
