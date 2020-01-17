---
title: DAC パッケージの検証 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data-tier application [SQL Server], validate
- data-tier application [SQL Server], compare
- validate DAC
- compare DACs
- data-tier application [SQL Server], view
- view DAC
ms.assetid: 726ffcc2-9221-424a-8477-99e3f85f03bd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56655f7d75635668d266b44853fc29969fd741ed
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782669"
---
# <a name="validate-a-dac-package"></a>DAC パッケージの検証
  DAC パッケージを運用環境に配置する前にパッケージの内容を確認し、既存の DAC をアップグレードする前にアップグレード処理を検証するようにしてください。 これは、特に、外部で開発されたパッケージを配置する場合に当てはまります。  
  
1.  **Before you begin:**  [Prerequisites](#Prerequisites)  
  
2.  **DAC のアップグレード:**  [DAC の内容の表示](#ViewDACContents)、 [データベースの変更の表示](#ViewDBChanges)、 [アップグレード処理の表示](#ViewUpgradeActions)、 [DAC の比較](#CompareDACs)  
  
##  <a name="Prerequisites"></a> の前提条件  
 ソースが不明または信頼されていない DAC パッケージは配置しないことをお勧めします。 こうした DAC には、意図しない [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを実行したり、スキーマを変更してエラーを発生させるような、悪意のあるコードが含まれている可能性があります。 DAC のソースが不明または信頼されていない場合は、使用する前に、[!INCLUDE[ssDE](../../includes/ssde-md.md)]の隔離されたテスト インスタンスに DAC を配置し、データベースに対して [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) を実行してください。また、ストアド プロシージャやその他のユーザー定義コードなど、データベースのコードを確認してください。  
  
##  <a name="ViewDACContents"></a> DAC の内容の表示  
 データ層アプリケーション (DAC) パッケージの内容を表示する方法は 2 つあります。 1 つは、SQL Server 開発者ツールの DAC プロジェクトに DAC パッケージをインポートする方法です。 もう 1 つは、パッケージの内容をフォルダーにアンパックする方法です。  
  
 **SQL Server 開発者ツールでの DAC の表示**  
  
1.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
2.  **[SQL Server]** プロジェクト テンプレートを選択し、 **[名前]** 、 **[場所]** 、および **[ソリューション名]** を指定します。  
  
3.  **ソリューション エクスプローラー**でプロジェクト ノードを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[プロジェクトの設定]** タブの **[出力の種類]** セクションで **[データ層アプリケーション (.dacpac File)]** チェック ボックスをオンにし、プロパティ ダイアログ ボックスを閉じます。  
  
5.  **ソリューション エクスプローラー**でプロジェクト ノードを右クリックし、 **[データ層アプリケーションのインポート]** をクリックします。  
  
6.  **ソリューション エクスプローラー** を使用して、サーバーの選択ポリシーや配置前スクリプトと配置後スクリプトなど、DAC 内のすべてのファイルを開くことができます。  
  
7.  **スキーマ ビュー** を使用すると、スキーマ内のすべてのオブジェクトを確認できます。特に、関数やストアド プロシージャなどのオブジェクトのコードを確認します。  
  
 **フォルダーでの DAC の表示**  
  
-   「 [Unpack a DAC Package](unpack-a-dac-package.md)」での指示に従って、DAC パッケージをフォルダーにアンパックします。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトの内容を表示するには、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]クエリ エディターでスクリプトを開きます。  
  
-   テキスト ファイルの内容を表示するには、メモ帳などのツールを使用します。  
  
##  <a name="ViewDBChanges"></a> データベースの変更の表示  
 現在のバージョンの DAC を実稼働環境に配置した後で、関連付けられているデータベースが直接変更され、その変更内容が新しいバージョンの DAC で定義されているスキーマと矛盾する場合があります。 新しいバージョンの DAC にアップグレードする前に、そのような変更がデータベースに対して行われたかどうかを確認してください。  
  
 **ウィザードの使用によるデータベースの変更の表示**  
  
1.  現在配置されている DAC と、新しいバージョンの DAC を含む DAC パッケージを指定して、 **データ層アプリケーションのアップグレード** ウィザードを実行します。  
  
2.  **[変更の検出]** ページで、データベースに対する変更のレポートを確認します。  
  
3.  アップグレードを続行しない場合は、 **[キャンセル]** をクリックします。  
  
4.  ウィザードの使用方法については、「 [データ層アプリケーションのアップグレード](upgrade-a-data-tier-application.md)」を参照してください。  
  
### <a name="view-database-changes-by-using-powershell"></a>PowerShell の使用によるデータベースの変更の表示
  
1.  SMO サーバー オブジェクトを作成し、表示する DAC を含んだインスタンスに設定します。  
  
2.  `ServerConnection` オブジェクトを開いて、同じインスタンスに接続します。  
  
3.  DAC の名前を変数で指定します。  
  
4.  `GetDatabaseChanges()` メソッドを使用して `ChangeResults` オブジェクトを取得し、そのオブジェクトをテキスト ファイルにパイプして、新しいオブジェクト、削除したオブジェクト、および変更したオブジェクトを含む簡単なレポートを生成します。  
  
### <a name="view-database-changes-example-powershell"></a>データベースの変更の表示の例 (PowerShell)
  
 次の例は、MyApplicaiton という名前の配置された DAC で行われた、データベースのすべての変更のレポートを生成します。  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the change list and save to file.  
$dacChanges = $dacstore.GetDatabaseChanges($dacName) | Out-File -Filepath C:\DACScripts\MyApplicationChanges.txt  
```  
  
##  <a name="ViewUpgradeActions"></a> アップグレード処理の表示  
 DAC パッケージの新しいバージョンを使用して前の DAC パッケージから配置された DAC をアップグレードする前に、アップグレード中に実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを含むレポートを生成して、ステートメントを確認することができます。  
  
 **ウィザードの使用によるアップグレードの処理のレポート生成**  
  
1.  現在配置されている DAC と、新しいバージョンの DAC を含む DAC パッケージを指定して、 **データ層アプリケーションのアップグレード** ウィザードを実行します。  
  
2.  **[概要]** ページで、アップグレード処理のレポートを確認します。  
  
3.  アップグレードを続行しない場合は、 **[キャンセル]** をクリックします。  
  
4.  ウィザードの使用方法については、「 [データ層アプリケーションのアップグレード](upgrade-a-data-tier-application.md)」を参照してください。  
  
 **PowerShell の使用によるアップグレードの処理のレポート生成**  
  
1.  SMO サーバー オブジェクトを作成し、配置された DAC を含んだインスタンスに設定します。  
  
2.  `ServerConnection` オブジェクトを開いて、同じインスタンスに接続します。  
  
3.  `System.IO.File` を使用して、DAC パッケージ ファイルを読み込みます。  
  
4.  DAC の名前を変数で指定します。  
  
5.  `GetIncrementalUpgradeScript()` メソッドを使用して、アップグレードで実行される Transact-SQL ステートメントのリストを取得し、リストをテキスト ファイルにパイプします。  
  
6.  DAC パッケージ ファイルの読み取りに使用するファイル ストリームを閉じます。  
  
### <a name="view-upgrade-actions-example-powershell"></a>アップグレード処理の表示の例 (PowerShell)
  
 次の例は、MyApplicaiton という名前の DAC を MyApplicationVNext.dacpac ファイルで定義されているスキーマにアップグレードするために実行される Transact-SQL ステートメントのレポートを生成します。  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplicationVNext.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the upgrade script and save to file.  
$dacstore.GetIncrementalUpgradeScript($dacName, $dacType) | Out-File -Filepath C:\DACScripts\MyApplicationUpgrade.sql  
  
## Close the filestream to the new DAC package.  
$fileStream.Close()  
```  
  
##  <a name="CompareDACs"></a> Compare DACs  
 DAC をアップグレードする前に、現在の DAC と新しい DAC に、データベースレベルおよびインスタンスレベルでオブジェクトにどんな相違があるか確認してください。 現在の DAC パッケージのコピーがない場合は、現在のデータベースからパッケージを抽出できます。  
  
 SQL Server 開発者ツールで両方の DAC パッケージを DAC プロジェクトにインポートする場合は、スキーマ比較ツールを使用して 2 つの DAC 間の相違を分析できます。  
  
 または、DAC を別々のフォルダーにアンパックします。 その後、WinDiff ユーティリティなどの比較ツールを使用して、相違を分析できます。  
  
## <a name="see-also"></a>参照  
 [データ層アプリケーション](data-tier-applications.md)   
 [データ層アプリケーションの配置](deploy-a-data-tier-application.md)   
 [データ層アプリケーションのアップグレード](upgrade-a-data-tier-application.md)  
