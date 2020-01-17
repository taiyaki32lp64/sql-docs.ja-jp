---
title: データベース エンジン クエリ エディター (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26a6e67287c7a2effdd62604fa492a532ed636bf
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263504"
---
# <a name="database-engine-query-editor-sql-server-management-studio"></a>データベース エンジン クエリ エディター (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターを使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを含んだスクリプトの作成と実行を行います。 **sqlcmd** コマンドを含んだスクリプトの実行もサポートされます。  
  
## <a name="transact-sql-f1-help"></a>Transact-SQL F1 ヘルプ  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターは F1 ヘルプをサポートしており、特定の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントから、関連するリファレンス トピックに移動することができます。 それには、Transact-SQL ステートメントの名前を強調表示し、F1 キーを押します。 強調表示した文字列と一致する F1 ヘルプ属性を持ったトピックが、ヘルプの検索エンジンによって検索されます。  
  
 強調表示した文字列と完全に一致する F1 ヘルプ キーワードに該当するトピックが見つからなかった場合は、このトピックが表示されます。 その場合は、次の 2 つの方法で、目的のヘルプを探すことができます。  
  
-   強調表示した文字列をエディターからコピーし、SQL Server オンライン ブックの検索タブに貼り付けて検索を実行します。  
  
-   Transact-SQL ステートメントで、トピックに適用されている F1 ヘルプ キーワードと一致しそうな部分を強調表示してから再度 F1 キーを押します。 トピックに割り当てられている F1 ヘルプ キーワードと強調表示した文字列とが完全に一致している必要があります。 強調表示した文字列に、列名やパラメーター名など、特定の環境にしか存在しないような要素が含まれていると、検索エンジンが一致を見つけることができません。 強調表示する文字列の例を次に示します。  
  
    -   Transact-SQL ステートメントの名前 (SELECT、CREATE DATABASE、BEGIN TRANSACTION など)。  
  
    -   組み込み関数の名前 (SERVERPROPERTY、@@VERSION など)。  
  
    -   システム ストアド プロシージャのテーブル名やビュー名 (sys.data_spaces、sp_tableoption など)。  
  
## <a name="working-with-the-database-engine-query-editor"></a>データベース エンジン クエリ エディターを使用した作業  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] に実装されている 4 つのエディターの 1 つです。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターに実装されている機能の詳細と、このエディターを使用して実行できる主な作業については、「[クエリおよびテキスト エディター &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)」をご覧ください。  
  
## <a name="sql-editor-toolbar"></a>SQL エディター ツール バー  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターが開いているときは、次のボタンを持つ SQL エディター ツール バーが表示されます。  
  
 **のインスタンスに接続するときには、**  
 **[サーバーへの接続]** ダイアログ ボックスを開きます。 このダイアログ ボックスを使用すると、サーバーへの接続を確立できます。  
  
 **[接続解除]**  
 現在のクエリ エディターをサーバーから接続解除します。  
  
 **[接続の変更]**  
 **[サーバーへの接続]** ダイアログ ボックスを開きます。 このダイアログ ボックスを使用すると、別のサーバーへの接続を確立できます。  
  
 **[新しいクエリを現在の接続で実行]**  
 新しいクエリ エディター ウィンドウを開き、現在のクエリ エディター ウィンドウの接続情報を使用します。  
  
 **[使用できるデータベース]**  
 接続を同じサーバー上の別のデータベースに変更します。  
  
 **Execute**  
 選択されているコードを実行します。コードが選択されていない場合は、クエリ エディター内のコード全体を実行します。  
  
 **デバッグ**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーを有効にします。 このデバッガーでは、ブレークポイントの設定、変数の監視、コードのステップ実行などのデバッグ操作がサポートされます。  
  
 **[クエリ実行のキャンセル]**  
 キャンセル要求をサーバーに送信します。 即座にキャンセルできないクエリもあります。そのようなクエリは、適切なキャンセル条件が整うまでキャンセルできません。 トランザクションが取り消されると、トランザクションがロールバックされる間に遅延が発生することがあります。  
  
 **[解析]**  
 選択されているコードの構文をチェックします。 コードが選択されていない場合は、クエリ エディター ウィンドウ内のコード全体の構文をチェックします。  
  
 **[推定実行プランの表示]**  
 実際にクエリを実行することなくクエリ プロセッサからクエリ実行プランを要求し、プランを **[実行プラン]** ウィンドウに表示します。 このプランでは、クエリ実行中の各部分で返される行数の推定として、インデックス統計が使用されます。 実際に使用されるクエリ プランは、推定実行プランとは異なる場合があります。 この状況は、返される行数が推定値と大幅に異なり、クエリ プロセッサによってプランが効率化される場合に発生する可能性があります。  
  
 **[クエリ オプション]**  
 **[クエリ オプション]** ダイアログ ボックスを開きます。 このダイアログ ボックスを使用すると、クエリの実行およびクエリ結果に関する既定のオプションを構成できます。  
  
 **[IntelliSense が有効]**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターで IntelliSense 機能が使用できるかどうかを示します。  
  
 **[実際の実行プランを含める]**  
 クエリを実行し、クエリ結果と、クエリに対して使用された実行プランを返します。 このクエリ結果と実行プランは、グラフィカルなクエリ プランとして **[実行プラン]** ウィンドウに表示されます。  
  
 **[クライアント統計を含める]**  
 クエリおよびネットワーク パケットに関する統計、およびクエリの経過時間を表示する **[クライアント統計]** ウィンドウを含めます。  
  
 **[結果をテキストで表示]**  
 クエリ結果をテキストとして **[結果]** ウィンドウに表示します。  
  
 **[結果をグリッドに表示]**  
 クエリ結果を 1 つまたは複数のグリッドとして **[結果]** ウィンドウに表示します。  
  
 **[結果をファイルに出力]**  
 クエリを実行したときに、 **[結果の保存]** ダイアログ ボックスが開きます。 ファイルを保存するフォルダーを **[保存先]** で選択します。 **[ファイル名]** にファイルの名前を入力し、 **[保存]** をクリックして、拡張子 .rpt を持つ **レポート** ファイルとしてクエリ結果を保存します。 詳細設定オプションを指定するには、 **[保存]** ボタンの下向き矢印をクリックし、 **[エンコード付きで保存]** をクリックします。  
  
 **[選択範囲のコメント]**  
 行の先頭にコメント演算子 (--) を追加することで、現在の行をコメントにします。  
  
 **[選択範囲のコメントを解除]**  
 行の先頭にあるコメント演算子 (--) をすべて削除することで、現在の行をアクティブなソース ステートメントにします。  
  
 **[行インデント解除]**  
 行の先頭にある空白を削除することで、行のテキストを左方向へ移動します。  
  
 **[行インデント]**  
 行の先頭に空白を追加することで、行のテキストを右方向へ移動します。  
  
 **[テンプレート パラメーターの値の指定]**  
 ストアド プロシージャや関数のパラメーター値を指定するためのダイアログ ボックスを開きます。  
  
 また、 **[表示]** メニューの **[ツール バー]** を選択し、 **[SQL エディター]** を選択して、SQL エディター ツール バーを追加することもできます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターのウィンドウが開いていない状態で SQL エディター ツール バーを追加した場合、ボタンは使用できません。  
  
## <a name="sql-editor-toolbar"></a>SQL エディター ツール バー  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウが開いているときに、 **[表示]** メニューから **[ツール バー]** 、 **[デバッグ]** の順に選択すると、[デバッグ] ツール バーが追加されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウが開いていない状態で [デバッグ] ツール バーを追加した場合、ボタンは使用できません。  
  
 **Continue**  
 ブレークポイントに達するまで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウ内のコードを実行します。  
  
 **[すべて中断]**  
 中断が生じたときに、デバッガーがアタッチされているすべてのプロセスを中断するようにデバッガーを設定します。  
  
 **[デバッグの停止]**  
 選択された [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウのデバッグ モードを解除して、標準の実行モードに戻します。  
  
 **[次のステートメントの表示]**  
 次に実行されるステートメントにカーソルを移動します。  
  
 **[ステップ イン]**  
 次のステートメントが実行されます。 ステートメントで Transact-SQL ストアド プロシージャ、関数、またはトリガーが呼び出される場合、モジュールのコードが含まれた新しい **クエリ エディター** ウィンドウが表示されます。 ウィンドウはデバッグ モードに設定され、実行はモジュールの最初のステートメントで一時停止します。 その後、モジュールに対して、ブレークポイントの設定やコードのステップ実行などの操作を行うことができます。  
  
 **[ステップ オーバー]**  
 次のステートメントが実行されます。 ステートメントで Transact-SQL ストアド プロシージャ、関数、またはトリガーが呼び出される場合、モジュールは完了するまで実行され、その結果が呼び出し元のコードに返されます。 モジュールにエラーがないことがわかっている場合は、それをステップ オーバーできます。 実行は、モジュールへの呼び出しに続くステートメントで一時停止します。  
  
 **[ステップ アウト]**  
 この次に高い呼び出しレベル (関数、ストアド プロシージャ、またはトリガー) に戻ります。 実行は、ストアド プロシージャ、関数、またはトリガーの呼び出しに続くステートメントで一時停止します。  
  
 **Windows**  
 **[ブレークポイント]** ウィンドウまたは **[イミディエイト]** ウィンドウを開きます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Management Studio のキーボード ショートカット](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
