---
title: sp_help_fulltext_catalogs_cursor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalogs_cursor
- sp_help_fulltext_catalogs_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalogs_cursor
ms.assetid: d44478d1-0cc4-415e-9d1a-6dccb64674fa
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 280d5eaf75c8b6775222a1dbde028f74feac842f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055143"
---
# <a name="sphelpfulltextcatalogscursor-transact-sql"></a>sp_help_fulltext_catalogs_cursor (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  カーソルを使用して、ID、名、ルート ディレクトリ、ステータス、および指定したフルテキスト カタログのフルテキスト インデックス付きテーブルの数を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用して、 [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)カタログ ビューを代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_fulltext_catalogs_cursor [ @cursor_return= ] @cursor_variable OUTPUT ,   
     [ @fulltext_catalog_name = ] 'fulltext_catalog_name'   
```  
  
## <a name="arguments"></a>引数  
`[ @cursor_return = ] @cursor_variable OUTPUT` 型の output 変数は、**カーソル**します。 カーソルの読み取り専用で、スクロール可能な動的カーソルです。  
  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'` フルテキスト カタログの名前です。 *fulltext_catalog_name*は**sysname**します。 このパラメーターを省略するか NULL には、現在のデータベースに関連付けられているすべてのフルテキスト カタログに関する情報が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または (1) の失敗  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|フルテキスト カタログ識別子。|  
|**NAME**|**sysname**|フルテキスト カタログの名前。|  
|**PATH**|**nvarchar(260)**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、この句は無効です。|  
|**状態**|**int**|カタログのフルテキスト インデックス作成の状態:<br /><br /> 0 = アイドル状態<br /><br /> 1 = カタログ全体を作成中<br /><br /> 2 = 一時停止<br /><br /> 3 = 絞込み<br /><br /> 4 = 復旧<br /><br /> 5 = シャットダウン<br /><br /> 6 = 増分作成中<br /><br /> 7 = インデックス作成<br /><br /> 8 = ディスク容量不足、 一時停止<br /><br /> 9 = 変更の追跡|  
|**NUMBER_FULLTEXT_TABLES**|**int**|フルテキストの数はインデックス、カタログに関連付けられたテーブルです。|  
  
## <a name="permissions"></a>アクセス許可  
 アクセス許可は既定の実行、**パブリック**ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、フルテキスト カタログ `Cat_Desc` に関する情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_catalogs_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>関連項目  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_catalog &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
