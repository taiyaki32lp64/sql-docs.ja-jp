---
title: sp_dbmmonitordropalert (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitordropalert_TSQL
- sp_dbmmonitordropalert
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], monitoring
- sp_dbmmonitordropalert
ms.assetid: fe4a134b-25bf-464e-a5c4-358de215b65a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4776e043505c787e74c9cecf766325d189c4f702
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108124"
---
# <a name="spdbmmonitordropalert-transact-sql"></a>sp_dbmmonitordropalert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  しきい値を NULL に設定することにより、指定されたパフォーマンス基準に対する警告を削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbmmonitordropalert database_name   
    [ , alert_id ]   
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 警告しきい値の削除の対象となるデータベースを指定します。  
  
 *alert_id*  
 削除する警告を識別する整数値を指定します。 この引数を省略した場合は、データベースのすべての警告が削除されます。 指定したパフォーマンス基準に対する警告を削除するには、次のいずれかの値を指定します。  
  
|値|パフォーマンス基準|警告しきい値|  
|-----------|------------------------|-----------------------|  
|1|最も古い未送信のトランザクション|送信キュー内にトランザクションを累積できる時間 (分単位) を指定します。この時間を経過すると、プリンシパル サーバー インスタンスで警告が生成されます。 この警告を使用すると、時間的な面からデータ損失の可能性を判断できます。この警告は特に高パフォーマンス モードに関係しますが、 パートナーとの通信が切断されたためにミラーリングが一時停止または中断している場合は、高安全モードにも関係します。|  
|2|未送信のログ|未送信のログのサイズ (KB) を指定します。このサイズを超えると、プリンシパル サーバー インスタンスで警告が生成されます。 この警告を使用すると、KB の面からデータ損失の可能性を判断できます。この警告は特に高パフォーマンス モードに関係しますが、 パートナーとの通信が切断されたためにミラーリングが一時停止または中断している場合は、高安全モードにも関係します。|  
|3|未復元のログ|未復元のログのサイズ (KB) を指定します。このサイズを超えると、ミラー サーバー インスタンスで警告が生成されます。 この警告を使用すると、フェールオーバー時間を判断できます。 *フェールオーバー時間* の大部分は、以前のミラー サーバーの再実行キューに残っているログをロールフォワードする場合に必要となる時間です。この時間にわずかな時間を加えます。|  
|4|ミラー コミットのオーバーヘッド|許容可能な、トランザクションあたりの平均遅延時間 (ミリ秒単位) を指定します。この時間を経過すると、プリンシパル サーバーで警告が生成されます。 この遅延時間は、ミラー サーバー インスタンスによってトランザクションのログ レコードが再実行キューに書き込まれるのをプリンシパル サーバー インスタンスが待機している間、発生したオーバーヘッドの量になります。 この値は高安全モードにのみ関係します。|  
|5|保有期間|データベース ミラーリングの状態テーブルにある行の保有期間を制御するメタデータです。|  
  
> [!NOTE]  
>  このプロシージャを使用して指定されているされたかどうかにかかわらず、警告のしきい値を削除する**sp_dbmmonitorchangealert**またはデータベース ミラーリング モニター。  
  
 警告に対応するイベント Id については、次を参照してください。[使用量の警告しきい値とアラートをミラーリング パフォーマンス基準&#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、保有期間の設定の削除、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]データベース。  
  
```  
EXEC sp_dbmmonitordropalert AdventureWorks2012, 5;  
```  
  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの保有期間とすべての警告しきい値を削除します。  
  
```  
EXEC sp_dbmmonitordropalert AdventureWorks2012 ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)  
  
  
