---
title: SSMA コンソール (OracleToSQL) の実行 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle SSMA Console
- Script File Commands, Script Generation Commands,Manageability Commands
- Script File Commands,Project Commands
ms.assetid: 7228ccba-c69f-4b4c-8664-01a2750183c5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 5cb3ff58156d35a348a432e6d7edb7f794e59e6f
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266093"
---
# <a name="executing-the-ssma-console-oracletosql"></a>SSMA コンソールの実行 (OracleToSQL)
Microsoft は、ファイルのコマンドを実行し、SSMA アクティビティを制御する堅牢なスクリプトのセットを提供します。 コンソール アプリケーションは、このセクションでは、列挙型として標準的なスクリプト ファイルの特定のコマンドを使用します。  
  
## <a name="project-script-file-commands"></a>プロジェクト スクリプト ファイルのコマンド  
プロジェクト コマンドでは、プロジェクトの作成、開く、保存、およびプロジェクトの終了を処理します。  
  
**Command**  
  
create-new-project  
                  :新しい SSMA プロジェクトを作成します。  
  
**[スクリプト]**  
  
-   `project-folder` プロジェクトの作成中のフォルダーを示します。  
  
-   `project-name` プロジェクトの名前を示します。 {string}  
  
-   `overwrite-if-exists`省略可能な属性は、既存のプロジェクトを上書きするかどうかを示します。 {boolean}  
  
-   `project-type:`省略可能な属性です。 プロジェクトの種類「sql server 2005」プロジェクトつまりまたは「sql server 2008」のプロジェクトまたはプロジェクトの「sql server 2012」または「sql server 2014」プロジェクトまたは"sql azure"を示します。 既定では「sql server 2014」です。  
  
**例:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014>"   (optional)  
  
/>  
```  
'上書きの場合-存在' 属性が**false**既定。  
  
'プロジェクトの種類' 属性が**sql server2008**既定。  
  
**Command**  
  
開くプロジェクト:既存のプロジェクトを開きます。  
  
**[スクリプト]**  
  
-   `project-folder` プロジェクトの作成中のフォルダーを示します。 指定したフォルダーが存在しない場合、コマンドが失敗します。  {string}  
  
-   `project-name` プロジェクトの名前を示します。 指定されたプロジェクトが存在しない場合、コマンドが失敗します。  {string}  
  
**構文例:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
SSMA for Oracle コンソール アプリケーションでは、旧バージョンとの互換性をサポートします。 SSMA の以前のバージョンで作成されたプロジェクトを開くことができます。  
  
**Command**  
  
save-project  
  
移行プロジェクトを保存します。  
  
**[スクリプト]**  
  
**構文例:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
close-project  
  
移行プロジェクトを閉じます。  
  
**[スクリプト]**  
  
**構文例:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
  
## <a name="database-connection-script-file-commands"></a>データベース接続のスクリプト ファイルのコマンド  
データベース接続のコマンドは、データベースに接続するのに役立ちます。  
  
-   **参照**コンソールで、UI の機能がサポートされていません。  
  
-   スクリプト ファイルの作成 ' の詳細については、次を参照してください。[スクリプト ファイルの作成&#40;OracleToSQL&#41;](../../ssma/oracle/creating-script-files-oracletosql.md)します。  
  
**Command**  
  
接続ソース データベース  
  
-   ソース データベースへの接続を実行し、ソース データベースが、すべてのメタデータの高レベルのメタデータを読み込みます。  
  
-   ソースへの接続を確立できない場合、エラーが生成され、さらに実行を停止するコンソール アプリケーション  
  
**[スクリプト]**  
  
サーバーの定義は、サーバー接続ファイルまたはスクリプト ファイルのサーバー セクションでは、各接続に対して定義されている name 属性から取得されます。  
  
**構文例:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
force-読み込み-ソース/ターゲットのデータベース  
  
-   ソースのメタデータを読み込みます。  
  
-   移行プロジェクトをオフラインで作業するために便利です。  
  
-   ソース/ターゲットへの接続を確立できない場合、エラーが生成され、さらに実行を停止するコンソール アプリケーション  
  
**[スクリプト]**  
  
コマンド ライン パラメーターとして 1 つまたはいくつかのメタベース ノードが必要です。  
  
**構文例:**  
  
```xml  
<force-load object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
または  
  
