---
title: Oracle CDC Service の使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 04be5896-2301-45f5-a8ce-5f4ef2b69aa5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f8854dba3c1d998d572481c285ee75dc933e480
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771182"
---
# <a name="working-with-the-oracle-cdc-service"></a>Oracle CDC Service の使用
  ここでは、Oracle CDC Service のいくつかの重要な概念について説明します。 このセクションで説明する概念は次のとおりです。  
  
-   [MSXDBCDC データベース](#BKMK_MSXDBCDC)  
  
     このセクションでは、このデータベースに含まれるテーブルと、CDC に対するこのデータベースの重要性について説明します。  
  
-   [CDC データベース](#BKMK_CDCdatabase)  
  
     このセクションでは、CDC データベースの簡単な説明を示します。 これらのデータベースは、Oracle CDC デザイナー コンソールを使用して作成されます。 CDC データベースの詳細については、CDC デザイナー コンソールのインストールに付属のドキュメントを参照してください。  
  
-   [コマンド ラインを使用した CDC サービスの構成](#BKMK_CommandConfigCDC)  
  
     このセクションでは、Oracle CDC Service の構成に使用できるコマンド ラインのコマンドについて説明します。  
  
##  <a name="BKMK_MSXDBCDC"></a> MSXDBCDC データベース  
 MSXDBCDC (Microsoft External-Database CDC) データベースは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで CDC Service for Oracle を使用する際に必要な特殊なデータベースです。  
  
 このデータベースの名前は変更できません。 MSXDBCDC という名前のデータベースがホスト [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにあり、CDC Service for Oracle で定義されたテーブル以外のテーブルがそのデータベースに含まれている場合、ホスト [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを使用することはできません。  
  
 このデータベースの主な用途を次に示します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに関連付けられた Oracle CDC Service のレジストリとして機能します。 この情報は、サービスの構成コンポーネントやデザイン コンポーネントに使用されるほか、異なるノードにある同じ名前の複数の CDC サービスのうち、どのサービスをアクティブにするかを調整するために使用されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに含まれる Oracle CDC インスタンス、各インスタンスを処理する CDC サービス、および各サービスで使用される構成バージョンのレジストリとして機能します。 この情報は、master データベースの **sys.databases** テーブルの **[is_cdc_enabled]** 列と同じです。 CDC サービスでは、 **dbo.xdbcdc_databases** テーブルを定期的にスキャンして、CDC の構成や一連のキャプチャ対象インスタンスに対する変更を識別します。  
  
-   CDC インスタンスの作成や管理に役立つ **sysadmin**所有のストアド プロシージャを格納します。 これらは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の CDC 機能の実装に使用されるシステム プロシージャに似ています。  
  
### <a name="creating-the-msxdbcdc-database"></a>MSXDBCDC データベースの作成  
 Oracle CDC Service を定義する前に、MSXDBCDC データベースを作成する必要があります。 MSXDBCDC データベースは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスごとに 1 つだけ作成できます。 MSXDBCDC データベースは、Oracle CDC 用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを準備するときに作成されます。 これを行うには、Oracle CDC Service 構成コンソールを使用するか、CDC Service 構成コンソールで生成される作成スクリプトを実行します。  
  
 このデータベースの所有者は Oracle CDC Service の管理者です。この管理者は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでホストされるすべての Oracle CDC インスタンスを制御できます。  
  
 **関連項目:**  
  
 [CDC 用に SQL Server を準備する方法](prepare-sql-server-for-cdc.md)  
  
### <a name="the-msxdbcdc-database-tables"></a>MSXDBCDC データベースのテーブル  
 ここでは、MSXDBCDC データベースの次のテーブルについて説明します。  
  
-   [dbo.xdbcdc_trace](#BKMK_dboxdbcdc_trace)  
  
-   [dbo.xdbcdc_databases](#BKMK_dboxdbcdc_databases)  
  
-   [dbo.xdbcdc_services](#BKMK_dboxdbcdc_services)  
  
###  <a name="BKMK_dboxdbcdc_trace"></a> dbo.xdbcdc_trace  
 このテーブルには、Oracle CDC Service のトレース情報が格納されます。 このテーブルに格納される情報には、重要な状態変更とトレース レコードが含まれます。  
  
 Oracle CDC Service では、エラー レコードと一部の情報レコードについては、Windows イベント ログとトレース テーブルの両方に書き込まれます。 そのため、トレース テーブルにアクセスできない場合でも、イベント ログからエラー情報にアクセスできます。  
  
 **dbo.xdbcdc_trace** テーブルに含まれるアイテムを以下に示します。  
  
|アイテム|説明|  
|----------|-----------------|  
|TIMESTAMP|トレース レコードが書き込まれたときの正確な UTC タイムスタンプ。|  
|型|次のいずれかの値が格納されます。<br /><br /> error<br /><br /> INFO<br /><br /> trace|  
|node|レコードが書き込まれたノードの名前。|  
|ステータス|状態テーブルで使用される状態コード。|  
|sub_status|状態テーブルで使用される副状態コード。|  
|status_message|状態テーブルで使用される状態メッセージ。|  
|source|トレース レコードを生成した Oracle CDC コンポーネントの名前。|  
|text_data|追加のテキスト データ (エラー レコードまたはトレース レコードにテキスト ペイロードが含まれている場合)。|  
|binary_data|追加のバイナリ データ (エラー レコードまたはトレース レコードにバイナリ ペイロードが含まれている場合)。|  
  
 Oracle CDC インスタンスでは、変更テーブルの保有ポリシーに従ってトレース テーブルの古い行が削除されます。  
  
###  <a name="BKMK_dboxdbcdc_databases"></a> dbo.xdbcdc_databases  
 このテーブルには、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに含まれる Oracle CDC データベースの CDC Service の名前が格納されます。 各データベースは、それぞれ 1 つの Oracle CDC インスタンスに対応しています。 Oracle CDC Service では、このテーブルを使用して、開始または停止するインスタンスや再構成するインスタンスを特定します。  
  
 **dbo.xdbcdc_databases** テーブルに含まれるアイテムを次の表に示します。  
  
|アイテム|説明|  
|----------|-----------------|  
|NAME|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに含まれる Oracle データベースの名前。|  
|config_version|対応する CDC データベースの **xdbcdc_config** テーブルで行われた最後の変更のタイムスタンプ (UTC)、またはこのテーブルの現在の行のタイムスタンプ (UTC)。<br /><br /> UPDATE トリガーでは、このアイテムの GETUTCDATE() の値が適用されます。 CDC サービスでは**config_version** を使用して、構成の変更や有効化/無効化について確認する必要がある CDC インスタンスを識別できます。|  
|cdc_service_name|選択された Oracle データベースを処理する Oracle CDC Service を示します。|  
|enabled|Oracle CDC インスタンスがアクティブ (1) か無効 (0) かを示します。 Oracle CDC Service の起動時には、有効 (1) とマークされたインスタンスだけが開始されます。<br /><br /> **注**:Oracle CDC インスタンスは、再試行できないエラーが原因で無効になることがあります。 この場合は、エラーを解決してからインスタンスを手動で再起動する必要があります。|  
  
###  <a name="BKMK_dboxdbcdc_services"></a> dbo.xdbcdc_services  
 このテーブルには、ホスト [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに関連付けられている CDC サービスが表示されます。 このテーブルは、ローカルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス用に構成された CDC サービスを特定するために CDC デザイナー コンソールで使用されます。 また、特定の Oracle CDC Service を処理している実行中の Windows サービスが 1 つだけであることを確認するために CDC サービスで使用されます。  
  
 **dbo.xdbcdc_databases** テーブルに含まれるキャプチャ状態アイテムを以下に示します。  
  
|アイテム|説明|  
|----------|-----------------|  
|cdc_service_name|Oracle CDC Service の名前 (Windows サービス名)。|  
|cdc_service_sql_login|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続するために Oracle CDC Service で使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前。 cdc_service という名前の新しい SQL ユーザーが作成されてこのログイン名に関連付けられ、サービスで処理される各 CDC データベースの db_ddladmin、db_datareader、および db_datawriter 固定データベース ロールのメンバーとして追加されます。|  
|ref_count|同じ Oracle CDC Service がインストールされているコンピューターの数を示します。 同じ名前の Oracle CDC Service が追加されるたびに値が増加し、それらのサービスが削除されると減少します。 この行はカウンターが 0 に達すると削除されます。|  
|active_service_node|CDC サービスを現在処理している Windows ノードの名前。 この列は、サービスが適切に停止されると null に設定され、アクティブなサービスがなくなったことが示されます。|  
|active_service_heartbeat|現在の CDC サービスがまだアクティブであるかどうかを示します。<br /><br /> このアイテムは、アクティブな CDC サービスに対する現在のデータベースの UTC タイムスタンプに基づいて一定の間隔で更新されます。 既定の間隔は 30 秒ですが、この間隔は構成することも可能です。<br /><br /> 構成された間隔が経過してもハートビートが更新されていないことが保留中の CDC サービスで検出されると、その保留中のサービスで、アクティブな CDC サービスの役割の引き継ぎが試行されます。|  
|options|トレースやチューニングなどの二次的なオプションを指定します。 **name[=value][; ]** の形式で記述されます。 options の文字列では、ODBC 接続文字列と同じセマンティクスを使用します。 オプションがブール値 (value が yes または no) の場合は、name だけでもかまいません。<br /><br /> トレースでは、次の値があります。<br /><br /> true<br /><br /> on<br /><br /> false<br /><br /> off<br /><br /> \<class name>[,class name>]<br /><br /> 既定値は **false**です。<br /><br /> <br /><br /> **service_heartbeat_interval** は、active_service_heartbeat 列を更新する間隔 (秒) です。 既定値は、 **30**です。 最大値は **3600**です。<br /><br /> **service_config_polling_interval** は、構成の変更を確認するポーリング間隔 (秒) です。 既定値は、 **30**です。 最大値は **3600**です。<br /><br /> **sql_command_timeout** は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に対するコマンドのタイムアウトです。 既定値は **1**です。 最大値は **3600**です。|  
||  
  
### <a name="the-msxdbcdc-database-stored-procedures"></a>MSXDBCDC データベースのストアド プロシージャ  
 ここでは、MSXDBCDC データベースの次のストアド プロシージャについて説明します。  
  
-   [dbo.xcbcdc_reset_db(Database Name)](#BKMK_dboxcbcdc_reset_db)  
  
-   [dbo.xdbcdc_disable_db(dbname)](#BKMK_dboxdbcdc_disable_db)  
  
-   [dbo.xcbcdc_add_service(svcname,sqlusr)](#BKMK_dboxcbcdc_add_service)  
  
-   [dbo.xdbcdc_start(dbname)](#BKMK_dboxdbcdc_start)  
  
-   [dbo.xdbcdc_stop(dbname)](#BKMK_dboxdbcdc_stop)  
  
###  <a name="BKMK_dboxcbcdc_reset_db"></a> dbo.xcbcdc_reset_db(Database Name)  
 このプロシージャでは、Oracle CDC インスタンスのデータをクリアします。 次の場合に使用されます。  
  
-   前のデータを無視してデータのキャプチャを再開する場合 (ソース データベースを復旧した場合や、Oracle トランザクション ログの一部を使用できなくなった場合など)。  
  
-   CDC の状態 (具体的には cdc.*tables のデータ) が破損している場合。  
  
 **dbo.xcbcdc_reset_db** プロシージャでは、次の処理が行われます。  
  
-   CDC インスタンスを停止する (アクティブな場合)。  
  
-   変更テーブル、 **cdc_lsn_mapping** テーブル、および **cdc_ddl_history** テーブルを切り捨てる。  
  
-   **cdc_xdbcdc_state** テーブルをクリアする。  
  
-   **cdc_change_table**の各行の start_lsn 列をクリアする。  
  
 **dbo.xcbcdc_reset_db** プロシージャを使用するには、対象の CDC インスタンス データベースの **db_owner** データベース ロールのメンバーであるか、 **sysadmin** または **serveradmin** 固定サーバー ロールのメンバーである必要があります。  
  
 CDC テーブルの詳細については、CDC デザイナー コンソールのヘルプ システムで「 *CDC データベース* 」を参照してください。  
  
###  <a name="BKMK_dboxdbcdc_disable_db"></a> dbo.xdbcdc_disable_db(dbname)  
 **dbo.xcbcdc_disable_db** プロシージャでは、次の処理が行われます。  
  
-   選択した CDC データベースのエントリを MSXDBCDC.xdbcdc_databases テーブルから削除する。  
  
 **dbo.xcbcdc_disable_db** プロシージャを使用するには、対象の CDC インスタンスの **db_owner** データベース ロールのメンバーであるか、 **sysadmin** または **serveradmin** 固定サーバー ロールのメンバーである必要があります。  
  
 CDC テーブルの詳細については、CDC デザイナー コンソールのヘルプ システムで「CDC データベース」を参照してください。  
  
###  <a name="BKMK_dboxcbcdc_add_service"></a> dbo.xcbcdc_add_service(svcname,sqlusr)  
 **dbo.xcbcdc_add_service** プロシージャでは、 **MSXDBCDC.xdbcdc_services** テーブルにエントリを追加し、 **MSXDBCDC.xdbcdc_services** テーブル内の該当するサービスの ref_count 列の値を 1 増やします。 また、**ref_count** が 0 になると、その行を削除します。  
  
 **dbo.xcbcdc_add_service\<service name, username>** プロシージャを使用するには、対象の CDC インスタンス データベースの **db_owner** データベース ロールのメンバーであるか、**sysadmin** または **serveradmin** 固定サーバー ロールのメンバーである必要があります。  
  
###  <a name="BKMK_dboxdbcdc_start"></a> dbo.xdbcdc_start(dbname)  
 **dbo.xdbcdc_start** プロシージャでは、変更の処理を開始するために、選択した CDC インスタンスを処理する CDC サービスに開始要求を送信します。  
  
 **dbo.xcdcdc_start** プロシージャを使用するには、CDC データベースの **db_owner** データベース ロールのメンバーであるか、 **インスタンスの** sysadmin **または** serveradmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロールのメンバーである必要があります。  
  
###  <a name="BKMK_dboxdbcdc_stop"></a> dbo.xdbcdc_stop(dbname)  
 **dbo.xdbcdc_stop** プロシージャでは、変更の処理を停止するために、選択した CDC インスタンスを処理する CDC サービスに停止要求を送信します。  
  
 **dbo.xcdcdc_stop** プロシージャを使用するには、CDC データベースの **db_owner** データベース ロールのメンバーであるか、 **インスタンスの** sysadmin **または** serveradmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロールのメンバーである必要があります。  
  
##  <a name="BKMK_CDCdatabase"></a> CDC データベース  
 CDC サービスで使用される Oracle CDC インスタンスはそれぞれ、CDC データベースと呼ばれる特定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに関連付けられます。 この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースは、Oracle CDC Service に関連付けられた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでホストされます。  
  
 CDC データベースには特殊な cdc スキーマがあります。 Oracle CDC Service でこのスキーマを使用するときは、 **xdbcdc_** というプレフィックスを付けてテーブル名を指定します。 このスキーマは、セキュリティや一貫性を確保する目的で使用されます。  
  
 Oracle CDC インスタンスと CDC データベースはどちらも、Oracle CDC デザイナー コンソールを使用して作成されます。 CDC データベースの詳細については、Oracle CDC デザイナー コンソールのインストールに付属のドキュメントを参照してください。  
  
##  <a name="BKMK_CommandConfigCDC"></a> コマンド ラインを使用した CDC サービスの構成  
 コマンド ラインから Oracle CDC Service プログラム (xdbcdcsvc.exe) を実行することができます。 CDC のサービス プログラムは、32 ビットまたは 64 ビットのネイティブの Windows 実行可能ファイルです。  
  
 **参照**  
  
 [CDC Service のコマンド ライン インターフェイスを使用する方法](how-to-use-the-cdc-service-command-line-interface.md)  
  
### <a name="service-program-commands"></a>サービス プログラムのコマンド  
 ここでは、CDC サービスの構成に使用する次のコマンドについて説明します。  
  
-   [Config](#BKMK_config)  
  
-   [作成](#BKMK_create)  
  
-   [Del](#BKMK_delete)  
  
###  <a name="BKMK_config"></a> Config  
 `Config` は、Oracle CDC Service の構成をスクリプトで更新する場合に使用します。 このコマンドを使用すると、CDC サービスの構成の特定の部分だけを更新できます (たとえば、非対称キーのパスワードがわからない場合に接続文字列だけを更新するなど)。 このコマンドを実行できるのはコンピューターの管理者だけです。 `Config` コマンドの例を次に示します。  
  
```  
"<path>xdbcdcsvc.exe" config  
     <cdc-service-name>  
     [connect= <sql-server-connection-string>]  
     [key= <asym-key-password>]  
     [svcacct= <windows-account> <windows-password>]  
     [sqlacct= <sql-username> <sql-password>]  
  
```  
  
 各要素の説明は次のとおりです。  
  
 **cdc-service-name** には、更新する CDC サービスの名前を指定します。 これは必須パラメーターです。  
  
 **sql-server-connection-string** には、更新する接続文字列を指定します。 接続文字列にスペースや引用符が含まれる場合は、二重引用符 (") で囲む必要があります。 また、引用符を埋め込む場合は、引用符を 2 つ入力してエスケープします。  
  
 **asym-key-password** には、更新するパスワードを指定します。  
  
 **windows-account**と **windows-password** には、更新するサービスの Windows アカウント資格情報を指定します。  
  
 **sql-username**と **sql-password** には、更新する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証資格情報を指定します。 sqlacct のユーザー名とパスワードをどちらも指定しなかった場合は、Windows 認証を使用して Oracle CDC Service から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続されます。  
  
 **注**:スペースや二重引用符が含まれる場合は、パラメーターを二重引用符 (") で囲む必要があります。 また、二重引用符を埋め込む場合は、二重引用符を 2 つ入力する必要があります (たとえば、 **"A#B" D** というパスワードを使用する場合は **""A#B"" D"** と入力します)。  
  
###  <a name="BKMK_create"></a> 作成  
 `Create` は、Oracle CDC Service をスクリプトで作成する場合に使用します。 このコマンドを実行できるのはコンピューターの管理者だけです。 `Create` コマンドの例を次に示します。  
  
```  
"<path>xdbcdcsvc.exe" create  
     <cdc-service-name>  
     [connect= "<sql-server-connection-string>"]  
     [key= <asym-key-password>]  
     [svcacct <windows-account> <windows-password>]  
     [sqlacct <sql-username> <sql-password>]  
```  
  
 各要素の説明は次のとおりです。  
  
 **cdc-service-name** には、新しく作成するサービスの名前を指定します。 この名前のサービスが既にある場合、プログラムからエラーが返されます。 長い名前やスペースを含む名前は使用しないでください。 文字 "/" および "\\" は、サービス名には使用できません。 これは必須パラメーターです。  
  
 **sql-server-connection-string** には、新しい Oracle CDC Service に関連付けられる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続に使用する接続文字列を指定します。  
  
 **asym-key-password** には、ソース データベース ログ マイニングの資格情報を格納するための非対称キーを保護するパスワードを指定します。  
  
 **windows-account**と **windows-password** には、作成する Oracle CDC Service に関連付けられるアカウント名とパスワードを指定します。  
  
 **sql-username**と **sql-password** には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続に使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアカウント名とパスワードを指定します。 これらのどちらのパラメーターも指定しなかった場合は、Windows 認証を使用して CDC Service for Oracle から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続されます。  
  
 **注**:スペースや二重引用符が含まれる場合は、パラメーターを二重引用符 (") で囲む必要があります。 また、二重引用符を埋め込む場合は、二重引用符を 2 つ入力する必要があります (たとえば、 **"A#B" D** というパスワードを使用する場合は **""A#B"" D"** と入力します)。  
  
###  <a name="BKMK_delete"></a> Del  
 `Delete` は、Oracle CDC Service をスクリプトで完全に削除する場合に使用します。 このコマンドを実行できるのはコンピューターの管理者だけです。 `Delete` コマンドの例を次に示します。  
  
```  
"<path>xdbcdcsvc.exe" delete  
    <cdc-service-name>  
  
```  
  
 各要素の説明は次のとおりです。  
  
 **cdc-service-name** には、削除する CDC サービスの名前を指定します。  
  
 **注**:スペースや二重引用符が含まれる場合は、パラメーターを二重引用符 (") で囲む必要があります。 また、二重引用符を埋め込む場合は、二重引用符を 2 つ入力する必要があります (たとえば、 **"A#B" D** というパスワードを使用する場合は **""A#B"" D"** と入力します)。  
  
## <a name="see-also"></a>関連項目  
 [CDC Service のコマンド ライン インターフェイスを使用する方法](how-to-use-the-cdc-service-command-line-interface.md)   
 [CDC 用に SQL Server を準備する方法](prepare-sql-server-for-cdc.md)  
