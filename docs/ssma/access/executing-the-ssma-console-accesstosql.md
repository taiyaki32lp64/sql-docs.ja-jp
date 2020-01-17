---
title: SSMA コンソール (AccessToSQL) の実行 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 97425a6795889f72b329280ff70f9638378e7799
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006568"
---
# <a name="executing-the-ssma-console-accesstosql"></a>SSMA コンソール (AccessToSQL) の実行
Microsoft は、堅牢な一連のスクリプト ファイルのコマンドとコマンド ライン オプションを実行し、SSMA アクティビティの制御を提供します。 次のセクションでは、同じについて説明します。  
  
## <a name="project--script-file-commands"></a>プロジェクト スクリプト ファイルのコマンド  
プロジェクト コマンドでは、プロジェクトの作成、開く、保存、およびプロジェクトの終了を処理します。  
  
**Command**  
  
create-new-project:新しい SSMA プロジェクトを作成します。  
  
**[スクリプト]**  
  
-   `project-folder` プロジェクトの作成中のフォルダーを示します。  
  
-   `project-name` プロジェクトの名前を示します。 {string}  
  
-   `overwrite-if-exists`省略可能な属性は、既存のプロジェクトを上書きするかどうかを示します。 {boolean}  
  
-   `project-type` 省略可能な属性です。  プロジェクトの種類は次のオプションです。  
  
    -   sql-server-2005  
  
    -   sql-server-2008  
  
    -   sql-server-2012  
  
    -   sql-server-2014  
  
    -   sql server の 2016  
  
    -   sql-azure  
  
    既定では「sql server 2008」です。  
  
**例:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>"  
  
  project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>"  
  
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
**注:** SSMA For Access コンソール アプリケーションでは、旧バージョンとの互換性をサポートします。 SSMA の以前のバージョンで作成されたプロジェクトを開くことができます。  
  
**Command**  
  
プロジェクトの保存。移行プロジェクトを保存します。  
  
**[スクリプト]**  
  
**構文例:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
閉じるプロジェクト:移行プロジェクトを閉じます。  
  
**[スクリプト]**  
  
**構文例:**  
  
```xml  
<close-project  
  
  if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
'If 変更' 属性は省略可能で**無視**既定。  
  
## <a name="database-connection-script-file-commands"></a>データベース接続のスクリプト ファイルのコマンド  
データベース接続のコマンドは、データベースに接続するのに役立ちます。  
  
**参照**コンソールで、UI の機能がサポートされていません。  
  
**Windows 認証**と**ポート**パラメーターは、SQL Azure に接続するときは適用されません。  
  
スクリプト ファイルの作成 ' の詳細については、次を参照してください。[スクリプト ファイルの作成&#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md)します。  
  
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
  
読み込み-アクセス-データベース:Access データベース ファイルを読み込むために使用  
  
**[スクリプト]**  
  
**構文例:**  
  
```xml  
<load-access-database  database-file="<Access-database>"/>  
```  
または  
  
```xml  
<load-access-database>  
  
  <access-database database-file="<Access-database1>"/>  
  
  <access-database database-file="<Access-database2>"/>  
  
</load-access-database>  
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
<force-load  
  
  object-name="<object-name>"  
  
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
  
-   ターゲット SQL Server または SQL Azure データベースに接続し、ターゲット データベースの高レベルのメタデータがメタデータではなくを完全に読み込みます。  
  
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
  
## <a name="report-script-file-commands"></a>レポートのスクリプト ファイルのコマンド  
レポート コマンドでは、SSMA コンソールのさまざまなアクティビティのパフォーマンス上のレポートを生成します。  
  
**Command**  
  
generate-assessment-report  
  
-   ソース データベースで評価レポートを生成します。  
  
-   ソース データベース接続がこのコマンドを実行する前に実行されない場合は、エラーが生成され、コンソール アプリケーションが終了します。  
  
-   コマンドの実行中に、ソース データベース サーバーへの接続に障害はまた、コンソール アプリケーションを終了になります。  
  
**[スクリプト]**  
  
-   `assessment-report-folder:` 評価レポートが格納するフォルダーを指定します。(省略可能な属性)  
  
-   `object-name:` 評価レポートの生成 (それが個々 のオブジェクト名またはグループ オブジェクトの名前) の対象オブジェクトを指定します。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `assessment-report-overwrite:` 既に存在する場合は、評価のレポート フォルダーを上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-summary-report-to:` レポートが生成される場所のパスを指定します。  
  
    フォルダーのパスが記載されている場合のみ、ファイル名で**AssessmentReport&lt;n&gt;します。XML**が作成されます。 (省略可能な属性)  
  
    レポートを作成するには、さらに 2 つのサブ カテゴリがあります。  
  
    -   `report-errors` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
    -   `verbose` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
**構文例:**  
  
```xml  
<generate-assessment-report  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  
  write-summary-report-to="<file>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  conversion-report-folder="<folder>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