```xml  
<force-load>  
  
   <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
再接続ソース データベース  
  
-   ソース データベースへの再接続がソース データベースの connect コマンドとは異なり、メタデータは読み込まれません。  
  
-   エラーが生成されます (再) ソースとの接続を確立できない場合、さらに実行を停止するコンソール アプリケーションです。  
  
**[スクリプト]**  
  
**構文例:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
connect-target-database  
  
-   対象の SQL Server データベースに接続し、ターゲット データベースの高レベルのメタデータがメタデータではなくを完全に読み込みます。  
  
-   ターゲットへの接続を確立できない場合は、エラーが生成され、さらに実行を停止するコンソール アプリケーションです。  
  
**[スクリプト]**  
  
サーバーの定義は、サーバー接続ファイルまたはスクリプト ファイルのサーバー セクションでは、各接続に対して定義されている name 属性から取得されます。  
  
**構文例:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
reconnect-target-database  
  
-   ターゲット データベースへの再接続が、接続先のデータベース コマンドとは異なり、メタデータは読み込まれません。  
  
-   エラーが生成されます (再) ターゲットへの接続を確立できない場合、さらに実行を停止するコンソール アプリケーションです。  
  
**[スクリプト]**  
  
**構文例:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file--commands"></a>レポートのスクリプト ファイルのコマンド  
レポート コマンドでは、SSMA コンソールのさまざまなアクティビティのパフォーマンス上のレポートを生成します。  
  
**Command**  
  
generate-assessment-report  
  
-   ソース データベースで評価レポートを生成します。  
  
-   ソース データベース接続がこのコマンドを実行する前に実行されない場合は、エラーが生成され、コンソール アプリケーションが終了します。  
  
-   コマンドの実行中に、ソース データベース サーバーへの接続に障害はまた、コンソール アプリケーションを終了になります。  
  
**[スクリプト]**  
  
-   `conversion-report-folder:` 評価レポートが格納するフォルダーを指定します。(省略可能な属性)  
  
-   `object-name:` 評価レポートの生成 (それが個々 のオブジェクト名またはグループ オブジェクトの名前) の対象オブジェクトを指定します。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `conversion-report-overwrite:` 既に存在する場合は、評価のレポート フォルダーを上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-summary-report-to:` 概要レポートが生成される場所のパスを指定します。  
  
    フォルダーのパスが記載されている場合のみ、ファイル名で**AssessmentReport&lt;n&gt;します。XML**が作成されます。 (省略可能な属性)  
  
    レポートを作成するには、さらに 2 つのサブ カテゴリがあります。  
  
    -   `report-errors` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
    -   `verbose` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
**構文例:**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   assessment-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
または  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>移行スクリプト ファイルのコマンド  
移行コマンドでは、送信元スキーマのターゲット データベースのスキーマの変換し、ターゲット サーバーにデータを移行します。  
  
設定の移行コマンドの既定のコンソール出力は、詳細なエラー レポートを作成しないとレポートを 'Full' の出力を示します。ソース オブジェクトのツリーのルート ノードでのみの概要です。  
  
**Command**  
  
変換とスキーマ  
  
-   ソースからターゲット スキーマへのスキーマの変換を実行します。  
  
-   ソースまたはターゲット データベース接続がこのコマンドを実行する前に実行されないか、コマンドの実行中にソースまたはターゲットのデータベース サーバーへの接続が失敗した場合は、エラーが生成され、コンソール アプリケーションが終了します。  
  
**[スクリプト]**  
  
-   `conversion-report-folder:` 評価レポートが格納するフォルダーを指定します。(省略可能な属性)  
  
-   `object-name:` (これが個々 のオブジェクト名またはグループ オブジェクトの名前) スキーマに変換すると見なされるソース オブジェクトを指定します。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `conversion-report-overwrite:` 既に存在する場合は、評価のレポート フォルダーを上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-summary-report-to:` 概要レポートが生成される場所のパスを指定します。  
  
    フォルダーのパスが記載されている場合のみ、ファイル名で**SchemaConversionReport&lt;n&gt;します。XML**が作成されます。 (省略可能な属性)  
  
    レポートを作成するには、さらに 2 つのサブ カテゴリがあります。  
  
    -   `report-errors` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
    -   `verbose` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
**構文例:**  
  
```xml  
<convert-schema  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
または  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Command**  
  
