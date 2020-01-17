---
title: データ層アプリケーションのアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.upgradedacwizard.reviewpolicy.f1
- sql12.swb.upgradedacwizard.selectoptions.f1
- sql12.swb.upgradedacwizard.selectpackage.f1
- sql12.swb.upgradedacwizard.reviewplan.f1
- sql12.swb.upgradedacwizard.checkdrift.f1
- sql12.swb.upgradedacwizard.summary.f1
- sql12.swb.upgradedacwizard.upgradedac.f1
- sql12.swb.upgradedacwizard.introduction.f1
helpviewer_keywords:
- upgrade DAC
- data-tier application [SQL Server], upgrade
- wizard [DAC], upgrade
- How to [DAC], upgrade
ms.assetid: c117df94-f02b-403f-9383-ec5b3ac3763c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 44c4bb7c01f18db6062ad1982fcf5a5f80e4d6b0
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797981"
---
# <a name="upgrade-a-data-tier-application"></a>データ層アプリケーションのアップグレード
  データ層アプリケーションのアップグレード ウィザードまたは Windows PowerShell スクリプトを使用すると、現在配置されているデータ層アプリケーション (DAC) のスキーマとプロパティを、新しいバージョンの DAC で定義されているスキーマとプロパティに一致するように変更できます。  
  
