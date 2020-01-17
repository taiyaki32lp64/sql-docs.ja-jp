---
title: フルテキスト インデックスのパフォーマンスの向上 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], full-text search
- full-text queries [SQL Server], performance
- crawls [full-text search]
- full-text indexes [SQL Server], performance
- full-text search [SQL Server], performance
- batches [SQL Server], full-text search
ms.assetid: ef39ef1f-f0b7-4582-8e9c-31d4bd0ad35d
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a755ba9aa8915734768c56c096ea917a6e0c5564
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021221"
---
# <a name="improve-the-performance-of-full-text-indexes"></a>フルテキスト インデックスのパフォーマンスの向上
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
このトピックでは、フルテキスト インデントとクエリのパフォーマンス低下の一般的な原因をいくつか説明します。 また、このような問題を軽減し、パフォーマンスを改善する提案もいくつか紹介します。
  
##  <a name="causes"></a> Common causes of performance issues
### <a name="hardware-resource-issues"></a>ハードウェア リソースの問題
フルテキスト インデックス作成とフルテキスト クエリのパフォーマンスは、メモリ、ディスク速度、CPU 速度、コンピューターのアーキテクチャなどのハードウェア リソースの影響を受けます。  

フルテキスト インデックス作成のパフォーマンス低下の主な原因となるのは、ハードウェア リソースの制限です。  
  
-   **CPU**。 フィルター デーモン ホスト プロセス (fdhost.exe) または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス (sqlservr.exe) の CPU 使用率が 100% に近くなっている場合は、CPU がボトルネックになっています。  
  
-   **メモリ**。 物理メモリが不足している場合は、メモリがボトルネックになっている可能性があります。  

-   **ディスク**。 ディスク待ちのキューの長さが平均でディスク ヘッド数の 2 倍を超えている場合は、ディスクがボトルネックになっています。 この場合の主な回避策は、作成するフルテキスト カタログを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース ファイルやログから切り離し、 ログ、データベース ファイル、およびフルテキスト カタログを別々のディスクに配置することです。 その他、高速なディスクの導入や RAID の使用も、インデックス作成のパフォーマンス向上に役立ちます。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、Full-Text Engine は sqlservr.exe プロセスの一部となったため、AWE メモリを使用できます。  

### <a name="full-text-batching-issues"></a>フルテキスト バッチ処理の問題
 システムにハードウェアのボトルネックがない場合、フルテキスト検索のインデックス作成パフォーマンスは、主に以下の条件に左右されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によるフルテキスト バッチの作成にかかる時間  
  
-   フィルター デーモンがバッチを処理する速度  

### <a name="full-text-index-population-issues"></a>フルテキスト インデックスの作成の問題
-   **作成の種類**。 増分、手動、および自動の変更追跡による作成は、完全作成とは違って、ハードウェア リソースを最大限に活用して処理を高速化するようには作られていません。 そのため、このトピックで提案する調整を実行しても、増分、手動、または自動の変更追跡を使用したときのフルテキスト インデックスのパフォーマンスが改善しない場合があります。  
  
-   **マスター マージ**。 作成が完了すると、最終的なマージ プロセスが起動され、インデックス フラグメントが 1 つのマスター フルテキスト インデックスにマージされます。 これにより、多数のインデックス フラグメントではなく、1 つのマスター インデックスのみをクエリすれば済むため、クエリのパフォーマンスが向上し、関連順位付けにもより的確なスコア (評価) 統計を適用できます。 ただし、マスターのマージ処理では、インデックス フラグメントをマージする際に大量のデータを読み書きする必要があるため、大量の I/O が発生しますが、クエリの着信がブロックされることはありません。  
  
    マスター マージで大量のデータを処理すると、実行時間が長いトランザクションが発生し、チェックポイント時のログの切り捨てが遅れる場合があります。 この場合、完全復旧モデルでは、トランザクション ログが非常に大きくなることがあります。 完全復旧モデルを使用するデータベースで大きなフルテキスト インデックスを再編成する前に、実行時間が長いトランザクションのための十分な領域をトランザクション ログに割り当てることをお勧めします。 詳細については、「 [トランザクション ログ ファイルのサイズの管理](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)」を参照してください。  
  
##  <a name="tuning"></a> フルテキスト インデックスのパフォーマンスの調整  
フルテキスト インデックスのパフォーマンスを最大化するには、次に示すベスト プラクティスを実装します。  
  
-   すべての CPU プロセッサまたはコアを最大限に使用するには、[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) '**max full-text crawl range**' をシステム上の CPU の数に設定します。 構成オプションの詳細については、「 [max full-text crawl range サーバー構成オプション](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)」を参照してください。  
  
