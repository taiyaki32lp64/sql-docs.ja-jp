---
title: Data Quality Server のインストールを完了するには、DQSInstaller を実行します
description: DQSInstaller を実行して SQL Server Data Quality Services (DQS) のインストールを完了する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7a8c96e0-1328-4f35-97fc-b6d9cb808bae
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 19805b5c5d41b5b39217c88cf565d9bd64c1ed9c
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558001"
---
# <a name="run-dqsinstallerexe-to-complete-data-quality-server-installation"></a>Data Quality Server のインストールを完了するための DQSInstaller.exe の実行

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] のインストールを完了するには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインストールを完了した後で、DQSInstaller.exe ファイルを実行する必要があります。 このトピックでは、 **[スタート]** 画面、 **[スタート]** メニュー、Windows エクスプローラー、またはコマンド プロンプトから DQSInstaller.exe を実行する方法について説明します。DQSInstaller.exe ファイルの実行には、これらの方法のいずれも使用できます。  
  
##  <a name="Prerequisites"></a>応募  
  
-   SQL Server のインストール時に SQL Server セットアップの [機能の選択] ページで **[データベース エンジン サービス]** の **[Data Quality Services]** が選択されていること、および SQL Server のインストールが完了していることが必要です。 詳細については、「 [Data Quality Services のインストール](../../data-quality-services/install-windows/install-data-quality-services.md)」を参照してください。  
  
-   Windows ユーザー アカウントが、SQL Server データベース エンジン インスタンスの sysadmin 固定サーバー ロールのメンバーであることが必要です。  
  
-   DQSInstaller.exe を実行中に、コンピューターの Administrators グループのメンバーとしてログオンする必要があります。  
  
##  <a name="WindowsExplorer"></a>[スタート] 画面、[スタート] メニュー、または Windows エクスプローラーから、DQSInstaller を実行します。  
  
1.  
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]をインストールするコンピューターで、次のうち適切ないずれかを使用して DQSInstaller.exe ファイルを実行します。  
  
    -   **スタート画面**: [**スタート**] 画面で、[ **Data Quality Server Installer** ] をクリックします。  
  
    -   **スタートメニュー**: タスクバーの [**スタート**] ボタンをクリックし、[すべて[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]の**プログラム**] をポイントし、[] をクリックします。 
  [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]で、 **[Data Quality Services]** をクリックし、 **[Data Quality Server Installer]** をクリックします。  
  
    -   **エクスプローラー**: DQSInstaller ファイルを見つけます。 SQL Server の既定のインスタンスをインストールした場合、DQSinstaller.exe ファイルは C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn に格納されます。 DQSInstaller.exe ファイルをダブルクリックします。  
  