-   **作業を開始する準備:**  [DAC アップグレード オプションの選択](#ChoseDACUpgOptions)、 [制限事項と制約事項](#LimitationsRestrictions)、 [前提条件](#Prerequisites)、 [セキュリティ](#Security)、 [権限](#Permissions)  
  
-   **DAC のアップグレード:**  [データ層アプリケーションのアップグレード ウィザードの使用](#UsingDACUpgradeWizard)、 [PowerShell の使用](#UpgradeDACPowerShell)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 DAC アップグレードは、既存のデータベースのスキーマを新しい DAC バージョンで定義されているスキーマに一致するように変更するインプレース アップグレードです。 新しい DAC バージョンは、DAC パッケージ ファイルで提供されます。 DAC パッケージの作成の詳細については、「 [データ層アプリケーション](data-tier-applications.md)」を参照してください。  
  
###  <a name="ChoseDACUpgOptions"></a> DAC アップグレード オプションの選択  
 インプレース アップグレードには 4 つのアップグレード オプションがあります。  
  
-   [**データ損失を無視**する]-`True`した場合、一部の操作によってデータが失われてもアップグレードが続行されます。 `False` の場合、これらの操作によってアップグレードは終了します。 たとえば、現在のデータベースにあるテーブルが新しい DAC のスキーマにない場合は、`True` が指定されていると、テーブルは削除されます。 既定の設定は `True` です。  
  
-   **[変更時にブロック**する]-`True`した場合、データベーススキーマが前の DAC で定義されているスキーマと異なる場合は、アップグレードが終了します。 `False` の場合、変更が検出されても、アップグレードは続行されます。 既定の設定は `False` です。  
  
-   **失敗時にロールバック**する-`True`した場合、アップグレードはトランザクションに含まれ、エラーが発生すると、ロールバックが試行されます。 `False` の場合、すべての変更が実行時にコミットされます。エラーが発生する場合は、データベースの前のバックアップの復元が必要になる場合があります。 既定の設定は `False` です。  
  
-   **[ポリシーの検証をスキップ]** : `True`した場合、DAC サーバーの選択ポリシーは評価されません。 `False` の場合は、ポリシーが評価され、検証エラーがあるとアップグレードは終了します。 既定の設定は `False` です。  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 DAC アップグレードは、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]または [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 以降でのみ実行できます。  
  
###  <a name="Prerequisites"></a> の前提条件  
 アップグレードを開始する前に、データベースの完全バックアップを実行することをお勧めします。 アップグレード時にエラーが発生し、すべての変更をロールバックできない場合は、バックアップの復元が必要になる場合があります。  
  
 アップグレードを開始する前に、DAC パッケージとアップグレード処理を検証するには、いくつかの操作を行う必要があります。 これらのチェックの実行方法の詳細については、「 [Validate a DAC Package](validate-a-dac-package.md)」をご覧ください。  
  
-   アップグレード時には、ソースが不明または信頼されていない DAC パッケージは使用しないことをお勧めします。 こうしたパッケージには、意図しない Transact-SQL コードを実行したり、スキーマを変更してエラーを発生したりする、悪意のあるコードが含まれている可能性があります。 パッケージのソースが不明または信頼されていない場合は、使用する前に、DAC をアンパックして、ストアド プロシージャやその他のユーザー定義コードなどのコードもご確認ください。  
  
-   最新バージョンの DAC が配置された後に現在のデータベースに変更が加えられている場合は、一部の変更によってアップグレードが正常に完了しなかったり、アップグレードによって一部の変更が削除されたりすることがあります。 まず、データベースで行った変更内容のレポートを生成して、確認してください。  
  
-   アップグレードによって実行されるスキーマの変更内容のリストを生成し、問題がないかどうかを確認してください。  
  
 DAC パッケージ内のアプリケーション名は、現在配置されている DAC のアプリケーション名と一致している必要があります。 たとえば、現在の DAC のアプリケーション名が **GeneralLedger**の場合、アップグレードできるのは、アプリケーション名が **GeneralLedger**の DAC パッケージを使用する場合だけです。  
  
 すべての変更をログ記録するための十分なトランザクション ログ領域があることを確認します。  
  
###  <a name="Security"></a> セキュリティ  
 セキュリティを強化するために、SQL Server 認証のログインは、パスワードなしで DAC パッケージに格納されます。 パッケージが配置またはアップグレードされると、ログインは、生成されたパスワードを伴う無効なログインとして作成されます。 ログインを有効にするには、ALTER ANY LOGIN 権限を持つユーザーとしてログインし、ALTER LOGIN を使用してログインを有効にします。さらに、新しいパスワードを割り当て、そのパスワードを該当ユーザーに通知します。 Windows 認証ログインの場合、ログインのパスワードは SQL Server で管理されていないため、この操作は必要ありません。  
  
####  <a name="Permissions"></a> アクセス許可  
 DAC をアップグレードできるのは、 **sysadmin** または **serveradmin** 固定サーバー ロールのメンバーか、 **dbcreator** 固定サーバー ロールに存在する ALTER ANY LOGIN 権限を持つログインのみです。 ログインは既存のデータベースの所有者である必要があります。 あらかじめ登録された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者アカウント ( **sa** ) も DAC をアップグレードできます。  
  
##  <a name="UsingDACUpgradeWizard"></a> データ層アプリケーションのアップグレード ウィザードの使用  
 **ウィザードを使用して、DAC をアップグレードするには**  
  
1.  **オブジェクト エクスプローラー**で、アップグレードする DAC を含んだインスタンスのノードを展開します。  
  
2.  **[管理]** ノードを展開し、 **[データ層のアプリケーション]** ノードを展開します。  
  
3.  アップグレードする DAC のノードを右クリックしてから、 **[データ層アプリケーションのアップグレード]** を選択します。  
  
4.  ウィザードの各ダイアログの手順を実行します。  
  
    1.  [[説明] ページ](#Introduction)  
  
    2.  [[パッケージの選択] ページ](#Select_dac_package)  
  
    3.  [[ポリシーの確認] ページ](#Review_policy)  
  
    4.  [[変更の検出] ページ](#Detect_change)  
  
    5.  [[アップグレード計画の確認]](#ReviewUpgPlan)  
  
    6.  [[概要] ページ](#Summary)  
  
    7.  [[DAC のアップグレード] ページ](#Upgrade)  
  
##  <a name="Introduction"></a> [説明] ページ  
 このページでは、データ層アプリケーションをアップグレードする手順について説明します。  
  
 **[次回からこのページを表示しない]** : 今後このページを表示しないようにするには、このチェック ボックスをオンにします。  
  
 **[次へ]** : **[パッケージの選択]** ページに進みます。  
  
 **[キャンセル]** : DAC をアップグレードせずにウィザードを終了します。  
  
##  <a name="Select_dac_package"></a> [パッケージの選択] ページ  
 このページでは、新しいバージョンのデータ層アプリケーションを含む DAC パッケージを指定します。 このページは、2 つの状態を遷移します。  
  
### <a name="select-the-dac-package"></a>DAC パッケージの選択  
 ページの初期状態では、配置する DAC パッケージを選択します。 DAC パッケージは有効な DAC パッケージ ファイルで、拡張子は .dacpac である必要があります。 DAC パッケージ内の DAC アプリケーション名は、現在の DAC のアプリケーション名と同じである必要があります。  
  
 **[DAC パッケージ]** : 新しいバージョンのデータ層アプリケーションを含む DAC パッケージのパスとファイル名を指定します。 ボックスの右にある **[参照]** をクリックして、DAC パッケージの場所に移動することができます。  
  
 **[アプリケーション名]** : DAC が作成されたとき、またはデータベースから抽出されたときに割り当てられた DAC アプリケーション名が表示される読み取り専用のボックスです。  
  
 **[バージョン]** : DAC が作成されたとき、またはデータベースから抽出されたときに割り当てられたバージョンが表示される読み取り専用のボックスです。  
  
 **[説明]** : DAC が作成されたとき、またはデータベースから抽出されたときに記述された説明が表示される読み取り専用のボックスです。  
  
 **\< [戻る]** : **概要** ページに進みます。  
  
 **[次へ >]** : 選択したファイルが有効な DAC パッケージかどうかが確認され、進捗状況バーが表示されます。  
  
 **[キャンセル]** : DAC をアップグレードせずにウィザードを終了します。  
  
### <a name="validating-the-dac-package"></a>DAC パッケージの検証  
 選択したファイルが有効な DAC パッケージかどうかが確認され、進捗状況バーが表示されます。 DAC パッケージが検証されると、ウィザードは **[ポリシーの確認]** ページに進みます。 ファイルが有効な DAC パッケージでない場合は、 **[DAC パッケージの選択]** ページが表示されたままになります。 別の有効な DAC パッケージを選択するか、ウィザードを取り消して新しい DAC パッケージを生成してください。  
  
 **[DAC パッケージの内容を検証しています]** : 検証プロセスの現在の状態を示す進捗状況バーです。  
  
 [**前\<** **]: [パッケージの選択**] ページの初期状態に戻ります。  
  
 **[次へ >]** : **[パッケージの選択]** ページの最終状態に進みます。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
##  <a name="Review_policy"></a> [ポリシーの確認] ページ  
 このページでは、DAC にポリシーが含まれている場合に DAC サーバーの選択ポリシーを評価した結果を確認します。 DAC サーバーの選択ポリシーは、省略可能で、Microsoft Visual Studio で作成された DAC に割り当てられます。 このポリシーでは、サーバーの選択ポリシーのファセットを使用して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスで DAC をホストするために満たす必要がある条件を指定します。  
  
 **[ポリシー条件の評価結果]** : DAC サーバーの選択ポリシーの条件の評価に成功したかどうかを示す読み取り専用のレポートです。 各条件の評価結果が、レポートの各行に表示されます。  
  
 **[ポリシー違反を無視します]** : ポリシー条件が満たされていない場合にアップグレードを続行するには、このチェック ボックスを使用します。 すべての条件が満たされていなくても DAC を正常に操作できるようにする場合のみ、このチェック ボックスをオンにしてください。  
  
 [**前\<** **]: [パッケージの選択**] ページに戻ります。  
  
 **[次へ]** : **[変更の検出]** ページに進みます。  
  
 **[キャンセル]** : DAC をアップグレードせずにウィザードを終了します。  
  
##  <a name="Detect_change"></a> [変更の検出] ページ  
 このページでは、 **msdb**内の DAC メタデータに格納されているスキーマ定義とは異なるスキーマを作成する、データベースへの変更についてウィザードで確認した結果がレポートされます。 たとえば、最初に DAC が配置された後に、CREATE、ALTER または DROP ステートメントを使用してデータベースでオブジェクトを追加、変更、または削除した場合です。 このページでは、まず進捗状況バーが表示されてから、分析結果が表示されます。  
  
 **[変更を検出しています。これには、数分間かかることがあります]** : ウィザードでデータベースの現在のスキーマと DAC 定義のオブジェクトの間で相違点がチェックされるときに、進捗状況バーが表示されます。  
  
 **[変更の検出結果]** : 分析が完了したことを示し、結果が下に表示されます。  
  
 **[データベース &lt;DatabaseName&gt; は変更されていません]** : ウィザードで、データベースで定義されているオブジェクトと DAC 定義の対応するオブジェクトの間で相違点が検出されませんでした。  
  
 **[データベース &lt;DatabaseName&gt; が変更されました]** : ウィザードで、データベースのオブジェクトと DAC 定義の対応するオブジェクトの間で変更点が検出されました。  
  
 **[変更が失われる可能性がありますが続行します]** : 現在のデータベース内のオブジェクトやデータの一部が新しいデータベースに存在しない場合があることがわかっていて、アップグレードを続行することを指定します。 このボタンは、変更レポートの分析が完了し、新しいデータベースで必要なオブジェクトやデータを手動で転送するための手順がわかっている場合にのみクリックしてください。 わからない場合は、 **[レポートの保存]** をクリックして変更レポートを保存し、 **[キャンセル]** をクリックします。 レポートを分析して、アップグレードの完了後に必要なオブジェクトやデータを転送する方法を計画し、ウィザードを再起動します。  
  
 **[レポートの保存]** : ウィザードで検出された、データベースのオブジェクトと DAC 定義の対応するオブジェクトの間の変更点のレポートを保存する場合に、このボタンをクリックします。 その後、レポートを確認し、アップグレードの完了後に、レポートに表示されたオブジェクトの一部またはすべてを新しいデータベースに組み込む操作を行う必要があるかどうかを判断できます。  
  
 [**前\<** **]: [DAC パッケージの選択**] ページに戻ります。  
  
 **[次へ]** : **[オプション]** ページに進みます。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
## <a name="options-page"></a>[オプション] ページ)  
 このページを使用すると、アップグレードの失敗時のロールバック オプションを選択できます。  
  
 **[失敗時にロールバック]** : このオプションを選択すると、アップグレードはトランザクションに含まれ、エラーが発生した場合はウィザードからロールバックを試行できます。 オプションの詳細については、「 [DAC アップグレード オプションの選択](#ChoseDACUpgOptions)」を参照してください。  
  
 **[既定値に戻す]** : オプションを既定値の false に戻します。  
  
 **\< Previous** -[変更の**検出**] ページに戻ります。  
  
 **[次へ]** : **[アップグレード計画の確認]** ページに進みます。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
##  <a name="ReviewUpgPlan"></a> [アップグレード計画の確認] ページ  
 このページでは、アップグレード プロセスで実行されるアクションを確認します。 アップグレードによって問題が発生しないことが確実である場合にのみ、アップグレードを続行してください。  
  
 **[次のアクションを使用して DAC をアップグレードします。]** : 表示された情報を確認し、実行されるアクションが正しいかどうかを確認します。 **[アクション]** 列には、アップグレードを行うために実行される Transact-SQL ステートメントなどのアクションが表示されます。 **[データ損失]** 列には、関連付けられたアクションによってデータが削除される可能性がある場合に、警告が表示されます。  
  
 **[更新]** : アクション リストを更新します。  
  
 **[アクション レポートの保存]** : アクション ウィンドウの内容を HTML ファイルに保存します。  
  
 **[変更が失われる可能性がありますが続行します]** : 現在のデータベース内のオブジェクトやデータの一部が新しいデータベースに存在しない場合があることがわかっていて、アップグレードを続行することを指定します。 このボタンは、変更レポートの分析が完了し、新しいデータベースで必要なオブジェクトやデータを手動で転送するための手順がわかっている場合にのみクリックしてください。 わからない場合は、 **[アクション レポートの保存]** をクリックして変更レポートを保存し、 **[スクリプトの保存]** をクリックして Transact-SQL スクリプトを保存してから、 **[キャンセル]** をクリックします。 レポートとスクリプトを分析して、アップグレードの完了後に必要なオブジェクトやデータを転送する方法を計画し、ウィザードを再起動します。  
  
 **[スクリプトの保存]** : アップグレードを実行するために使用される Transact-SQL ステートメントをテキスト ファイルに保存します。  
  
 **[既定値に戻す]** : オプションを既定値の false に戻します。  
  
 **\< Previous** -[変更の**検出**] ページに戻ります。  
  
 **[次へ >]** : **[概要]** ページに進みます。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
##  <a name="Summary"></a> [概要] ページ  
 このページでは、DAC のアップグレード時にウィザードが行うアクションを最終的に確認します。  
  
 **[次の設定を使用して DAC をアップグレードします。]** : 表示された情報を確認し、実行されるアクションが正しいかどうかを確認します。 このウィンドウには、アップグレード対象として選択した DAC と、新しいバージョンの DAC が含まれている DAC パッケージが表示されます。 また、現在のバージョンのデータベースが現在の DAC 定義と同じかどうか、またはデータベースが変更されているかどうかも表示されます。  
  
 **\< 前**へ-**アップグレード計画の確認** ページに戻ります。  
  
 **[次へ]** : DAC を配置し、 **[DAC のアップグレード]** ページに結果を表示します。  
  
 **[キャンセル]** : DAC を配置せずにウィザードを終了します。  
  
##  <a name="Upgrade"></a> [DAC のアップグレード] ページ  
 このページには、アップグレード操作の成功または失敗が表示されます。  
  
 **[DAC をアップグレードしています]** : DAC をアップグレードするために行った各アクションの成功または失敗が表示されます。 内容を確認して、各アクションの成功または失敗を判断します。 エラーが発生したアクションには、 **[結果]** 列にリンクが表示されます。 そのアクションのエラーのレポートを表示するには、リンクをクリックします。  
  
 **[レポートの保存]** : アップグレード レポートを HTML ファイルに保存します。 ファイルには、アクションで発生したすべてのエラーを含む、各アクションのステータスが報告されます。 既定のフォルダーは、Windows アカウントの Documents フォルダーにある SQL Server Management Studio\DAC Packages フォルダーです。  
  
 **[完了]** : ウィザードを終了します。  
  
##  <a name="UpgradeDACPowerShell"></a> PowerShell の使用  
 **PowerShell スクリプトから IncrementalUpgrade() メソッドを使用して DAC をアップグレードするには**  
  
1.  SMO サーバー オブジェクトを作成し、アップグレードする DAC が含まれたインスタンスにそれを設定します。  
  
2.  `ServerConnection` オブジェクトを開いて、同じインスタンスに接続します。  
  
3.  `System.IO.File` を使用して、DAC パッケージ ファイルを読み込みます。  
  
4.  `add_DacActionStarted` および `add_DacActionFinished` を使用して、DAC アップグレード イベントをサブスクライブします。  
  
5.  `DacUpgradeOptions`を設定します。  
  
6.  `IncrementalUpgrade` メソッドを使用して DAC をアップグレードします。  
  
7.  DAC パッケージ ファイルの読み取りに使用するファイル ストリームを閉じます。  
  
### <a name="example-powershell"></a>例 (PowerShell)  
 次の例では、MyApplicationVNext.dacpac パッケージで新しい DAC バージョンを使用して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の既定のインスタンスの MyApplication という名前の DAC をアップグレードします。  
  
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
  
## Subscribe to the DAC upgrade events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Upgrade the DAC and close the package.  
$dacName  = "MyApplication"  
  
## Set the upgrade options.  
$upgradeProperties = New-Object Microsoft.SqlServer.Management.Dac.DacUpgradeOptions  
$upgradeProperties.blockonchanges = $true  
$upgradeProperties.ignoredataloss = $false  
$upgradeProperties.rollbackonfailure = $true  
$ upgradeProperties.skippolicyvalidation = $false  
  
## Upgrade the DAC  
$dacstore.IncrementalUpgrade($dacName, $dacType, $upgradeProperties)  
## Close the package file.  
$fileStream.Close()  
```  
  
## <a name="see-also"></a>参照  
 [データ層アプリケーション](data-tier-applications.md)   
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
