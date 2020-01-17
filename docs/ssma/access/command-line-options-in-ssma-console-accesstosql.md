---
title: SSMA コンソール (AccessToSQL) コマンド ライン オプション |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c1f3b3f0-0f3e-4e07-b745-2fbdde85c67e
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: f6a2bb7e10e487d65c0fa8dfd406a30f9acd557a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265534"
---
# <a name="command-line-options-in-the-ssma-console-accesstosql"></a>SSMA コンソール (AccessToSQL) コマンド ライン オプション
Microsoft は、堅牢な実行および SSMA アクティビティを制御するコマンド ライン オプションのセットを提供します。 次のセクションでは、追加の詳細情報を提供します。  
  
## <a name="command-line-options-in-the-ssma-console"></a>SSMA コンソールのコマンド ライン オプション  
コンソールにコマンド オプションは、ここに記載されました。  
  
ここでは、用語 'option' と呼ばれるもを 'switch'。  
  
オプションは、小文字は区別されず、いずれかで始めることは、' **-** 'または' **/** ' 文字。  
  
オプションを指定する場合は、対応する、オプション パラメーターを指定することが必須です。  
  
オプション パラメーターは、オプションの文字から空白で区切る必要があります。  
  
**構文例:**  
  
`C:\> SSMAforAccessConsole.EXE -s scriptfile`  
  
`C:\> SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\VariableValueFileSample.xml" -c "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml"`  
  
二重引用符で囲まれた空白を含むフォルダーまたはファイルの名前を指定する必要があります。  
  
コマンドラインの入力とエラー メッセージの出力は STDOUT に出力される、または指定したファイルに格納されます。  
  
### <a name="script-file-option--sscript"></a>ファイル オプションのスクリプトを作成します-s/スクリプト。  
必須のスイッチでは、スクリプト ファイルのパス/名前は、SSMA によって実行されるコマンドのシーケンスのスクリプトを指定します。  
  
**構文例:**  
  
`C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="variable-value-file-option--vvariable"></a>変数値ファイルのオプション: - v/変数  
変数値ファイルには、スクリプト ファイルで使用される変数が構成されています。 スイッチは省略可能です。 変数がない変数ファイル内で宣言されているし、スクリプト ファイルで使用される、アプリケーションは、エラーが発生し、コンソールの実行を終了します。  
  
**構文例:**  
  
-   既定値はおそらく 1 つと、該当する場合は、インスタンス固有の値を使用した異なる複数の変数値ファイルで定義された変数。 変数の重複がある場合、コマンドラインの引数で指定された最後の変数ファイルは、基本設定を受け取ります。  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml" -v c:\migration`  
  
    `projects\global_variablevaluefile.xml -v "c:\migrationprojects\instance_variablevaluefile.xml"`  
  
### <a name="server-connection-file-option--cserverconnection"></a>サーバー接続ファイルのオプション:-c/serverconnection  
このファイルには、各サーバーのサーバー接続情報が含まれています。 各サーバーの定義 ID によって識別されます、一意なサーバー サーバー Id は、接続に関連するコマンドのスクリプト ファイルで参照されます。  
  
サーバー定義には、サーバー接続ファイル、またはスクリプト ファイルの一部を指定できます。 スクリプト ファイル内のサーバー id は、サーバー接続ファイルに優先されるサーバー id の重複がある場合します。  
  
**構文例:**  
  
-   サーバー Id は、スクリプト ファイルで使用されます。 別のサーバー接続ファイルで定義されています。 このファイルには、変数値ファイルで定義されている変数が使用されます。  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -v`  
  
    `c:\SsmaProjects\myvaluefile1.xml -c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   サーバーの定義がスクリプト ファイルに埋め込まれます。  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 出力オプション:-x/xmloutput [xmloutputfile]  
このコマンドは、コンソールまたは xml ファイルのいずれかの xml 形式でコマンドの出力メッセージを出力するために使用されます。  
  
利用して 2 つのオプションを xmloutput、つまり。  
  
