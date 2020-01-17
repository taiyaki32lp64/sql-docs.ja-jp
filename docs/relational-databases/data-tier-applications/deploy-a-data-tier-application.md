---
title: データ層アプリケーションの配置 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.deploydacwizard.introduction.f1
- sql13.swb.deploydacwizard.deploydac.f1
- sql13.swb.deploydacwizard.summary.f1
- sql13.swb.deploydacwizard.updateconfiguration.f1
- sql13.swb.deploydacwizard.selectdac.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 842a6519c1493162d06c853f11a9494d8dc3ca5b
ms.sourcegitcommit: ba44730f5cc33295ae2ed1f281186dd266bad4ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74190118"
---
# <a name="deploy-a-data-tier-application"></a>データ層アプリケーションの配置
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  ウィザードまたは PowerShell スクリプトを使用して、データ層アプリケーション (DAC) パッケージからデータベース エンジンまたは Azure SQL Database の既存のインスタンスに DAC を配置できます。 
  
 配置プロセスでは、**msdb** システム データベース ([!INCLUDE[ssSDS](../../includes/sssds-md.md)] では **master** データベース) に DAC 定義を格納することで DAC インスタンスを登録し、データベースを作成して、DAC で定義されたすべてのデータベース オブジェクトをそのデータベースに設定します。  
 
  
