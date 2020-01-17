---
title: sp_dbmmonitorupdate (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorupdate
- sp_dbmmonitorupdate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorupdate
- database mirroring [SQL Server], monitoring
ms.assetid: 9ceb9611-4929-44ee-a406-c39ba2720fd5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 190b4f0598afa6d434b5dada8c8464cb8209dac7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061259"
---
# <a name="spdbmmonitorupdate-transact-sql"></a>sp_dbmmonitorupdate (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース ミラーリング監視の状態テーブルにミラー化されたデータベースごとの新しい行を挿入し、現在の保有期間より古い行を切り捨てます。 既定の保有期間は、7 日 (168 時間) です。 テーブルを更新するときに**sp_dbmmonitorupdate**パフォーマンス基準を評価します。  
  
> [!NOTE]  
>  初めて**sp_dbmmonitorupdate**実行されると、データベース ミラーリング状態テーブルを作成、 **dbm_monitor**固定データベース ロール、 **msdb**データベース。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbmmonitorupdate [ database_name ]  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 ミラーリングの状態を更新するデータベースの名前を指定します。 場合*database_name*が指定されていない、サーバー インスタンス上のミラー化されたデータベースごとに状態テーブルが更新されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **sp_dbmmonitorupdate**のコンテキストでのみ実行できる、 **msdb**データベース。  
  
 状態テーブルの列がパートナーのロールに該当しない場合、そのパートナーについて、値は NULL になります。 関連情報が利用できない場合、ように、フェールオーバーまたはサーバーの再起動中に、列は NULL 値もがあります。  
  
 後**sp_dbmmonitorupdate**作成、 **dbm_monitor**固定データベース ロール、 **msdb**のメンバー、 **sysadmin**すべてのユーザーを追加できるは、固定サーバー ロール、 **dbm_monitor**固定データベース ロール。 **Dbm_monitor**役割は、データベース ミラーリングの状態を表示がない更新しますが、ない表示または構成するデータベース ミラーリング イベントは、そのメンバーを使用できます。  
  
 データベースのミラーリングの状態を更新するときに**sp_dbmmonitorupdate**をミラーリングのパフォーマンス測定基準の警告しきい値が指定されている最新の値を検査します。 値がしきい値を超えている場合は情報イベントをイベント ログに追加します。 すべての料金は、前回の更新の平均です。 詳細については、「 [ミラーリング パフォーマンス基準の警告しきい値および警告の使用 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに対してのみ、ミラーリングの状態を更新します。  
  
```  
USE msdb;  
EXEC sp_dbmmonitorupdate AdventureWorks2012 ;  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [sp_dbmmonitorchangemonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [sp_dbmmonitorhelpalert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
