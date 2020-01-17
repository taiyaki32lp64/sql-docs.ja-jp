---
title: SSMA コンソール (SybaseToSQL) の実行 |Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Database Connection Commands
- Sybase Console,Manageability Commands
- Sybase Console,Migration Commands
- Sybase Console,Migration Preparation Command
- Sybase Console,Project Commands
- Sybase Console,Report Commands
- Sybase Console,Script File Commands
- Sybase Console,Script Generation Commands
ms.assetid: ea8950b7-fabc-4aa4-89f8-9573a2617d70
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 602bc0ac1584f9ff369efa8a2484a16a97a92285
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029153"
---
# <a name="executing-the-ssma-console-sybasetosql"></a>SSMA コンソールの実行 (SybaseToSQL)
Microsoft は、ファイルのコマンドを実行し、SSMA アクティビティを制御する堅牢なスクリプトのセットを提供します。 次のセクションでは、同じについて説明します。  
  
## <a name="script-file-commands"></a>ファイルのスクリプト コマンド  
コンソール アプリケーションは、このセクションでは、列挙型として標準的なスクリプト ファイルの特定のコマンドを使用します。  
  
## <a name="project-commands"></a>プロジェクト コマンド  
プロジェクト コマンドでは、プロジェクトの作成、開く、保存、およびプロジェクトの終了を処理します。  
  
### <a name="create-new-project"></a>create-new-project  
このコマンドは、新しい SSMA プロジェクトを作成します。  
  
-   `project-folder` プロジェクトの作成中のフォルダーを示します。  
  
-   `project-name` プロジェクトの名前を示します。 {string}  
  
-   `overwrite-if-exists`省略可能な属性は、既存のプロジェクトを上書きするかどうかを示します。 {boolean}  
  
-   `project-type:`省略可能な属性です。 「Sql server 2005」プロジェクトまたは「sql server 2008」のプロジェクトまたはプロジェクトの「sql server 2012」または「sql server 2014」プロジェクト"sql azure"プロジェクトをプロジェクトの種類を示します。 既定値は「sql のサーバーで 2008」  
  
**構文例:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type="<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>"  
/>  
```  
'上書きの場合-存在' 属性が**false**既定。  
  
'プロジェクトの種類' 属性が**sql server2008**既定。  
  
### <a name="open-project"></a>open-project  
このコマンドは、プロジェクトを開きます。

-   `project-folder` プロジェクトの作成中のフォルダーを示します。 指定したフォルダーが存在しない場合、コマンドが失敗します。  {string}  
  
-   `project-name` プロジェクトの名前を示します。 指定されたプロジェクトが存在しない場合、コマンドが失敗します。  {string}  
  
**構文例:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA for SAP ASE のコンソール アプリケーションでは、旧バージョンとの互換性をサポートします。 SSMA の以前のバージョンで作成されたプロジェクトを開くには、これを使用できます。  
  
### <a name="save-project"></a>save-project  
このコマンドは、移行プロジェクトを保存します。  
  
**構文例:**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>close-project  
このコマンドは、移行プロジェクトを閉じます。  
  
**構文例:**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
'If 変更' 属性は省略可能で**無視**既定。  
  
## <a name="database-connection-commands"></a>データベース接続コマンド  
データベース接続のコマンドは、データベースに接続するのに役立ちます。  
  
> [!NOTE]  
> - **参照**コンソールで、UI の機能がサポートされていません。  
> - スクリプト ファイルの作成 ' の詳細については、次を参照してください。[スクリプト ファイルの作成&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md)します。  
  
### <a name="connect-source-database"></a>接続ソース データベース  
このコマンドは、ソース データベースへの接続を実行し、ソース データベースはすべてのメタデータの高レベルのメタデータを読み込みます。
  
ソースへの接続を確立できない場合は、エラーが生成され、さらに実行を停止するコンソール アプリケーションです。
  
サーバーの定義は、サーバー接続ファイルまたはスクリプト ファイルのサーバー セクションでは、各接続に対して定義されている name 属性から取得されます。  
  
**構文例:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>force-読み込み-ソース/ターゲットのデータベース  
このコマンドは、ソースのメタデータを読み込み、移行プロジェクトをオフラインで作業するために便利です。  
  
ソース/ターゲットへの接続を確立できない場合は、エラーが生成され、さらに実行を停止するコンソール アプリケーションです。  
  
このコマンドでは、コマンド ライン パラメーターとして 1 つまたはいくつかのメタベース ノードが必要です。  
  
**構文例:**  
  
```xml  
<force-load metabase="<source/target>" >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>再接続ソース データベース  
このコマンドは、ソース データベースへの再接続がソース データベースの connect コマンドとは異なり、メタデータは読み込まれません。  
  