## <a name="deploy-the-same-dac-package-multiple-times"></a>同じ DAC パッケージを複数回配置する 
 同じ DAC パッケージを [!INCLUDE[ssDE](../../includes/ssde-md.md)] の単一のインスタンスに複数回配置することはできますが、配置は一度に 1 つずつ実行する必要があります。 各配置に指定される DAC インスタンス名は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンス内で一意である必要があります。  
  
 データベース エンジンのインスタンスに DAC を配置した場合、その配置した DAC は、次回ユーティリティ コレクション セットがインスタンスからユーティリティ コントロール ポイントへと送信されるときに **SQL Server ユーティリティ**に組み込まれます。 その後、DAC は [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の**ユーティリティ エクスプローラー**の **[配置済みのデータ層アプリケーション]** ノードに現れるようになり、 **[配置済みのデータ層アプリケーション]** の詳細ページで報告されます。  
  
###  <a name="database-options-and-settings"></a>データベースのオプションと設定  
 既定では、配置中に作成されたデータベースには、CREATE DATABASE ステートメントによる既定の設定すべてが適用されます。ただし、次の設定は除きます。  
  
-   データベースの照合順序および互換性レベルは、DAC パッケージで定義された値に設定されます。 SQL Server 開発者ツールでデータベース プロジェクトから構築された DAC パッケージでは、データベース プロジェクトに設定された値が使用されます。 既存のデータベースから抽出されたパッケージでは、元のデータベースの値が使用されます。  
  
-   一部のデータベース設定 (データベース名やファイル パスなど) は、 **[構成の更新]** ページで調整できます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に配置する場合、ファイル パスは設定できません。  
  
 TRUSTWORTHY、DB_CHAINING、HONOR_BROKER_PRIORITY など、データベース オプションによっては、配置作業中の調整はできない場合があります。 ファイル グループの数、ファイルの数やサイズなどの物理プロパティは、配置作業中に変更することはできません。 配置が完了すれば、ALTER DATABASE ステートメント、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell を使用して、データベースを調整できます。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 DAC を配置できるのは、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、または [!INCLUDE[ssDE](../../includes/ssde-md.md)] Service Pack 4 (SP4) 以降を実行している [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスです。 新しいバージョンを使用して DAC を作成した場合、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ではサポートされないオブジェクトが DAC に含まれている可能性があります。 このような DAC を [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のインスタンスに配置することはできません。  
    
## <a name="security-and-permissions"></a>セキュリティとアクセス許可
認証のログインは、パスワードなしで DAC パッケージに格納されます。 パッケージが配置またはアップグレードされると、ログインは、生成されたパスワードを伴う無効なログインとして作成されます。 ログインを有効にするには、ALTER ANY LOGIN 権限のあるログインでログインし、ALTER LOGIN を使用してログインを有効にします。さらに、新しいパスワードを割り当て、そのパスワードを該当ユーザーに通知します。 Windows 認証ログインの場合、ログインのパスワードは SQL Server で管理されていないため、この操作は必要ありません。  
  
 DAC を配置できるのは、**sysadmin** または **serveradmin** 固定サーバー ロールのメンバーか、**dbcreator** 固定サーバー ロールに存在する ALTER ANY LOGIN 権限を持つログインのみです。 あらかじめ登録された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者アカウント ( **sa** ) でも DAC を配置できます。 

[!INCLUDE[ssSDS](../../includes/sssds-md.md)] へのログインが含まれる DAC を配置するには、loginmanager ロールまたは serveradmin ロールのメンバーシップが必要です。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] へのログインが含まれない DAC を配置するには、dbmanager ロールまたは serveradmin ロールのメンバーシップが必要です。  
  
## <a name="deploy-a-dac-using-the-wizard"></a>ウィザードを使用して DAC を配置する  
  
1.  **オブジェクト エクスプローラー**で、DAC を配置するインスタンスのノードを展開します。  
  
2.  **[データベース]** ノードを右クリックし、 **[データ層アプリケーションの配置]** をクリックします。  
  
3.  ウィザードのダイアログを完了し、[完了] をクリックします。

以下は、ウィザード ページの詳細の一部です。 
     
### <a name="select-dac-package-page"></a>[DAC パッケージの選択] ページ  
 配置するデータ層アプリケーションを含む DAC パッケージを指定します。 このページは、3 つの状態を遷移します。  
    
### <a name="select-the-dac-package"></a>DAC パッケージの選択  
 配置する DAC パッケージを選択します。 DAC パッケージは有効な DAC パッケージ ファイルで、拡張子は .dacpac である必要があります。  
  
 **[DAC パッケージ]** : 配置するデータ層アプリケーションを含む DAC パッケージのパスとファイル名を指定します。 ボックスの右にある **[参照]** をクリックして、DAC パッケージの場所に移動することができます。  
  
 **[アプリケーション名]** : DAC が作成されたとき、またはデータベースから抽出されたときに割り当てられた DAC 名が表示される読み取り専用のボックスです。  
  
 **[バージョン]** : DAC が作成されたとき、またはデータベースから抽出されたときに割り当てられたバージョンが表示される読み取り専用のボックスです。  
  
 **[説明]** : DAC が作成されたとき、またはデータベースから抽出されたときに記述された説明が表示される読み取り専用のボックスです。  
  
### <a name="validating-the-dac-package"></a>DAC パッケージの検証  
 選択したファイルが有効な DAC パッケージかどうかが確認され、進捗状況バーが表示されます。 DAC パッケージが検証されると、 **[DAC パッケージの選択]** ページの最終状態に進み、検証の結果を確認できます。 ファイルが有効な DAC パッケージでない場合は、 **[DAC パッケージの選択]** が表示されたままになります。 別の有効な DAC パッケージを選択するか、ウィザードを取り消して新しい DAC パッケージを生成してください。  
  
  ### <a name="review-policy-page"></a>[ポリシーの確認] ページ  
 DAC にポリシーが含まれている場合に DAC サーバーの選択ポリシーを評価した結果を確認します。 DAC サーバーの選択ポリシーは、省略可能で、Visual Studio で DAC を作成するときに割り当てられます。 このポリシーでは、サーバーの選択ポリシーのファセットを使用して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスで DAC をホストするために満たす必要がある条件を指定します。  
  
 **[ポリシー条件の評価結果]** : DAC 配置ポリシーの条件が満たされたかどうかを示します。 各条件の評価結果が、レポートの各行に表示されます。  
  
 サーバーの選択ポリシー (オペレーティング システムのバージョン、言語、名前付きパイプの有効化、プラットフォーム、および TCP の有効化) は、DAC を [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に配置する場合は常に false となります。  
  
 **[ポリシー違反を無視します]** : ポリシー条件が満たされていない場合に配置を続行するには、このチェック ボックスを使用します。 すべての条件が満たされていなくても DAC を正常に操作できるようにする場合のみ、このチェック ボックスをオンにしてください。  
   
### <a name="update-configuration-page"></a>[構成の更新] ページ  
 配置された DAC インスタンスの名前と、配置によって作成されたデータベースの名前を指定し、データベース オプションを設定します。  
  
 **[データベース名]** : 配置によって作成されるデータベースの名前を指定します。 既定では、DAC の抽出元であるソース データベースの名前です。 この名前は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンス内で一意であり、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 識別子のルールに従っている必要があります。  
  
 データベース名を変更した場合、データ ファイルとログ ファイルの名前も新しいデータベース名に合わせて変更されます。  
  
 また、データベース名は、DAC インスタンスの名前としても使用されます。 インスタンス名は、 **オブジェクト エクスプローラー** の **[データ層アプリケーション]** ノードまたは **ユーティリティ エクスプローラー** の **[配置済みのデータ層アプリケーション]** ノードの下にある、DAC のノードに表示されます。  
  
 次のオプションは [!INCLUDE[ssSDS](../../includes/sssds-md.md)]には適用されず、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]の配置時には表示されません。  
  
 **[既定のデータベースの場所の使用]** : データベースのデータ ファイルおよびログ ファイルを [!INCLUDE[ssDE](../../includes/ssde-md.md)]インスタンスの既定の場所に作成するには、このオプションを選択します。 ファイル名は、データベース名を使用して作成されます。  
  
 **[データベース ファイルの指定]** : データ ファイルおよびログ ファイルに別の場所または名前を指定するには、このオプションを選択します。  
  
 **[データ ファイルのパスと名前]** : データ ファイルの完全パスとファイル名を指定します。 このボックスには、既定のパスとファイル名が表示されます。 ボックス内の文字列を編集して既定値を変更するか、[参照] をクリックしてデータ ファイルを配置するフォルダーに移動してください。  
  
 **[ログ ファイルのパスと名前]** : ログ ファイルの完全パスとファイル名を指定します。 このボックスには、既定のパスとファイル名が表示されます。 ボックス内の文字列を編集して既定値を変更するか、 **[参照]** をクリックしてログ ファイルを配置するフォルダーに移動してください。  
  
###  <a name="Summary"></a> [概要] ページ  
 このページでは、DAC の配置時にウィザードが行うアクションを確認します。  
  
 **[次の設定を使用して DAC を配置します。]** : 表示された情報を確認し、実行されるアクションが正しいかどうかを確認します。 このウィンドウには、選択した DAC パッケージと、配置される DAC インスタンス用に選択した名前が表示されます。 また、DAC に関連付けられたデータベースを作成する際に使用される設定も表示されます。  
   
### <a name="deploy-page"></a>[配置] ページ  
 このページには、配置操作の成功または失敗が表示されます。  
  
 **[DAC を配置しています]** : DAC を配置するために行った各アクションの成功または失敗が表示されます。 内容を確認して、各アクションの成功または失敗を判断します。 エラーが発生したアクションには、 **[結果]** 列にリンクが表示されます。 そのアクションのエラーのレポートを表示するには、リンクをクリックします。  
  
 **[レポートの保存]** : 配置レポートを HTML ファイルに保存します。 ファイルには、アクションで発生したすべてのエラーを含む、各アクションのステータスが報告されます。 既定のフォルダーは、Windows アカウントの Documents フォルダーにある SQL Server Management Studio\DAC Packages フォルダーです。  
  
  
##  <a name="using-powershell"></a>PowerShell の使用  
  
1.  SMO サーバー オブジェクトを作成し、DAC を配置するインスタンスに設定します。  
  
2.  **ServerConnection** オブジェクトを開いて、同じインスタンスに接続します。  
  
3.  **System.IO.File** を使用して、DAC パッケージ ファイルを読み込みます。  
  
4.  **add_DacActionStarted** と **add_DacActionFinished** を使用して、DAC 配置イベントをサブスクライブします。  
  
5.  **DatabaseDeploymentProperties**を設定します。  
  
6.  **DacStore.Install** メソッドを使用して、DAC を配置します。  
  
7.  DAC パッケージ ファイルの読み取りに使用するファイル ストリームを閉じます。  

次の例では、MyApplication.dacpac パッケージから DAC 定義を使用して、MyApplication という名前の DAC を [!INCLUDE[ssDE](../../includes/ssde-md.md)]の既定のインスタンスに配置します。  
  
## <a name="powershell-examples"></a>PowerShell の例  

次の例では、MyApplication.dacpac パッケージから DAC 定義を使用して、MyApplication という名前の DAC を [!INCLUDE[ssDE](../../includes/ssde-md.md)]の既定のインスタンスに配置します。  

```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$server = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverConnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($server.ConnectionContext.SqlConnectionObject)  
$serverConnection.Connect()  
$dacStore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverConnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacStore.add_DacActionStarted({Write-Host `n`nStarting at $(Get-Date) :: $_.Description})  
$dacStore.add_DacActionFinished({Write-Host Completed at $(Get-Date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverConnection,$dacName)  
$dacStore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## <a name="more-information"></a>詳細情報 
 [[データ層アプリケーション]](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [データベースからの DAC の抽出](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)   
 [データベース識別子](../../relational-databases/databases/database-identifiers.md)  
  
  
