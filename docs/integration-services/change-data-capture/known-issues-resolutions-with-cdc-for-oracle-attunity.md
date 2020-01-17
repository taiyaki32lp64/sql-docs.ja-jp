---
title: Change Data Capture for Oracle by Attunity の既知のエラーと解決策 | Microsoft Docs
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ee1e8f3ae65b4a906d42a4b00644456d89f9b900
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71713427"
---
# <a name="known-errors-and-resolutions-with-change-data-capture-for-oracle-by-attunity"></a>Change Data Capture for Oracle by Attunity の既知のエラーと解決策
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md.md)]

このトピックでは、Oracle CDC Designer 構成ツールで CDC (変更データ キャプチャ) インスタンスを表示するときに発生する主な問題と既知の解決策を説明します。 このツールは、SQL Server 2012 以降に付属する Change Data Capture for Oracle by Attunity に含まれています。 

## <a name="bug-fixes"></a>バグの修正
問題解決にあまりに多くの時間を費やす前に、最新版の CDC for Oracle by Attunity を使用して、次のような既知の問題を回避することが重要です。

### <a name="sql-server-2017"></a>SQL Server 2017

**バージョン 5.0.0.111** には次の修正プログラムが含まれています。
- バグの修正 - Oracle テーブルを追加すると、"キーワード 'KEY' 付近に不適切な構文があります" というエラーが発生して、Oracle CDC Designer が失敗します。 
- 改善 - RAC ノードの再起動時の処理が改善されるなど、RAC のサポートが強化されました。 
- バグの修正 - v$log から NEXT_CHANGE# を要求したため、CDC と Oracle 10.2 が連動しません。 


**バージョン 5.0.0.93** には、次の修正プログラムが含まれています。 
- Oracle テーブルを追加すると、"ワード 'KEY' 付近に不適切な構文があります" というエラーが発生して、Microsoft CDC for Oracle by Attunity Designer が失敗します。 

 
### <a name="sql-server-2016"></a>SQL Server 2016

**バージョン 4.0.107** には次の修正プログラムが含まれています。
- バグの修正 - Oracle テーブルを追加すると、"キーワード 'KEY' 付近に不適切な構文があります" というエラーが発生して、Oracle CDC Designer が失敗します。
- 改善 - RAC ノードの再起動時の処理が改善されるなど、RAC のサポートが強化されました。
- バグの修正 - v$log から NEXT_CHANGE# を要求したため、CDC と Oracle 10.2 が連動しません。

**バージョン 4.0.0.95** には次の修正プログラムが含まれています。 
- バグの修正 - Oracle テーブルを追加すると、"キーワード 'KEY' 付近に不適切な構文があります" というエラーが発生して、Oracle CDC Designer が失敗します。

**バージョン 4.0.0.88** には次の修正プログラムが含まれています。
-  テーブルが CDC に追加されるか、CDC から削除されると、Attunity CDC インスタンスの [詳細] オプションに追加されたプロパティが削除されます。 
- __$command_id 列を追加する SQL 修正プログラムを追加すると、Attunity CDC は動作を停止します。

### <a name="sql-server-2014"></a>SQL Server 2014 

**バージョン 2.0.0.114** には次の修正プログラムが含まれています。
- バグの修正 - Oracle テーブルを追加すると、"キーワード 'KEY' 付近に不適切な構文があります" というエラーが発生して、Oracle CDC Designer が失敗します。
- 改善 - RAC ノードの再起動時の処理が改善されるなど、RAC のサポートが強化されました。
- バグの修正 - v$log から NEXT_CHANGE# を要求したため、CDC と Oracle 10.2 が連動しません。

