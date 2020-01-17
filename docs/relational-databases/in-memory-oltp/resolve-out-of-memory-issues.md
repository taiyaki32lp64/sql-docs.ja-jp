---
title: メモリ不足の問題の解決 | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8171a91d18650285c7bcaf4eb780083e958a8789
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908452"
---
# <a name="resolve-out-of-memory-issues"></a>メモリ不足の問題の解決
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] では、さまざまな形で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]より多くのメモリが使用されます。 インストールして [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 用に割り当てたメモリ量が、ニーズの拡大に合わなくなる場合があります。 その場合は、メモリが不足する可能性があります。 このトピックでは、OOM 状態から回復する方法について説明します。 多数の OOM 状態を回避するのに役立つガイドについては、「 [メモリ使用量の監視とトラブルシューティング](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md) 」を参照してください。  
  
## <a name="covered-in-this-topic"></a>このトピックの内容  
  
|トピック|概要|  
|-----------|--------------|  
|[OOM によるデータベース復元の障害を解決する](#bkmk_resolveRecoveryFailures)|"リソース プール ' *\<resourcePoolName>* ' 内のメモリ不足が原因で、データベース ' *\<databaseName>* ' の復元操作に失敗しました" というエラー メッセージが表示された場合の対処方法。|  
|[低メモリまたは OOM 状態によるワークロードへの影響を解決する](#bkmk_recoverFromOOM)|低メモリの問題によるパフォーマンス低下が見つかった場合の対処方法。|  
|[十分なメモリがある状況でのメモリ不足によるページの割り当てエラーを解決する](#bkmk_PageAllocFailure)|"リソース プール ' *\<resourcePoolName>* ' のメモリが不足しているため、データベース ' *\<databaseName>* ' のページ割り当ては禁止されています" というエラー メッセージが表示された場合の対処方法。 ..." というエラー メッセージが発生した場合の対処方法。|
|[VM 環境でのインメモリ OLTP の使用のベスト プラクティス](#bkmk_VMs)|仮想化環境でインメモリ OLTP を使用するときの留意事項。|
  
##  <a name="bkmk_resolveRecoveryFailures"></a> OOM によるデータベース復元の障害を解決する  
 データベースを復元しようとすると次のエラー メッセージが表示されることがあります。"リソース プール ' *\<resourcePoolName>* ' 内のメモリが不足しているため、データベース ' *\<databaseName>* ' の復元操作に失敗しました。"これは、データベースを復元するのに十分なメモリがサーバーにないことを示します。 
   
データベースの復元先であるサーバーでは、データベース バックアップのメモリ最適化テーブル用に十分なメモリが確保されている必要があります。メモリが十分でない場合、データベースはオンラインにならず、問題ありの印が付きます。  
  
サーバーは十分な物理メモリを備えているのに、このエラーが引き続き発生する場合は、他のプロセスで大量のメモリを使用されているか、または構成上の問題で復元用に十分なメモリが確保されていないことが考えられます。 この種の問題については、次の対策を実施して、復元操作でより多くのメモリを使用できるようにします。 
  
-   実行中のアプリケーションを一時的に閉じます。   
    実行中のアプリケーションを 1 つ以上閉じるか、または現時点で必要のないサービスを停止することにより、それらのアプリケーションまたはサービスで使用されていたメモリを復元操作で使用できるようにします。 閉じたアプリケーションは、復元操作の正常完了後に再起動できます。  
  
-   MAX_MEMORY_PERCENT の値を増やします。   
    データベースが [リソース プールにバインドされている](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)場合 (ベスト プラクティス)、復元で使用できるメモリは MAX_MEMORY_PERCENT によって管理されます。 値が小さすぎると、復元は失敗します。 このコード スニペットでは、リソース プール PoolHk の MAX_MEMORY_PERCENT を変更して、インストールされているメモリの 70% に設定します。  
  
    > [!IMPORTANT]  
    > サーバーが VM 上で実行されており、専用用途ではない場合は、MIN_MEMORY_PERCENT を MAX_MEMORY_PERCENT と同じ値に設定してください。   
    > 詳細については、「[VM 環境でのインメモリ OLTP の使用のベスト プラクティス](#bkmk_VMs) 」をご覧ください。  
  
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
  
     MAX_MEMORY_PERCENT の最大値については、「 [メモリ最適化テーブルおよびインデックスで使用可能なメモリの割合](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)」をご覧ください。  
  
-   **max server memory**の値を大きくします。  
    **max server memory** の構成については、トピック「[サーバー メモリに関するサーバー構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)」をご覧ください。  
  
##  <a name="bkmk_recoverFromOOM"></a> 低メモリまたは OOM 状態によるワークロードへの影響を解決する  
 言うまでもなく、低メモリまたは OOM (メモリ不足) の状態にならないことがベストです。 適切なプラン作成と監視によって、OOM 状態を回避することができます。 ただし、最適なプランを作成しても、実際に起こることを予測できるとは限らず、結果として低メモリまたは OOM の状態になる場合もあります。 OOM からの復旧には、次の 2 段階があります。  
  
1.  [DAC (専用管理者接続) を開く](#bkmk_openDAC)  
  
2.  [修正措置を行う](#bkmk_takeCorrectiveAction)  

###  <a name="bkmk_openDAC"></a> DAC (専用管理者接続) を開く  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には専用管理者接続 (DAC) があります。 DAC を使用すると、サーバーが他のクライアント接続に応答しない場合でも、SQL Server データベース エンジンの実行中のインスタンスにアクセスして、サーバーの問題をトラブルシューティングすることができます。 DAC は、`sqlcmd` ユーティリティと [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で使用できます。  
  
 SSMS または `sqlcmd` で DAC を使用する方法については、「[データベース管理者用の診断接続](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)」を参照してください。  
  
###  <a name="bkmk_takeCorrectiveAction"></a> 修正措置を行う  
 OOM 状態を解決するには、使用率を削減して既存メモリを解放するか、インメモリ テーブルに使用できるメモリ量を増やす必要があります。  
  
#### <a name="free-up-existing-memory"></a>既存メモリを解放する  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>メモリ最適化テーブルの不要な行を削除し、ガベージ コレクションを待機する  
 メモリ最適化テーブルから、不要な行を削除できます。 ガベージ コレクターによって、これらの行で使用されていたメモリが使用可能メモリに返されます。 インメモリ OLTP エンジンは、ガベージ行を積極的に回収します。 ただし、実行時間が長いトランザクションではガベージ コレクションが行われないことがあります。 たとえば、5 分間実行されているトランザクションの場合、トランザクションがアクティブな状態で更新操作または削除操作によって作成された行バージョンは、ガベージ コレクションで回収することができません。  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>1 つ以上の行をディスク ベース テーブルに移動する  
 TechNet の次の資料では、メモリ最適化テーブルからディスク ベース テーブルに行を移動する方法について説明しています。  
  
-   [アプリケーション レベルのパーティション分割](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
  
-   [メモリ最適化テーブルのパーティション分割に関するアプリケーションのパターン](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
#### <a name="increase-available-memory"></a>使用可能なメモリを増やす  
  
##### <a name="increase-value-of-max_memory_percent-on-the-resource-pool"></a>リソース プールの MAX_MEMORY_PERCENT 値を増やす  
 インメモリ テーブル用に名前付きリソース プールを作成していない場合は、作成して [!INCLUDE[hek_2](../../includes/hek-2-md.md)] データベースをバインドします。 [データベースを作成してリソース プールにバインドする方法については、「](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) メモリ最適化テーブルを持つデータベースのリソース プールへのバインド [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 」を参照してください。  
  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] データベースがリソース プールにバインドされている場合は、プールがアクセスできるメモリのパーセントを増やせることがあります。 リソース プールの MIN_MEMORY_PERCENT および MAX_MEMORY_PERCENT の値を変更する方法については、サブトピック「 [既存のプール内での MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT の変更](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) 」をご覧ください。  
  
 MAX_MEMORY_PERCENT の値を増やします。   
このコード スニペットでは、リソース プール PoolHk の MAX_MEMORY_PERCENT を変更して、インストールされているメモリの 70% に設定します。  
  
> [!IMPORTANT]  
>  サーバーが VM 上で実行されており、専用用途ではない場合は、MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT を同じ値に設定してください。   
> 詳細については、「[VM 環境でのインメモリ OLTP の使用のベスト プラクティス](#bkmk_VMs) 」をご覧ください。  
  
```sql  
-- disable resource governor  
ALTER RESOURCE GOVERNOR DISABLE  
  
-- change the value of MAX_MEMORY_PERCENT  
ALTER RESOURCE POOL PoolHk  
WITH  
     ( MAX_MEMORY_PERCENT = 70 )  
GO  
  
-- reconfigure the Resource Governor to enabled it
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
 MAX_MEMORY_PERCENT の最大値については、「 [メモリ最適化テーブルおよびインデックスで使用可能なメモリの割合](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)」をご覧ください。  
  
##### <a name="install-additional-memory"></a>追加メモリをインストールする  
 可能であれば、最終的に最上のソリューションは、追加の物理メモリをインストールすることです。 その場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でそれ以上のメモリが必要である可能性は低いため、新しくインストールされたメモリのすべてがリソース プールで使用可能でない場合はそれを活用して、MAX_MEMORY_PERCENT 値 (サブトピック「[既存のプール内での MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT の変更](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)」を参照) も増やせる可能性があります。  
  
> [!IMPORTANT]  
>  サーバーが VM 上で実行されており、専用用途ではない場合は、MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT を同じ値に設定してください。   
> 詳細については、「[VM 環境でのインメモリ OLTP の使用のベスト プラクティス](#bkmk_VMs) 」をご覧ください。  
  
##  <a name="bkmk_PageAllocFailure"></a> 十分なメモリがある状況でのメモリ不足によるページの割り当てエラーを解決する  
 エラー メッセージ `Disallowing page allocations for database '*\<databaseName>*' due to insufficient memory in the resource pool '*\<resourcePoolName>*'. See 'https://go.microsoft.com/fwlink/?LinkId=330673' for more information.` がエラー ログに記録される場合は、原因として、リソース ガバナーが無効になっている可能性があります。 リソース ガバナーが無効になっていると、MEMORYBROKER_FOR_RESERVE によって擬似的なメモリ不足が引き起こされます。  
  
 これを解決するには、リソース ガバナーを有効にする必要があります。  
  
 オブジェクト エクスプローラー、リソース ガバナーのプロパティ、または Transact-SQL を使用してリソース ガバナーを有効にする方法や、制限事項と制約事項については、「 [リソース ガバナーの有効化](../../relational-databases/resource-governor/enable-resource-governor.md) 」をご覧ください。  
 
## <a name="bkmk_VMs"></a> VM 環境でのインメモリ OLTP の使用のベスト プラクティス
サーバー仮想化に伴い、各企業は IT の資本コストと運用コストを削減し、アプリケーションの準備、メンテナンス、可用性、バックアップと復旧の各プロセスを向上させることにより、IT 効率の大幅な上昇を達成しています。 最近の技術的な進歩により、仮想化を使用して、複雑なデータベース ワークロードを従来より容易に統合することができます。 ここでは、仮想化環境内での SQL Server インメモリ OLTP の使用に関して推奨されるベスト プラクティスについて取り扱います。

### <a name="memory-pre-allocation"></a>メモリの事前割り当て
仮想化環境でのメモリに関して、パフォーマンス向上とサポート拡張は重要な考慮事項です。 仮想マシンの需要 (ピーク負荷とオフピーク負荷) に応じてメモリを迅速に仮想マシンに割り当てる能力が必須であり、メモリが浪費されていないことを確認する必要もあります。 Hyper-V 動的メモリ機能により、1 台のホスト上で実行する複数の仮想マシン間でのメモリ割り当てと管理がより迅速に行われます。

メモリ最適化テーブルを含むデータベースを仮想化する場合は、SQL Server の仮想化と管理に関するいくつかのベスト プラクティスを変更する必要があります。 メモリ最適化されたテーブルが存在しない場合、次の 2 つのベスト プラクティスがあります。
-  min server memory を使用する場合は、必要とされる量のメモリのみを割り当てる方が適切です。その結果、他のプロセス用に十分なメモリを残すことができます (その結果、ページングを回避できます)。
-  メモリの事前割り当ての値を過度に大きく設定しないでください。 そうしない場合は、他のプロセスがメモリを必要とする時点で十分なメモリを取得できず、メモリのページングが発生する可能性があります。

メモリ最適化テーブルがデータベース内に含まれている場合に上記のプラクティスに従うと、データベースの復元と復旧を試みたときに、データベースを復旧するための十分なメモリが存在するにもかかわらず、データベースが "復旧の保留中" という状態にとどまる可能性があります。 その理由は、動的メモリ割り当て機能がメモリをデータベースに割り当てる場合に比べて、インメモリ OLTP は起動時により積極的にデータをメモリ内に読み込むことにあります。

### <a name="resolution"></a>解決策
この問題を軽減するためには、必要に応じて追加のメモリを提供する動的メモリ機能に依存して最小限のメモリを割り当てる代わりに、データベースを復旧または再起動するために十分なメモリをデータベースに事前に割り当ててください。
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP のメモリ管理](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)   
 [メモリ使用量の監視とトラブルシューティング](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)   
 [データベースを作成してリソース プールにバインドする方法については、「](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [メモリ管理アーキテクチャ ガイド](../../relational-databases/memory-management-architecture-guide.md)  
 [サーバー メモリに関するサーバー構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md) 
  