2.  インストールの状態を表示するコマンド プロンプト ウィンドウが表示されます。 次の 3 つのことが確認できます。  
  
    1.  DQSInstaller.exe ファイルの実行時に行われた操作に関する情報を格納するインストール ログ ファイル DQS_install.log が作成されます。 SQL Server の既定のインスタンスをインストールした場合、DQS_install.log ファイルは C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log に格納されます。  
  
    2.  インストーラーは、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]のインストールに、既定のサーバー照合順序 (SQL_Latin1_General_CP1_CI_AS) を使用します。  
  
        > [!IMPORTANT]  
        >  
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] のインストール用に異なるサーバー照合順序値を指定できるのは、DQSInstaller.exe をコマンド ラインから実行する場合だけです。 詳細については、このトピックの「 [コマンド プロンプトから DQSInstaller.exe を実行する](#CommandPrompt) 」を参照してください。  
  
    3.  インストーラーは、コンピューターに最近インストールされた更新プログラムに起因する、保留中の再起動がないかどうかをチェックします。 保留中の再起動が見つかった場合は、そのことを通知するメッセージが表示されます。その場合は、インストールを続行するか中止するかを、Y または N を押すことで選択できます。 保留中の再起動がある場合は、インストールを中止し、コンピューターを再起動したうえで、DQSInstaller.exe を再度実行することをお勧めします。  
  
3.  データベース マスター キーのパスワードの入力を求めるメッセージが表示されます。 後で [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) に参照データ プロバイダーを設定するときに DQS_MAIN データベースに保存される参照データ サービス プロバイダー キーを暗号化するには、データベース マスター キーが必要です。  
  
    > [!IMPORTANT]  
    >  パスワードは8文字以上である必要があり、次の4つのカテゴリのうちの3つのカテゴリの文字を含める必要があります。英語の大文字 (A、B、C,...Z)、英語の小文字 (a、b、c,...z)、数字 (0、1、2,...9) と英数字以外の特殊文字 (~! @ # $% ^& * () _-+ = |\\{}[]:;"'<>,.?/). (例: P@ssword)。 現在のパスワードがこの要件を満たしていない場合は、別のパスワードの入力を求めるメッセージが表示されます。  
  
4.  パスワードを入力し、さらに確認のためにもう一度そのパスワードを入力してから、Enter キーを押してインストールを続行します。  
  
    > [!IMPORTANT]  
    >  データベース マスター キーに指定したパスワードは、後でバックアップから DQS データベースを復元するときに必要になるため、保管する必要があります。 DQS データベースの復元の詳細については、「 [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)」を参照してください。  
  
5.  マスター データ サービス データベースが [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]と同じ SQL Server インスタンス上に存在する場合は、マスター データ サービス ログインにマップされたユーザーが作成され、DQS_MAIN データベースに対する dqs_administrator ロールが付与されます。 マスター データ サービスのインストールとマスター データ サービス データベースの作成については、「 [Install Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)」を参照してください。  
  
6.  インストールが正常に完了すると、完了のメッセージが表示されます。 任意のキーを押してコマンド プロンプト ウィンドウを閉じます。  
  
##  <a name="CommandPrompt"></a>コマンドプロンプトからの DQSInstaller の実行  
 DQSInstaller.exe をコマンド プロンプトから実行する場合は、次のコマンド ライン パラメーターを使用します。  
  
|DQSInstaller.exe のパラメーター|説明|サンプル構文|  
|--------------------------------|-----------------|-------------------|  
|-collation|
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]のインストールに使用するサーバー照合順序。<br /><br /> DQS は、大文字と小文字を区別しない照合順序のみをサポートします。 大文字と小文字が区別される照合順序を指定した場合、インストーラーは、指定された照合順序の大文字と小文字を区別しないバージョンを使用して処理を実行しようとします。 大文字と小文字を区別しないバージョンが存在しない場合や、照合順序が SQL によってサポートされていない場合、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] のインストールは失敗します。<br /><br /> サーバーの照合順序を指定しなかった場合は、既定の照合順序 (SQL_Latin1_General_CP1_CI_AS) が使用されます。|`dqsinstaller.exe -collation <collation_name>`|  
|-upgradedlls|DQS データベース (DQS_MAIN、DQS_PROJECTS、および DQS_STAGING_DATA) の再作成をスキップし、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] データベースで DQS によって使用される SQL 共通言語ランタイム アセンブリ (SQLCLR) の更新のみを行います。<br /><br /> 詳細については、「 [.NET Framework 更新後の SQLCLR アセンブリのアップグレード](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)」を参照してください。|`dqsinstaller.exe -upgradedlls`|  
|-exportkbs|すべてのナレッジ ベースを DQS バックアップ ファイル (.dqsb) にエクスポートします。 また、エクスポート先の完全なパスとファイル名を指定する必要があります。<br /><br /> 詳細については、「 [DQSInstaller.exe を使用した DQS ナレッジ ベースのエクスポートとインポート](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)」を参照してください。|`dqsinstaller.exe -exportkbs <path><filename>`<br /><br /> たとえば、`dqsinstaller.exe -exportkbs c:\DQSBackup.dqsb` のように指定します。|  
|-importkbs|
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] のインストールが完了した後にすべてのナレッジ ベースを DQS バックアップ ファイル (.dqsb) からインポートします。 また、インポート元の完全なパスとファイル名を指定する必要があります。<br /><br /> 詳細については、「 [DQSInstaller.exe を使用した DQS ナレッジ ベースのエクスポートとインポート](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)」を参照してください。|`dqsinstaller.exe -importkbs <path><filename>`<br /><br /> たとえば、`dqsinstaller.exe -importkbs c:\DQSBackup.dqsb` のように指定します。|  
|-upgrade|DQS データベース スキーマをアップグレードします。 あらかじめ構成された DQS インスタンスに SQL Server 更新プログラムをインストールした後に、このパラメーターを使用する必要があります。 詳細については、「 [SQL Server 更新プログラムのインストール後の DQS データベース スキーマのアップグレード](../../data-quality-services/install-windows/upgrade-dqs-databases-schema-after-installing-sql-server-update.md)」を参照してください。|`dqsinstaller.exe -upgrade`|  
|-uninstall|
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] を現在の SQL Server インスタンスからアンインストールします。<br /><br /> また、Data Quality Server の既存のインストールに含まれるすべてのナレッジ ベースを DQS バックアップ ファイル (.dqsb) にエクスポートしてから、Data Quality Server をアンインストールすることもできます。 詳細については、「 [DQSInstaller.exe を使用した DQS ナレッジ ベースのエクスポートとインポート](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)」を参照してください。<br /><br /> ** \*重要\* \* **コマンドラインパラメーター [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]を使用して SQL server インスタンスからをアンインストールすると、すべての DQS オブジェクトがアンインストールプロセスの一部として削除されます。 `-uninstall` 「 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] Data Quality Server オブジェクトの削除 [」でも述べているように、](../../sql-server/install/remove-data-quality-server-objects.md)のアンインストール後に手動でそれらを削除する必要はありません。|**Data Quality Server をアンインストールするだけの場合:**<br /><br /> `dqsinstaller.exe -uninstall`<br /><br /> **すべてのナレッジベースをファイルにエクスポートしてから、Data Quality Server をアンインストールするには、次のようにします。**<br /><br /> `dqsinstaller.exe -uninstall <path><filename>`<br /><br /> たとえば、`dqsinstaller.exe -uninstall c:\DQSBackup.dqsb` のように指定します。|  
  
 **コマンドプロンプトから DQSInstaller を実行するには、次のようにします。**  
  
