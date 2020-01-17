---
title: クエリ ストアでデータを収集する方法 | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, data collection
ms.assetid: 8d5eec36-0013-480a-9c11-183e162e4c8e
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f60ded18e88d57c5a2975b567fa246923ece7ebe
ms.sourcegitcommit: f6bfe4a0647ce7efebaca11d95412d6a9a92cd98
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2019
ms.locfileid: "71974359"
---
# <a name="how-query-store-collects-data"></a>クエリ ストアでデータを収集する方法
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server クエリ ストアの動作は、フライト データ レコーダーとよく似ており、クエリやプランに関連するコンパイルおよびランタイムの情報を常に収集します。 クエリ関連のデータは内部テーブルに保存され、一連のビューでユーザーに表示されます。
  
## <a name="views"></a>ビュー 
 次の図は、クエリ ストアのビューとその論理関係を示しています。コンパイル時間の情報は青のエンティティで表しています。
  
 ![クエリ ストアのプロセス ビュー](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
**ビューの説明**  
  
|表示|[説明]|  
|----------|-----------------|  
|**sys.query_store_query_text**|データベースに対して実行された一意のクエリ テキストを表示します。 クエリ テキストの前後のコメントとスペースは無視されます。 テキスト内のコメントとスペースは無視されません。 バッチ内のすべてのステートメントが、個別のクエリ テキスト エントリを生成します。|  
|**sys.query_context_settings**|クエリが実行されるプランに影響する設定の一意の組み合わせを示します。 同じクエリ テキストが、プランに影響する異なる設定で実行されると、`context_settings_id` はクエリキーの一部であるため、クエリ ストアに個別のクエリ エントリが生成されます。|  
|**sys.query_store_query**|クエリ ストアで個別に追跡および強制されるクエリ エントリ。 単一のクエリ テキストが異なるコンテキスト設定で実行される場合、または異なる [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュール (ストアド プロシージャやトリガーなど) の外側と内側で実行される場合は、複数のクエリ エントリが生成される可能性があります。|  
|**sys.query_store_plan**|コンパイル時間の統計を含むクエリの見積もりプランを表示します。 格納されたプランは、`SET SHOWPLAN_XML ON` を使用して取得したものと同じです。|  
|**sys.query_store_runtime_stats_interval**|クエリ ストアは、自動的に生成される時間枠 (間隔) ごとに時間を分割し、すべての実行済みプランにその間隔で集計された統計を格納します。 間隔のサイズは、([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の) 構成オプションの**統計収集間隔**、または [ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) を使用する `INTERVAL_LENGTH_MINUTES` によって制御されます。|  
|**sys.query_store_runtime_stats**|実行済みプランで集計されたランタイム統計です。 キャプチャされたすべてのメトリックは、次の 4 つの統計関数の形式で表されます。平均、最小、最大、標準偏差の 4 つの統計関数の形式で表されます。|  
  
 クエリ ストアのビューについて詳しくは、「[クエリのストアを使用した、パフォーマンスの監視](monitoring-performance-by-using-the-query-store.md)」の「関連するビュー、関数、プロシージャ」セクションを参照してください。 
  
## <a name="query-processing"></a>クエリ処理
 クエリ ストアでは、次の主なポイントでクエリ処理パイプラインとやり取りします。
  
1.  クエリを初めてコンパイルすると、クエリ テキストと初期プランがクエリ ストアに送信されます。
  
2.  クエリを再コンパイルすると、プランがクエリ ストアで更新されます。 新しいプランが作成されると、クエリ ストアでクエリの新しいプラン エントリが追加され、前のものはその実行統計とともに保持されます。
  
3.  クエリを実行すると、ランタイム統計がクエリ ストアに送信されます。 クエリ ストアは、現在アクティブになっている間隔内で実行されたすべてのプランに対して正確な集計統計を保持します。 
  
4.  コンパイルおよび再コンパイルの確認フェーズ時に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、現在実行中のクエリに対して適用する必要があるプランがクエリ ストアにあるかどうかを判断します。 強制プランがあり、プロシージャ キャッシュのプランが強制プランと異なる場合は、クエリが再コンパイルされます。 これは、実質的にはプラン ヒントがそのクエリに適用された場合と同じ方法です。 この処理は、ユーザーのアプリケーションに透過的に行われます。 
  
 次の図は、前の手順で説明した統合のポイントを示しています。
  
 ![クエリ ストアのプロセス](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor") 

## <a name="remarks"></a>Remarks
 I/O のオーバーヘッドを最小限に抑えるため、新しいデータはメモリ内にキャプチャされます。 書き込み操作はキューに登録され、その後、ディスクにフラッシュされます。 下図でプラン ストアとして示されている、クエリおよびプランの情報は、最小限の待機時間でフラッシュされます。 ランタイム統計情報として示されるランタイム統計は、`SET QUERY_STORE` ステートメントの `DATA_FLUSH_INTERVAL_SECONDS` オプションで定義された一定期間、メモリ内に保持されます。 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] クエリ ストア ダイアログ ボックスを使用して、 **[データ フラッシュ間隔 (分)]** の値を入力できます。これは、内部的に秒に変換されます。 
  
 ![クエリ ストアのプロセス プラン](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan") 
  
 システムがクラッシュした場合、または[トレース フラグ 7745](../../relational-databases/performance/best-practice-with-the-query-store.md#Recovery) を使用しているときにシャットダウンが発生した場合、クエリ ストアでは、`DATA_FLUSH_INTERVAL_SECONDS` で定義された時間枠まで、収集されたもののまだ保存されていないランタイム データが失われる可能性があります。 クエリ キャプチャのパフォーマンスとデータの可用性のバランスを取るために、既定値の 900 秒 (15 分) を使用することをお勧めします。
 
 > [!IMPORTANT] 
 > **[最大サイズ (MB)]** の制限は、厳密には適用されません。 ストレージ サイズは、クエリ ストアでディスクにデータが書き込まれる場合にのみ確認されます。 この間隔は、 **[データのフラッシュ間隔]** の値によって設定されます。 クエリ ストアでストレージ サイズの確認の合間に最大サイズの制限を超えた場合は、読み取り専用モードに移行します。 **[サイズ ベースのクリーン アップモード]** が有効になっている場合は、最大サイズの制限を適用するクリーンアップ メカニズムもトリガーされます。
 
 > [!NOTE]
 > メモリ不足が発生した場合、`DATA_FLUSH_INTERVAL_SECONDS` で定義されている時間より前に、ランタイム統計がディスクにフラッシュされる可能性があります。
 
 クエリ ストア データの読み取り中は、メモリ内のデータとディスク上のデータが透過的に統合されます。 
 
 セッションが終了された場合、またはクライアント アプリケーションが再起動またはクラッシュした場合、クエリ統計は記録されません。 
  
 ![クエリ ストア プロセス プランの情報](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

## <a name="see-also"></a>参照
 [クエリ ストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [クエリ ストアを使用する際のベスト プラクティス](../../relational-databases/performance/best-practice-with-the-query-store.md)  
 [クエリ ストアのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md) 
  
  