または  
  
```xml  
<generate-assessment-report  
  
  conversion-report-folder="<folder>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
    <metabase-object object-name="ssma.Procedures"  
  
        object-type="category"/>  
  
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
  
-   `conversion-report-folder:` 評価レポートを格納するフォルダーを指定します。(省略可能な属性)  
  
-   `object-name:` (これが個々 のオブジェクト名またはグループ オブジェクトの名前) スキーマに変換すると見なされるソース オブジェクトを指定します。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `conversion-report-overwrite:` 既に存在する場合は、評価のレポート フォルダーを上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-summary-report-to:` レポートが生成される場所のパスを指定します。  
  
    フォルダーのパスが記載されている場合のみ、ファイル名で**SchemaConversionReport&lt;n&gt;します。XML**が作成されます。 (省略可能な属性)  
  
    レポートを作成するには、さらに 2 つのサブ カテゴリがあります。  
  
    -   `report-errors` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
    -   `verbose` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
**構文例:**  
  
```xml  
<convert-schema  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  write-summary-report-to="<filepath/folder>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
または  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder>"         (optional)  
  
  conversion-report-overwrite="<true/false>"  (optional)  
  
  <metabase-object object-name="ssma.Procedures"  
  
    object-type="category"/>  
  
</convert-schema>  
```  
**Command**  
  
データの移行  
  
1.  ソース データをターゲットに移行します。  
  
**[スクリプト]**  
  
-   `object-name:` 移行すると見なされるソース オブジェクトを指定します (これが個々 のオブジェクト名またはグループ オブジェクトの名前) データ。  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `write-summary-report-to:` レポートが生成される場所のパスを指定します。  
  
    フォルダーのパスが記載されている場合のみ、ファイル名で**DataMigrationReport&lt;n&gt;します。XML**が作成されます。 (省略可能な属性)  
  
    レポートを作成するには、さらに 2 つのサブ カテゴリがあります。  
  
    -   `report-errors` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
    -   `verbose` (="true/false"に、既定値は"false"(省略可能な属性) として)  
  
**構文例:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true">  
  
    <metabase-object object-name="ssma.TT1"/>  
  
    <metabase-object object-name="ssma.TT2"/>  
  
    <metabase-object object-name="ssma.TT3"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
または  
  
```xml  
<migrate-data  
  
  object-name="ssma.Tables"  
  
  object-type="category"  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true"/>  
```  
**Command**  
  
リンク テーブル:このコマンドは、対象のテーブルにソース (アクセス) テーブルをリンクします。  
  
**[スクリプト]**  
  
**構文例:**  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</link-tables>  
```  
または  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</link-tables>  
```  
**Command**  
  
リンクを解除-テーブル:このコマンドは、対象のテーブルから (アクセス) をソース テーブルをリンク解除します。  
  
**[スクリプト]**  
  
**構文例:**  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</unlink-tables>  
```  
または  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</unlink-tables>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>移行の準備スクリプト ファイル コマンド  
移行の準備中のコマンドは、ソースとターゲット データベース間のスキーマ マッピングを開始します。  
  
**Command**  
  
マップとスキーマ:ターゲット スキーマにソース データベースのスキーマ マッピングです。  
  
**[スクリプト]**  
  
-   `source-schema` 移行する予定の送信元スキーマを指定します。  
  
-   `sql-server-schema` 移行するにするターゲット スキーマを指定します。  
  
**構文例:**  
  
```xml  
<map-schema source-schema="source-schema"  
  
            sql-server-schema="target-schema"/>  
```  
  
## <a name="manageability-commands"></a>管理コマンド  
管理コマンドは、ソース データベースとターゲットのデータベース オブジェクトを同期するのに役立ちます。  
  
設定の移行コマンドの既定のコンソール出力は、詳細なエラー レポートを作成しないとレポートを 'Full' の出力を示します。ソース オブジェクトのツリーのルート ノードでのみの概要です。  
  
**Command**  
  
同期ターゲット  
  
1.  ターゲット オブジェクトは、ターゲット データベースと同期されます。  
  
2.  ソース データベースに対しては、このコマンドを実行する場合は、エラーが発生しました。  
  
3.  ターゲット データベースの接続がこのコマンドを実行する前に実行されない、またはコマンドの実行中に、ターゲット データベース サーバーへの接続が失敗した、エラーが発生し、コンソール アプリケーションが終了します。  
  
**[スクリプト]**  
  
1.  `object-name:` (これが個々 のオブジェクト名またはグループ オブジェクトの名前)、ターゲット データベースとの同期と見なされるターゲット オブジェクトを指定します。  
  
2.  `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
3.  `on-error:` 同期エラーを警告またはエラーとして指定するかどうかを指定します。 エラー時の使用可能なオプション:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   フェールオーバー スクリプト  
  
