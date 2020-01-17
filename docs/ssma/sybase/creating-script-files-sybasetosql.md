---
title: スクリプト ファイル (SybaseToSQL) の作成 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Configuring Settings
- Sybase Console,Script Commands
- Sybase Console,Script File Validation
- Sybase Console,Server Connection Parameters
ms.assetid: e6baf106-abbd-4200-b3de-33b4b4f1b294
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9d7df0fe0917a684f1050197e6706ba5b5414f6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948476"
---
# <a name="creating-script-files-sybasetosql"></a>スクリプト ファイルの作成 (SybaseToSQL)
SSMA コンソールのアプリケーションを起動すると、スクリプト ファイルを作成する前に、変数値ファイルとサーバー接続ファイルを作成するために必要な場合、最初の手順します。  
  
スクリプト ファイルを viz 3 つのセクションに分割できますします..,:  
  
1.  **構成:** コンソール アプリケーションの構成パラメーターを設定するユーザーを有効にします。  
  
2.  **サーバー:** ソース/ターゲットのサーバー定義を設定するユーザーを有効にします。 別のサーバー接続ファイルにこのことができます。  
  
3.  **スクリプト コマンド。** SSMA ワークフロー コマンドを実行するユーザーを有効にします。  
  
各セクションは後で詳しく説明します。  
  
## <a name="configuring-sybase-console-settings"></a>Sybase Console の設定を構成します。  
コンソール スクリプト ファイルには、スクリプトの構成が表示されます。  
  
設定されている場合は、[構成] ノードでは、要素のいずれかが指定された、つまりグローバル設定として適用しているすべてのスクリプト コマンド。 これらの構成要素も設定できます各コマンド内でスクリプト コマンドのセクションでは、ユーザーは、グローバル設定を上書きする必要がある場合。  
  
ユーザー構成可能なオプションは次のとおりです。  
  
1.  **出力ウィンドウ プロバイダー:** 抑制メッセージの属性が 'true'、固有のコマンドに設定されている場合、コンソールにメッセージが表示されません実行を取得します。 属性の説明のとおりです。  
  
    -   移行先:出力をファイルまたは stdout に出力を取得する必要があるかどうかを指定します。 これは、既定では false。  
  
    -   ファイル名:(省略可能) ファイルのパス。  
  
    -   抑制メッセージ:コンソールにメッセージを抑制します。 これは、既定では ' false' です。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <output-window  
  
        suppress-messages="<true/false>"   (optional)  
  
        destination="<file/stdout>"        (optional)  
  
        file-name="<file-name>"            (optional)  
  
       />  
  
    </output-providers>  
    ```  
    *または*  
  
    ```xml  
    <...All commands...>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </...All commands...>  
    ```  
  
2.  **データ移行の接続プロバイダー:** これを指定するソース/ターゲット サーバーはデータ移行の対象にします。  ソースの使用-最後に使用するには、データの移行に対して最後に使用される移行元サーバーを使用することを示します。 同様にターゲットの使用-最後に使用された場合は、データの移行に対して最後に使用されるターゲット サーバーを使用することを示します。 ユーザーは、属性のソース サーバーまたはターゲット サーバーを使用して、サーバー (ソースまたはターゲット) を指定もできます。  
  
    1 つだけ、または指定した属性は、つまり使用できます。  
  
    -   ソースの使用-最後に使用された ="true"(既定値) またはソース サーバー ="source_servername"  
  
    -   ターゲットの使用-最後に使用された ="true"(既定値) またはターゲット サーバー ="target_servername"  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection   source-use-last-used="true"  
  
                                   target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *または*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **ユーザー入力のポップアップ:** これにより、オブジェクトがデータベースから読み込まれるときに、エラーの処理。 入力のモード、ユーザーとユーザーが指定するとき、エラーが発生した場合、コンソールが進行します。  
  
    モードは次のとおりです。  
  
    -   **質問-ユーザー -** continue('yes') またはエラー ('いいえ') にユーザーにメッセージが表示されます。  
  
    -   **エラー-** コンソール エラーが表示および実行を中止します。  
  
    -   **続行-** コンソールが実行を続行します。  
  
    既定のモードは**エラー**します。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *または*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **プロバイダーを再接続するには。** これにより、ユーザーは、接続エラーの設定が何らかの再接続を設定できます。 これは、ソースとターゲットの両方のサーバーを設定できます。  
  
    再接続モードは次のとおりです。  
  
    -   再接続と最後の使用-サーバー:接続がアクティブでない場合、最後に、最大で 5 回を使用するサーバーに再接続しようとします。  
  
    -   生成-、-エラー:接続がアクティブでない場合は、エラーが生成されます。  
  
    既定のモードは**エラーを生成**します。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <reconnect-manager  on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                          on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *または*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *または*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="<target-server-unique-name>">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **コンバーターは、プロバイダーを上書きします。** これにより、既にターゲットに存在するオブジェクトを処理するためにユーザー メタベースです。 実行可能なアクションは次のとおりです。  
  
    -   エラー:コンソールでは、エラーが表示され、実行を停止します。  
  
    -   上書きされます。既存のオブジェクトの値を上書きします。 このアクションは、既定で行われます。  
  
    -   スキップするには。コンソールで、データベースに既に存在するオブジェクトをスキップします  
  
    -   ユーザーの確認:ユーザーに入力を求められます ('yes '/' いいえ')  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *または*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **失敗した前提条件のプロバイダー:** これにより、コマンドを処理するために必要な前提条件を処理するために、ユーザーができます。 既定では、厳格モードが 'false' です。 'True'、例外に設定されている場合、前提条件を満たすエラーの生成を取得します。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **操作を停止します。** ユーザーがその後、操作を停止する場合は、中間操作中に **' Ctrl + C'** ホットキーを使用することができます。 SSMA for Sybase Console は、操作の完了を待機し、コンソールの実行を終了します。  
  
    ユーザーは、次に、すぐに、実行を停止する必要がある場合 **' Ctrl + C'** SSMA コンソール アプリケーションを強制的に終了のホットキーをもう一度押すこともできます  
  
8.  **進行中のプロバイダー:** 各コンソール コマンドの進行状況を通知します。 これは既定で無効です。 進行状況レポート属性が含まれています。  
  
    -   off  
  
    -   1-すべての %  
  
    -   2-すべての %  
  
    -   すべての 5%  
  
    -   every-10%  
  
    -   すべての 20%  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <progress-reporting enable="<true/false>"           (optional)  
  
                          report-messages="<true/false>"  (optional)  
  
                          report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off" (optional)/>  
  
    </output-providers>  
    ```  
    *または*  
  
    ```xml  
    <...All commands...>  
  
      <progress-reporting  
  
        enable="<true/false>"          (optional)  
  
        report-messages="<true/false>" (optional)  
  
        report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off (optional)/>  
  
    </...All commands...>  
    ```  
  
