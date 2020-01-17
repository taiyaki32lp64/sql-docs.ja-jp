---
title: sp_help_fulltext_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables
- sp_help_fulltext_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables
ms.assetid: 86e24a5f-a869-43f6-b83e-c52b7b01b5ff
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4ac8e09eff53c04377ccd48a47cc31d9d7ddc5e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055019"
---
# <a name="sphelpfulltexttables-transact-sql"></a>sp_help_fulltext_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  フルテキスト インデックス作成のために登録されているテーブルの一覧を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用**sys.fulltext_indexes**カタログ ビューを代わりにします。 詳細については、次を参照してください。 [sys.fulltext_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_fulltext_tables [ [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'` フルテキスト カタログの名前です。 *fulltext_catalog_name*は**sysname**、既定値は NULL です。 場合*fulltext_catalog_name*を省略するかが null の場合、データベースに関連付けられているすべてのフルテキスト インデックス付きのテーブルが返されます。 場合*fulltext_catalog_name*が指定されているが、 *table_name*を省略するかが null の場合、このカタログに関連付けられているすべてのフルテキスト インデックス付きテーブルについて、フルテキスト インデックス情報を取得します。 両方*fulltext_catalog_name*と*table_name*指定する場合、行が返されます*table_name*に関連付けられている*fulltext_catalog_name*;それ以外の場合、エラーが発生します。  
  
`[ @table_name = ] 'table_name'` フルテキスト メタデータが要求される 1 つまたは 2 つの部分のテーブルの名前です。 *table_name*は**nvarchar (517)** 既定値は NULL です。 だけの場合*table_name*指定すると、関連する行のみ*table_name*が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または (1) の失敗  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|テーブル所有者 これは、テーブルを作成したデータベース ユーザーの名前です。|  
|**TABLE_NAME**|**sysname**|テーブル名です。|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|一意のキー列として指定された列に UNIQUE 制約を課すインデックス。|  
|**FULLTEXT_KEY_COLID**|**int**|FULLTEXT_KEY_NAME で指定された一意のインデックスの列 ID。|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|このテーブルでフルテキスト インデックス作成のマークが付いている列がクエリに適しているかどうか。<br /><br /> 0 = 非アクティブ<br /><br /> 1 = アクティブ|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|フルテキスト カタログがフルテキスト インデックス データが存在します。|  
  
## <a name="permissions"></a>アクセス許可  
 実行権限は、既定のメンバーに、**パブリック**ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、フルテキスト カタログ `Cat_Desc` に関連付けられた、フルテキスト インデックスが作成されているテーブルの名前を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_tables 'Cat_Desc';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_fulltext_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
