---
title: Transact-SQL エディターのオプション | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.RESULTS_TO_GRID
- sql.data.tools.SqlExecutionAdvancedSettingsOption
- sql.data.tools.SqlExecutionAnsiSettingsDlg
- sql.data.tools.SqlResultToTextSettingsDlg
- sql.data.tools.SqlExecutionGeneralSettingsDlg
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.GENERAL
- sql.data.tools.unittesting.tsqleditor
- sql.data.tools.SqlResultsToGridSettingsDlg
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.EDITOR_TAB_AND_STATUS_BAR
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.RESULTS_TO_TEXT
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.ANSI
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.ONLINE_EDITING
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.ADVANCED
ms.assetid: fa9a250f-7feb-433e-91bd-a09779d74c8b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e5de3a6bef68955611290cce77b95989b7ff72c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110632"
---
# <a name="transact-sql-editor-options"></a>Transact-SQL エディターのオプション
このトピックでは、Transact-SQL エディターのいくつかのオプションについて説明します。 これらのオプションを設定するには、 **[ツール] > [オプション]** を選択して、 **[オプション]** ダイアログ ボックスに移動します。  
  
[クエリの実行](#QueryExecution)  
  
[クエリの結果](#QueryResults)  
  
## <a name="QueryExecution"></a>クエリの実行  
  
|プロパティ|[説明]|  
|------------|---------------|  
|**SET ROWCOUNT**|既定値の 0 は、SQL Server がすべての結果を受け取るまで待機することを意味します。 SQL Server が指定された行数を取得した後にクエリを停止するように設定するには、0 より大きい値を指定します。 このオプションをオフにして、すべての行が返されるようにするには、SET ROWCOUNT 0 を指定してください。|  
|**SET TEXTSIZE**|既定値の 2,147,483,647 バイトは、SQL Server が text、ntext、nvarchar(max)、および varchar(max) の各データ フィールドの上限まで、完全なデータ フィールドを提供することを示します。 XML データ型は影響を受けません。 大きな値の場合に結果を制限するには、これより小さなサイズを指定します。 指定されたサイズよりも大きい列は切り捨てられます。|  
|**[実行タイムアウト]**|クエリを取り消すまで待機する秒数を示します。 値 0 は、待ち時間が無限 (タイムアウトなし) であることを示します。|  
|**既定で、新しいクエリを SQLCMD モードで開始する**|新しいクエリを SQLCMD モードで開始するには、このチェック ボックスをオンにします。 このチェック ボックスは、[ツール] メニューからダイアログ ボックスを開いたときだけ表示されます。<br /><br />このオプションを選択する場合は、次の制限事項に注意してください。<br /><br />-   データベース エンジン クエリ エディターの IntelliSense が無効になります。<br />-   クエリ エディターはコマンド ラインから実行できないため、変数などのコマンド ライン パラメーターを渡すことができません。<br />-   クエリ エディターはオペレーティング システムのプロンプトに応答できないため、対話型のステートメントを実行しないように注意する必要があります。|  
|**SET NOCOUNT**|Transact-SQL ステートメントで処理された行数を示すメッセージが結果の一部として返されないようにします。 詳細については、「 [SET NOCOUNT](https://go.microsoft.com/fwlink/?LinkID=238731)」を参照してください。|  
|**SET NOEXEC**|**ON** のとき、Microsoft® SQL Server™ に対して、Transact-SQL ステートメントの各バッチをコンパイルしても実行しないように指示します。 **OFF** のとき、Microsoft® SQL Server™ に対して、コンパイルした後にすべてのバッチを実行するように指示します。詳しくは、「[SET NOEXEC](https://go.microsoft.com/fwlink/?LinkId=238770)」をご覧ください。|  
|**SET PARSEONLY**|各 Transact-SQL ステートメントのコンパイルや実行を行わずに、ステートメントの構文をチェックし、エラーがあるときはエラー メッセージを返します。 詳細については、「 [SET PARSEONLY](https://go.microsoft.com/fwlink/?LinkId=238734)」を参照してください。|  
|**SET CONCAT_NULL_YIELDS_NULL**|連結の結果を NULL として取り扱うのか、空文字列として取り扱うのかを制御します。詳しくは、「[SET CONCAT_NULL_YIELDS_NULL](https://go.microsoft.com/fwlink/?LinkId=238733)」をご覧ください。|  
|**SET ARITHABORT**|クエリ実行中にオーバーフローまたは 0 除算のエラーが発生した場合に、クエリを終了します。 詳しくは、「[SET ARITHABORT](https://msdn.microsoft.com/library/aa259212(v=SQL.80).aspx)」をご覧ください。|  
|**SET SHOWPLAN_TEXT**|Microsoft® SQL Server™ で Transact-SQL ステートメントを実行せず、 代わりにステートメントの実行方法に関する詳細情報を返します。 詳しくは、「[SET SHOWPLAN_TEXT](https://go.microsoft.com/fwlink/?LinkID=238737)」をご覧ください。|  
|**SET STATISTICS TIME**|各ステートメントの解析、コンパイル、および実行に必要な時間をミリ秒単位で表示します。|  
|**SET STATISTICS IO**|Microsoft® SQL Server™ で、Transact-SQL ステートメントのディスク利用状況に関する情報を表示します。|  
|**SET TRANSACTION ISOLATION LEVEL**|接続で実行される Microsoft® SQL Server™ のすべての **SELECT** ステートメントに対する既定のトランザクション ロック動作を制御します。 詳細については、「  [SET TRANSACTION ISOLATION LEVEL](https://go.microsoft.com/fwlink/?LinkId=238730)」を参照してください。|  
|**SET LOCK_TIMEOUT**|ロックが解除されるまでのステートメントの待ち時間をミリ秒単位で指定します。 詳しくは、「[SET LOCK_TIMEOUT](https://go.microsoft.com/fwlink/?LinkId=238747)」をご覧ください。|  
|**SET QUERY_GOVERNOR_COST_LIMIT**|現在の接続に対して現在の構成値をオーバーライドします。 詳しくは、「[SET QUERY_GOVERNOR_COST_LIMIT](https://go.microsoft.com/fwlink/?LinkId=238749)」をご覧ください。|  
|**SET ANSI_DEFAULTS**|一部の SQL-92 標準動作をまとめて指定する、Microsoft® SQL Server™ 設定のグループを制御します。 詳しくは、「[SET ANSI_DEFAULTS](https://go.microsoft.com/fwlink/?LinkId=238750)」をご覧ください。|  
|**SET QUOTED_IDENTIFIER**|Microsoft® SQL Server™ に対して、識別子とリテラル文字列を区切る引用符に関して、SQL-92 規格に従うことを指定します。 二重引用符で区切ることで、Transact-SQL の予約済みキーワードを識別子として指定することや、Transact-SQL の構文規則で通常は識別子として使用が認められていない文字を使用することができます。詳しくは、「[SET QUOTED_IDENTIFIER](https://go.microsoft.com/fwlink/?LinkId=238751)」をご覧ください。|  
|**SET ANSI_NULL_DFLT_ON**|データベースの Ansi Null Default オプションが false に設定されているときに、セッションの動作を変更して、新しい列で NULL 値を許可するかどうかの既定の設定をオーバーライドします。 詳しくは、「[SET ANSI_NULL_DFLT_ON](https://go.microsoft.com/fwlink/?LinkID=238752)」をご覧ください。|  
|**[SET IMPLICIT_TRANSACTIONS]**|**ON**のとき、接続は暗黙のトランザクション モードに設定されます。 **OFF**のとき、接続は自動コミット トランザクション モードに戻ります。 詳しくは、「[SET IMPLICIT_TRANSACTIONS](https://go.microsoft.com/fwlink/?LinkId=238753)」をご覧ください。|  
|**SET CURSOR_CLOSE_ON_COMMIT**|トランザクションをコミットするときにカーソルを閉じるかどうかを制御します。 詳しくは、「[SET CURSOR_CLOSE_ON_COMMIT](https://go.microsoft.com/fwlink/?LinkId=238754)」をご覧ください。|  
|**SET ANSI_PADDING**|**char**、 **varchar**、 **binary**、 **varbinary** 型のデータにおいて、列の定義サイズより短い値や末尾に空白がある値を格納する方法を制御します。 詳しくは、「[SET ANSI_PADDING](https://go.microsoft.com/fwlink/?LinkId=238755)」をご覧ください。|  
|**SET ANSI_WARNINGS**|いくつかのエラー条件に対して SQL-92 標準の動作を実行することを指定します。詳しくは、「[SET ANSI_WARNINGS](https://go.microsoft.com/fwlink/?LinkId=238758)」をご覧ください。|  
|**SET ANSI_NULLS**|等号 ( **=** ) 比較演算子と不等号 ( **<>** ) 比較演算子を NULL 値に対して使用した場合の、SQL-92 準拠動作を指定します。詳しくは、「[SET ANSI_NULLS](https://go.microsoft.com/fwlink/?LinkId=238759)」をご覧ください。|  
  
## <a name="QueryResults"></a>クエリの結果  
  
|プロパティ|[説明]|  
|------------|---------------|  
|**結果セットにクエリを含める**|クエリのテキストを結果セットの一部として返します。|  
|**結果のコピーまたは保存時に列のヘッダーを含める**|結果をクリップボードにコピーしたりファイルに保存したりするときに、列のヘッダー (タイトル) を含めます。 保存またはコピーされる結果データに列の見出しを含めずに、データだけ保存またはコピーするには、このチェック ボックスをオフにします。|  
|**実行後に結果を破棄する**|画面表示がクエリ結果を受け取った後にクエリ結果を破棄することによって、メモリを解放します。|  
|**結果を別のタブに表示する**|結果セットを、クエリ ドキュメント ウィンドウの下部ではなく、新しいドキュメント ウィンドウに表示します。|  
|**クエリ実行後に [結果] タブに切り替える**|画面のフォーカスを自動的に結果セットに設定します。|  
|**取得される最大文字数**|[XML 以外のデータ]<br /><br />1 ～ 65,535 の値を入力して、各セルに表示される最大文字数を指定します。 **注:** 大きな文字数を指定すると、結果セット内のデータが切り捨てられたように見える場合があります。 各セルに表示される最大文字数は、フォントのサイズに依存します。 大きな結果セットが返された場合、このボックスに大きな値を指定していると、SQL Server Management Studio のメモリ上での実行速度が低下したり、システムのパフォーマンスに悪影響が及んだりすることがあります。<br /><br />[XML データ]<br /><br />[1 MB]、[2 MB]、または [5 MB] を選択します。 すべての文字を取得する場合は、[無制限] を選択します。|  
|**出力形式**|既定では、スペースを埋め込んで作成された結果が列に表示されます。 他のオプションは、コンマ、タブ、またはスペースを使用して列を区切るオプションです。 **[独自の区切り記号]** ボックスに他の区切り記号を指定するには、 **[独自の区切り記号]** チェック ボックスをオンにします。|  
|**独自の区切り記号**|列を区切るために使用する文字を指定します。 このオプションは、 **[出力形式]** ボックスの **[独自の区切り記号]** チェック ボックスをオンにした場合にのみ利用できます。|  
|**列のヘッダーを結果セットに含める**|各列に列タイトルのラベルを付けない場合は、このチェック ボックスをオフにします。|  
|**受け取った順に結果をスクロールする**|末尾の最新の取得レコードに常に表示フォーカスを置く場合は、このチェック ボックスをオンにします。 常に、取得した最初の行に表示フォーカスを置く場合は、このチェック ボックスをオフにします。|  
|**数値を右揃えにする**|数値を列の右揃えにする場合は、このチェック ボックスをオンにします。 このオプションにより、固定小数点数の数値を簡単に調べることができます。|  
|**クエリの実行後に結果を破棄する**|画面表示が、クエリ結果を受け取った後にクエリ結果を破棄することによって、メモリを解放します。|  
|**結果を別のタブに表示する**|クエリ ドキュメント ウィンドウの下部ではなく、新しいドキュメント ウィンドウに結果セットを表示する場合は、このチェック ボックスをオンにします。|  
|**クエリ実行後に [結果] タブに切り替える**|画面のフォーカスを自動的に結果セットに設定するには、これをクリックします。|  
|**各列に表示される最大文字数**|この値は既定で 256 になっています。 この値を大きくすると、結果セットが切り詰めなしで大きく表示されます。|  
|**既定値にリセット**|このページ上のすべての値を元の既定値にリセットします。|  
  
