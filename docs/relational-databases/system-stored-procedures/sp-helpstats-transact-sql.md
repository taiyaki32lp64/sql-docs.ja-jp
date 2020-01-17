---
title: sp_helpstats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpstats
- sp_helpstats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpstats
ms.assetid: 00ab3cfd-2736-4fc0-b1b2-16dd49fb2fe5
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fba09255204b796a5134e8b8098e650430b7de63
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048408"
---
# <a name="sphelpstats-transact-sql"></a>sp_helpstats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定したテーブルの列およびインデックスに関する統計を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] 統計に関する情報を取得するクエリ、 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)と[sys.stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)カタログ ビューです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpstats[ @objname = ] 'object_name'   
     [ , [ @results = ] 'value' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'object_name'` 統計情報を提供する対象のテーブルを指定します。 *object_name*は**nvarchar (520)** null にすることはできません。 1 つまたは 2 つの部分で構成される名前を指定できます。  
  
`[ @results = ] 'value'` 提供情報の範囲を指定します。 有効なエントリは**すべて**と**STATS**します。 **すべて**すべてのインデックスとも; 作例された統計がある列の統計情報を一覧表示されます。**STATS**インデックスに関連付けられていない統計のみを表示します。 *値*は**nvarchar (5)** 既定値は STATS です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の表では、結果セットの列について説明します。  
  
|列名|説明|  
|-----------------|-----------------|  
|**statistics_name**|統計の名前。 返します**sysname** null にすることはできません。|  
|**statistics_keys**|統計情報の基になるキー。 返します**nvarchar (2078)** null にすることはできません。|  
  
## <a name="remarks"></a>コメント  
 特定のインデックスまたは統計に関する詳細な統計情報を表示するのにには、DBCC SHOW_STATISTICS を使用します。 詳細については、次を参照してください。 [DBCC SHOW_STATISTICS &#40;TRANSACT-SQL&#41; ](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)と[sp_helpindex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`sp_createstats` を実行し、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内のすべてのユーザー テーブルを対象にして、条件を満たすすべての列に関する統計を 1 列ずつ作成します。 次に、`sp_helpstats`で作成された結果統計を検索するために実行、`Customer`テーブル。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_createstats;  
GO  
EXEC sp_helpstats   
@objname = 'Sales.Customer',  
@results = 'ALL';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `statistics_name               statistics_keys`  
  
 `----------------------------  ----------------`  
  
 `_WA_Sys_00000003_22AA2996     AccountNumber`  
  
 `AK_Customer_AccountNumber     AccountNumber`  
  
 `AK_Customer_rowguid           rowguid`  
  
 `CustomerType                  CustomerType`  
  
 `IX_Customer_TerritoryID       TerritoryID`  
  
 `ModifiedDate                  ModifiedDate`  
  
 `PK_Customer_CustomerID        CustomerID`  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