エラーが生成されます (再) ソースとの接続を確立できない場合、さらに実行を停止するコンソール アプリケーションです。  
  
**構文例:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>connect-target-database  
このコマンドは、対象の SQL Server データベースに接続し、完全ではなくメタデータではなく、ターゲット データベースの高レベルのメタデータを読み込みます。  
  
ターゲットへの接続を確立できない場合は、エラーが生成され、さらに実行を停止するコンソール アプリケーションです。  
  
サーバーの定義は、サーバー接続ファイルまたはスクリプト ファイルのサーバー セクションでは、各接続に対して定義されている name 属性から取得されます。  
  
**構文例:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>reconnect-target-database  
  
このコマンドは、ターゲット データベースへの再接続が、ターゲット データベース接続のコマンドとは異なり、メタデータは読み込まれません。  
  
エラーが生成されます (再) ターゲットへの接続を確立できない場合、さらに実行を停止するコンソール アプリケーションです。  
  
**構文例:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>レポート コマンド  
レポート コマンドでは、SSMA コンソールのさまざまなアクティビティのパフォーマンス上のレポートを生成します。  
  
### <a name="generate-assessment-report"></a>generate-assessment-report  
  
このコマンドは、元のデータベースに対して評価レポートを生成します。  
  
ソース データベース接続がこのコマンドを実行する前に実行されない場合は、エラーが生成され、コンソール アプリケーションが終了します。  
  
コマンドの実行中に、ソース データベース サーバーへの接続に障害はまた、コンソール アプリケーションを終了になります。  
  
-   `conversion-report-folder:` 評価レポートを格納できるフォルダーを指定します。 (省略可能な属性)  
  
-   `object-name:` 評価レポートの生成 (サポートの個々 のオブジェクト名またはグループのオブジェクト名) の対象オブジェクトを指定します。  
  
-   `object-type:` (オブジェクトのカテゴリを指定すると、オブジェクトの種類が"category"になる) 場合は、オブジェクト名の属性で示されて、オブジェクトの種類を指定します。  
  
-   `conversion-report-overwrite:` 既に存在する場合は、評価のレポート フォルダーを上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-summary-report-to:` レポートが生成するパスを指定します。  
  
    フォルダーのパスが記載されている場合のみ、ファイル名で**AssessmentReport&lt;n&gt;します。XML**が作成されます。 (省略可能な属性)  
  
    レポートを作成するには、さらに 2 つのサブカテゴリがあります。  
  
    -   `report-errors` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
    -   `verbose` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
**構文例:**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
または  
  
```xml  
<generate-assessment-report  
  
  assessment-report-folder="<folder-name>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
<metabase-object object-name="<object-name>"  
  
        object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-commands"></a>移行コマンド  
移行コマンドでは、ターゲット データベースのスキーマを送信元スキーマに変換し、対象サーバーにデータを移行します。  
  
### <a name="convert-schema"></a>変換とスキーマ  
このコマンドは、ソースからターゲット スキーマへのスキーマの変換を実行します。  
  
ソースまたはターゲット データベース接続がこのコマンドを実行する前に実行されないか、コマンドの実行中にソースまたはターゲットのデータベース サーバーへの接続が失敗した場合は、エラーが生成され、コンソール アプリケーションが終了します。  
  
-   `conversion-report-folder:` 評価レポートを保存するフォルダーを指定します。 (省略可能な属性)  
  
-   `object-name:` スキーマ (サポートの個々 のオブジェクト名またはグループのオブジェクト名) に変換すると見なされるソース オブジェクトを指定します。  
  
-   `object-type:` (オブジェクトのカテゴリを指定すると、オブジェクトの種類が"category"になる) 場合は、オブジェクト名の属性で示されて、オブジェクトの種類を指定します。  
  
-   `conversion-report-overwrite:` 既に存在する場合は、評価のレポート フォルダーを上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-summary-report-to:` 概要レポートが生成するパスを指定します。  
  
    フォルダーのパスが記載されている場合のみ、ファイル名で**SchemaConversionReport&lt;n&gt;します。XML**が作成されます。 (省略可能な属性)  
  
    レポートを作成するには、さらに 2 つのサブカテゴリがあります。  
  
    -   `report-errors` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
    -   `verbose` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
**構文例:**  
  
```xml  
<convert-schema  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  write-summary-report-to="<file-name/folder-name>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder-name>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
または  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>データの移行  
このコマンドは、ソース データをターゲットに移行します。  
  
-   `object-name:` 移行すると見なされるソース オブジェクトを指定します (サポートの個々 のオブジェクト名またはグループのオブジェクト名) のデータ。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で示されて、オブジェクトの種類を指定します。  
  