データの移行  
  
ソース データをターゲットに移行します。  
  
**[スクリプト]**  
  
-   `conversion-report-folder:` 評価レポートが格納するフォルダーを指定します。(省略可能な属性)  
  
-   `object-name:` 移行すると見なされるソース オブジェクトを指定します (これが個々 のオブジェクト名またはグループ オブジェクトの名前) データ。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `conversion-report-overwrite:` 既に存在する場合は、評価のレポート フォルダーを上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-summary-report-to:` 概要レポートが生成される場所のパスを指定します。  
  
    フォルダーのパスが記載されている場合のみ、ファイル名で**DataMigrationReport&lt;n&gt;します。XML**が作成されます。 (省略可能な属性)  
  
    レポートを作成するには、さらに 2 つのサブ カテゴリがあります。  
  
    -   `report-errors` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
    -   `verbose` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
**構文例:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>">  
  
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
  
   report-errors="<true/false>"  
  
   verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>移行の準備スクリプト ファイル コマンド  
移行の準備中のコマンドは、ソースとターゲット データベース間のスキーマ マッピングを開始します。  
  
**Command**  
  
マップとスキーマ  
  
ターゲット スキーマにソース データベースのスキーマ マッピングです。  
  
ソース データをターゲットに移行します。  
  
**[スクリプト]**  
  
-   `source-schema` 移行する予定の送信元スキーマを指定します。  
  
-   `sql-server-schema` 移行するにするターゲット スキーマを指定します。  
  
**構文例:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>スクリプト コマンド ファイルの管理の容易性  
管理コマンドは、ソース データベースとターゲットのデータベース オブジェクトを同期するのに役立ちます。 設定の移行コマンドの既定のコンソール出力は、詳細なエラー レポートを作成しないとレポートを 'Full' の出力を示します。ソース オブジェクトのツリーのルート ノードでのみの概要です。  
  
**Command**  
  
同期ターゲット  
  
-   ターゲット オブジェクトは、ターゲット データベースと同期されます。  
  
-   ソース データベースに対しては、このコマンドを実行する場合は、エラーが発生しました。  
  
-   ターゲット データベースの接続がこのコマンドを実行する前に実行されない、またはコマンドの実行中に、ターゲット データベース サーバーへの接続が失敗した、エラーが発生し、コンソール アプリケーションが終了します。  
  
**[スクリプト]**  
  
-   `object-name:` (これが個々 のオブジェクト名またはグループ オブジェクトの名前)、ターゲット データベースとの同期と見なされるターゲット オブジェクトを指定します。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `on-error:` 同期エラーを警告またはエラーとして指定するかどうかを指定します。 エラー時の使用可能なオプション:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   フェールオーバー スクリプト  
  
-   `report-errors-to:` 同期操作 (省略可能な属性) だけフォルダーのパスを指定すると、ファイル名では、エラー レポートの場所を指定します**TargetSynchronizationReport.XML**が作成されます。  
  
**構文例:**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
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
**Command**  
  
データベースからの更新  
  
-   データベースからのソース オブジェクトを更新します。  
  
-   ターゲット データベースに対してこのコマンドを実行すると、エラーが生成されます。  
  
**[スクリプト]**  
  
コマンド ライン パラメーターとして 1 つまたはいくつかのメタベース ノードが必要です。  
  
-   `object-name:` (これが個々 のオブジェクト名またはグループ オブジェクトの名前)、ソース データベースから更新すると見なされるソース オブジェクトを指定します。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `on-error:` 更新エラーを警告またはエラーとして指定するかどうかを指定します。 エラー時の使用可能なオプション:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   フェールオーバー スクリプト  
  
-   `report-errors-to:` エラー レポートの場所を指定します (省略可能な属性) の更新操作だけフォルダーのパスを指定すると、し、ファイル名で**SourceDBRefreshReport.XML**が作成されます。  
  
**構文例:**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
/>  
```  
または  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
または  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>スクリプトの生成スクリプト ファイル コマンド  
スクリプトの生成コマンドでは、2 つのタスクを実行します。コンソール出力スクリプト ファイルに保存できます。コンソールまたは指定したパラメーターに基づいてファイルを T-SQL で出力を記録します。  
  
