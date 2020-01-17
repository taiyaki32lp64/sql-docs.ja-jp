---
title: MSdatatype_mappings (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: ee1a0cc83b55fc265ae2bb490fd9d5e11fd73f22
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129620"
---
# <a name="msdatatype_mappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdatatype_mappings**ビューでは、SQL Server データ型を SQL Server 以外のデータベース管理システム (DBMS) によって使用されるデータ型にマップします。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|DBMS の名前です。 使用可能な値とその説明を次に示します。<br /><br /> **MSSQLSERVER**:変換先は、SQL Server データベースです。<br />**ORACLE**:変換先は、Oracle データベースです。<br />**DB2**:マップ先は IBM DB2 データベース。<br />**SYBASE**:変換先は、Sybase データベース。|  
|**sql_type**|**nvarchar(128)**|SQL Server のデータ型です。|  
|**dest_type**|**nvarchar(128)**|SQL Server 以外のデータ型の名前です。|  
|**dest_prec**|**bigint**|SQL Server 以外のデータ型の有効桁数です。|  
|**dest_create_params**|**int**|内部使用のみです。|  
|**dest_nullable**|**bit**|SQL Server 以外のデータ型が NULL 値をサポートするかどうかです。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle パブリッシャーのデータ型マッピングの指定](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
