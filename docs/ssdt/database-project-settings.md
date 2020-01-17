---
title: データベース プロジェクトの設定 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.DebugProperties
- sql.data.tools.dacsettings.dialog
- sql.data.tools.dbsqlclrlanguagevb
- SQL.DATA.TOOLS.DBADVANCEDBUILDSETTINGSCS
- sql.data.tools.dbadvancedbuildsettingscs
- ql.data.tools.criticalerror.dialog
- sql.data.tools.dbassemblysigningchangekeypassword
- sql.data.tools.advanceddeploymentsystemdefined.dialog
- sql.data.tools.advanceddatabasesettings.dialog
- sql.data.tools.extendedpropertiesvalueeditor.dialog
- sql.data.tools.dbsqlclrlanguagecs
- ql.data.tools.dbassemblysigningpasswordneeded
- sql.data.tools.vbadvancedsettings.dialog
- sql.data.tools.dbsqlclr
- sql.data.tools.SqlCmdVariablesProperties
- sql.data.tools.dbassemblysigning
- sql.data.tools.advanceddeploymentsettings.dialog
- sql.data.tools.advancedpublishsettings.dialog
- sql.data.tools.BuildActionProperties
- sql.data.tools.serverselectionpolicy.dialog
- sql.data.tools.dbadvancedbuildsettingsvb
- sql.data.tools.dbprojectwizard.buildeventcommandline
- sql.data.tools.dbreferencepaths
- sql.data.tools.GeneralProperties
- sql.data.tools.BuildProperties
- sql.data.tools.DeployProperties
- sql.data.tools.csadvancedsettings.dialog
- sql.data.tools.dbassemblyinfo
- sql.data.tools.extendedpropertieseditor.dialog
ms.assetid: 34418730-1aaa-4948-aee2-8f1e62cda85c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4921df6e1602d4cfc98aa6da3733452d6b5d33d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912853"
---
# <a name="database-project-settings"></a>データベース プロジェクトの設定
データベース プロジェクト設定を使用して、データベースの特性とデバッグおよびビルドの構成を制御します。 これらの設定は、以下のカテゴリに分けられます。  
  