**Command**  
  
save-as-script  
  
オブジェクトのスクリプトと指定したファイルに保存するために使用メタベース = ターゲット、同期コマンドの場所でスクリプトを取得し、ターゲット データベースで同じように実行する代わりになります。  
  
**[スクリプト]**  
  
コマンド ライン パラメーターとして 1 つまたはいくつかのメタベース ノードが必要です。  
  
-   `object-name:` そのスクリプトが保存されるオブジェクトを指定します。 (これが個々 のオブジェクト名またはグループ オブジェクトの名前)  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `metabase:` 指定するかどうか、このソースか、メタベースを対象します。  
  
-   `destination:` パスまたはファイル名を指定しない場合、ファイル名形式 (object_name 属性値) .out で、スクリプトに保存するのには、フォルダーを指定します  
  
-   `overwrite:` true の場合、上書き同じファイル名が存在しない場合。 値 (真/偽) ことができます。  
  
**構文例:**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file/folder>"  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
または  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file/folder>"  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Command**  
  
convert-sql-statement  
  
-   `context` スキーマ名を指定します。  
  
-   `destination` ファイルに出力を保存するかどうかを指定します。  
  
    この属性が指定されていない場合、変換された T-SQL ステートメントは、コンソールに表示されます。 (省略可能な属性)  
  
-   `conversion-report-folder` 評価レポートが格納するフォルダーを指定します。(省略可能な属性)  
  
-   `conversion-report-overwrite` 既に存在する場合は、評価のレポート フォルダーを上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-converted-sql-to` ファイル (または)、変換後の T-SQL が格納されるフォルダーのパスを指定します。 と共にフォルダーのパスが指定されている場合、`sql-files`属性に、各ソース ファイルが対応するターゲット T-SQL ファイルを指定したフォルダーの下に作成します。 と共にフォルダーのパスが指定されている場合、`sql`属性、変換された T-SQL はという名前のファイルに書き込まれる**Result.out**指定したフォルダーの下。  
  
-   `sql` Oracle の sql ステートメントに変換する、1 つまたは複数のステートメントを指定します区切りを使用することを「;」  
  
-   `sql-files` T-SQL コードに変換する必要がある sql ファイルのパスを指定します。  
  
-   `write-summary-report-to` レポートが生成される場所のパスを指定します。 フォルダーのパスが記載されている場合のみ、ファイル名で**ConvertSQLReport.XML**が作成されます。 (省略可能な属性)  
  
    レポートの作成が可視のサブカテゴリの一覧をさらに 2。  
  
    -   レポートのエラー (="true/false"、"false"(省略可能な属性) として既定値)。  
  
    -   詳細 (="true/false"に、既定値は"false"(省略可能な属性) として)。  
  
**[スクリプト]**  
  
コマンド ライン パラメーターとして 1 つまたはいくつかのメタベース ノードが必要です。  
  
**構文例:**  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   file-name="<file-name>"  
  
   sql="SELECT 1 FROM DUAL;">  
  
   <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
または  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>" (optional)  
  
   verbose="<true/false>" (optional)  
  
   report-errors="<true/false>"  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
または  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
  
## <a name="next-step"></a>次の手順  
コマンド ライン オプションについては、次を参照してください。 [SSMA コンソールのコマンド ライン オプション&#40;OracleToSQL&#41; ](../../ssma/oracle/command-line-options-in-ssma-console-oracletosql.md)します。  
  
サンプルのコンソール スクリプト ファイルについては、次を参照してください[サンプルのコンソール スクリプト ファイルを扱う&#40;OracleToSQL。&#41;](../../ssma/oracle/working-with-the-sample-console-script-files-oracletosql.md)  
  
次の手順は、プロジェクトの要件によって異なります。  
  
-   パスワードまたはエクスポートを指定する]、[パスワードのインポートを参照してください[管理パスワード&#40;OracleToSQL&#41;](../../ssma/oracle/managing-passwords-oracletosql.md)します。  
  
-   レポートを生成するため、次を参照してください。[レポートを生成する&#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md)します。  
  
-   コンソールで問題をトラブルシューティングするには、次を参照してください。[トラブルシューティング&#40;OracleToSQL&#41;](../../ssma/oracle/troubleshooting-oracletosql.md)します。  
  
