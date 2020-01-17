---
title: sp_refreshview (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refreshview
- sp_refreshview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refreshview
ms.assetid: 9ce1d07c-ee66-4a83-8c73-cd2cc104dd08
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3b8c1b95d8d04e2b11982af14971e43e83db146f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075772"
---
# <a name="sprefreshview-transact-sql"></a>sp_refreshview (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定された非スキーマ バインド ビューのメタデータを更新します。 ビューのメタデータを永続的なは、ビューが依存している基になるオブジェクトが変更されたのため、古くなることができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_refreshview [ @viewname = ] 'viewname'   
```  
  
## <a name="arguments"></a>引数  
`[ @viewname = ] 'viewname'` ビューの名前です。 *viewname*は**nvarchar**、既定値はありません。 *viewname* 、マルチパート識別子を指定できますが、現在のデータベース内のビューに参照できるのみです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 0 以外の値の数 (失敗)  
  
## <a name="remarks"></a>コメント  
 ビューは、schemabinding を指定して作成されていない場合**sp_refreshview**ビューの定義に影響を与える、ビューの基になるオブジェクトに変更されたときに実行する必要があります。 それ以外の場合、ビューは、クエリが実行時に、予期しない結果を生成可能性があります。  
  
## <a name="permissions"></a>アクセス許可  
 ビューに対する ALTER 権限と、共通言語ランタイム (CLR) ユーザー定義型およびビュー列で参照される XML スキーマ コレクションに対する REFERENCES 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-updating-the-metadata-of-a-view"></a>A. ビューのメタデータの更新  
 次の例では、ビュー `Sales.vIndividualCustomer` のメタデータを更新します。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sp_refreshview N'Sales.vIndividualCustomer';  
```  
  
### <a name="b-creating-a-script-that-updates-all-views-that-have-dependencies-on-a-changed-object"></a>B. 変更されたオブジェクトに対する依存関係のあるすべてのビューを更新するスクリプトの作成  
 テーブル `Person.Person` に対して作成された任意のビューの定義に影響を与える形で、このテーブルが変更されたとします。 次の例では、テーブル `Person.Person` に対する依存関係があるすべてのビューについて、メタデータを更新するスクリプトを作成しています。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT 'EXEC sp_refreshview ''' + name + ''''   
FROM sys.objects AS so   
INNER JOIN sys.sql_expression_dependencies AS sed   
    ON so.object_id = sed.referencing_id   
WHERE so.type = 'V' AND sed.referenced_id = OBJECT_ID('Person.Person');  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_refreshsqlmodule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md)  
  
  