-   `write-summary-report-to:` レポートが生成するパスを指定します。  
  
    フォルダーのパスが記載されている場合のみ、ファイル名で**DataMigrationReport&lt;n&gt;します。XML**が作成されます。 (省略可能な属性)  
  
    レポートを作成するには、さらに 2 つのサブカテゴリがあります。  
  
    -   `report-errors` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
    -   `verbose` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
**構文例:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>">  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
または  
  
```xml  
<migrate-data  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>移行準備コマンド  
移行の準備中のコマンドは、ソースとターゲット データベース間のスキーマ マッピングを開始します。  
  
> [!NOTE]  
> 設定の移行コマンドの既定のコンソール出力は、詳細なエラー レポートを作成しないとレポートを 'Full' の出力を示します。ソース オブジェクトのツリーのルート ノードでのみの概要です。  
  
### <a name="map-schema"></a>マップとスキーマ  
このコマンドは、ターゲット スキーマにソース データベースのスキーマ マッピングを提供します。  
  
-   `source-schema` 移行する送信元スキーマを指定します。  
  
-   `sql-server-schema` 送信元スキーマの移行されたターゲット スキーマを指定します。  
  
**構文例:**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>管理コマンド  
管理コマンドは、ソース データベースとターゲットのデータベース オブジェクトを同期するのに役立ちます。  
  
> [!NOTE]  
> 設定の移行コマンドの既定のコンソール出力は、詳細なエラー レポートを作成しないとレポートを 'Full' の出力を示します。ソース オブジェクトのツリーのルート ノードでのみの概要です。  
  
### <a name="synchronize-target"></a>同期ターゲット  
このコマンドは、ターゲット データベースとターゲット オブジェクトを同期します。  
 
ソース データベースに対しては、このコマンドを実行する場合は、エラーが発生しました。  
  
ターゲット データベースの接続がこのコマンドを実行する前に実行されない、またはコマンドの実行中に、ターゲット データベース サーバーへの接続が失敗した、エラーが発生し、コンソール アプリケーションが終了します。  
  
-   `object-name:` ターゲット データベース (サポートの個々 のオブジェクト名またはグループのオブジェクト名) との同期と見なされるターゲット オブジェクトを指定します。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で示されて、オブジェクトの種類を指定します。  
  
-   `on-error:` 同期エラーを警告またはエラーとして指定するかどうかを指定します。 エラー時の使用可能なオプション:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   フェールオーバー スクリプト  
  
-   `report-errors-to:` 同期操作 (省略可能な属性) のエラー レポートの場所を指定します。 フォルダーのパスを指定すると、専用の場合、ファイル名で**TargetSynchronizationReport.XML**が作成されます。  
  
**構文例:**  
  
```xml  
<synchronize-target  
  
object-name="<object-name>"  
  
on-error="<report-total-as-warning/  
  
report-each-as-warning/  
  
fail-script>" (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
または  
  
```xml  
<synchronize-target  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"/>  
```  
または  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
  
### <a name="refresh-from-database"></a>データベースからの更新  
このコマンドは、データベースからのソース オブジェクトを更新します。  
  
ターゲット データベースに対してこのコマンドを実行すると、エラーが生成されます。  
  
このコマンドでは、コマンド ライン パラメーターとして 1 つまたはいくつかのメタベース ノードが必要です。  
  
-   `object-name:` (サポートの個々 のオブジェクト名またはグループのオブジェクト名)、ソース データベースから更新すると見なされるソース オブジェクトを指定します。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `on-error:` 警告またはエラーとして更新エラーを呼び出すかどうかを指定します。 エラー時の使用可能なオプション:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   フェールオーバー スクリプト  
  
-   `report-errors-to:` 更新操作 (省略可能な属性) のエラー レポートの場所を指定します。 フォルダーのパスを指定すると、専用の場合、ファイル名で**SourceDBRefreshReport.XML**が作成されます。  
  
**構文例:**  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  on-error="<report-total-as-warning/  
  
             report-each-as-warning/  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
または  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
または  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>スクリプトの生成コマンド  
デュアルのタスクを実行するスクリプトの生成コマンド: コンソール出力スクリプト ファイルに保存できるし、コンソールまたは指定したパラメーターに基づいてファイルを T-SQL で出力が記録されます。  
  
### <a name="save-as-script"></a>save-as-script  
このコマンドを使用して、保存をファイルにオブジェクトのスクリプトで説明したときにメタベース ターゲットを = です。 これは、同じように、ターゲット データベースで実行し、スクリプトを取得することで、同期コマンドの代替です。  
  
