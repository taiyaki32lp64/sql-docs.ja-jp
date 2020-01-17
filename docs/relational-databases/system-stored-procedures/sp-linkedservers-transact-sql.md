---
title: sp_linkedservers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_linkedservers
- sp_linkedservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_linkedservers
ms.assetid: d8f82f78-8a1f-4831-bcee-7c36c6e7dfbb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 675707453fbc79f3f9c578469ed5e78b73d2fbfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139830"
---
# <a name="splinkedservers-transact-sql"></a>sp_linkedservers (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ローカル サーバーに定義されているリンク サーバーの一覧を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_linkedservers  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 0 以外の値の数 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**SRV_NAME**|**sysname**|リンク サーバーの名前|  
|**SRV_PROVIDERNAME**|**nvarchar(** 128 **)**|指定したリンク サーバーへのアクセスを管理する OLE DB プロバイダーのフレンドリ名。|  
|**SRV_PRODUCT**|**nvarchar(** 128 **)**|リンク サーバーの製品名。|  
|**SRV_DATASOURCE**|**nvarchar(** 4000 **)**|指定したリンク サーバーに対応する OLE DB データ ソース プロパティ。|  
|**SRV_PROVIDERSTRING**|**nvarchar(** 4000 **)**|リンク サーバーに対応する OLE DB プロバイダーの文字列プロパティ。|  
|**SRV_LOCATION**|**nvarchar(** 4000 **)**|指定したリンク サーバーに対応する OLE DB の場所のプロパティ。|  
|**SRV_CAT**|**sysname**|指定したリンク サーバーに対応する OLE DB カタログのプロパティ。|  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [sp_catalogs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_columns_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_foreignkeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_primarykeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_table_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [sp_tables_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [分散クエリ ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