-   ベース テーブルにクラスター化インデックスがあることを確認します。 クラスター化インデックスの最初の列には整数データ型を使用します。 GUID は使用しないようにしてください。 クラスター化インデックスで複数の範囲の作成を使用すると、作成速度を最大限に高めることができます。 フルテキスト キーとして機能する列は整数データ型にすることをお勧めします。  
  
-   [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) ステートメントを使用してベース テーブルの統計を更新します。 さらに重要な点は、クラスター化インデックスの統計や完全作成のフルテキスト キーを更新することです。 これにより、複数の範囲の作成によってテーブルに適切なパーティションが生成されるようになります。  
  
-   大型のマルチ CPU コンピューター上で完全作成を実行する前に、fdhost.exe プロセスおよびオペレーティング システムが使用するメモリを十分に確保するために、 **max server memory** 値を設定してバッファー プールのサイズを一時的に制限することをお勧めします。 詳細については、このトピックの「フィルター デーモン ホスト プロセス (fdhost.exe) のメモリ要件の推定」を参照してください。

-   timestamp 列に基づいて増分作成を使用する場合は、**timestamp** 列にセカンダリ インデックスを構築し、増分作成のパフォーマンスを向上します。  
  
##  <a name="full"></a> 完全作成のパフォーマンスに関するトラブルシューティング  
### <a name="review-the-full-text-crawl-logs"></a>フルテキスト クロール ログを確認する
 パフォーマンスの問題を診断するには、フルテキスト クロール ログを調べます。
 
クロール時にエラーが発生すると、フルテキスト検索クロール ログ記録機能によってクロール ログが作成および保持されます。このログはプレーンテキスト ファイルです。 各クロール ログは特定のフルテキスト カタログに対応します。 既定では、所与のインスタンス (この例では、既定のインスタンス) のクロール ログは `%ProgramFiles%\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\LOG` フォルダーにあります。
 
クロール ログは次のような規則に従って命名されます。  
  
`SQLFT<DatabaseID\><FullTextCatalogID\>.LOG[<n\>]`
  
クロール ログ ファイルの可変部分は次のようになります。
-   \<**DatabaseID**> - データベースの ID。 <**dbid**> は、ゼロで始まる 5 桁の数字です。  
-   <**FullTextCatalogID**> - フルテキスト カタログ ID。 \<**catid**> は、ゼロで始まる 5 桁の数字です。  
-   <**n**> - 同じフルテキスト カタログに 1 つ以上のクロール ログが存在することを示す整数です。  
  
 たとえば、`SQLFT0000500008.2` はデータベース ID が 5 で、フルテキスト カタログ ID が 8 のクロール ログ ファイルです。 ファイル名の最後の 2 は、このデータベースとカタログのペアに 2 つのクロール ログ ファイルが存在することを示しています。  

### <a name="check-physical-memory-usage"></a>物理メモリの使用量を確認する  
 フルテキスト作成時は、fdhost.exe または sqlservr.exe がメモリ不足またはメモリ枯渇の状態で実行される可能性があります。
-   フルテキスト クロールのログを確認した結果、fdhost.exe が頻繁に再起動されているか、エラー コード 8007008 が返されていることが判明した場合は、これらのプロセスのいずれかでメモリ不足が生じています。
-   特に大型のマルチ CPU コンピューター上で fdhost.exe がダンプを生成している場合、メモリが不足してきている可能性があります。  
-   フルテキスト クロールで使用されるメモリ バッファーに関する情報を取得する方法については、「[sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)」を参照してください。  
  
 低メモリまたはメモリ不足は、次の原因が考えられます。  
  
