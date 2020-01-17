---
title: core.sp_remove_collector_type (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_remove_collector_type
- sp_remove_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- core.sp_remove_collector_type stored procedure
- management data warehouse, data collector stored procedures
- sp_remove_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 88ceba25-e41a-405f-a416-bb68918a0024
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9c2b3bf93abd6acfad699f47344f05ddbc34e85a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942475"
---
# <a name="corespremovecollectortype-transact-sql"></a>core.sp_remove_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  管理データ ウェアハウス データベースの core.supported_collector_types ビューからエントリを削除します。 管理データ ウェアハウス データベースのコンテキストでプロシージャを実行する必要があります。  
  
 core.supported_collector_types ビューには、管理データ ウェアハウスにデータをアップロードできる登録済みのコレクター型が表示されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
core.sp_remove_collector_type [ @collector_type_uid = ] 'collector_type_uid'  
```  
  
## <a name="arguments"></a>引数  
 [ @collector_type_uid = ] '*collector_type_uid*'  
 コレクター型の GUID を指定します。 *collector_type_uid*は**uniqueidentifier**既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **mdw_admin** (EXECUTE 権限) を持つ固定データベース ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、core.supported_collector_types ビューからジェネリック T-SQL Query コレクター型を削除します。  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @RC int;  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = (SELECT collector_type_uid FROM msdb.dbo.syscollector_collector_types WHERE name = N'Generic T-SQL Query Collector Type');  
EXECUTE @RC = core.sp_remove_collector_type @collector_type_uid;  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [管理データ ウェアハウス](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
