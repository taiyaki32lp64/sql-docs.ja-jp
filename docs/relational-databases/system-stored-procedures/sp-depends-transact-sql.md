---
title: sp_depends (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_depends
- sp_depends_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_depends
ms.assetid: d9934590-c6ae-4936-91c3-146055ef2c57
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9ee6b9df37e61dcb4eed45bc11431d49b160cf87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053104"
---
# <a name="spdepends-transact-sql"></a>sp_depends (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース オブジェクト依存関係のビューとテーブルまたはビューと、テーブルとビューが従属するビューまたはプロシージャに依存する手順などに関する情報が表示されます。 現在のデータベース内に存在しないオブジェクトへの参照はレポートされません。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)と[sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_depends [ @objname = ] '<object>'   
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name.  
    object_name  
}  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 データベースの名前です。  
  
 *schema_name*  
 オブジェクトが所属するスキーマの名前を指定します。  
  
 *object_name*  
 依存関係を確認するデータベース オブジェクトです。 オブジェクトは、テーブル、ビュー、ストアド プロシージャ、ユーザー定義関数、またはトリガーできます。 o*bject_name*は**nvarchar (776)** 、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 **sp_depends** 2 つの結果セットが表示されます。  
  
 次の結果セットをオブジェクトを表示する *\<オブジェクト >* によって異なります。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(257** **)**|依存関係が存在する項目の名前。|  
|**type**|**nvarchar(16)**|項目の種類。|  
|**更新**|**nvarchar(7)**|項目を更新するかどうか。|  
|**選択されています。**|**nvarchar(8)**|かどうか、項目は、SELECT ステートメントで使用されます。|  
|**column**|**sysname**|従属性が存在する列またはパラメーター。|  
  
 次の結果セットに依存するオブジェクトを表示する *\<オブジェクト >* します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(257** **)**|依存関係が存在する項目の名前。|  
|**type**|**nvarchar(16)**|項目の種類。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-dependencies-on-a-table"></a>A. テーブルの従属性を一覧表示する  
 次の例に依存するデータベース オブジェクトを一覧表示、`Sales.Customer`テーブルに、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]データベース。 ここではスキーマ名とテーブル名の両方を指定します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_depends @objname = N'Sales.Customer' ;  
```  
  
### <a name="b-listing-dependencies-on-a-trigger"></a>B. トリガーの従属性を一覧表示する  
 次の例では、対象のデータベース オブジェクトを表示するトリガー`iWorkOrder`によって異なります。  
  
```  
EXEC sp_depends @objname = N'AdventureWorks2012.Production.iWorkOrder' ;  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sql_dependencies &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