-   **不十分なメモリ**。 完全作成時に使用可能な物理メモリの量がゼロの場合、システム上の物理メモリのほとんどを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バッファー プールが消費している可能性があります。  
  
     sqlservr.exe プロセスは、構成されている最大サーバー メモリ量に達するまで、バッファー プールで使用できるすべてのメモリを獲得しようとします。 **max server memory** の割り当てが大きすぎる場合は、fdhost.exe プロセスのメモリ不足や共有メモリの割り当ての失敗が発生することがあります。  
  
     **バッファー プールの** max server memory [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 値を適切に設定することにより、この問題を解決できます。 詳細については、このトピックの「フィルター デーモン ホスト プロセス (fdhost.exe) のメモリ要件の推定」を参照してください。 フルテキスト インデックスの作成に使用されるバッチのサイズを小さくすると、有効な場合があります。  

-   **メモリの競合**。 マルチ CPU コンピューター上でのフルテキスト作成時、fdhost.exe または sqlservr.exe との間でバッファー プール メモリの競合が発生する場合があります。 その結果、共有メモリが不足すると、バッチの再試行、メモリ スラッシング、および fdhost.exe プロセスによるダンプが発生します。  

-   **ページングの問題**。 拡張が制限された小さなページ ファイルが使用されているシステムにおいてページ ファイルのサイズが不足した場合、fdhost.exe または sqlservr.exe でメモリ不足が発生します。 クロール ログにメモリ関連の障害が見当たらない場合、過剰なページングが原因でパフォーマンスが低下していることが考えられます。  
  
### <a name="estimate-the-memory-requirements-of-the-filter-daemon-host-process-fdhostexe"></a>フィルター デーモン ホスト プロセス (fdhost.exe) のメモリ要件を推定する  
 fdhost.exe プロセスが作成のために必要とするメモリ量は、主に、プロセスが使用するフルテキスト クロール範囲の数、受信共有メモリ (ISM) のサイズ、および ISM インスタンスの最大数に依存します。  
  
 フィルター デーモン ホストによって使用されるメモリ量 (バイト単位) は、次の式を使用して概算できます。  
  
`number_of_crawl_ranges * ism_size * max_outstanding_isms * 2`  
  
 この式の変数の既定値は次のとおりです。  
  
|**変数**|**既定値**|  
|------------------|-----------------------|  
|*number_of_crawl_ranges*|CPU の数|  
|*ism_size*|1 MB (x86 コンピューターの場合)<br /><br /> 合計物理メモリにより、4 MB、8 MB、または 16 MB (x64 コンピューターの場合)|  
|*max_outstanding_isms*|25 (x86 コンピューターの場合)<br /><br /> 5 (x64 コンピューターの場合)|  
  
 fdhost.exe のメモリ要件の推定方法に関するガイドラインを、以下の表に示します。 この表の数式では次の値を使用します。  
  
-   *F*: fdhost.exe に必要なメモリの推定値 (MB 単位)。  
  
-   *T*: システムで使用できる合計物理メモリ (MB 単位)。  
  
-   *M*: **max server memory** の最適な設定  
  
次の式の基本情報については、表の後の注意事項を参照してください。  
  
|プラットフォーム|fdhost.exe のメモリ要件の推定 (MB 単位) - *F*^1|max server memory の計算式 - *M*^2|  
|--------------|-----------------------------------------------------------|-----------------------------------------------------|  
|x86|*F* = *クロール範囲の数* \* 50|*M* =minimum(*T*, 2000) - F - 500|  
|x64|*F* = *クロール範囲の数* \* 10 \* 8|*M* = *T* - *F* - 500|  

**式に関する注意事項**
1.  複数の完全作成を実行中の場合は、それぞれの fdhost.exe のメモリ要件を、*F1*、*F2* などのように個別に計算してください。 その後、*M* as _T_ **-** sigma **(** _F_i **)** で計算します。  
2.  500 MB は、システムの他のプロセスに必要なメモリの推定値です。 システムで追加の作業を実行している場合、適宜この値を大きくします。  
3.  」を参照してください。*ism_size* は 8 MB と見なされます (x64 プラットフォームの場合)。  
  
 #### <a name="example-estimate-the-memory-requirements-of-fdhostexe"></a>例:fdhost.exe のメモリ要件を推定する  
  
 この例は、8 GM の RAM と 4 つのデュアル コア プロセッサを搭載した 64 ビット コンピューターを対象としています。 最初の計算では、fdhost.exe に必要なメモリ (*F*) を推定します。 クロール範囲の数は `8`です。  
  
 `F = 8*10*8=640`  
  
 次の計算では、最適な **max server memory** 値 (*M*) を算出します。 このシステムで使用可能な合計物理メモリ (MB 単位) (*T*) は `8192` です。  
  
 `M = 8192-640-500=7052`  
  
 #### <a name="example-setting-max-server-memory"></a>例:max server memory の設定  
  
 この例では、 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) ステートメントおよび [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して、前の例で計算した **M** の値 *を* max server memory `7052`として設定します:  
  
```  
USE master;  
GO  
EXEC sp_configure 'max server memory', 7052;  
GO  
RECONFIGURE;  
GO  
```  
  
サーバー メモリ オプションの詳細については、「[Server Memory Server Configuration Options](../../database-engine/configure-windows/server-memory-server-configuration-options.md)」(サーバー メモリに関するサーバー構成オプション) を参照してください。
  
### <a name="check-cpu-usage"></a>CPU 使用量を確認する  
平均 CPU 消費率が約 30% 未満になると、完全作成のパフォーマンスは低下します。 CPU 消費率に影響するいくつかの要因を次に示します。  
  
-   ページの待機時間が長い  
  
     ページ待機時間が長いかどうかを調べるには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します。  
  
    ```  
    SELECT TOP 10 * FROM sys.dm_os_wait_stats ORDER BY wait_time_ms DESC;  
    ```  
  
     次の表で、主な待機の種類について説明します。  
  
    |待機の種類|[説明]|解決方法|  
    |---------------|-----------------|-------------------------|  
    |PAGEIO_LATCH_SH (_EX または _UP)|IO がボトルネックとなっている可能性があります。この場合は通常、平均のディスク キューも長くなります。|別のディスクの別のファイル グループにフルテキスト インデックスを移動すると、IO のボトルネックを軽減できる場合があります。|  
    |PAGELATCH_EX (または _UP)|複数のスレッドが同じデータベース ファイルへの書き込みを試行し、多数の競合が発生している可能性があります。|フルテキスト インデックスが格納されているファイル グループにファイルを追加すると、このような競合を軽減できる場合があります。|  
  
     詳細については、「[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」を参照してください。  
  
-   非効率的なベース テーブル スキャン  
  
     完全作成では、バッチを生成するためにベース テーブルをスキャンします。 次のようなシナリオでは、このテーブル スキャンの効率が下がる可能性があります。  
  
    -   フルテキスト インデックスが作成される行外の列がベース テーブルに高い比率で含まれている場合、バッチ生成のためのベース テーブル スキャンがボトルネックとなることがあります。 その場合、 **varchar(max)** または **nvarchar(max)** を使用して、比較的小さなデータを行内に移動すると解決することがあります。  
  
    -   ベース テーブルが過度に断片化されていると、スキャンの効率が下がります。 行外データの計算とインデックスの断片化の詳細については、「[」sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)」および「[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)」を参照してください。  
  
         断片化を解消するには、クラスター化インデックスを再構成または再構築します。 詳細については、「 [インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。  
  
##  <a name="filters"></a> ドキュメントのインデックス作成が遅い問題のトラブルシューティング

> [!NOTE]
> ここでは、他のドキュメントの種類が埋め込まれているドキュメント (Microsoft Word 文書など) のインデックスを作成する場合にのみ影響する問題について説明します。

Full-Text Engine では、フルテキスト インデックスを作成するときに、マルチスレッド フィルターとシングル スレッド フィルターの 2 種類のフィルターを使用します。
-   フィルター処理するドキュメントに応じて、マルチスレッド フィルターを使用する場合 ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 文書など) と、
-   シングル スレッド フィルターを使用する場合 (Adobe Acrobat Portable Document Format (PDF) ドキュメントなど) があります。  
  
 セキュリティ上の理由から、フィルターはフィルター デーモン ホスト プロセスによって読み込まれます。 サーバー インスタンスでは、マルチスレッド フィルターに対してはすべてマルチスレッド処理が使用され、シングル スレッド フィルターに対してはすべてシングル スレッド処理が使用されます。 マルチスレッド フィルターを使用するドキュメントにシングル スレッド フィルターを使用するドキュメントが埋め込まれていると、Full-Text Engine では埋め込まれたドキュメントに対してシングル スレッド処理を開始します。 たとえば、PDF ドキュメントが埋め込まれた Word 文書の場合、Full-Text Engine は、Word コンテンツに対してはマルチスレッド プロセスを使用し、PDF の内容に対してはシングル スレッド プロセスを開始します。 ただし、このような環境では、シングル スレッド フィルターが適切に機能しない場合があり、フィルター処理が不安定になることがあります。 このような埋め込みが通例であるような特定の状況では、不安定になった結果、プロセスがクラッシュすることもあります。 クラッシュが発生すると、エラーが発生したドキュメント (たとえば、PDF の内容が埋め込まれた Word 文書) がシングル スレッド フィルター処理に再ルーティングされます。 再ルーティングが頻繁に起こると、フルテキスト インデックス作成処理のパフォーマンスが低下します。  
  
この問題を回避するには、コンテナー ドキュメント (この例では Word 文書) に対するフィルターとして、シングル スレッド フィルターを設定します。 シングル スレッド フィルターとして設定するには、フィルターの **ThreadingModel** レジストリ値を **Apartment Threaded** に設定します。 シングル スレッド アパートメントの詳細については、ホワイト ペーパー「 [COM スレッド モデルの概要と使用方法](https://go.microsoft.com/fwlink/?LinkId=209159)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [サーバー メモリに関するサーバー構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [max full-text crawl range サーバー構成オプション](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)   
 [フルテキスト インデックスの作成](../../relational-databases/search/populate-full-text-indexes.md)   
 [フルテキスト インデックスの作成と管理](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)   
 [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)   
 [フルテキスト インデックスの作成のトラブルシューティング](../../relational-databases/search/troubleshoot-full-text-indexing.md)  
  
  
