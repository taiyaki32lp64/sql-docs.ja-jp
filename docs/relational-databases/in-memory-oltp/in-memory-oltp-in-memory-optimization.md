---
title: インメモリ OLTP (インメモリ最適化) | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87ad093d5be6f4fa394e934e6c0d88796a22e196
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401653"
---
# <a name="in-memory-oltp-and-memory-optimization"></a>インメモリ OLTP とメモリ最適化

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] は、トランザクション処理、データの取り込み、データの読み込みのパフォーマンス、および一時的なデータのシナリオを大幅に向上させることができます。  独自のメモリ最適化テーブルとネイティブ コンパイル ストアド プロシージャをすばやくテストするために必要な基本的なコードと知識については、
 -  [クイック スタート 1:Transact-SQL のパフォーマンスを向上させるインメモリ OLTP テクノロジ](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)」を参照してください。  
 
SQL Server 上のインメモリ OLTP について説明し、パフォーマンス上の利点を示す [**17 分の動画**](#anchorname-17minute-video)を YouTube にアップロードしました。

インメモリ OLTP の詳細な概要、およびテクノロジからパフォーマンスの利点を享受するシナリオのレビュー:

- [概要と使用シナリオ](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)
 
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] は、トランザクション処理のパフォーマンスを向上させる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テクノロジであることに注意してください。 報告と分析クエリのパフォーマンスを向上させる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テクノロジについては、「 [列ストア インデックスの説明](../../relational-databases/indexes/columnstore-indexes-overview.md)」を参照してください。
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]、[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]、および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、インメモリ OLTP はいくつかの機能強化が行われています。 データベース アプリケーションの移行を容易にできるように、Transact-SQL の表層が拡大されています。 アプリケーションのメンテナンスを容易にできるように、メモリ最適化テーブルとネイティブ コンパイル ストアド プロシージャの ALTER 操作を実行するためのサポートが追加されています。
  
