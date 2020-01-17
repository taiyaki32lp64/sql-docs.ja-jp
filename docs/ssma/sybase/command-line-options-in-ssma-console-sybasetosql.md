---
title: SSMA コンソール (SybaseToSQL) コマンド ライン オプション |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Command Line Options
ms.assetid: 337cbd26-67b7-4c88-9deb-d0a69a3d7714
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 285f5c58c94db0f5506f84d19c992dfcdbbd00d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083483"
---
# <a name="command-line-options-in-ssma-console-sybasetosql"></a>SSMA コンソールのコマンド ライン オプション (SybaseToSQL)
Microsoft は、堅牢なコマンド ライン オプションを実行し、制御 SSMA アクティビティのセットを提供します。 次のセクションでは、同じについて説明します。  
  
## <a name="command-line-options-in-ssma-console"></a>SSMA コンソールのコマンド ライン オプション  
コンソールにコマンド オプションは、ここに記載されました。  
  
ここでは、用語 'option' と呼ばれるもを 'switch'。  
  
-   オプションは、小文字は区別されず、いずれかで始めることは ' **-** '、' **/** ' 文字。  
  
-   オプションを指定する場合、対応するオプションのパラメーターの指定が必須になります。  
  
-   オプション パラメーターは、オプションの文字から空白で区切る必要があります。  
  
    **構文例:**  
  
    `C:\> SSMAforSybaseConsole.EXE -s scriptfile`  
  
    `C:\> SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\VariableValueFileSample.xml" -c "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ServersConnectionFileSample.xml"`  
  
-   二重引用符で囲まれた空白を含むフォルダーまたはファイルの名前を指定する必要があります。  
  
-   コマンドラインのエントリとエラー メッセージの出力は STDOUT に出力される、または指定したファイルに格納されます。  
  
### <a name="script-file-option--sscript"></a>スクリプト ファイルのオプション:-s/スクリプト  
必須のスイッチでは、スクリプト ファイルのパス/名前は、SSMA によって実行されるコマンドのシーケンスのスクリプトを指定します。  
  
**構文例:**  
  
`C:\>SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="variable-value-file-option--vvariable"></a>変数値ファイルのオプション: - v/変数  
このファイルには、スクリプト ファイルで使用される変数が構成されています。 これは、オプションのスイッチです。 変数がない変数ファイル内で宣言されているし、スクリプト ファイルで使用される、アプリケーションは、エラーが発生し、コンソールの実行を終了します。  
  
**構文例:**  
  
-   変数は、おそらく 1 つで、既定値と該当する場合に、インスタンス固有値を持つ別の複数の変数値ファイルで定義されています。 変数の重複がある場合、コマンドライン引数で指定された最後の変数ファイルは、基本設定を受け取ります。  
  
    `C:\>SSMAforSybaseConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml" -v c:\migration`  
  
    `projects\global_variablevaluefile.xml -v "c:\migrationprojects\instance_variablevaluefile.xml"`  
  
### <a name="server-connection-file-option--cserverconnection"></a>サーバー接続ファイルのオプション: -c/serverconnection  
このファイルには、各サーバーのサーバー接続情報が含まれています。 各サーバーの定義 ID によって識別されます、一意なサーバー サーバー Id は、接続用のスクリプト ファイルで参照される関連するコマンド。  
  
サーバー定義には、サーバー接続ファイル、またはスクリプト ファイルの一部を指定できます。 スクリプト ファイル内のサーバー id は、サーバー接続ファイルに優先されるサーバー id の重複がある場合します。  
  
**構文例:**  
  
-   スクリプト ファイルでサーバー Id を使用して、別のサーバー接続ファイルで定義されている、サーバー接続ファイルは、変数値ファイルで定義されている変数を使用します。  
  
    `C:\>SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -v`  
  
    `c:\SsmaProjects\myvaluefile1.xml -c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   サーバーの定義がスクリプト ファイルに埋め込まれます。  
  
    `C:\>SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 出力のオプション: x/xmloutput [xmloutputfile]  
