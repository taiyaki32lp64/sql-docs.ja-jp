---
title: SSMS を使用して SQL Server on Linux を管理する
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 05/21/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.openlocfilehash: 753845d41c946d955b80a927901f827ee4643567
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000092"
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Windows で SQL Server Management Studio を使用して SQL Server on Linux を管理する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) の概要と、いくつかの一般的なタスクについて説明します。 SSMS は Windows アプリケーションです。Linux 上のリモート SQL Server インスタンスに接続できる Windows コンピューターがある場合は SSMS を使用してください。

> [!TIP]
> SSMS を実行する Windows コンピューターがない場合は、新しい [Azure Data Studio](../azure-data-studio/index.md) の使用を検討してください。 これは SQL Server を管理するためのグラフィカル ツールで、Linux と Windows の両方で実行できます。

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) は、開発や管理上のニーズに向けて Microsoft が無料で提供している一連の SQL ツールの一部です。 SSMS は、SQL Server のすべてのコンポーネントを構成、管理、開発し、それらのコンポーネントへアクセスするための統合環境です。 オンプレミス、Docker コンテナー、クラウドのいずれのプラットフォームで実行されている SQL Server にも接続できます。 また、Azure SQL Database と Azure SQL Data Warehouse にも接続できます。 SSMS では、さまざまなグラフィック ツールと、機能の豊富な多くのスクリプト エディターが用意されています。これにより、あらゆるスキル レベルの開発者や管理者が SQL Server にアクセスできるようになっています。

SSMS には、SQL Server 用のさまざまな開発機能や管理機能が用意されています。具体的には次のことが行なえます。

- 単一または複数の SQL Server インスタンスを構成、監視、管理する
- データベースやデータ ウェアハウスなどのデータ層コンポーネントをデプロイ、監視、アップグレードする
- データベースをバックアップし、復元する
- T-SQL クエリやスクリプトを作成して実行し、結果を表示する
- データベース オブジェクト用の T-SQL スクリプトを生成する
- データベース内のデータを表示および編集する
- T-SQL クエリやデータベース オブジェクト (ビュー、テーブル、ストアド プロシージャなど) を視覚的にデザインする

SSMS の詳細については、「[SSMS とは](../ssms/sql-server-management-studio-ssms.md)」を参照してください。

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>最新バージョンの SQL Server Management Studio (SSMS) をインストールする

SQL Server を操作する際には、常に最新版の SQL Server Management Studio (SSMS) を使用してください。 最新バージョンの SSMS は継続的に更新および最適化されています。現在、SSMS は SQL Server on Linux で動作します。 最新バージョンをダウンロードしてインストールする方法については、「[SQL Server Management Studio (SSMS) のダウンロード](../ssms/download-sql-server-management-studio-ssms.md)」を参照してください。 最新バージョンの SSMS では、最新の状態を維持するため、ダウンロード可能な新バージョンがある場合にメッセージが表示されます。

> [!NOTE]
> SSMS を使用して Linux を管理する前に、Linux 上での SSMS に関する[既知の問題](sql-server-linux-release-notes.md)を確認してください。

## <a name="connect-to-sql-server-on-linux"></a>SQL Server on Linux への接続

接続するには、次の基本的な手順を使用します。

1. Windows の検索ボックスに「**Microsoft SQL Server Management Studio**」と入力して SSMS を起動し、デスクトップ アプリをクリックします。

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png)

1. **[サーバーに接続]** ウィンドウで、次の情報を入力します (SSMS が既に実行されている場合は、 **[接続] > [データベース エンジン]** をクリックして **[サーバーに接続]** ウィンドウを開きます)。

   | 設定 | [説明] |
   |-----|-----|
   | **サーバーの種類** | 既定値はデータベース エンジンです。この値は変更しないでください。 |
   | **サーバー名** | ターゲットの Linux SQL Server マシンの名前か、その IP アドレスを入力します。 |
   | **[認証]** | SQL Server on Linux の場合は、 **[SQL Server 認証]** を使用します。 |
   | **Login** | サーバー上のデータベースへのアクセス権を持つユーザーの名前 (たとえば、セットアップ中に作成された既定の **SA** アカウント) を入力します。 |
   | **パスワード** | 指定したユーザーのパスワードを入力します (**SA** アカウントの場合は、セットアップ時に作成したものを入力します)。 |

    ![SQL Server Management Studio:SQL Database サーバーへの接続](./media/sql-server-linux-manage-ssms/connect.png)