> [!NOTE]  
>  **お試しください**  
>   
>  インメモリ OLTP は、Premium および Business Critical 層の Azure SQL Database およびエラスティック プールで使用できます。 インメモリ OLTP および Azure SQL Database の列ストアの使用を開始するには、「 [SQL Database でのインメモリ (プレビュー) の使用](https://azure.microsoft.com/documentation/articles/sql-database-in-memory/)」をご覧ください。  
  

## <a name="in-this-section"></a>このセクションの内容  
 このセクションの内容は次のとおりです。  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[クイック スタート 1:Transact-SQL のパフォーマンスを向上させるインメモリ OLTP テクノロジ](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)|インメモリ OLTP について深く掘り下げて考えます|
|[概要と使用シナリオ](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)|インメモリ OLTP の内容、およびパフォーマンス上の利点を活用するシナリオの概要です。|
|[メモリ最適化テーブルを使用するための要件](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)|メモリ最適化テーブルを使用するためのハードウェア要件、ソフトウェア要件、およびガイドラインについて説明します。|  
|[インメモリ OLTP のコード サンプル](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)|メモリ最適化テーブルを作成して使用する方法を示すコード例が記載されています。|  
|[メモリ最適化テーブル](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)|メモリ最適化テーブルの概要を示します。|  
|[メモリ最適化テーブル変数](https://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|tempdb の使用を減らすために、従来のテーブル変数の代わりにメモリ最適化テーブル変数を使用する方法を示すコード例です。|  
|[メモリ最適化テーブルのインデックス](https://msdn.microsoft.com/library/86805eeb-6972-45d8-8369-16ededc535c7)|メモリ最適化インデックスを示します。|  
|[ネイティブ コンパイル ストアド プロシージャ](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)|ネイティブ コンパイル ストアド プロシージャについて説明します。|  
|[インメモリ OLTP のメモリ管理](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)|システムのメモリ使用量について説明し、メモリ使用量を管理する方法を示します。|  
|[メモリ最適化オブジェクト用ストレージの作成と管理](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)|メモリ最適化テーブルでのトランザクションに関する情報を格納するデータ ファイルとデルタ ファイルについて説明します。|  
|[メモリ最適化テーブルのバックアップ、復元、復旧](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)|メモリ最適化テーブルのバックアップ、復元、および復旧について説明します。|  
|[Transact-SQL によるインメモリ OLTP のサポート](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] による [!INCLUDE[hek_2](../../includes/hek-2-md.md)]のサポートについて説明します。|  
|[インメモリ OLTP データベースにおける高可用性のサポート](../../relational-databases/in-memory-oltp/high-availability-support-for-in-memory-oltp-databases.md)|[!INCLUDE[hek_2](../../includes/hek-2-md.md)]での可用性グループおよびフェールオーバー クラスタリングについて説明します。|  
|[SQL Server によるインメモリ OLTP のサポート](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)|新しい構文および機能、更新された構文および機能のうち、メモリ最適化テーブルをサポートするものを一覧にして紹介します。|  
|[インメモリ OLTP への移行](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)|ディスク ベース テーブルをメモリ最適化テーブルに移行する方法について説明します。|  
| &nbsp; | &nbsp; |

## <a name="links-to-other-websites"></a>他の Web サイトへのリンク

このセクションでは、SQL Server 上のインメモリ OLTP に関する情報を含むその他の Web サイトへのリンクを紹介します。

- [インメモリ OLTP について説明し、パフォーマンス上の利点を示す**動画**](#anchorname-17minute-video)

- [インメモリ OLTP パフォーマンス デモ v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

-   [SQL Server インメモリ OLTP 内部技術ホワイト ペーパー](https://msdn.microsoft.com/library/mt764316.aspx)  

-   [SQL Server のインメモリ OLTP と列ストア機能の比較](https://download.microsoft.com/download/D/0/0/D0075580-6D72-403D-8B4D-C3BD88D58CE4/SQL_Server_2016_In_Memory_OLTP_and_Columnstore_Comparison_White_Paper.pdf)

-   SQL Server 2016 のインメモリ OLTP の新機能の[パート 1](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/11/12/in-memory-oltp-whats-new-in-sql2016-ctp3/) と[パート 2](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/25/whats-new-for-in-memory-oltp-in-sql-server-2016-since-ctp3/)
  
-   [インメモリ OLTP - 一般的なワークロード パターンと移行に関する考慮事項](https://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [インメモリ OLTP ブログ](https://go.microsoft.com/fwlink/?LinkId=311696)  

## <a name="anchorname-17minute-video"></a>17 分の動画、インデックス付き

- _動画のタイトル:_ &nbsp; **SQL Server 2016 のインメモリ OLTP**
- _公開日:_ &nbsp; 2019-03-10 (`YouTube.com` 上)。
- _期間:_ &nbsp; 17:32 &nbsp; &nbsp; (ビデオへのリンクについては、次の[**インデックス**](#anchorname-index-17minute-video)に関する記事を参照してください。)
- _ホスト元:_ &nbsp; SQL Server のシニア プログラム マネージャーである Jos de Bruijn

### <a name="demo-can-be-downloaded"></a>デモをダウンロードできます

時間マーク 08:09 では、動画でデモンストレーションが 2 回実行されます。 動画で使用されている実行可能なパフォーマンス デモのソース コードは、次のリンクからダウンロードできます。

- [インメモリ OLTP パフォーマンス デモ v1.0、ソース コード](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

動画で見られる一般的な手順は次のとおりです。

1. 最初に、通常のテーブルを使用してデモを実行します。
2. 次に、SQL Server Management Studio (SSMS.exe) で数回のクリックでテーブルのメモリ最適化エディションを作成し、設定する方法を確認します。
3. 次に、メモリ最適化テーブルを使用してデモを再実行します。 大幅な速度の向上が測定されます。

### <a name="anchorname-index-17minute-video"></a>動画の各セクションへのインデックス

| 時間マークのリンク | セクションのタイトル |
| :------------- | :------------ |
| A.&nbsp;[00:00](https://www.youtube.com/watch?v=l5l5eophmK4&t=0) | はじめに。 |
| <br/>B.&nbsp;[00:56](https://www.youtube.com/watch?v=l5l5eophmK4&t=56) | <br/>顧客がインメモリ OLTP について注意する必要がある理由。 |
| &nbsp; &nbsp; [01:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=63) | 最新のハードウェアには、データベース システムの最新のアーキテクチャが必要です。 |
| &nbsp; &nbsp; [02:10](https://www.youtube.com/watch?v=l5l5eophmK4&t=130) | 生成されているデータの急増。操作は瞬時に行う必要があります (低待機時間)。 |
| &nbsp; &nbsp; [03:19](https://www.youtube.com/watch?v=l5l5eophmK4&t=199) | TCO を削減 - お持ちのリソースでさらに多くのことを行います。 |
| <br/>C.&nbsp;[03:33](https://www.youtube.com/watch?v=l5l5eophmK4&t=213) | <br/>インメモリ OLTP とは。<br/>メモリ最適化テクノロジを使用して最適化されるパフォーマンス。 |
| &nbsp; &nbsp; [05:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=303) | 最大 30 倍の高速トランザクション処理。 |
| &nbsp; &nbsp; [05:22](https://www.youtube.com/watch?v=l5l5eophmK4&t=322) | 完全な持続性 - データはサーバー エラーに耐えます。 |
| &nbsp; &nbsp; [06:15](https://www.youtube.com/watch?v=l5l5eophmK4&t=375) | SQL Server への完全な統合。 そのため、新しい言語やツールを習得することはできません。 |
| &nbsp; &nbsp; [07:22](https://www.youtube.com/watch?v=l5l5eophmK4&t=442) | 最初に SQL Server 2014 でリリースされましたが、2016 で大幅に改善されました。 |
| &nbsp; &nbsp; [07:58](https://www.youtube.com/watch?v=l5l5eophmK4&t=558) | Azure SQL Database でも利用できます (クラウド内)。 |
| <br/>D.&nbsp;[08:09](https://www.youtube.com/watch?v=l5l5eophmK4&t=489) | <br/>パフォーマンスのデモンストレーション。<br/> 通常のテーブルを使用してデモを実行します。 |
| &nbsp; &nbsp; [09:11](https://www.youtube.com/watch?v=l5l5eophmK4&t=551) | SSMS コンテキスト メニュー:**レポート** &gt; **トランザクション パフォーマンス分析** |
| &nbsp; &nbsp; [10:38](https://www.youtube.com/watch?v=l5l5eophmK4&t=638) | SSMS コンテキスト メニュー:**メモリ最適化アドバイザー**<br/> &nbsp; &nbsp; 実際には、通常のテーブルからメモリ最適化テーブルを作成し、さらにデータを移行します。 |
| &nbsp; &nbsp; [11:28](https://www.youtube.com/watch?v=l5l5eophmK4&t=688) | デモを再実行します。45 倍の速度向上を参照してください。 |
| <br/>E.&nbsp;[12:17](https://www.youtube.com/watch?v=l5l5eophmK4&t=737) | <br/>SQL Server 2016 では (2014 と比較して) インメモリ OLTP を使いやすくなりました。 |
| &nbsp; &nbsp; [12:43](https://www.youtube.com/watch?v=l5l5eophmK4&t=763) | アプリの移行に役立つ簡単な分析。 |
| &nbsp; &nbsp; [13:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=783) | Transact-SQL 言語のサポートが強化されたため、アプリの移行の複雑さが軽減されました (たとえば、外部キーやトリガーなど)。 |
| &nbsp; &nbsp; [13:56](https://www.youtube.com/watch?v=l5l5eophmK4&t=836) | 管理の容易性の向上。<br/> &nbsp; &nbsp; たとえば、スキーマとインデックスの変更、統計の自動更新などです。 |
| <br/>F.&nbsp;[14:46](https://www.youtube.com/watch?v=l5l5eophmK4&t=886) | <br/>スケーラビリティの向上。 |
| &nbsp; &nbsp; [15:12](https://www.youtube.com/watch?v=l5l5eophmK4&t=912) | 大規模なメモリ最適化テーブル (データベースあたり最大 2 TB)。 |
| &nbsp; &nbsp; [15:34](https://www.youtube.com/watch?v=l5l5eophmK4&t=934) | さらに優れたスケーリング。 |
| &nbsp; &nbsp; [16:41](https://www.youtube.com/watch?v=l5l5eophmK4&t=1001) | 既存のリソースを使用して、さらに多くのことを行うことができます。 |
| <br/>G.&nbsp;[16:53](https://www.youtube.com/watch?v=l5l5eophmK4&t=1013) | <br/>最後のコメント (17:32 で終了)。 |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>参照  
 [データベース機能](../../relational-databases/database-features.md)  
  
  