このコマンドは、コンソールまたは xml ファイルのいずれかの xml 形式でコマンドの出力メッセージを出力するために使用されます。  
  
2 つのオプションに使用できるは、xmloutput 可視。  
  
-   Xmloutput スイッチの後にファイル パスが指定されている場合、出力はファイルにリダイレクトされます。  
  
    **構文例:**  
  
    `C:\>SSMAforSybaseConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -x d:\xmloutput\project1output.xml`  
  
-   Xmloutput スイッチの後にファイル パスが指定されていない場合、xmlout が自体、コンソールに表示されます。  
  
    **構文例:**  
  
    `C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -xmloutput`  
  
### <a name="log-file-option--llog"></a>-L/ログのログ ファイルのオプション:  
コンソール アプリケーションのすべての SSMA 操作ログ ファイルに記録します。 これは、オプションのスイッチです。 ログ ファイルとそのパスをコマンドラインで指定する場合は、指定した場所にログが生成されます。 それ以外の場合、既定の場所に生成されるを取得します。  
  
**構文例:**  
  
`C:\>SSMAforSybaseConsole.EXE`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option--eprojectenvironment"></a>プロジェクトの環境のフォルダー オプション:-e/projectenvironment  
これは、現在の SSMA プロジェクトのプロジェクト環境の設定 フォルダーを示します。 このスイッチは省略可能です。  
  
**構文例:**  
  
`C:\>SSMAforSybaseConsole.EXE -s`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -e c:\SsmaProjects\CommonEnvironment`  
  
### <a name="secure-password-option--psecurepassword"></a>セキュリティで保護されたパスワード オプション:-p/securepassword  
このオプションでは、サーバー接続の暗号化パスワードを指定します。 その他のすべてのオプションとは異なる: オプションで任意のスクリプトの実行も移行に関連するアクティビティが、移行プロジェクトで使用するサーバー接続のパスワードの暗号化の管理を支援します。  
  
コマンド ライン パラメーターとして他のオプションまたはパスワードを入力することはできません。 それ以外の場合、エラーが発生します。 詳細についてを参照してください、[管理パスワード](managing-passwords-sybasetosql.md)セクション。  
  
次のサブ オプションはサポートされて`-p/securepassword`:  
  
-   パスワードを追加するには、指定したサーバー ID に対して、またはサーバー接続ファイルに定義されているすべてのサーバー Id のストレージを保護しました。 既に存在する場合、更新プログラムの下のオプションのパスワードを上書きします。  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}` `-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
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
  
### <a name="help-option--help"></a>ヘルプ オプション:-?/help  
SSMA コンソールのオプションの構文の概要が表示されます。  
  
`C:\>SSMAforSybaseConsole.EXE -?`  
  
SSMA コンソールのコマンド ライン オプションの表を参照してください[付録 - 1 &#40;SybaseToSQL&#41;](../../ssma/sybase/appendix-1-sybasetosql.md)します。  
  
### <a name="securepassword-help-option--securepassword--help"></a>SecurePassword ヘルプ オプション: securepassword-?/help  
SSMA コンソールのオプションの構文の概要が表示されます。  
  
`C:\>SSMAforSybaseConsole.EXE -securepassword -?`  
  
SSMA コンソールのコマンド ライン オプションの表を参照してください[付録 - 1 &#40;SybaseToSQL&#41;](../../ssma/sybase/appendix-1-sybasetosql.md)  
  
### <a name="next-step"></a>次の手順  
次の手順は、プロジェクトの要件によって異なります。  
  
-   パスワードまたはエクスポートを指定する]、[パスワードのインポートを参照してください[管理パスワード&#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md)します。  
  
-   レポートを生成するため、次を参照してください。[レポートを生成する&#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)します。  
  
-   コンソールで問題をトラブルシューティングするには、次を参照してください。[トラブルシューティング&#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md)します。  
  