1.  コマンド プロンプトを起動します。  
  
2.  コマンド プロンプトで、DQSInstaller.exe が格納されている場所にディレクトリを変更します。 SQL Server の既定のインスタンスをインストールした場合、DQSinstaller.exe ファイルは C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn に格納されます。  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  コマンド プロンプトで、DQSInstaller.exe を実行します。コマンド ライン パラメーターは必要に応じて使用します。  
  
    -   **コマンドラインパラメーターを指定**しない`dqsinstaller.exe`場合: 「」と入力し、enter キーを押します。  
  
    -   **コマンドラインパラメーターを使用**して、上の表に記載されている必要なコマンドを入力し、enter キーを押します。  
  
4.  指定したコマンドに基づいて、必要なアクションが実行されます。 コマンド ライン パラメーターを使用せずに [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] をインストールした場合、残りの手順は、前のセクション (「 [[スタート] 画面、[スタート] メニュー、または Windows エクスプローラーから DQSInstaller.exe を実行する](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer)」) の手順 2. ～ 6. と同じです。  
  
## <a name="next-steps"></a>次の手順  
  
-   作業プロファイルに基づき適切な DQS ロールをユーザーに付与します。 「 [ユーザーに DQS ロールを付与する](../../data-quality-services/install-windows/grant-dqs-roles-to-users.md)」を参照してください。  
  
-   
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] が [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]からリモートでアクセスされる場合は、このコンピューターで SQL Server 構成マネージャーを使用して TCP/IP プロトコルを有効にしてください。  
  
-   ソース データにアクセスして DQS 操作を実行できることと、処理後のデータをデータベース内のテーブルにエクスポートできることを確認します。 「 [DQS 操作のためのデータへのアクセス](../../data-quality-services/install-windows/access-data-for-the-dqs-operations.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Data Quality Services のインストール](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [.NET Framework の更新後に SQLCLR アセンブリをアップグレードする](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)   
 [DQSInstaller を使用した DQS ナレッジベースのエクスポートとインポート](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)  
  
  
