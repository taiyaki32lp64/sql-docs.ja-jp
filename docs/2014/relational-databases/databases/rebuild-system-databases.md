---
title: システム データベースの再構築 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], rebuilding
- REBUILDDATABASE parameter
- rebuilding databases, master
- system databases [SQL Server], rebuilding
ms.assetid: af457ecd-523e-4809-9652-bdf2e81bd876
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b58378e8ba2193a186fb58e3e784bf9bc3cb4d4c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871279"
---
# <a name="rebuild-system-databases"></a>システム データベースの再構築
  [master](master-database.md)、 [model](model-database.md)、 [msdb](msdb-database.md)、または [resource](resource-database.md) の各システム データベースの損傷による問題を解決するか、既定のサーバー レベルの照合順序を変更するには、システム データベースを再構築する必要があります。 このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]でシステム データベースを再構築する手順について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [前提条件](#Prerequisites)  
  
-   **手順:**  
  
     [システム データベースの再構築](#RebuildProcedure)  
  
     [resource データベースの再構築](#Resource)  
  
     [新しい msdb データベースの作成](#CreateMSDB)  
  
-   **補足情報:**  
  
     [再構築エラーのトラブルシューティング](#Troubleshoot)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 master、model、msdb、および tempdb の各システム データベースを再構築する場合は、元の場所からデータベースを削除して再作成する必要があります。 再構築ステートメントに新しい照合順序を指定する場合は、その照合順序の設定でシステム データベースが作成されます。 これらのデータベースに対するユーザーの変更はすべて失われます。 たとえば、master データベースのユーザー定義オブジェクト、msdb にスケジュールされたジョブ、または model データベースの既定のデータベース設定に対する変更が対象になります。  
  
###  <a name="Prerequisites"></a> 前提条件  
 システム データベースを再構築する前に次の作業を行い、システム データベースを現在の設定に復元できるようにしておいてください。  
  
1.  サーバー全体のすべての構成値を記録します。  
  
    ```  
    SELECT * FROM sys.configurations;  
    ```  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および現在の照合順序のインスタンスに適用されているすべてのサービス パックと修正プログラムを記録します。 システム データベースの再構築後にこれらの更新を再適用する必要があります。  
  
    ```  
    SELECT  
    SERVERPROPERTY('ProductVersion ') AS ProductVersion,  
    SERVERPROPERTY('ProductLevel') AS ProductLevel,  
    SERVERPROPERTY('ResourceVersion') AS ResourceVersion,  
    SERVERPROPERTY('ResourceLastUpdateDateTime') AS ResourceLastUpdateDateTime,  
    SERVERPROPERTY('Collation') AS Collation;  
    ```  
  
3.  システム データベースのすべてのデータとログ ファイルの現在の場所を記録します。 システム データベースを再構築すると、すべてのシステム データベースがそれぞれ元の場所にインストールされます。 システム データベースのデータまたはログ ファイルを別の場所に移動していた場合は、そのファイルを再度移動する必要があります。  
  
    ```  
    SELECT name, physical_name AS current_file_location  
    FROM sys.master_files  
    WHERE database_id IN (DB_ID('master'), DB_ID('model'), DB_ID('msdb'), DB_ID('tempdb'));  
    ```  
  
4.  master、model、および msdb の各データベースの現在のバックアップを探します。  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがレプリケーション ディストリビューターとして構成されている場合は、ディストリビューション データベースの現在のバックアップを探します。  
  
6.  システム データベースの再構築に必要な権限を持っていることを確認してください。 この操作を実行するには、`sysadmin` 固定サーバー ロールのメンバーである必要があります。 詳細については、「 [サーバー レベルのロール](../security/authentication-access/server-level-roles.md)」を参照してください。  
  
7.  master、model、msdb のデータおよびログのテンプレート ファイルのコピーがローカル サーバーに存在することを確認します。 テンプレート ファイルの既定の場所は、C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Templates です。 これらのファイルは再構築プロセスで使用され、セットアップを成功させるにはこれらのファイルが存在する必要があります。 これらのファイルがない場合は、セットアップの修復機能を実行するか、インストール メディアからファイルを手動でコピーします。 インストール メディアのファイルを探すには、適切なプラットフォーム ディレクトリ (x86 または x64) に移動し、次に setup\sql_engine_core_inst_msi\Pfiles\SqlServr\MSSQL.X\MSSQL\Binn\Templates に移動します。  
  
##  <a name="RebuildProcedure"></a> システム データベースの再構築  
 次の手順では、master、model、msdb、および tempdb の各システム データベースを再構築します。 再構築するシステム データベースを指定することはできません。 クラスター化されたインスタンスの場合、この手順はアクティブ ノードで実行する必要があります。また、手順を実行する前に、対応するクラスター アプリケーション グループ内の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースをオフラインにしておく必要があります。  
  
 この手順では resource データベースが再構築されません。 このトピックで後述する「resource データベースの再構築手順」セクションを参照してください。  
  
#### <a name="to-rebuild-system-databases-for-an-instance-of-sql-server"></a>SQL Server のインスタンスのシステム データベースを再構築するには  
  
1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストール メディアをディスク ドライブに挿入するか、コマンド プロンプトから、ディレクトリをローカル サーバーの setup.exe ファイルがある場所に変更します。 サーバーの既定の場所は C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Release です。  
  
2.  コマンド プロンプト ウィンドウから、次のコマンドを入力します。 角かっこは省略可能なパラメーターであることを示します。 角かっこは入力しません。 ユーザー アカウント制御 (UAC) が有効な Windows オペレーション システムを使用する場合は、セットアップの実行に高度な特権が必要になります。 管理者としてコマンド プロンプトを実行する必要があります。  
  
     `Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName /SQLSYSADMINACCOUNTS=accounts [ /SAPWD= StrongPassword ] [ /SQLCOLLATION=CollationName]`  
  
    |[パラメーター名]|説明|  
    |--------------------|-----------------|  
    |/QUIET または /Q|セットアップがユーザー インターフェイスなしで実行されるように指定します。|  
    |/ACTION=REBUILDDATABASE|セットアップでシステム データベースを再作成することを指定します。|  
    |/INSTANCENAME=*InstanceName*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの名前を指定します。 既定のインスタンスには「MSSQLSERVER」と入力します。|  
    |/SQLSYSADMINACCOUNTS=*accounts*|`sysadmin` 固定サーバー ロールに追加する Windows グループまたは個々のアカウントを指定します。 複数のアカウントを指定する場合、各アカウントを空白で区切ります。 たとえば、「 **BUILTIN\Administrators MyDomain\MyUser**」と入力します。 アカウント名に空白を含むアカウントを指定する場合は、アカウントを二重引用符で囲みます。 たとえば、`NT AUTHORITY\SYSTEM` と入力します。|  
    |[ /SAPWD=*StrongPassword* ]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sa` アカウントのパスワードを指定します。 このパラメーターは、インスタンスが混合モード認証 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および Windows 認証) を使用する場合に必要になります。<br /><br /> **\*\* セキュリティに関する注意\* \***  、`sa`アカウントはよく知られている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]アカウントで、多くの場合、悪意のあるユーザーを対象とします。 `sa` ログインには、複雑なパスワードを使用することが非常に重要です。<br /><br /> Windows 認証モードにはこのパラメーターを指定しないでください。|  
    |[ /SQLCOLLATION=*CollationName* ]|新しいサーバー レベルの照合順序を指定します。 このパラメーターはオプションです。 これを指定しない場合は、サーバーの現在の照合順序が使用されます。<br /><br /> **\*\* 重要 \*\*** サーバー レベルの照合順序を変更しても、既存のユーザー データベースの照合順序は変更されません。 新しく作成されたすべてのユーザー データベースには、既定で新しい照合順序が使用されます。<br /><br /> 詳細については、「 [サーバーの照合順序の設定または変更](../collations/set-or-change-the-server-collation.md)」を参照してください。|  
  
3.  セットアップによりシステム データベースの再構築が完了すると、メッセージが表示されることなく、コマンド プロンプトに戻ります。 Summary.txt ログ ファイルを調査し、プロセスが正常に完了したことを確認します。 このファイルは C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Logs にあります。  
  
## <a name="post-rebuild-tasks"></a>再構築後の作業  
 データベースを再構築した後は、次の追加作業の実行が必要になる場合があります。  
  
-   master、model、および msdb の各データベースを最新の完全バックアップの状態に復元します。 詳細については、「[システム データベースのバックアップと復元 &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  サーバー照合順序を変更した場合は、システム データベースを復元しないでください。 復元すると、新しい照合順序が元の照合順序の設定に置き換わります。  
  
     バックアップが存在しないか、復元されたバックアップが最新のものでない場合は、存在しないエントリを再作成します。 たとえば、ユーザー データベース、バックアップ デバイス、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン、エンドポイントなどの存在しないエントリをすべて再作成します。 エントリを再作成する場合、エントリの作成時と同じスクリプトを実行してください。  
  
> [!IMPORTANT]  
>  不正ユーザーによる変更を防ぐために、スクリプトを保護しておくことをお勧めします。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがレプリケーション ディストリビューターとして構成されている場合は、ディストリビューション データベースを復元する必要があります。 詳細については、「 [レプリケートされたデータベースのバックアップと復元](../replication/administration/back-up-and-restore-replicated-databases.md)」を参照してください。  
  
-   システム データベースを記録した以前の場所に移動します。 詳細については、「 [システム データベースの移動](system-databases.md)」を参照してください。  
  
-   サーバー全体の構成値が記録した以前の値と一致することを確認します。  
  
##  <a name="Resource"></a> resource データベースの再構築  
 次の手順では、resource システム データベースを再構築します。 resource システム データベースを再構築する場合は、サービス パックと修正プログラムがすべて失われるため、再適用する必要があります。  
  
#### <a name="to-rebuild-the-resource-system-database"></a>resource システム データベースを再構築するには  
  
1.  配布メディアから、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップ プログラム (setup.exe) を起動します。  
  
2.  左側のナビゲーション領域の **[メンテナンス]** をクリックし、 **[修復]** をクリックします。  
  
3.  セットアップ サポート ルールおよびセットアップ サポート ファイルのルーチンが実行されて、システムに必須コンポーネントがインストールされていること、およびコンピューターがセットアップの検証ルールに合格していることが確認されます。 続行するには、 **[OK]** または **[インストール]** をクリックします。  
  
4.  [インスタンスの選択] ページで、修復するインスタンスを選択し、 **[次へ]** をクリックします。  
  
5.  修復ルールが実行され、操作が検証されます。 続行するには、 **[次へ]** をクリックします。  
  
6.  **[修復の準備完了]** ページで **[修復]** をクリックします。 [完了] ページでは、操作が完了したことが示されます。  
  
##  <a name="CreateMSDB"></a> 新しい msdb データベースの作成  
 場合、`msdb`データベースが破損しているしのバックアップがない、 `msdb` 、データベースを作成、新しい`msdb`を使用して、 **instmsdb**スクリプト。  
  
> [!WARNING]  
>  再構築、`msdb`データベースを使用して、 **instmsdb**スクリプトが格納されたすべての情報を排除`msdb`など、ジョブ、警告、オペレーター、メンテナンス プラン、バックアップ履歴、ポリシー ベースの管理設定、データベース メール、パフォーマンス データ ウェアハウス、など。  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]エージェント、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、および [!INCLUDE[ssRS](../../includes/ssrs.md)]と、 [!INCLUDE[ssIS](../../includes/ssis-md.md)]をデータ ストアとして使用しているすべてのアプリケーションを含め、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続しているすべてのサービスを停止します。  
  
2.  というコマンドを使用して、コマンド ラインから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を開始します。 `NET START MSSQLSERVER /T3608`  
  
     詳細については、「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md) 」を参照してください。  
  
3.  別のコマンド ライン ウィンドウでは、デタッチ、`msdb`次のコマンドを実行してデータベースを交換 *\<servername >* のインスタンスと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: `SQLCMD -E -S<servername> -dmaster -Q"EXEC sp_detach_db msdb"`  
  
4.  Windows エクスプ ローラーを使用して名前を変更、`msdb`データベース ファイル。 これらのファイルは、既定で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの DATA サブフォルダーにあります。  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスを通常の方法で停止および再起動します。  
  
6.  コマンド ライン ウィンドウで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、コマンド `SQLCMD -E -S<servername> -i"C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.sql" -o" C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.out"`  
  
     *<servername\<* は [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに置き換えます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスのファイル システム パスを使用してください。  
  
7.  Windows のメモ帳を使用して **instmsdb.out** ファイルを開き、エラーの出力を確認します。  
  
8.  インスタンスにインストールされていたサービス パックまたは修正プログラムがあれば、再適用します。  
  
9. 格納されているユーザーのコンテンツを再作成、`msdb`ジョブや警告など、データベースなどです。  
  
10. バックアップ、`msdb`データベース。  
  
##  <a name="Troubleshoot"></a> 再構築エラーのトラブルシューティング  
 コマンド プロンプト ウィンドウには、構文エラーおよびその他の実行時エラーが表示されます。 セットアップ ステートメントに次の構文エラーがないか調査してください。  
  
-   パラメーター名の前のスラッシュ記号 (/) の欠如。  
  
-   パラメーター名とパラメーター値の間の等号 (=) の欠如。  
  
-   パラメーター名と等号の間の空白文字の存在。  
  
-   構文に指定されていないコンマ (,) またはその他の文字の存在。  
  
 再構築操作が完了した後で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログにエラーがないか調査します。 ログの既定の場所は C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Logs です。 再構築プロセスの結果を含むログ ファイルを探すには、ディレクトリをコマンド プロンプトから Logs フォルダーに変更し、 `findstr /s RebuildDatabase summary*.*`を実行します。 この検索により、システム データベースの再構築結果を含むログ ファイルが検出されます。 ログ ファイルを開き、該当するエラー メッセージがないか調査します。  
  
## <a name="see-also"></a>参照  
 [システム データベース](system-databases.md)  
  
  
