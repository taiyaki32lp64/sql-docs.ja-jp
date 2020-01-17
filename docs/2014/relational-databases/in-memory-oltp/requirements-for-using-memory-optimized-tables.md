---
title: メモリ最適化テーブルを使用するための要件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9b9e442fb97245d32c398602cdfd727de8239cb8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62467909"
---
# <a name="requirements-for-using-memory-optimized-tables"></a>メモリ最適化テーブルを使用するための要件
  加え、 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)、インメモリ OLTP を使用するための要件を次に示します。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]の 64 ビット Enterprise Edition、Developer Edition、または Evaluation Edition。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、メモリ最適化テーブルおよびインデックスでデータを保持するために十分なメモリが必要です。 行バージョンも保持するためには、メモリ最適化テーブルおよびインデックスの予想サイズの 2 倍となるメモリ量を用意する必要があります。 ただし、必要なメモリの実際の容量はワークロードによって異なります。 メモリの使用量を監視し、必要に応じて調整を加える必要があります。 メモリ最適化テーブル データのサイズは、プールの容量のうち、許可されたパーセンテージを超えないようにする必要があります。 メモリ最適化テーブルのサイズを検出するには、次を参照してください。 [sys.dm_db_xtp_table_memory_stats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql)します。  
  
     データベースにディスク ベース テーブルがある場合、それらのテーブルのバッファー プールとクエリ処理に十分なメモリを提供する必要があります。  
  
     インメモリ OLTP アプリケーションで必要になるメモリの量を把握しておくことが重要です。 詳細については、「 [メモリ最適化テーブルのメモリ必要量の推定](memory-optimized-tables.md) 」を参照してください。  
  
-   持続性メモリ最適化テーブルの 2 倍のサイズの空きディスク領域。  
  
-   インメモリ OLTP を使用するための **cmpxchg16b** 命令をサポートするプロセッサ。 最新のすべての 64 ビット プロセッサでは **cmpxchg16b**がサポートされています。  
  
     VM ホスト アプリケーションを使用していて、古いプロセッサが原因のエラーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって表示される場合は、アプリケーションに **cmpxchg16b**を許可する構成オプションがあるかどうかをご確認ください。 該当する構成オプションがない場合は、Hyper-V を使用できます。Hyper-V では、構成オプションを変更しなくても、 **cmpxchg16b** がサポートされています。  
  
-   インメモリ OLTP をインストールするには、 **のインストール時に** [データベース エンジン サービス] [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]を選択します。  
  
     レポートの生成をインストールする ([Determining if テーブルまたはストアド プロシージャ Should Be Ported to インメモリ OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) と[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)](を使用して、インメモリ OLTP を管理する[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]オブジェクト エクスプ ローラー) を選択します**管理ツール-基本**または**管理ツール-高度な**インストールするときに[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]します。  
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>[!INCLUDE[hek_2](../../../includes/hek-2-md.md)]  
  
-   データベース内の持続性のあるすべてのテーブルのメモリ内サイズの合計は 250 GB を超えないようにする必要があります。 詳細については、次を参照してください。[メモリ最適化テーブルの持続性](durability-for-memory-optimized-tables.md)します。  
  
-   このリリースの [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] は、2 または 4 ソケットおよび 60 未満のコアを備えたシステムで適切に機能するように設定されています。  
  
-   チェックポイント ファイルは手動で削除しないでください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって自動的に不要なチェックポイント ファイルのガベージ コレクションを実行します。 詳細については、内のデータとデルタ ファイルをマージする方法の説明を参照してください。[メモリ最適化テーブルの持続性](durability-for-memory-optimized-tables.md)します。  
  
-   インメモリ OLTP の最初のリリースであるこのリリース ( [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) で、メモリ最適化ファイル グループを削除する唯一の方法は、データベースを削除することです。  
  
-   多数の行を一括処理で削除しようとした場合に、削除対象の行範囲に影響する同時実行の挿入または更新ワークロードが存在すると、削除は失敗する可能性があります。 回避策は、削除を行う前に挿入または更新ワークロードを停止することです。 また、トランザクションを分割し、同時実行ワークロードによって妨害されにくい小さなトランザクションに構成することもできます。 メモリ最適化テーブルに対するすべての書き込み操作と同様に、再試行ロジックを使用します (「[Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](../../database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)」をご覧ください)。  
  
-   メモリ最適化テーブルが含まれるデータベースを 1 つ以上作成する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対してファイルの瞬時初期化を有効にする ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサービス開始アカウントに SE_MANAGE_VOLUME_NAME ユーザー権限を付与する) 必要があります。 ファイルの瞬時初期化を使用しない場合、メモリ最適化ストレージ ファイル (データ ファイルとデルタ ファイル) が作成時に初期化されるため、ワークロードのパフォーマンスが低下する場合があります。 ファイルの瞬時初期化に関する詳細については、「 [データベース ファイルの初期化](../databases/database-instant-file-initialization.md)」をご覧ください。 ファイルの瞬時初期化を有効にする方法については、「 [How and Why to Enable Instant File Initialization (ファイルの瞬時初期化を有効にする方法と理由)](https://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx)」をご覧ください。  
  
## <a name="did-this-article-help-you-were-listening"></a>この記事は役に立ちましたか? 待ちしています  
 どのような情報をお探しでしたか? お探しの情報は見つかりましたか? コンテンツを向上させるためにお客様のフィードバックを受け付けています。 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Requirements%20for%20Using%20Memory-Optimized%20Tables%20page) にコメントをお送りください。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
