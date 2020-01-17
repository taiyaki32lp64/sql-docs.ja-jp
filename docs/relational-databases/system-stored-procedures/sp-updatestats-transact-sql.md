---
title: sp_updatestats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c00bdd453bc4d1bf467b37aca3639eb43f55e022
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085791"
---
# <a name="spupdatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

実行`UPDATE STATISTICS`に対する現在のデータベース内のすべてのユーザー定義および内部テーブルです。  
  
詳細については`UPDATE STATISTICS`を参照してください[UPDATE STATISTICS &#40;TRANSACT-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)します。 統計の詳細については、「[統計](../../relational-databases/statistics/statistics.md)」を参照してください。  
    
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="arguments"></a>引数  
`[ @resample = ] 'resample'` 指定します**sp_updatestats**の RESAMPLE オプションを使用、 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md)ステートメント。 場合 **'resample'** が指定されていない**sp_updatestats**既定のサンプリングを使用して統計を更新します。 **リサンプル**、 **varchar(8)** を既定値は [いいえ]  
  
## <a name="remarks"></a>コメント  
 **sp_updatestats**実行`UPDATE STATISTICS`、指定することによって、`ALL`データベース内のすべてのユーザー定義および内部テーブルでのキーワード。 sp_updatestats は、その進行状況を示すメッセージが表示されます。 更新が完了したら、すべてのテーブルの統計情報が更新されたことを報告します。  
  
sp_updatestats は、無効化された非クラスター化インデックスの統計を更新し、無効になっているクラスター化インデックスの統計を更新できません。  
  
ディスク ベース テーブルでは、 **sp_updatestats**に基づいて統計を更新、 **modification_counter**内の情報、 **sys.dm_db_stats_properties**カタログ ビュー少なくとも 1 つの行が変更されている統計を更新しています。 実行するときに常にメモリ最適化テーブルで統計が更新される**sp_updatestats**します。 実行されません**sp_updatestats**以上必要です。  
  
**sp_updatestats**ストアド プロシージャやその他のコンパイル済みコードの再コンパイルをトリガーできます。 ただし、 **sp_updatestats** 1 つのクエリ プランが参照されているテーブルやインデックスに対するだけの場合、再コンパイルをされない可能性があります。 このような場合は、統計が更新されても再コンパイルの必要はありません。  
  
実行 90 未満の互換性レベル データベースについて**sp_updatestats**は特定の統計に対する最新の NORECOMPUTE 設定は保持されません。 互換性レベルが 90 以上のデータベースは、sp_updatestats は特定の統計に対する最新の NORECOMPUTE オプションを保持します。 統計の更新の無効化および再有効化について詳しくは、「[統計](../../relational-databases/statistics/statistics.md)」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**固定サーバー ロール、またはデータベースの所有権 (**dbo**)。  

## <a name="examples"></a>使用例  
内のテーブルの統計情報を更新する例を次の[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]データベースです。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  

## <a name="automatic-index-and-statistics-management"></a>インデックスと統計の自動管理
[Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) のようなソリューションを活用し、1 つまたは複数のデータベースに対するインデックスの最適化と統計更新を自動管理します。 このプロシージャでは、断片化レベルやその他のパラメーターに基づいてインデックスを再構築または再構成するか、線形しきい値で統計を更新するかが自動的に選択されます。

## <a name="see-also"></a>関連項目  
 [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [システム ストアド プロシージャ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
 