4.  `report-errors-to:` 同期操作 (省略可能な属性) だけフォルダーのパスを指定すると、ファイル名では、エラー レポートの場所を指定します**TargetSynchronizationReport.XML**が作成されます。  
  
**構文例:**  
  
```xml  
<synchronize-target  
  
  object-name="ots_triggers.dbo"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
または  
  
```xml  
<synchronize-target  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"/>  
```  
または  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="ssma.dbo.TT1"/>  
  
  <metabase-object object-name="ssma.dbo.TT2"/>  
  
  <metabase-object object-name="ssma.dbo.TT3"/>  
  
</synchronize-target>  
```  
**Command**  
  
データベースからの更新  
  
-   データベースからのソース オブジェクトを更新します。  
  
-   ターゲット データベースに対してこのコマンドを実行すると、エラーが生成されます。  
  
**[スクリプト]**  
  
コマンド ライン パラメーターとして 1 つまたはいくつかのメタベース ノードが必要です。  
  
1.  `object-name:` (これが個々 のオブジェクト名またはグループ オブジェクトの名前)、ソース データベースから更新すると見なされるソース オブジェクトを指定します。  
  
2.  `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
3.  `on-error:` 更新エラーを警告またはエラーとして指定するかどうかを指定します。 エラー時の使用可能なオプション:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   フェールオーバー スクリプト  
  
4.  `report-errors-to:` エラー レポートの場所を指定します (省略可能な属性) の更新操作だけフォルダーのパスを指定すると、し、ファイル名で**SourceDBRefreshReport.XML**が作成されます。  
  
**構文例:**  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.TT1"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
または  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.Procedures"  
  
  object-type="category"/>  
```  
または  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="ssma.TT_1"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>スクリプトの生成スクリプト ファイル コマンド  
コマンドにより、スクリプトの生成は、スクリプト ファイルで、コンソールの出力を保存します。  
  
**Command**  
  
save-as-script  
  
オブジェクトのスクリプトと指定したファイルに保存するために使用メタベース = ターゲット、同期コマンドの場所でスクリプトを取得し、ターゲット データベースで同じように実行する代わりになります。  
  
**[スクリプト]**  
  
コマンド ライン パラメーターとして 1 つまたはいくつかのメタベース ノードが必要です。  
  
-   `object-name:` そのスクリプトが保存されるオブジェクトを指定します。 (これが個々 のオブジェクト名またはグループ オブジェクトの名前)  
  
-   `object-type:` (オブジェクトの種類が"category"になる、オブジェクトのカテゴリが指定された) 場合は、オブジェクト名の属性で指定されたオブジェクトの種類を指定します。  
  
-   `metabase:` ソースがあるかどうかを指定またはメタベースのターゲットします。  
  
-   `destination:` パスまたはファイル名を指定しない場合、ファイル名形式 (object_name 属性値) .out で、スクリプトに保存するのには、フォルダーを指定します  
  
-   `overwrite:` true の場合、上書き同じファイル名が存在しない場合。 値 (真/偽) ことができます。  
  
**構文例:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"  
  
  destination="<file/folder>"  
  
  overwrite="<true/false>"             (optional)  
  
/>  
```  
または  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file/folder>"  
  
    <metabase-object object-name="ssma.dbo.Procedures"  
  
                     object-type="category"/>  
  
</save-as-script>  
```  
  
## <a name="next-step"></a>次の手順  
コマンド ライン オプションについては、次を参照してください。 [SSMA コンソールのコマンド ライン オプション&#40;AccessToSQL&#41; ](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md)します。  
  
サンプルのコンソール スクリプト ファイルについては、次を参照してください[サンプルのコンソール スクリプト FilesExecuting SSMA コンソールの操作&#40;AccessToSQL。&#41;](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)  
  
次の手順は、プロジェクトの要件によって異なります。  
  
-   パスワードまたはエクスポートを指定する]、[パスワードのインポートを参照してください[管理パスワード&#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md)します。  
  
-   レポートを生成するため、次を参照してください。[レポートを生成する&#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)します。  
  
-   コンソールで問題をトラブルシューティングするには、次を参照してください。[トラブルシューティング&#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md)します。  
  