-   Xmloutput スイッチの後にファイル パスを指定すると、ファイルに出力がリダイレクトされます。  
  
    **構文例:**  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -x d:\xmloutput\project1output.xml`  
  
-   Xmloutput スイッチの後にファイル パスが指定されていない場合、xmlout が自体、コンソールに表示されます。  
  
    **構文例:**  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -xmloutput`  
  
### <a name="log-file-option--llog"></a>ログ ファイルのオプション:-l/ログ  
コンソール アプリケーションのすべての SSMA 操作がログ ファイルに記録され、スイッチは省略可能です。 ログ ファイルとそのパスをコマンドラインで指定する場合は、指定した場所にログが生成されます。 それ以外の場合、既定の場所に生成されるを取得します。  
  
**構文例:**  
  
`C:\>SSMAforAccessConsole.EXE`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option--eprojectenvironment"></a>プロジェクトの環境のフォルダー オプション:-e/projectenvironment  
このオプションのスイッチでは、現在の SSMA プロジェクトのプロジェクト環境の設定 フォルダーを表します。  
  
**構文例:**  
  
`C:\>SSMAforAccessConsole.EXE -s`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -e c:\SsmaProjects\CommonEnvironment`  
  
||  
|-|  
||  
  
### <a name="secure-password-option--psecurepassword"></a>パスワードのオプションをセキュリティで保護します -p/securepassword。  
このオプションでは、サーバー接続の暗号化パスワードを指定します。 任意のスクリプトを実行したり、移行に関連するアクティビティで役立つしないが、移行プロジェクトで使用するサーバー接続のパスワードの暗号化の管理に役立つその他のすべてのオプションとは異なります。  
  
コマンド ライン パラメーターとして他のオプションまたはパスワードを入力することはできません。 それ以外の場合、エラーが発生します。 詳細については、次を参照してください。、[管理パスワード](managing-passwords-accesstosql.md)セクション。  
  
次のサブオプションがサポートされている`-p/securepassword`:  
  
-   パスワードを追加または既存のパスワードを指定したサーバー ID に対して、またはサーバー接続ファイルに定義されているすべてのサーバー Id の保護された記憶域に更新します。  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   指定したサーバー ID のまたはすべてのサーバー Id の保護されたストレージから暗号化されたパスワードを削除します。  
  
    `-p/securepassword -r/remove {<server_id> [, ...n] | all}`  
  
-   パスワードの暗号化をサーバー Id の一覧を表示するには。  
  
    `-p/securepassword -l/list`  
  
-   暗号化されたファイルに保護されたストレージに格納されているパスワードをエクスポートします。 このファイルは、パス フレーズをユーザー指定で暗号化されます。  
  
    `-p/securepassword -e/export {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
-   暗号化-ファイル以前エクスポートされたは、パス フレーズをユーザー指定を使用してローカルの保護されたストレージにインポートされます。 ファイルを暗号化解除すると、さらに、ローカル コンピューターで暗号化された、新しいファイルに格納されます。  
  
    `-p/securepassword -i/import {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
    コンマ区切り記号を使用して、複数のサーバー Id を指定できます。  
  
### <a name="help-option--help"></a>Help オプション:-?/help  
SSMA コンソールのオプションの構文の概要が表示されます。  
  
`C:\>SSMAforAccessConsole.EXE -?`  
  
SSMA コンソールのコマンド ライン オプションの表を参照してください[付録 - 1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md)します。  
  
### <a name="securepassword-help-option--securepassword--help"></a>SecurePassword ヘルプ オプション: - securepassword-?/help  
SSMA コンソールのオプションの構文の概要が表示されます。  
  
`C:\>SSMAforAccessConsole.EXE -securepassword -?`  
  
SSMA コンソールのコマンド ライン オプションの表を参照してください[付録 - 1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md)  
  
### <a name="next-steps"></a>次の手順  
次の手順は、プロジェクトの要件によって異なります。  
  
1.  パスワードまたはエクスポートを指定する]、[パスワードのインポートを参照してください[管理パスワード&#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md)します。  
  
2.  レポートを生成するため、次を参照してください。[レポートを生成する&#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)します。  
  
3.  コンソールで問題をトラブルシューティングするには、次を参照してください。[トラブルシューティング&#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md)します。  
  
