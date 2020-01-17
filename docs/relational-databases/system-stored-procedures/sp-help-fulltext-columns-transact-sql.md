---
title: 照会する (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns
- sp_help_fulltext_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns
ms.assetid: 92c8656b-f7fd-4904-9796-acc9ffed4106
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8009c9d2aa5f4b8f8be873633420bd1b088ece16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055093"
---
# <a name="sphelpfulltextcolumns-transact-sql"></a>照会する (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  フルテキスト インデックス作成用として指定された列を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用して、 [sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)カタログ ビューを代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_fulltext_columns [ [ @table_name = ] 'table_name' ] ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_name = ] 'table\_name'` フルテキスト インデックス情報を要求する対象の 1 つまたは 2 部テーブルの名前です。 *table_name*は**nvarchar (517)** 既定値は NULL です。 場合*table_name*を省略すると、すべてのフルテキスト インデックス付きテーブルのフルテキスト インデックス列情報を取得します。  
  
`[ @column_name = ] 'column\_name'` フルテキスト インデックスのメタデータを要求する対象の列の名前です。 *column_name*は**sysname**既定値は NULL です。 場合*column_name*を省略するかが null の場合のすべてのフルテキスト インデックス付き列のフルテキスト列情報が返されます*table_name*します。 場合*table_name*はも省略するかが null の場合、データベース内のすべてのテーブルのすべてのフルテキスト インデックス付き列のフルテキスト インデックス列情報が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または (1) の失敗  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|テーブル所有者 これは、テーブルを作成したデータベース ユーザーの名前です。|  
|**TABLE_ID**|**int**|テーブルの ID。|  
|**TABLE_NAME**|**sysname**|テーブルの名前。|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|インデックス作成のために指定されているフルテキスト インデックス付きテーブルの列。|  
|**FULLTEXT_COLID**|**int**|フルテキスト インデックスが作成された列の列 ID。|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|フルテキスト インデックスが作成されたテーブル内の列で、フルテキスト インデックス列のドキュメントの種類を指定する列。 この値は、フルテキスト インデックス列がときにのみ適用されます、 **varbinary (max)** または**イメージ**列。|  
|**FULLTEXT_BLOBTP_COLID**|**int**|ドキュメント型の列の列 ID。 この値は、フルテキスト インデックス列がときにのみ適用されます、 **varbinary (max)** または**イメージ**列。|  
|**FULLTEXT_LANGUAGE**|**sysname**|列のフルテキスト検索に使用される言語です。|  
  
## <a name="permissions"></a>アクセス許可  
 実行権限は、既定のメンバーに、**パブリック**ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、`Document` テーブルでフルテキスト インデックス作成用に指定された列に関する情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_columns 'Production.Document';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
