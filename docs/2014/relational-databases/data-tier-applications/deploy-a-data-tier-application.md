---
title: データ層アプリケーションの配置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.deploydacwizard.updateconfiguration.f1
- sql12.swb.deploydacwizard.selectdac.f1
- sql12.swb.deploydacwizard.deploydac.f1
- sql12.swb.deploydacwizard.introduction.f1
- sql12.swb.deploydacwizard.summary.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 00208b1c0f11faf8f392e47e275c7e239249d3d6
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783068"
---
# <a name="deploy-a-data-tier-application"></a>データ層アプリケーションの配置
  ウィザードまたは PowerShell スクリプトを使用して、データ層アプリケーション (DAC) パッケージから[!INCLUDE[ssDE](../../includes/ssde-md.md)]または [!INCLUDE[ssSDS](../../includes/sssds-md.md)] の既存のインスタンスに DAC を配置できます。 配置プロセスでは、 **msdb** システム データベース (**では** master [!INCLUDE[ssSDS](../../includes/sssds-md.md)]データベース) に DAC 定義を格納することで DAC インスタンスを登録し、データベースを作成して、DAC で定義されたすべてのデータベース オブジェクトをそのデータベースに設定します。  
  
-   **作業を開始する準備:**  [SQL Server ユーティリティ](#SQLUtility)、 [データベースのオプションと設定](#DBOptSettings)、 [制限事項と制約事項](#LimitationsRestrictions)、 [前提条件](#Prerequisites)、 [セキュリティ](#Security)、 [権限](#Permissions)  
  
-   **DAC を配置するために使用するもの:**  [データ層アプリケーションの配置ウィザード](#UsingDeployDACWizard)、 [PowerShell](#DeployDACPowerShell)  
  
##  <a name="BeforeBegin"></a> はじめに  
 同じ DAC パッケージを [!INCLUDE[ssDE](../../includes/ssde-md.md)] の単一のインスタンスに複数回配置することはできますが、配置は一度に 1 つずつ実行する必要があります。 各配置に指定される DAC インスタンス名は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンス内で一意である必要があります。  
  
###  <a name="SQLUtility"></a>SQL Server ユーティリティ  
 データベース エンジンのマネージド インスタンスに DAC を配置した場合、その配置した DAC は、次回ユーティリティ コレクション セットがインスタンスからユーティリティ コントロール ポイントへと送信されるときに SQL Server ユーティリティに組み込まれます。 その後、DAC は、 **の** ユーティリティ エクスプローラー [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **[配置済みのデータ層アプリケーション]** ノードに表示され、 **の** 詳細ページで報告されます。  
  
###  <a name="DBOptSettings"></a> データベースのオプションと設定  
 既定では、配置中に作成されたデータベースには、CREATE DATABASE ステートメントによる既定の設定すべてが適用されます。ただし、次の設定は除きます。  
  
-   データベースの照合順序および互換性レベルは、DAC パッケージで定義された値に設定されます。 SQL Server 開発者ツールでデータベース プロジェクトから構築された DAC パッケージでは、データベース プロジェクトに設定された値が使用されます。 既存のデータベースから抽出されたパッケージでは、元のデータベースの値が使用されます。  
  
-   一部のデータベース設定 (データベース名やファイル パスなど) は、 **[構成の更新]** ページで調整できます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に配置する場合、ファイル パスは設定できません。  
  
 TRUSTWORTHY、DB_CHAINING、HONOR_BROKER_PRIORITY など、データベース オプションによっては、配置作業中の調整はできない場合があります。 ファイル グループの数、ファイルの数やサイズなどの物理プロパティは、配置作業中に変更することはできません。 配置が完了すれば、ALTER DATABASE ステートメント、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell を使用して、データベースを調整できます。  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 DAC を配置できるのは、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、または [!INCLUDE[ssDE](../../includes/ssde-md.md)] Service Pack 4 (SP4) 以降を実行している [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスです。 新しいバージョンを使用して DAC を作成した場合、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ではサポートされないオブジェクトが DAC に含まれている可能性があります。 このような DAC を [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のインスタンスに配置することはできません。  
  
###  <a name="Prerequisites"></a> の前提条件  
 ソースが不明または信頼されていない DAC パッケージは配置しないことをお勧めします。 こうしたパッケージには、意図しない Transact-SQL コードを実行したり、スキーマを変更してエラーを発生したりする、悪意のあるコードが含まれている可能性があります。 パッケージのソースが不明または信頼されていない場合は、使用する前に、DAC をアンパックして、ストアド プロシージャやその他のユーザー定義コードなどのコードもご確認ください。 これらのチェックの実行方法の詳細については、「 [Validate a DAC Package](validate-a-dac-package.md)」をご覧ください。  
  
###  <a name="Security"></a> セキュリティ  
 セキュリティを強化するために、SQL Server 認証のログインは、パスワードなしで DAC パッケージに格納されます。 パッケージが配置またはアップグレードされると、ログインは、生成されたパスワードを伴う無効なログインとして作成されます。 ログインを有効にするには、ALTER ANY LOGIN 権限を持つユーザーとしてログインし、ALTER LOGIN を使用してログインを有効にします。さらに、新しいパスワードを割り当て、そのパスワードを該当ユーザーに通知します。 Windows 認証ログインの場合、ログインのパスワードは SQL Server で管理されていないため、この操作は必要ありません。  
  
####  <a name="Permissions"></a> アクセス許可  
 DAC を配置できるのは、 **sysadmin** または **serveradmin** 固定サーバー ロールのメンバーか、 **dbcreator** 固定サーバー ロールに存在する ALTER ANY LOGIN 権限を持つログインのみです。 あらかじめ登録された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者アカウント ( **sa** ) でも DAC を配置できます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] へのログインが含まれる DAC を配置するには、loginmanager ロールまたは serveradmin ロールのメンバーシップが必要です。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] へのログインが含まれない DAC を配置するには、dbmanager ロールまたは serveradmin ロールのメンバーシップが必要です。  
  
##  <a name="UsingDeployDACWizard"></a>データ層アプリケーションの配置ウィザードの使用  
 **ウィザードを使用して DAC を配置するには**  
  
1.  **オブジェクト エクスプローラー**で、DAC を配置するインスタンスのノードを展開します。  
  
2.  **[データベース]** ノードを右クリックし、 **[データ層アプリケーションの配置]** をクリックします。  
  
3.  ウィザードの各ダイアログの手順を実行します。  
  
    -   [[説明] ページ](#Introduction)  
  
    -   [[DAC パッケージの選択] ページ](#Select_dac_package)  
  
    -   [[ポリシーの確認] ページ](#Review_policy)  
  
    -   [[構成の更新] ページ](#Update_configuration)  
  
    -   [[概要] ページ](#Summary)  
  
    -   [[配置] ページ](#Deploy)  
  
##  <a name="Introduction"></a> [説明] ページ  
 このページでは、データ層アプリケーションを配置する手順について説明します。  
  
 **[次回からこのページを表示しない]** : 今後このページを表示しないようにするには、このチェック ボックスをオンにします。  
  
 **[次へ >]** : **[DAC パッケージの選択]** ページに進みます。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
##  <a name="Select_dac_package"></a>[DAC パッケージの選択] ページ  
 このページでは、配置するデータ層アプリケーションを含む DAC パッケージを指定できます。 このページは、3 つの状態を遷移します。  
  
### <a name="select-the-dac-package"></a>DAC パッケージの選択  
 ページの初期状態では、配置する DAC パッケージを選択します。 DAC パッケージは有効な DAC パッケージ ファイルで、拡張子は .dacpac である必要があります。  
  
 **[DAC パッケージ]** : 配置するデータ層アプリケーションを含む DAC パッケージのパスとファイル名を指定します。 ボックスの右にある **[参照]** をクリックして、DAC パッケージの場所に移動することができます。  
  
 **[アプリケーション名]** : DAC が作成されたとき、またはデータベースから抽出されたときに割り当てられた DAC 名が表示される読み取り専用のボックスです。  
  
 **[バージョン]** : DAC が作成されたとき、またはデータベースから抽出されたときに割り当てられたバージョンが表示される読み取り専用のボックスです。  
  
 **[説明]** : DAC が作成されたとき、またはデータベースから抽出されたときに記述された説明が表示される読み取り専用のボックスです。  
  
 **\< [戻る]** : **概要** ページに進みます。  
  
 **[次へ >]** : 選択したファイルが有効な DAC パッケージかどうかが確認され、進捗状況バーが表示されます。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
### <a name="validating-the-dac-package"></a>DAC パッケージの検証  
 選択したファイルが有効な DAC パッケージかどうかが確認され、進捗状況バーが表示されます。 DAC パッケージが検証されると、 **[DAC パッケージの選択]** ページの最終状態に進み、検証の結果を確認できます。 ファイルが有効な DAC パッケージでない場合は、 **[DAC パッケージの選択]** が表示されたままになります。 別の有効な DAC パッケージを選択するか、ウィザードを取り消して新しい DAC パッケージを生成してください。  
  
 **[DAC パッケージの内容を検証しています]** : 検証プロセスの現在の状態を示す進捗状況バーです。  
  
 [**前\<** **]: [パッケージの選択**] ページの初期状態に戻ります。  
  
 **[次へ >]** : **[パッケージの選択]** ページの最終状態に進みます。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
##  <a name="Review_policy"></a> [ポリシーの確認] ページ  
 このページでは、DAC にポリシーが含まれている場合に DAC サーバーの選択ポリシーを評価した結果を確認します。 DAC サーバーの選択ポリシーは、省略可能で、Visual Studio で DAC を作成するときに割り当てられます。 このポリシーでは、サーバーの選択ポリシーのファセットを使用して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスで DAC をホストするために満たす必要がある条件を指定します。  
  
 **[ポリシー条件の評価結果]** : DAC 配置ポリシーの条件が満たされたかどうかを示す読み取り専用のレポートです。 各条件の評価結果が、レポートの各行に表示されます。  
  
 サーバーの選択ポリシー (オペレーティング システムのバージョン、言語、名前付きパイプの有効化、プラットフォーム、および TCP の有効化) は、DAC を [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に配置する場合は常に false となります。  
  
 **[ポリシー違反を無視します]** : ポリシー条件が満たされていない場合に配置を続行するには、このチェック ボックスを使用します。 すべての条件が満たされていなくても DAC を正常に操作できるようにする場合のみ、このチェック ボックスをオンにしてください。  
  
 [**前\<** **]: [パッケージの選択**] ページに戻ります。  
  
 **[次へ >]** : **[構成の更新]** ページに進みます。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
##  <a name="Update_configuration"></a>[構成の更新] ページ  
 このページでは、配置された DAC インスタンスと配置によって作成されたデータベースの名前を指定し、データベース オプションを設定します。  
  
 **[データベース名]** : 配置によって作成されるデータベースの名前を指定します。 既定では、DAC の抽出元であるソース データベースの名前です。 この名前は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンス内で一意であり、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 識別子のルールに従っている必要があります。  
  
 データベース名を変更した場合、データ ファイルとログ ファイルの名前も新しいデータベース名に合わせて変更されます。  
  
 また、データベース名は、DAC インスタンスの名前としても使用されます。 インスタンス名は、 **オブジェクト エクスプローラー** の **[データ層アプリケーション]** ノードまたは **ユーティリティ エクスプローラー** の **[配置済みのデータ層アプリケーション]** ノードの下にある、DAC のノードに表示されます。  
  
 次のオプションは [!INCLUDE[ssSDS](../../includes/sssds-md.md)]には適用されず、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]の配置時には表示されません。  
  
 **[既定のデータベースの場所の使用]** : データベースのデータ ファイルおよびログ ファイルを [!INCLUDE[ssDE](../../includes/ssde-md.md)]インスタンスの既定の場所に作成するには、このオプションを選択します。 ファイル名は、データベース名を使用して作成されます。  
  
 **[データベース ファイルの指定]** : データ ファイルおよびログ ファイルに別の場所または名前を指定するには、このオプションを選択します。  
  
 **[データ ファイルのパスと名前]** : データ ファイルの完全パスとファイル名を指定します。 このボックスには、既定のパスとファイル名が表示されます。 ボックス内の文字列を編集して既定値を変更するか、[参照] をクリックしてデータ ファイルを配置するフォルダーに移動してください。  
  
 **[ログ ファイルのパスと名前]** : ログ ファイルの完全パスとファイル名を指定します。 このボックスには、既定のパスとファイル名が表示されます。 ボックス内の文字列を編集して既定値を変更するか、 **[参照]** をクリックしてログ ファイルを配置するフォルダーに移動してください。  
  
 [**前\<** **]: [DAC パッケージの選択**] ページに戻ります。  
  
 **[次へ >]** : **[概要]** ページに進みます。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
##  <a name="Summary"></a> [概要] ページ  
 このページでは、DAC の配置時にウィザードが行うアクションを確認します。  
  
 **[次の設定を使用して DAC を配置します。]** : 表示された情報を確認し、実行されるアクションが正しいかどうかを確認します。 このウィンドウには、選択した DAC パッケージと、配置される DAC インスタンス用に選択した名前が表示されます。 また、DAC に関連付けられたデータベースを作成する際に使用される設定も表示されます。  
  
 **\< 前**へ-**構成の更新** ページに戻り、選択内容を変更します。  
  
 **[次へ >]** : DAC を配置し、 **[DAC の配置]** ページに結果を表示します。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
##  <a name="Deploy"></a>[配置] ページ  
 このページには、配置操作の成功または失敗が表示されます。  
  
 **[DAC を配置しています]** : DAC を配置するために行った各アクションの成功または失敗が表示されます。 内容を確認して、各アクションの成功または失敗を判断します。 エラーが発生したアクションには、 **[結果]** 列にリンクが表示されます。 そのアクションのエラーのレポートを表示するには、リンクをクリックします。  
  
 **[レポートの保存]** : 配置レポートを HTML ファイルに保存します。 ファイルには、アクションで発生したすべてのエラーを含む、各アクションのステータスが報告されます。 既定のフォルダーは、Windows アカウントの Documents フォルダーにある SQL Server Management Studio\DAC Packages フォルダーです。  
  
 **[完了]** : ウィザードを終了します。  
  
##  <a name="DeployDACPowerShell"></a> PowerShell の使用  
 **PowerShell スクリプトで Install () メソッドを使用して DAC を配置するには**  
  
1.  SMO サーバー オブジェクトを作成し、DAC を配置するインスタンスに設定します。  
  
2.  `ServerConnection` オブジェクトを開いて、同じインスタンスに接続します。  
  
3.  `System.IO.File` を使用して、DAC パッケージ ファイルを読み込みます。  
  
4.  `add_DacActionStarted` および `add_DacActionFinished` を使用して、DAC 配置イベントをサブスクライブします。  
  
5.  `DatabaseDeploymentProperties`を設定します。  
  
6.  `DacStore.Install` メソッドを使用して DAC を配置します。  
  
7.  DAC パッケージ ファイルの読み取りに使用するファイル ストリームを閉じます。  
  
### <a name="example-powershell"></a>例 (PowerShell)  
 次の例では、MyApplication.dacpac パッケージから DAC 定義を使用して、MyApplication という名前の DAC を [!INCLUDE[ssDE](../../includes/ssde-md.md)]の既定のインスタンスに配置します。  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverconnection,$dacName)  
$dacstore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## <a name="see-also"></a>参照  
 [データ層アプリケーション](data-tier-applications.md)   
 [データベースからの DAC の抽出](extract-a-dac-from-a-database.md)   
 [データベース識別子](../databases/database-identifiers.md)  