-   [プロジェクトの設定](#bkmk_proj_settings)  
  
-   [拡張 Transact-SQL 検証](#bkmk_evf)  
  
-   [SQLCLR](#bkmk_sqlclr)  
  
-   [SQLCLR および SQLCLR ビルド](#bkmk_sqlclr_sqlclrbuild)  
  
-   [ビルド](#bkmk_build)  
  
-   [SQLCMD 変数](#bkmk_sqlcmd_variables)  
  
-   [ビルド イベント](#bkmk_build_events)  
  
-   [デバッグ](#bkmk_debug)  
  
-   [参照パス](#bkmk_ref_paths)  
  
-   [コード分析](#bkmk_code_analysis)  
  
### <a name="to-configure-properties-for-your-database-project"></a>データベース プロジェクトのプロパティを構成するには  
  
1.  **ソリューション エクスプローラー**で、プロパティを構成するデータベース プロジェクトを右クリックし、 **[プロパティ]** をクリックします。  
  
    または、 **ソリューション エクスプローラー** で、プロジェクトの **[プロパティ]** ノードをダブルクリックします。  
  
2.  データベース プロジェクトのプロパティ シートが表示されます。  
  
3.  **[プロジェクトの設定]** タブをクリックします。ここで、データベース プロジェクトのプロパティのうち、全般プロパティを構成できます。 左のペインには、異なるカテゴリのさまざまなタブがあります。  
  
## <a name="bkmk_proj_settings"></a>プロジェクトの設定  
次の表の設定は、このデータベース プロジェクトのすべての構成に対して適用されます。  
  
|フィールド|既定値|[説明]|  
|---------|-----------------|---------------|  
|対象プラットフォーム|Microsoft SQL Server 2012|このデータベース プロジェクトの対象となる SQL Server のバージョンを指定します。|  
|共通オブジェクトに対する拡張 Transact\-SQL 検証を有効にします。|新しいオブジェクトを作成するときは有効になりません。<br /><br />SQL Azure に接続された SQL Server オブジェクト エクスプローラーからプロジェクトを作成するとき、SQL Azure データベースをプロジェクトにインポートするとき、またはプロジェクトのターゲット プラットフォームを SQL Azure に変更するときに有効になります。|このオプションを有効にすると、SQL Server コンパイラの検証に失敗したプロジェクト内で見つかったエラーが報告されます。 ターゲット プラットフォームを SQL Azure に変更すると、拡張検証が有効になります。 ターゲット プラットフォームを変更した場合、オプションはオフになりません。<br /><br />このオプションは他のバージョンの SQL Server に対して有効にすることができますが、検証は Microsoft SQL Server 2012 の部分的包含データベースと SQL Azure に限定されます。 すべての Transact\-SQL 構文がすべてのバージョンの SQL Server でサポートされているわけではありません。<br /><br />詳しくは、このトピックの後半の「[拡張 Transact-SQL 検証](#bkmk_evf)」をご覧ください|  
|出力の種類|||  
|データ層アプリケーション (.dacpac ファイル)|有効な状態でロックされています。 データベース プロジェクトのビルド出力により、プロジェクトのビルド時に .dacpac パッケージが必ず生成されます。|[追加のダウンレベル .dacpac ファイル (v2.0) を作成する] チェック ボックスがある SQL Server Data Tools (SSDT) のバージョンを使用している場合、パッケージに SQL Server Management Studio または SQL Azure Management Portal との互換性を持たせるには、このチェック ボックスをオンにします。 .dacpac パッケージは SSDT から直接配置できますが、SQL Server Data Tools のリリース時点では、SQL Server Management Studio を使用して配置できるのはバージョン 2.0 の .dacpac ファイルのみです。|  
|スクリプト (.sql ファイル) を作成する||プロジェクト内のすべてのオブジェクトを対象に完全な .sql の CREATE スクリプトを生成し、プロジェクトのビルド時にそれを bin\debug フォルダーに保存するかどうかを指定します。 **[プロジェクトの公開]** または SQL Compare ユーティリティを使用して、増分更新スクリプトを作成できます。|  
|ジェネリック|||  
|既定のスキーマ|dbo|SQLCLR オブジェクトと Transact\-SQL オブジェクトの両方が作成される既定のスキーマを指定します。 オブジェクトに対してスキーマを直接指定することによって、この設定をオーバーライドできます。|  
|スキーマ名をファイル名に含める|いいえ|ファイル名にプレフィックスとしてスキーマを含めるかどうかを指定します (たとえば、dbo.Products.table.sql)。 このチェック ボックスをオフにすると、オブジェクトのファイル名は、ObjectName.ObjectType.sql の形式になります (たとえば、Products.table.sql)。|  
|識別子の文字を確認する|はい|プロジェクトのビルド時に、プロジェクトの SQL オブジェクトの識別子の文字種が検証されるかどうかを指定します。 このオプションは、データベースに対して大文字と小文字を区別する照合順序を指定するデータベース プロジェクトに適用されます。|  
|データベースの設定|データベースの標準の構成設定に基づく既定の設定|指定できる設定には、SQL Server データベースの照合の方式やデータベース レベル設定などがあります。|  
  
## <a name="bkmk_evf"></a>拡張 Transact-SQL 検証  
  
> [!IMPORTANT]  
> 拡張 Transact-SQL 検証機能は、SQL Server Data Tools の次回リリースと Visual Studio の次回メジャー リリースから削除されます。  
  
拡張 Transact-SQL 検証は、データベース プロジェクト システム内の機能です。この機能を使用すると、開発者はビルド時にデータベース プロジェクトを Transact-SQL コンパイラ サービスに送信し、SQL Server エンジンのパーサーおよびインタープリターに対してコードを検証できます。  
  
### <a name="transact-sql-compiler-service"></a>Transact-SQL コンパイラ サービス  
Transact-SQL コンパイラ サービスは、Microsoft SQL Server 2012 データベース エンジンに基づくコンポーネントです。 このサービスでは、Microsoft SQL Server 2012 データベース エンジンと同じ忠実性で DDL ステートメントの構文とセマンティクスを検証することができます。 つまり、本質的に、コンパイラ サービスは Microsoft SQL Server 2012 で非推奨になっている構文や機能をサポートしません。 非推奨の機能の詳細については、「[SQL Server 2012 で廃止されたデータベース エンジンの機能](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)」を参照してください。  
  
データベース プロジェクトを検証するために、コンパイラ サービスは部分的包含データベースを作成し、そのデータベースに対して DDL ステートメントの実行をシミュレートします。 詳細については、「 [部分的包含データベース](https://msdn.microsoft.com/library/ff929071%28v=SQL.110%29.aspx)」を参照してください。  
  
コンパイラ サービスには、2 つのカテゴリの制限があります。  
  
以下を含む、データベースやインスタンスの構成に依存する機能  
  
-   3 部または 4 部のオブジェクト参照  
  
-   FileTables  
  
-   変更の追跡  
  
-   行セット関数 - OPENROWSET、OPENQUERY、OPENDATASOURCE  
  
-   フルテキスト セマンティック検索  
  
以下を含む、現在、検証でサポートされていない機能  
  
-   Service Broker  
  
-   ユーザー定義のファイル グループを含むパーティション スキーマ  
  
-   SQL Azure メタデータ照合順序 (コンパイラ サービスでは、SQL Server 2012 部分的包含データベースのメタデータ照合順序を使用します - Latin1_General_100_CI_AS_KS_WS_SC)  
  
### <a name="enablingdisabling-extended-verification"></a>拡張検証の有効化/無効化  
拡張 Transact-SQL 検証は、SQL Azure データベースから、またはターゲット プラットフォームが SQL Azure に設定されているプロジェクトから直接作成されるデータベース プロジェクトで既定で有効になっています。 SQL Azure 向け、または SQL Server 2012 を対象とするアプリケーション スコープ データベース向けの開発をする際には、拡張検証を使用することをお勧めします。 アプリケーション スコープ データベースの詳細については、「 [部分的包含データベース](https://msdn.microsoft.com/library/ff929071%28v=SQL.110%29.aspx)」を参照してください。  
  
SQL Server 2008/R2 用のアプリケーション スコープ データベースを開発する際に、拡張検証の機能を使用して Microsoft SQL Server 2012 および SQL Azure との互換性を実現することもできます。  
  
##### <a name="to-enable-or-disable-extended-verification-at-the-project-level"></a>プロジェクト レベルで拡張検証を有効または無効にするには  
  
1.  **ソリューション エクスプローラー**でプロジェクト ファイルを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[ターゲット プラットフォーム]** の **[プロジェクトの設定]** で、 **[共通オブジェクトに対する拡張 Transact-SQL 検証を有効にする]** チェック ボックスをオンまたはオフにします。  
  
##### <a name="to-disable-extended-verification-at-the-file-level"></a>ファイル レベルで拡張検証を無効にするには  
  
1.  **ソリューション エクスプローラー**で、.sql ファイルを右クリックします。  
  
    > [!NOTE]  
    > ファイル レベルで拡張された Transact\-SQL の検証の機能を無効にするには、ファイルの **[ビルド アクション]** プロパティを **[ビルド]** に設定する必要があります。  
  
2.  **[プロパティ]** で、**拡張 T-SQL 検証**プロパティを **[False]** に変更します。  
  
![ファイルのプロパティ](../ssdt/media/ssdt-evf.gif "ファイルのプロパティ")  
  
### <a name="special-considerations-for-collations"></a>照合順序に関する注意事項  
部分的包含データベースでの照合順序に関する詳細については、「 [包含データベースの照合順序](https://msdn.microsoft.com/library/ff929080%28v=sql.110%29.aspx)」を参照してください。  
  
## <a name="bkmk_sqlclr"></a>SQLCLR  
アセンブリ オプションの詳細については、「 [[アセンブリ情報] ダイアログ ボックス](https://msdn.microsoft.com/library/1h52t681.aspx?queryresult=true)」を参照してください。  
  
署名の詳細については、「」の「 **[署名] ページ (プロジェクト デザイナー)** [アセンブリの署名](https://msdn.microsoft.com/library/0k50fs3b.aspx?queryresult=true) 」を参照してください。  
  
## <a name="bkmk_sqlclr_sqlclrbuild"></a>SQLCLR および SQLCLR ビルド  
**SQLCLR** および **SQLCLR ビルド** のプロパティ ページには、SQL CLR オブジェクトをプロジェクトで使用するための設定が多数含まれています。 具体的には、 **SQLCLR** プロパティ ページには SQLCLR アセンブリに対するアクセス許可を設定するためのアクセス許可レベル設定が含まれています。 また、プロジェクトに追加された SQLCLR オブジェクトの動的データ言語 (DDL) を作成するかどうかを制御する "DDL を作成する" 設定も含まれています。 **SQLCLR ビルド** のプロパティ ページには、プロジェクト内の SQLCLR コードのコンパイルを構成するために設定できるコンパイラ オプションがすべて含まれています。  
  
**SQLCLR ビルド** のプロパティ ページには、SQL CLR オブジェクトをビルドするためのビルドの詳細設定が含まれています。 SQL CLR オブジェクトのコーディングに使用されている言語 (VB または C#) に基づくさまざまなオプションが用意されています。  
  
1.  オブジェクトが C# で記述されている場合は、**SQLCLR ビルド**のプロパティ ページで **[詳細]** をクリックして、オプションにアクセスできます。 C# のオプションに関する説明については、「[[ビルドの詳細設定] ダイアログ ボックス (C#)](https://msdn.microsoft.com/library/s4wcexbc.aspx)」をご覧ください。  
  
2.  オブジェクトが VB で記述されている場合は、最初に **[言語]** ボックスの一覧で VB を選択してから、 **[詳細]** をクリックします。 VB のオプションに関する説明については、「[[コンパイラの詳細設定] ダイアログ ボックス (Visual Basic)](https://msdn.microsoft.com/library/07bysfz2.aspx)」をご覧ください  
  

## <a name="bkmk_build"></a>ビルド  
ソフトウェアの各データベース プロジェクトに対して、ビルド構成を選択できます。 既定で含まれる構成は 1 つですが、カスタム構成を追加できます。 たとえば、データベースを常に削除して再作成するカスタム構成が必要な場合は、追加できます。 異なる種類のプロジェクトを含んでいるソリューションでは、プロジェクトごとに特定のビルド構成を使用するカスタム ソリューション構成を作成できます。  
  
#### <a name="to-specify-a-build-configuration-for-a-solution"></a>ソリューションのビルド構成を指定するには  
  
1.  **ソリューション エクスプローラー**で、ビルド構成を指定するソリューション ノードをクリックします。  
  
2.  **[ビルド]** メニューの **[構成マネージャー]** をクリックします。 **[構成マネージャー]** ダイアログ ボックスが表示されます。  
  
    ソリューションの各プロジェクトに使用する構成設定を指定します。  
  
#### <a name="to-specify-a-build-configuration-for-a-database-project"></a>データベース プロジェクトのビルド構成を指定するには  
  
1.  **ソリューション エクスプローラー**で、ビルド構成を指定するデータベース プロジェクトを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[ビルド]** タブの **[構成]** ボックスの一覧を使用して、このプロジェクトに使用する構成設定を指定します。  
  
次の表の設定は、このデータベース プロジェクトのビルド構成に適用されます。  
  
|フィールド|既定値|[説明]|  
|---------|-----------------|---------------|  
|ビルド出力パス|bin\Debug\|データベース プロジェクトをビルドまたは配置するときにビルド出力を生成する場所を指定します。 相対パスを指定する場合、データベース プロジェクト パスに対する相対パスを指定します。 パスが存在しない場合は、作成されます。|  
|ビルドの出力ファイル名|*DatabaseProjectName*|データベース プロジェクトをビルドするときに生成される出力の名前を指定します。|  
|Transact\-SQL の警告をエラーとして扱う|いいえ|Transact\-SQL の警告によってビルドおよび配置プロセスが取り消されるようにするかどうかを指定します。 このチェックボックスをオフにすると、警告が表示されますが、ビルドおよび配置プロセスは続行されます。 この設定は、ユーザーではなくプロジェクトに固有です。設定は .sqlproj ファイルに保存されます。|  
|Transact\-SQL の警告を表示しない|空白|非表示にする警告を示す警告番号の一覧を、コンマまたはセミコロンで区切って指定します。<br /><br />表示しないように指定した警告は、 **[エラー一覧]** ウィンドウに表示されず、 **[Transact\-SQL の警告をエラーとして扱う]** チェック ボックスをオンにした場合でも、ビルドの成功に影響しません。|  
  
## <a name="bkmk_sqlcmd_variables"></a>SQLCMD 変数  
SQL Server データベース プロジェクトでは、SQLCMD 変数を使用して、デバッグまたは公開に使用する動的置換を指定できます。 変数名と値を入力すると、ビルド時に値が置換されます。 ローカル値がない場合は、既定値が使用されます。 プロジェクトのプロパティにこれらの変数を入力すると、その変数が公開時に自動的に提供され、公開プロファイルに格納されます。 [値の読み込み] ボタンを使用して、変数のプロジェクト値を公開時に使用できます。  
  
プロジェクトのプロパティには、必ず適切な変数を入力してください。これらの変数はプロジェクトのスクリプトに対して検証されません。また、スクリプトで使用される変数は自動的には生成されません。  
  
さらに、コマンド ラインによる公開では、コマンド ラインまたはプロファイルを使用してこれらの値をオーバーライドすることができます。  
  
## <a name="bkmk_build_events"></a>ビルド イベント  
次の設定を使用すると、ビルド操作が始まる前に実行するコマンド ラインと、ビルド操作の完了時に実行するコマンド ラインを指定できます。  
  
|フィールド|既定値|[説明]|  
|---------|-----------------|---------------|  
|ビルド前に実行するコマンド ライン|なし|プロジェクトをビルドする前に実行するコマンド ラインを指定します。 **[ビルド前の編集]** をクリックしてコマンド ラインを変更します。|  
|ビルド後に実行するコマンド ライン|なし|プロジェクトをビルドした後に実行するコマンド ラインを指定します。 **[ビルド後の編集]** をクリックしてコマンド ラインを変更します。|  
|ビルド後イベントの実行|ビルドが成功したとき|ビルド後のコマンド ラインを、常に実行するか、ビルドが成功したときにだけ実行するか、または、ビルドすることによってプロジェクト出力 (ビルド スクリプト) が更新されたときにだけ実行するかを指定します。|  
  
## <a name="bkmk_debug"></a>デバッグ  
以下の設定を使用してデータベース オブジェクトのデバッグを制御できます。  
  
|フィールド|既定値|[説明]|  
|---------|-----------------|---------------|  
|開始動作|なし|プロジェクトのデバッグ時に実行されるスクリプトまたは外部プログラムを指定します。|  
|ターゲット接続文字列|Data Source=(localdb)\\*SolutionName*;Initial Catalog=*DatabaseProjectName*;Integrated Security=True;Pooling=False;Connect Timeout=30|指定したビルド構成のターゲットにするデータベース サーバーの接続情報を指定します。 既定の接続文字列は、動的に作成された SQL Server LocalDB インスタンスおよびデータベースに対する接続文字列です。|  
|データベース プロパティを配置する|はい|データベース プロジェクトを配置するときに、DatabaseProerties.DatabaseProperties 設定を配置または更新するかどうかを指定します。|  
|データベースを常に再作成|いいえ|増分アップグレードを実行する代わりにデータベースを削除して再作成するかどうかを指定します。 たとえば、データベースの新規の配置に対してデータベース単体テストを実行する場合、このチェック ボックスをオンにします。 このチェック ボックスがオフの場合、削除と再作成を行う代わりに、既存のデータベースが更新されます。|  
|データ損失が発生する場合に増分配置をブロック|はい|更新するとデータが失われる可能性がある場合に配置を中止するかどうかを指定します。 このチェック ボックスをオンにすると、データが損失する変更の場合は配置が中止され、エラーが表示されます。そのため、データの損失を回避できます。 たとえば、 `varchar(50)` 列が `varchar(30)`に変更される場合、配置は中止されます。<br /><br />**注:** 配置がブロックされるのは、データ損失が発生する可能性のあるテーブルにデータが含まれる場合のみです。 データが損失しない場合、配置は続行されます。|  
|プロジェクトではなくターゲットに含まれている DROP オブジェクト|いいえ|ターゲット データベースにあってデータベース プロジェクトにないオブジェクトを配置スクリプトから削除するかどうかを指定します。 プロジェクトの一部のファイルを除外して、ビルド スクリプトから一時的に削除できます。 ただし、ターゲット データベースに既存のバージョンのオブジェクトを残す場合があります。 **[データベースを常に再作成]** チェック ボックスがオンに設定されているとデータベースが削除されるため、このチェック ボックスの設定は無効になります。|  
|ALTER ASSEMBLY ステートメントを使用して CLR 型を更新しないでください。|いいえ|ALTER ASSEMBLY ステートメントを使用して共通言語ランタイム (CLR) 型を更新するか、代わりに変更の配置時に、CLR 型をインスタンス化するオブジェクトを削除して再作成するかを指定します。|  
|[詳細設定]|いいえ|イベントと配置の動作を制御するオプションを指定できるコマンド ボタンです。|  
  
## <a name="bkmk_ref_paths"></a>参照パス  
このページを使用すると、データベース間参照に関連付けられたサーバー変数およびデータベース変数を定義できます。 また、それらの変数の値も指定できます。 詳細については、「 [データベース プロジェクトでの参照の使用](https://msdn.microsoft.com/library/bb386242.aspx)」を参照してください。  
  
## <a name="bkmk_code_analysis"></a>コード分析  
コード分析を使用すると、デザイン、名前、パフォーマンスに関する問題など、スクリプト内の潜在的な問題を検出できます。 データベース プロジェクト用の規則は、特定の分野を対象とする定義済みの規則セットにまとめられています。 **[プロジェクトのプロパティ]** ページの **[コード分析]** タブでは、任意の規則を有効化または無効化できます。 同じタブで、プロジェクトがビルドされるたびにコード分析が自動的に実行されるように指定することも、警告をエラーとして処理するかどうかを指定することもできます。  
  
コード分析を手動で使用するには、**ソリューション エクスプローラー**でプロジェクトを右クリックし、 **[コード分析の実行]** をクリックします。 コード分析の警告が **[エラー一覧]** ウィンドウに一覧表示されます。 警告をダブルクリックすると、その問題が含まれるソース コードに移動できます。 **[エラーのヘルプを表示]** コンテキスト メニューを使用すると、警告の追加情報および修正候補を表示できます。 コード分析の詳細については、「 [データベース コードの分析によるコードの品質の向上](https://msdn.microsoft.com/library/dd172133.aspx)」を参照してください。  
  
