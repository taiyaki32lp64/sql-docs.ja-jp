---
title: メモリ不足の問題の解決 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e31f36624e8923722612810836df5d2a57b6b686
ms.sourcegitcommit: 9af07bd57b76a34d3447e9e15f8bd3b17709140a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624406"
---
# <a name="resolve-out-of-memory-issues"></a>メモリ不足の問題の解決
  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] では、さまざまな形で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]より多くのメモリが使用されます。 インストールして [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 用に割り当てたメモリ量が、ニーズの拡大に合わなくなる場合があります。 その場合は、メモリが不足する可能性があります。 このトピックでは、OOM 状態から回復する方法について説明します。 多数の OOM 状態を回避するのに役立つガイドについては、「 [メモリ使用量の監視とトラブルシューティング](monitor-and-troubleshoot-memory-usage.md) 」を参照してください。  
  
## <a name="covered-in-this-topic"></a>このトピックの内容  
  
|トピック|概要|  
|-----------|--------------|  
| [OOM によるデータベース復元の障害を解決する](#resolve-database-restore-failures-due-to-oom) |"リソース プール ' *\<resourcePoolName>* ' 内のメモリ不足が原因で、データベース ' *\<databaseName>* ' の復元操作に失敗しました" というエラー メッセージが表示された場合の対処方法。|  
| [低メモリまたは OOM 状態によるワークロードへの影響を解決する](#resolve-impact-of-low-memory-or-oom-conditions-on-the-workload)|低メモリの問題によるパフォーマンス低下が見つかった場合の対処方法。|  
| [十分なメモリがある状況でのメモリ不足によるページの割り当てエラーを解決する](#resolve-page-allocation-failures-due-to-insufficient-memory-when-sufficient-memory-is-available) |"リソース プール ' *\<resourcePoolName>* ' のメモリが不足しているため、データベース ' *\<databaseName>* ' のページ割り当ては禁止されています" というエラー メッセージが表示された場合の対処方法。 ..." というエラー メッセージが発生した場合の対処方法。|  
  
## <a name="resolve-database-restore-failures-due-to-oom"></a>OOM によるデータベース復元の障害を解決する  
 データベースを復元しようとしたときに、エラー メッセージを表示する可能性があります。"復元操作に失敗しました ' *\<databaseName >* 'により、リソース プールでメモリ不足' *\<resourcePoolName >* '."データベースを正しく復元するには、先に使用可能なメモリを増やして、メモリ不足の問題を解決する必要があります。  
  
 OOM による復旧エラーを解決するには、次の方法のいずれかまたはすべてを使用して、復旧操作で使用できるメモリを一時的に増やします。  
  
-   実行中のアプリケーションを一時的に閉じます。   
    Visual Studio、Internet Explorer、OneNote など、実行中のアプリケーションを 1 つ以上閉じることにより、これらのアプリケーションによって使用されていたメモリを復元操作で使用できるようになります。 閉じたアプリケーションは、復元操作の正常完了後に再起動できます。  
  
-   MAX_MEMORY_PERCENT の値を増やします。   
    このコード スニペットでは、リソース プール PoolHk の MAX_MEMORY_PERCENT を変更して、インストールされているメモリの 70% に設定します。  
  
    > [!IMPORTANT]  
    >  サーバーが VM 上で実行されており、専用用途ではない場合は、MIN_MEMORY_PERCENT を MAX_MEMORY_PERCENT と同じ値に設定してください。   
    > トピックを参照して[ベスト プラクティス。VM 環境でのインメモリ OLTP を使用して](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)詳細についてはします。  
  
    ```sql  
  
    -- disable resource governor  
    ALTER RESOURCE GOVERNOR DISABLE  
  
    -- change the value of MAX_MEMORY_PERCENT  
    ALTER RESOURCE POOL PoolHk  
    WITH  
         ( MAX_MEMORY_PERCENT = 70 )  
    GO  
  
    -- reconfigure the Resource Governor  
    --    RECONFIGURE enables resource governor  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
  
    ```  
  
     MAX_MEMORY_PERCENT の最大値については、トピックのセクションを参照してください[メモリ最適化テーブルおよびインデックスの使用可能なメモリの割合。](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#percent-of-memory-available-for-memory-optimized-tables-and-indexes)
  
-   **max server memory** を再構成します。  
    **max server memory** の構成については、「[メモリ構成オプションを使用したサーバー パフォーマンスの最適化](https://technet.microsoft.com/library/ms177455\(v=SQL.105\).aspx)」をご覧ください。  
  
## <a name="resolve-impact-of-low-memory-or-oom-conditions-on-the-workload"></a>低メモリまたは OOM 状態によるワークロードへの影響を解決する  
 言うまでもなく、低メモリまたは OOM (メモリ不足) の状態にならないことがベストです。 適切なプラン作成と監視によって、OOM 状態を回避することができます。 ただし、最適なプランを作成しても、実際に起こることを予測できるとは限らず、結果として低メモリまたは OOM の状態になる場合もあります。 OOM からの復旧には、次の 2 段階があります。  
  
1.  [DAC (専用管理者接続) を開く](#open-a-dac-dedicated-administrator-connection) 
  
2.  [修正措置を行う](#take-corrective-action) 
  
### <a name="open-a-dac-dedicated-administrator-connection"></a>DAC (専用管理者接続) を開く  
 Microsoft SQL Server は、専用管理者接続 (DAC) を提供します。 DAC を使用すると、サーバーが他のクライアント接続に応答しない場合でも、SQL Server データベース エンジンの実行中のインスタンスにアクセスして、サーバーの問題をトラブルシューティングすることができます。 DAC は、 `sqlcmd` ユーティリティおよび SQL Server Management Studio (SSMS) を介して利用できます。  
  
 `sqlcmd` および DAC の使用方法については、「 [専用管理者接続の使用](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)」をご覧ください。 SSMS を介して DAC を使用する方法についてを参照してください。[方法。SQL Server Management Studio で専用管理者接続を使用して](https://msdn.microsoft.com/library/ms178068.aspx)します。  
  
### <a name="take-corrective-action"></a>修正措置を行う  
 OOM 状態を解決するには、使用率を削減して既存メモリを解放するか、インメモリ テーブルに使用できるメモリ量を増やす必要があります。  
  
#### <a name="free-up-existing-memory"></a>既存メモリを解放する  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>メモリ最適化テーブルの不要な行を削除し、ガベージ コレクションを待機する  
 メモリ最適化テーブルから、不要な行を削除できます。 ガベージ コレクターによって、これらの行で使用されていたメモリが使用可能メモリに返されます。 . インメモリ OLTP エンジンは、ガベージ行を積極的に回収します。 ただし、実行時間が長いトランザクションではガベージ コレクションが行われないことがあります。 たとえば、5 分間実行されているトランザクションの場合、トランザクションがアクティブな状態で更新操作または削除操作によって作成された行バージョンは、ガベージ コレクションで回収することができません。  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>1 つ以上の行をディスク ベース テーブルに移動する  
 TechNet の次の資料では、メモリ最適化テーブルからディスク ベース テーブルに行を移動する方法について説明しています。  
  
-   [アプリケーション レベルのパーティション分割](https://technet.microsoft.com/library/dn296452\(v=sql.120\).aspx)  
  
-   [メモリ最適化テーブルのパーティション分割に関するアプリケーションのパターン](https://technet.microsoft.com/library/dn133171\(v=sql.120\).aspx)  
  
#### <a name="increase-available-memory"></a>使用可能なメモリを増やす  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>リソース プールの MAX_MEMORY_PERCENT 値を増やす  
 インメモリ テーブル用に名前付きリソース プールを作成していない場合は、作成して [!INCLUDE[hek_2](../../includes/hek-2-md.md)] データベースをバインドします。 [データベースを作成してリソース プールにバインドする方法については、「](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) メモリ最適化テーブルを持つデータベースのリソース プールへのバインド [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 」を参照してください。  
  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] データベースがリソース プールにバインドされている場合は、プールがアクセスできるメモリのパーセントを増やせることがあります。 リソース プールの MIN_MEMORY_PERCENT および MAX_MEMORY_PERCENT の値を変更する方法については、サブトピック「 [既存のプール内での MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT の変更](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#change-min-memory-percent-and-max-memory-percent-on-an-existing-pool) 」をご覧ください。  
  
 MAX_MEMORY_PERCENT の値を増やします。   
このコード スニペットでは、リソース プール PoolHk の MAX_MEMORY_PERCENT を変更して、インストールされているメモリの 70% に設定します。  
  
> [!IMPORTANT]  
>  サーバーが VM 上で実行されており、専用用途ではない場合は、MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT を同じ値に設定してください。   
> トピックを参照して[ベスト プラクティス。VM 環境でのインメモリ OLTP を使用して](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)詳細についてはします。  
  
```sql  
  
-- disable resource governor  
ALTER RESOURCE GOVERNOR DISABLE  
  
-- change the value of MAX_MEMORY_PERCENT  
ALTER RESOURCE POOL PoolHk  
WITH  
     ( MAX_MEMORY_PERCENT = 70 )  
GO  
  
-- reconfigure the Resource Governor  
--    RECONFIGURE enables resource governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
  
```  
  
 MAX_MEMORY_PERCENT の最大値については、「 [メモリ最適化テーブルおよびインデックスで使用可能なメモリの割合](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#percent-of-memory-available-for-memory-optimized-tables-and-indexes)」をご覧ください。  
  
##### <a name="install-additional-memory"></a>追加メモリをインストールする  
 可能であれば、最終的に最上のソリューションは、追加の物理メモリをインストールすることです。 その場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でそれ以上のメモリが必要である可能性は低いため、新しくインストールされたメモリのすべてがリソース プールで使用可能でない場合はそれを活用して、MAX_MEMORY_PERCENT 値 (サブトピック「[既存のプール内での MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT の変更](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#change-min-memory-percent-and-max-memory-percent-on-an-existing-pool)」を参照) も増やせる可能性があります。  
  
> [!IMPORTANT]  
>  サーバーが VM 上で実行されており、専用用途ではない場合は、MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT を同じ値に設定してください。   
> トピックを参照して[ベスト プラクティス。VM 環境でのインメモリ OLTP を使用して](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)詳細についてはします。  
  
## <a name="resolve-page-allocation-failures-due-to-insufficient-memory-when-sufficient-memory-is-available"></a>十分なメモリがある状況でのメモリ不足によるページの割り当てエラーを解決する  
 エラー メッセージが発生した場合"データベースのページ割り当てが許可 ' *\<databaseName >* 'により、リソース プールでメモリ不足' *\<resourcePoolName >* '. 参照してください '<https://go.microsoft.com/fwlink/?LinkId=330673>' 詳細についてはします"。 エラー ログに記録される場合は、原因として、リソース ガバナーが無効になっている可能性があります。 リソース ガバナーが無効になっていると、MEMORYBROKER_FOR_RESERVE によって擬似的なメモリ不足が引き起こされます。  
  
 これを解決するには、リソース ガバナーを有効にする必要があります。  
  
 オブジェクト エクスプローラー、リソース ガバナーのプロパティ、または Transact-SQL を使用してリソース ガバナーを有効にする方法や、制限事項と制約事項については、「 [リソース ガバナーの有効化](https://technet.microsoft.com/library/bb895149.aspx) 」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP のメモリ管理](../../database-engine/managing-memory-for-in-memory-oltp.md)   
 [メモリ使用量の監視とトラブルシューティング](monitor-and-troubleshoot-memory-usage.md)   
 [データベースを作成してリソース プールにバインドする方法については、「](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [ベスト プラクティス:VM 環境でのインメモリ OLTP の使用](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)  
  
  
