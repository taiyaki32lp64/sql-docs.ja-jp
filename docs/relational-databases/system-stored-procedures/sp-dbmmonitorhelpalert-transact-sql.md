---
title: sp_dbmmonitorhelpalert (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorhelpalert_TSQL
- sp_dbmmonitorhelpalert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorhelpalert
- database mirroring [SQL Server], monitoring
ms.assetid: 43911660-b4e4-4934-8c02-35221160aaec
author: stevestein
ms.author: sstein
ms.openlocfilehash: fc850c8be9b5222fe178563de78e34e2ba263c12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899188"
---
# <a name="spdbmmonitorhelpalert-transact-sql"></a>sp_dbmmonitorhelpalert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース ミラーリング監視の主要なパフォーマンス基準の 1 つまたはすべてについて、警告しきい値に関する情報を返します。  
 
  ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbmmonitorhelpalert database_name   
    [ , alert_id ]   
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 データベースを指定します。  
  
 [ *alert_id* ]  
 返す警告を識別する整数値を指定します。 この引数を省略すると、保有期間以外のすべての警告が返されます。  
  
 特定の警告を返すには、次のいずれかの値を指定します。  
  
|値|パフォーマンス基準|警告しきい値|  
|-----------|------------------------|-----------------------|  
|1|最も古い未送信のトランザクション|送信キュー内にトランザクションを累積できる時間 (分単位) を指定します。この時間を経過すると、プリンシパル サーバー インスタンスで警告が生成されます。 この警告を使用すると、時間的な面からデータ損失の可能性を判断できます。この警告は特に高パフォーマンス モードに関係しますが、 パートナーとの通信が切断されたためにミラーリングが一時停止または中断している場合は、高安全モードにも関係します。|  
|2|未送信のログ|未送信のログのサイズ (KB) を指定します。このサイズを超えると、プリンシパル サーバー インスタンスで警告が生成されます。 この警告を使用すると、KB の面からデータ損失の可能性を判断できます。この警告は特に高パフォーマンス モードに関係しますが、 パートナーとの通信が切断されたためにミラーリングが一時停止または中断している場合は、高安全モードにも関係します。|  
|3|未復元のログ|未復元のログのサイズ (KB) を指定します。このサイズを超えると、ミラー サーバー インスタンスで警告が生成されます。 この警告を使用すると、フェールオーバー時間を判断できます。 *フェールオーバー時間* の大部分は、以前のミラー サーバーの再実行キューに残っているログをロールフォワードする場合に必要となる時間です。この時間にわずかな時間を加えます。|  
|4|ミラー コミットのオーバーヘッド|許容可能な、トランザクションあたりの平均遅延時間 (ミリ秒単位) を指定します。この時間を経過すると、プリンシパル サーバーで警告が生成されます。 この遅延時間は、ミラー サーバー インスタンスによってトランザクションのログ レコードが再実行キューに書き込まれるのをプリンシパル サーバー インスタンスが待機している間、発生したオーバーヘッドの量になります。 この値は高安全モードにのみ関係します。|  
|5|保有期間|データベース ミラーリングの状態テーブルにある行の保有期間を制御するメタデータです。|  
  
 警告に対応するイベント Id については、次を参照してください。[使用量の警告しきい値とアラートをミラーリング パフォーマンス基準&#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 警告ごとに、次の列を含む行を返します。  
  
|[列]|データ型|説明|  
|------------|---------------|-----------------|  
|**alert_id**|**int**|次の表、 **alert_id**各パフォーマンス基準とに表示されるメトリックの測定単位の値、 **sp_dbmmonitorresults**結果セット。|  
|**threshold**|**int**|警告しきい値を指定します。 ミラーリングの状態が更新されたときに、このしきい値より大きな値が返されると、Windows のイベント ログにエントリが作成されます。 この値は、警告に応じて、KB、分、またはミリ秒となります。 現在しきい値が設定されていない場合、値は NULL です。<br /><br /> **注:** 現在の値を表示するには、実行、 [sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)ストアド プロシージャ。|  
|**enabled**|**bit**|0 = イベントは無効です。<br /><br /> 1 = イベントは有効です。<br /><br /> **注:** 保有期間は常に有効になります。|  
  
|[値]|パフォーマンス基準|ユニット|  
|-----------|------------------------|----------|  
|1|最も古い未送信のトランザクション|Minutes|  
|2|未送信のログ|KB|  
|3|未復元のログ|KB|  
|4|ミラー コミットのオーバーヘッド|ミリ秒|  
|5|保有期間|Hours|  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースにある最も古い未送信のトランザクションのパフォーマンス基準に対し、警告が有効になっているかどうかを示す行を返します。  
  
```  
EXEC sp_dbmmonitorhelpalert AdventureWorks2012, 1 ;  
```  
  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースにあるパフォーマンス基準ごとに、基準が有効になっているかどうかを示す行を返します。  
  
```  
EXEC sp_dbmmonitorhelpalert AdventureWorks2012;  
```  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [sp_dbmmonitorchangemonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