このコマンドでは、コマンド ライン パラメーターとして 1 つまたはいくつかのメタベース ノードが必要です。  
  
-   `object-name:` そのスクリプトが (サポートの個々 のオブジェクト名またはグループのオブジェクト名) に保存されるオブジェクトを指定します。  
  
-   `object-type:` (オブジェクトのカテゴリを指定すると、オブジェクトの種類が"category"になる) 場合は、オブジェクト名の属性で示されて、オブジェクトの種類を指定します。  
  
-   `metabase:` ソースがあるかどうかを指定またはメタベースのターゲットします。  
  
-   `destination:` スクリプトの保存されているフォルダーのパスを指定します。 ファイル名が指定されていない場合は、形式 (object_name 属性値) .out 内のファイル名が提供されます。
  
-   `overwrite:` True の場合、上書きされます同じファイル名が存在する場合。 値 (真/偽) ことができます。  
  
**構文例:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  destination="<file-name/folder-name>"  
  
  overwrite="<true/false>"   (optional)  
  
/>  
```  
または  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>convert-sql-statement
このコマンドでは、SQL ステートメントに変換します。  
  
-   `context` スキーマ名を指定します。  
  
-   `destination` ファイルに出力を保存するかどうかを指定します。  
  
    この属性が指定されていない場合、変換された T-SQL ステートメントは、コンソールに表示されます。 (省略可能な属性)  
  
-   `conversion-report-folder` 評価レポートを格納できるフォルダーを指定します。 (省略可能な属性)  
  
-   `conversion-report-overwrite` 既に存在する場合は、評価のレポート フォルダーを上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-converted-sql-to` 変換後の T-SQL を格納するファイル (または) フォルダーのパスを指定します。 と共にフォルダーのパスが指定されている場合、`sql-files`属性、各ソース ファイルに対応するターゲット T-SQL ファイルを指定したフォルダーの下に作成します。 と共にフォルダーのパスが指定されている場合、`sql`属性、変換された T-SQL は、指定したフォルダーの下で Result.out をという名前のファイルに書き込まれます。  
  
-   `sql` 変換するには、Sybase sql ステートメントを指定を使用して 1 つまたは複数のステートメントを区切ることができます、「;」  
  
-   `sql-files` T-SQL コードに変換する必要がある sql ファイルのパスを指定します。  
  
-   `write-summary-report-to` 概要レポートが生成される場所のパスを指定します。 フォルダーのパスが記載されている場合のみ、ファイル名で**ConvertSQLReport.XML**が作成されます。 (省略可能な属性)  
  
    概要レポートの作成では、2 つのさらにサブカテゴリを namely があります。  
  
    -   レポートのエラー (="true/false"、"false"(省略可能な属性) として既定値)。  
  
    -   詳細 (="true/false"に、既定値は"false"(省略可能な属性) として)。  
  
このコマンドでは、コマンド ライン パラメーターとして 1 つまたはいくつかのメタベース ノードが必要です。  
  
**構文例:**  
  
```  
<convert-sql-statement  
  
       context="<database-name>.<schema-name>"  
  
        conversion-report-folder="<folder-name>"  
  
        conversion-report-overwrite="<true/false>"  
  
        write-summary-report-to="<file-name/folder-name>"   (optional)  
  
        verbose="<true/false>"   (optional)  
  
        report-errors="<true/false>"   (optional)  
  
        destination="<stdout/file>"   (optional)  
  
        write-converted-sql-to ="<file-name/folder-name>"  
  
        sql="SELECT 1 FROM DUAL;">  
  
    <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
または  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         write-summary-report-to="<file-name/folder-name>"   (optional)  
  
         verbose="<true/false>"   (optional)  
  
         report-errors="<true/false>"   (optional)  
  
         destination="<stdout/file>"   (optional)  
  
         write-converted-sql-to ="<file-name/folder-name>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
または  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-steps"></a>次の手順  
コマンド ライン オプションについては、次を参照してください。 [(AccessToSQL) SSMA コンソールのコマンド ライン オプション](../access/command-line-options-in-ssma-console-accesstosql.md)します。  
  
サンプルのコンソール スクリプト ファイルについては、次を参照してください[サンプルのコンソール スクリプト ファイルを扱う&#40;SybaseToSQL。&#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
次の手順は、プロジェクトの要件によって異なります。  
  
-   パスワードまたはエクスポートを指定する]、[パスワードのインポートを参照してください[管理パスワード&#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md)します。  
  
-   レポートを生成するため、次を参照してください。[レポートを生成する&#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)します。  
  
-   コンソールで問題をトラブルシューティングするには、次を参照してください。[トラブルシューティング&#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md)します。  
  