9. **ロガーの詳細:** 詳細レベルをセットにログインします。 これは、UI にすべてのカテゴリのオプションに対応します。 既定では、ログの詳細レベルは、"error"は。  
  
    ロガー レベルのオプションは次のとおりです。  
  
    -   致命的なエラー:致命的なエラー メッセージのみが記録されます。  
  
    -   エラー:唯一のエラーと致命的なエラー メッセージが記録されます。  
  
    -   警告:デバッグおよび情報メッセージを除くすべてのレベルが記録されます。  
  
    -   情報:デバッグ メッセージを除くすべてのレベルが記録されます。  
  
    -   デバッグ:記録されたメッセージのすべてのレベル。  
  
    > [!NOTE]  
    > 必須のメッセージは、任意のレベルで記録されます。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *または*  
  
    ```xml  
    <...All commands...>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </...All commands...>  
    ```  
  
10. **暗号化されたパスワードをオーバーライドします。** 'True' の場合、サーバー接続ファイルのサーバー定義のセクションで、またはスクリプト ファイルに上書きの場合は、保護されたストレージに格納されている暗号化されたパスワードが存在するクリア テキスト パスワードが指定されました。 クリア テキストでパスワードが指定されていない場合は、パスワードの入力を求められます。  
  
    ここでは 2 つのケースが生じます。  
  
    1.  場合オプションをオーバーライドは**false**、検索の順序になる保護されたストレージ -&gt;スクリプト ファイル -&gt;サーバー接続ファイル-&gt;をユーザーに要求します。  
  
    2.  場合上書きオプションは**true**、検索の順序になりますスクリプト ファイル -&gt;サーバー接続ファイルの&gt;をユーザーに要求します。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
構成可能なオプションです。  
  
-   **試行を最大に再接続します。** 確立された接続がタイムアウトになるか、ネットワーク エラーにより中断する、サーバーが再接続する必要があります。 再接続の試行が最大に許可されている**5**その後、再試行、コンソールが自動的に再接続を実行します。 自動再接続の機能で、スクリプトを再実行する作業が軽減されます。  
  
## <a name="server-connection-parameters"></a>サーバーの接続パラメーター  
スクリプト ファイル、またはサーバーの接続ファイルには、サーバーの接続パラメーターを定義できます。 参照してください、[サーバー接続ファイルを作成する&#40;SybaseToSQL&#41; ](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)セクションの詳細  
  
## <a name="script-commands"></a>スクリプト コマンド  
スクリプト ファイルには、XML 形式で移行ワークフロー コマンドのシーケンスが含まれています。 SSMA コンソールのアプリケーションでは、スクリプト ファイルに表示されるコマンドの順序で移行を処理します。  
  
たとえば、Sybase データベース内の特定のテーブルの一般的なデータ移行では、階層を次に示します。データベース -&gt;スキーマ -&gt;テーブル。  
  
スクリプト ファイル内のすべてのコマンドが正常に実行された、SSMA コンソールのアプリケーションは終了し、ユーザーにコントロールを返します。 スクリプト ファイルの内容は詳細またはのいずれかに含まれる小さい静的変数の情報を[変数値ファイル](creating-variable-value-files-sybasetosql.md)または変数の値をスクリプト ファイル内の別のセクションでします。  
  
**例:**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="<project-folder>"  
  
                        project-name="<project-name>"  
  
                        overwrite-if-exists="<true/false>"/>  
  
    <connect-source-database server="<source-server-unique-name>"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
製品ディレクトリのサンプルのコンソール スクリプト フォルダーには、変数値ファイル、およびサーバー接続ファイル (を実行するためのさまざまなシナリオ)、3 つのスクリプト ファイルから成るテンプレートが用意されています。  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
関連性をそこに表示されるパラメーターを変更した後、テンプレート (ファイル) を実行できます。  
  
スクリプト コマンドの完全な一覧が記載されて[SSMA コンソールの実行&#40;SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)  
  
## <a name="script-file-validation"></a>スクリプト ファイルの検証  
ユーザーがスキーマ定義ファイルに対してそのスクリプト ファイルを簡単に検証できます **'S2SSConsoleScriptSchema.xsd'** 'スキーマ' フォルダー内にあります。  
  
## <a name="next-step"></a>次の手順  
コンソールの運用には、次の手順は[変数値ファイルの作成&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)します。  
  
## <a name="see-also"></a>関連項目  
[変数値ファイルを作成する&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
