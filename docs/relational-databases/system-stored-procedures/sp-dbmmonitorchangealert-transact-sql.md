---
title: sp_dbmmonitorchangealert (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorchangealert_TSQL
- sp_dbmmonitorchangealert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorchangealert
- database mirroring [SQL Server], monitoring
ms.assetid: 1b29f82b-9cf8-4539-8d5c-9a1024db8a50
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2749e964b33179d5bf87ee6d464d251c14ee82d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108145"
---
# <a name="spdbmmonitorchangealert-transact-sql"></a>sp_dbmmonitorchangealert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したミラーリングのパフォーマンス基準に対する警告しきい値を追加または変更します。  

  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbmmonitorchangealert database_name   
    , alert_id   
    , alert_threshold   
    , enabled   
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 警告しきい値の追加や変更の対象となるデータベースを指定します。  
  
 *alert_id*  
 追加または変更する警告を識別する整数値を指定します。 次のいずれかの値を指定します。  
  
|値|パフォーマンス基準|警告しきい値|  
|-----------|------------------------|-----------------------|  
|1|最も古い未送信のトランザクション|送信キュー内にトランザクションを累積できる時間 (分単位) を指定します。この時間を経過すると、プリンシパル サーバー インスタンスで警告が生成されます。 この警告を使用すると、時間的な面からデータ損失の可能性を判断できます。この警告は特に高パフォーマンス モードに関係しますが、 パートナーとの通信が切断されたためにミラーリングが一時停止または中断している場合は、高安全モードにも関係します。|  
|2|未送信のログ|未送信のログのサイズ (KB) を指定します。このサイズを超えると、プリンシパル サーバー インスタンスで警告が生成されます。 この警告を使用すると、KB の面からデータ損失の可能性を判断できます。この警告は特に高パフォーマンス モードに関係しますが、 パートナーとの通信が切断されたためにミラーリングが一時停止または中断している場合は、高安全モードにも関係します。|  
|3|未復元のログ|未復元のログのサイズ (KB) を指定します。このサイズを超えると、ミラー サーバー インスタンスで警告が生成されます。 この警告を使用すると、フェールオーバー時間を判断できます。 *フェールオーバー時間* の大部分は、以前のミラー サーバーの再実行キューに残っているログをロールフォワードする場合に必要となる時間です。この時間にわずかな時間を加えます。|  
|4|ミラー コミットのオーバーヘッド|許容可能な、トランザクションあたりの平均遅延時間 (ミリ秒単位) を指定します。この時間を経過すると、プリンシパル サーバーで警告が生成されます。 この遅延時間は、ミラー サーバー インスタンスによってトランザクションのログ レコードが再実行キューに書き込まれるのをプリンシパル サーバー インスタンスが待機している間、発生したオーバーヘッドの量になります。 この値は高安全モードにのみ関係します。|  
|5|保有期間|データベース ミラーリングの状態テーブルにある行の保有期間を制御するメタデータです。|  
  
 警告に対応するイベント Id については、次を参照してください。[使用量の警告しきい値とアラートをミラーリング パフォーマンス基準&#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)します。  
  
 *alert_threshold*  
 警告しきい値を指定します。 ミラーリングの状態が更新されたときに、このしきい値より大きな値が返されると、Windows のイベント ログにエントリが作成されます。 この値は、パフォーマンス基準に応じて、KB、分、またはミリ秒となります。  
  
> [!NOTE]  
>  現在の値を表示するには、実行、 [sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)ストアド プロシージャ。  
  
 *enabled*  
 警告が有効かどうかを指定します。  
  
 0 = 警告は無効です。  
  
 1 = 警告は有効です。  
  
> [!NOTE]  
>  保有期間は常に有効になります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースについて、各パフォーマンス基準のしきい値と保有期間を設定します。 この例で使用する値を次の表に示します。  
  
|*alert_id*|パフォーマンス基準|警告しきい値|警告が有効かどうかを指定します。|  
|-----------------|------------------------|-----------------------|-----------------------------|  
|1|最も古い未送信のトランザクション|30 分|はい|  
|2|未送信のログ|10,000 KB|はい|  
|3|未復元のログ|10,000 KB|はい|  
|4|ミラー コミットのオーバーヘッド|1,000 ミリ秒|いいえ|  
|5|保有期間|8 時間|はい|  
  
```  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 1, 30, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 2, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 3, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 4, 1000, 0 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 5, 8, 1 ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorhelpalert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
  
