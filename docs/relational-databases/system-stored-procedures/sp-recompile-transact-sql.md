---
title: sp_recompile (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_recompile_TSQL
- sp_recompile
dev_langs:
- TSQL
helpviewer_keywords:
- sp_recompile
ms.assetid: 6192ca87-febd-4075-8199-14b4fa609b8c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f9b72c1a97c17f975144ad0fd364260afab1fb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002566"
---
# <a name="sprecompile-transact-sql"></a>sp_recompile (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  ストアド プロシージャ、トリガー、およびユーザー定義関数が次回実行時に再コンパイルされるようにします。 これは、次回作成する新しいプランをプロシージャ キャッシュから既存のプランを削除することにより、プロシージャまたはトリガーが実行されます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] コレクションでは、SP:Recompile イベントではなく SP:CacheInsert イベントがログに記録されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
  
sp_recompile [ @objname = ] 'object'  
```  
  
## <a name="arguments"></a>引数  
 [ @objname=] '*オブジェクト*'  
 現在のデータベースにあるストアド プロシージャ、トリガー、テーブル、ビュー、またはユーザー定義関数の修飾名または非修飾名を指定します。 *オブジェクト*は**nvarchar (776)** 、既定値はありません。 場合*オブジェクト*ストアド プロシージャ、トリガー、またはユーザー定義関数、ストアド プロシージャ、トリガーの名前を指定しますまたは、次回実行する関数を再コンパイルされます。 場合*オブジェクト*テーブルまたはビューでは、すべてのストアド プロシージャ、トリガーの名前を指定しますまたは、次回実行されるテーブルまたはビューを参照するユーザー定義関数を再コンパイルされます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 0 以外の値の数 (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_recompile は、現在のデータベース内でのみオブジェクトを検索します。  
  
 ストアド プロシージャ、トリガー、およびユーザー定義関数が使用するクエリは、コンパイル時にだけ最適化されます。 データベースにインデックスを追加したり、変更を加えたりすると、統計が変化するため、コンパイルされたストアド プロシージャ、トリガー、およびユーザー定義関数の効率が低下する場合があります。 そのテーブルに作用するストアド プロシージャやトリガーを再コンパイルすることにより、クエリを再び最適化できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自動的にこれを行うことをお勧めときにストアド プロシージャ、トリガー、およびユーザー定義関数を再コンパイルします。  
  
## <a name="permissions"></a>アクセス許可  
 指定したオブジェクトに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`Customer` テーブルを対象とするストアド プロシージャ、トリガー、およびユーザー定義関数が次回実行時に再コンパイルされます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