**バージョン 2.0.0.92** には次の修正プログラムが含まれています。 
- テーブルが CDC に追加されるか、CDC から削除されると、Attunity CDC インスタンスの [詳細] オプションに追加されたプロパティが削除されます。 __$command_id 列を追加する SQL 修正プログラムを追加すると、Attunity CDC は動作を停止します。
- Oracle テーブル cdc.table_name のメタデータ検証が失敗しました。 列 column_name インデックスが範囲外です。  また、「CDC for Oracle by Attunity を使用すると、Oracle CDC サービスに中止状態が表示される」の問題が発生します。
    - KB [2894025](https://support.microsoft.com/kb/2894025) で説明されているとおり、_SQL Server 2014 RTM 向け累積更新プログラム 1_ で修正されました。
- 一部の変更が失われ、SQL Server データベースにはレプリケートされません。 この問題は、テーブルに複数の CLOB (Character Large Binary Object) が含まれ、そのうちの 1 つで値が大きいときに発生します。 
    - KB [3029096](https://support.microsoft.com/kb/3029096) で説明されているとおり、_SQL Server 2014 SP1 向け累積更新プログラム 1_ と _SQL Server 2014 RTM 向け累積更新プログラム 8_ で修正されました。 
- Long データ型の列が Oracle テーブルにあると、Change Data Capture for Oracle by Attunity が停止します。
    - KB [3145983](https://support.microsoft.com/kb/3145983) で説明されているとおり、_SQL Server 2014 SP1 向け累積更新プログラム 5_ と _SQL 2014 RTM 向け累積更新プログラム 12_ で修正されました。

### <a name="sql-server-2012"></a>SQL Server 2012

**バージョン 1.1.0.102** には次の修正プログラムが含まれています。 
 
- テーブルが CDC に追加されるか、CDC から削除されると、Attunity CDC インスタンスの [詳細] オプションに追加されたプロパティが削除されます。 __$command_id 列を追加する SQL 修正プログラムを追加すると、Attunity CDC は動作を停止します。
- CDC for Oracle インスタンスが起動時にハングし、変更をキャプチャしません。 Oracle サーバーのメモリがメモリ不足になるか、クラッシュするまで増えることがあります。
- [2672759](https://support.microsoft.com/kb/2672759): Microsoft Change Data Capture Service for Oracle by Attunity の使用時のエラー メッセージ: "ORA-00600: 内部エラー コード"。 SOURCE レベル トレースを追加し、同じ ORA-00600 エラーが表示されるかどうかを確認します。 Oracle パッチ ダウンロードによって修正されました。
- 複数パーティション
    - Oracle テーブルで 10 個を超えるパーティションを使用すると、CDC インスタンスでは、そのテーブルの変更を全部キャプチャできません。 Oracle テーブルが 10 個を超えるパーティションで定義されると、変更は最後の 10 個のパーティションからのみキャプチャされます。 _SQL Server 2012 向け Service Pack 1 リリース_で修正されました。 [SP1 用 Feature Pack のダウンロード ページ](https://www.microsoft.com/download/details.aspx?id=35580)を参照してください。 
- 変更が失われます
    - イベントのキャプチャが無限ループに入り、新しいデータ変更のキャプチャが停止することがあります (Oracle バグ 5623813 に関連)。 Oracle RAC 環境で CDC インスタンスの停止または再開を実行しているとき、変更はスキップされたり、失われたりすることがあります。 つまり、SQL Server 変更データ キャプチャで重要な行が失われ、そのため、データ ウェアハウスやサブスクリプション システムでデータが失われます。 _SQL Server 2012 向け Service Pack 1 リリース_で修正されました。 [SP1 用 Feature Pack のダウンロード ページ](https://www.microsoft.com/download/details.aspx?id=35580)を参照してください
- SQL で列の幅が 2 倍になる
    - CDC for Oracle インスタンスの作成時、SQL Server に対して実行するスクリプトで、変数の幅のデータ型列の長さが、スクリプトで作成された SQL Server テーブルで 2 倍になります。 たとえば、Oracle テーブルで VARCHAR2(10) 列の変更を追跡しようとすると、SQL Server テーブルのそれに対応する列が配置スクリプトで NVARCHAR(20) になります。 KB [2769673](https://support.microsoft.com/kb/2769673) で説明されているとおり、_SQL Server 2012 SP1 向け累積更新プログラム 2_ または _SQL Server 2012 向け累積更新プログラム 5_ で修正されました。 
- DDL データが切り捨てられます
    - ラテン文字以外の文字が含まれる Oracle データベースに 4,000 バイトを超えるデータ定義言語 (DDL) ステートメントを実行すると、CDC for Oracle by Attunity が失敗します。 さらに、エラー メッセージ `ORA-01406: fetched column value was truncated.` が表示されます。 KB [2839806](https://support.microsoft.com/kb/2839806) で説明されているとおり、_SQL Server 2012 SP1 向け累積更新プログラム 4_ で修正されました。 
- 最後の 2 つの列で変更が失われます
    - KB [2874879](https://support.microsoft.com/kb/2874879) で説明されているとおり、_SQL Server 2012 SP1 向け累積更新プログラム 6_ で修正されました。 
- CDC for Oracle を使用すると、SQL Transaction ログが増大します
     - Change Data Capture for Oracle インスタンスを構成するとき、変更後のデータを受け取る SQL データベースにミラー化されたテーブルが与えられ、トランザクションにレプリケーションのマークが付きます。 この動作は、CDC for Oracle が、CDC for SQL Server で使用されているものに似た基礎システム ストアド プロシージャに依存しているために発生します。 しかしながら、CDC for Oracle が単体で使用されるとき、SQL CDC レプリケーションがないため、レプリケーションのマークが付いているトランザクションを消去するログ リーダーはありません。 トランザクションは SQL Server でレプリケートする必要がないため、この記事の後半で説明する回避策を利用し、トランザクションに配布済みのマークを手動で付けるほうが安全です。 詳細は KB [2871474](https://support.microsoft.com/kb/2871474) にあります。 
- エラー `ORACDC000T: Error encountered at position to change event - SCN not found - EOF simulated`。 KB [2883524](https://support.microsoft.com/kb/2883524) で説明されているとおり、_SQL Server 2012 SP1 向け累積更新プログラム 7_ で修正されました。 
- Oracle テーブル cdc.table_name のメタデータ検証が失敗しました。 列 column_name インデックスが範囲外です。 KB [2883524](https://support.microsoft.com/kb/2883524) で説明されているとおり、_SQL Server 2012 SP1 向け累積更新プログラム 7_ で修正されました。
- SQL Server 2012 で CDC for Oracle by Attunity を使用すると、Oracle CDC サービスに中止状態が表示されます。 KB [2923839](https://support.microsoft.com/kb/2923839) で説明されているとおり、_SQL Server 2012 SP1 向け累積更新プログラム 8_ で修正されました。  
- 一部の変更が失われ、SQL Server データベースにはレプリケートされません。 この問題は、テーブルに複数の CLOB (Character Large Binary Object) が含まれ、そのうちの 1 つで値が大きいときに発生します。 KB [2923839](https://support.microsoft.com/kb/2923839) で説明されているとおり、_SQL Server 2012 SP1 向け累積更新プログラム 8_ で修正されました。   
- Long データ型の列が Oracle テーブルにあると、Change Data Capture for Oracle by Attunity が停止します。 KB [3145983](https://support.microsoft.com/kb/3145983) で説明されているとおり、_SQL Server 2012 SP3 向け累積更新プログラム 2_ と _SQL 2012 SP2 向け累積更新プログラム 11_ で修正されました。 

## <a name="collect-detailed-logs"></a>詳細ログの収集 

このセクションでは、CDC インスタンスからエラーとイベントを収集する方法について説明します。 

### <a name="management-console"></a>管理コンソール

Oracle Change Data Capture Designer 管理コンソールでは、CDC インスタンスが左側のペインで強調表示されると、**ステータス** メッセージ フィールドにエラーが表示されます。 

### <a name="query-trace-table"></a>トレース テーブルにクエリを実行する

SQL Server 内で CDC データベースのトレース テーブルにクエリを実行し、ログに記録されているエラーを表示できます。 

### <a name="save-output-from-basic-logging"></a>基本ログからの出力を保存する 

診断をキャプチャするには、Oracle Change Data Capture 管理コンソールの [状態] タブで **[診断情報の収集]** を選択します。 

![診断情報の収集のリンク](media/known-issues-resolutions-with-cdc-for-oracle-attunity/collect-diagnostics.png)

開始時刻を選択し、ログ ファイルの場所を選択します。 次に、 **[作成]** を選択し、診断情報収集を開始します。 

![診断情報の収集のリンク](media/known-issues-resolutions-with-cdc-for-oracle-attunity/start-diagnostics.png)

### <a name="detailed-errors"></a>詳細なエラー

インスタンスによって収集されるトレースのレベルを上げ、シナリオを繰り返して詳細ログをさらに集めることができます。 これを行うには、 **[アクション]** の下で **[プロパティ]** を選択し、 **[詳細]** タブの **[詳細設定]** グリッドで新しいプロパティを追加します。プロパティの名前を `trace` に設定し、値を `SOURCE` に設定します。 

![診断情報の収集のリンク](media/known-issues-resolutions-with-cdc-for-oracle-attunity/properties.png)

エラーを再現し、 **[診断情報の収集]** オプションを選択してログを収集します。 

![診断情報の収集のリンク](media/known-issues-resolutions-with-cdc-for-oracle-attunity/collect-diagnostics.png)

## <a name="ora-00942-table-of-view-does-not-exist"></a>ORA-00942 ビューのテーブルがありません 

これは CDC インスタンスの**ステータス** メッセージ フィールドに表示される一般的なエラーです。 インスタンスの再試行は何回も行われます。そのため、ステータス アイコンは一瞬、緑に変わりますが、その後、赤の感嘆符と UNEXPECTED ステータスが表示され、失敗します。 

![Oracle エラー](media/known-issues-resolutions-with-cdc-for-oracle-attunity/oracle-error.png)

```
"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC508E:Oracle method OCIStmtExecute failed with error: ORA-00942: table or view does not exist ","source","",""

"ERROR","computername","RUNNING","IDLE",
"ORACDC518E:Failed to verify archive log mode.","source","",""

"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC517E:Oracle Call Interface (OCI) method failed: ORA-00942: table or view does not exist .","source","",""

"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC414E:The Engine component failed with return code 1.","engine","",""
```

これは、CDC インスタンスから Oracle サーバーに接続しようとしている Oracle アカウントにシステム ログ ビューを表示する権限が与えられていないときに発生します。 

### <a name="resolution"></a>解決策

このエラーを解決するには、現在構成されているユーザーに、Oracle データベース システム内で適切なアクセス許可を与えるか、CDC インスタンスから Oracle サーバーに接続する際に使用されるアカウントを変更します。 

必須アクセス許可の全リストについては、インストール プログラム ファイル フォルダー `C:\Program Files\Change Data Capture for Oracle by Attunity\Attunity.SqlServer.XdbCdcDesigner.chm` に含まれているヘルプ ファイルで説明されています。  完全なリストが必要であれば、.chm ファイル内にある "Oracle ソース データベースに接続する" というタイトルが付いたページを参照してください。

ユーザー アカウントは、**CDC Designer** ウィンドウ内で、左側のペインから CDCInstance を選択し、右端にある [アクション] ペインで [プロパティ] ボタンを選択して設定できます。 Oracle ログ マイニング認証アカウントはプロパティ ダイアログ ページから変更できます。

![Oracle エラー](media/known-issues-resolutions-with-cdc-for-oracle-attunity/oracle-connection.png)


  
## <a name="see-also"></a>参照  
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [変更データの処理 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [変更データ キャプチャの管理と監視 &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