1. **[接続]** をクリックします。

    > [!TIP]
    > 接続エラーが発生した場合は、まずエラー メッセージから問題を診断します。 次に、[接続のトラブルシューティングに関する推奨事項](sql-server-linux-troubleshooting-guide.md#connection)を確認します。
 
1. SQL Server に正常に接続すると**オブジェクト エクスプローラー**が開き、データベースにアクセスして管理タスクを実行したり、データを照会したりできるようになります。

## <a name="run-transact-sql-queries"></a>Transact-SQL クエリの実行

サーバーに接続したら、データベースに接続して Transact-SQL クエリを実行できます。 Transact-SQL クエリは、ほぼすべてのデータベース タスクに使用できます。

1. **オブジェクト エクスプローラー**で、サーバー上のターゲット データベースに移動します。 たとえば、**master** データベースを操作するには、 **[システム データベース]** を展開します。

1. データベースを右クリックし、 **[新しいクエリ]** をクリックします。

1. クエリ ウィンドウで、サーバー上のすべてのデータベースの名前を返す Transact-SQL クエリを記述します。

   ```sql
   SELECT [Name]
   FROM sys.Databases
   ```

   クエリの記述についてよく知らない場合は、「[Transact-SQL ステートメントの作成](../t-sql/tutorial-writing-transact-sql-statements.md)」を参照してください。

1. **[実行]** ボタンをクリックしてクエリを実行し、結果を確認します。

   ![正常終了しました。 SQL Database サーバーへの接続:SQL Server Management Studio](./media/sql-server-linux-manage-ssms/execute-query.png)

Transact-SQL クエリはほとんどの管理タスクに使用できますが、SSMS のグラフィカル ツールを使用すれば、SQL Server をより簡単に管理することができます。 以下のセクションでは、グラフィカル ユーザー インターフェイスの使用例をいくつか紹介します。

## <a name="create-and-manage-databases"></a>データベースの作成と管理

*master* データベースに接続しているときには、サーバー上にデータベースを作成したり、既存のデータベースを変更または削除したりできます。 次の手順では、Management Studio を使用していくつかの一般的なデータベース管理タスクを実行する方法について説明します。 これらのタスクを実行する際には、SQL Server on Linux を設定するときに作成したサーバーレベルのプリンシパル ログインを使用して *master* データベースに接続していることを確認してください。

### <a name="create-a-new-database"></a>新しいデータベースの作成

1. SSMS を起動し、SQL Server on Linux 内のサーバーに接続します

2. オブジェクト エクスプローラーで、 *[データベース]* フォルダーを右クリックし、[*新しいデータベース...] をクリックします

3. *[新しいデータベース]* ダイアログで、新しいデータベースの名前を入力し、 *[OK]* をクリックします

サーバーに新しいデータベースが正常に作成されます。 T-SQL を使用して新しいデータベースを作成する場合は、「[CREATE DATABASE (SQL Server Transact-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md)」を参照してください。

### <a name="drop-a-database"></a>データベースの削除

1. SSMS を起動し、SQL Server on Linux 内のサーバーに接続します

2. オブジェクト エクスプローラーで、 *[データベース]* フォルダーを展開して、サーバー上のすべてのデータベースの一覧を表示します。

3. オブジェクト エクスプローラーで、削除するデータベースを右クリックし、 *[削除]* をクリックします

4. *[オブジェクトの削除]* ダイアログで、 *[既存の接続を閉じる]* をオンにし、 *[OK]* をクリックします

データベースがサーバーから正常に削除されます。 T-SQL を使用してデータベースを削除する場合は、「[DROP DATABASE (SQL Server Transact-SQL)](../t-sql/statements/drop-database-transact-sql.md)」を参照してください。

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>利用状況モニターを使用して SQL Server のアクティビティに関する情報を表示する

SQL Server Management Studio (SSMS) には、[利用状況モニター](../relational-databases/performance-monitor/activity-monitor.md) ツールが組み込まれています。このツールでは、SQL Server プロセスに関する情報や、それらのプロセスが SQL Server の現在のインスタンスに与える影響について確認できます。

1. SSMS を起動し、SQL Server on Linux 内のサーバーに接続します

1. オブジェクト エクスプローラーで、"*サーバー*" ノードを右クリックし、"*利用状況モニター*" をクリックします

利用状況モニターには、展開と折りたたみが可能なペインと、次の情報が表示されます。

- 概要
- プロセス
- リソースの待機
- データ ファイル I/O
- 最近コストの高いクエリ
- アクティブなコストの高いクエリ

ペインが展開されると、利用状況モニターによってインスタンスに対して情報のクエリが実行されます。 ペインを折りたたむと、そのペインのすべての利用状況クエリが停止します。 1 つ以上のペインを同時に展開し、インスタンスのさまざまな利用状況を表示することができます。

## <a name="see-also"></a>参照
- [SSMS とは](../ssms/sql-server-management-studio-ssms.md)
- [SSMS を使用したデータベースのエクスポートとインポート](sql-server-linux-migrate-ssms.md)
- [チュートリアル: SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
- [チュートリアル: Transact-SQL ステートメントの作成](../t-sql/tutorial-writing-transact-sql-statements.md)
- [サーバーのパフォーマンスと利用状況の監視](../relational-databases/performance/server-performance-and-activity-monitoring.md)
