---
title: データ層アプリケーションの削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.deletedacwizard.deletedac.f1
- sql13.swb.deletedacwizard.summary.f1
- sql13.swb.deletedacwizard.introduction.f1
- sql13.swb.deletedacwizard.choosemethod.f1
helpviewer_keywords:
- How to [DAC], delete
- data-tier application [SQL Server], delete
- wizard [DAC], delete
- delete DAC
ms.assetid: 16fe1c18-4486-424d-81d6-d276ed97482f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 07a4d09e55999c9e6f85e059f576c1460baf750a
ms.sourcegitcommit: af5e1f74a8c1171afe759a4a8ff2fccb5295270a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2019
ms.locfileid: "71823559"
---
# <a name="delete-a-data-tier-application"></a>データ層アプリケーションの削除
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  データ層アプリケーションの削除ウィザードまたは Windows PowerShell スクリプトを使用して、データ層アプリケーションを削除できます。 関連付けられたデータベースの保持、デタッチ、または削除を指定することができます。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **DAC のアップグレード:** [データ層アプリケーションの登録ウィザードの使用](#UsingDeleteDACWizard)、[PowerShell の使用](#DeleteDACPowerShell)  
  
## <a name="before-you-begin"></a>はじめに  
 データ層アプリケーション (DAC) インスタンスを削除する場合、3 つのオプションのいずれかを選択して、データ層アプリケーションに関連付けられたデータベースの処理を指定します。 どのオプションを選択した場合も、DAC 定義のメタデータが削除されます。 各オプションは、データ層アプリケーションに関連付けられたデータベースの処理方法が異なります。 DAC またはデータベースに関連付けられたインスタンスレベルのオブジェクト (ログインなど) が、ウィザードによって削除されることはありません。  
  
|オプション|データベース アクション|  
|------------|----------------------|  
|登録の削除|関連付けられているデータベースは、そのまま保持されます。|  
|データベースのデタッチ|関連付けられたデータベースはデタッチされます。 データベース エンジンのインスタンスはデータベースを参照できませんが、データ ファイルとログ ファイルはそのまま保持されます。|  
|データベースの削除|関連付けられたデータベースは削除されます。 データ ファイルとログ ファイルも削除されます。|  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 DAC を削除した後に DAC 定義のメタデータ、またはデータベースを自動的に復元するメカニズムはありません。 DAC インスタンスを手動で再構築する方法は、削除オプションによって異なります。  
  
|オプション|DAC インスタンスの再構築方法|  
|------------|-------------------------------------|  
|登録の削除|同じ場所に残っているデータベースから DAC を登録します。|  
|データベースのデタッチ|**sp_attachdb** または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してデータベースを再アタッチして、データベースから新しい DAC インスタンスを登録します。|  
|データベースの削除|DAC が削除される前に作成された完全バックアップからデータベースを復元して、データベースから新しい DAC インスタンスを登録します。|  
  
> [!WARNING]  
>  復元または再アタッチされたデータベースから DAC を登録して DAC インスタンスを再構築しても、サーバーの選択ポリシーなど、元の DAC の一部は再作成されません。  
  
###  <a name="Permissions"></a> 権限  
 DAC を削除できるのは、 **sysadmin** または **serveradmin** 固定サーバー ロールのメンバーか、データベース所有者のみです。 あらかじめ登録された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者アカウント ( **sa** ) もこのウィザードを起動できます。  
  
##  <a name="UsingDeleteDACWizard"></a> データ層アプリケーションの削除ウィザードの使用  
 **ウィザードを使用して DAC を削除するには**  
  
1.  **オブジェクト エクスプローラー**で、削除する DAC を含んだインスタンスのノードを展開します。  
  
2.  **[管理]** ノードを展開します。  
  
3.  **[データ層アプリケーション]** ノードを展開します。  
  
4.  削除する DAC を右クリックし、 **[データ層アプリケーションの削除]** をクリックします。  
  
5.  ウィザードの各ダイアログの手順を実行します。  
  
    1.  [概要](#Introduction)  
  
    2.  [方法の選択](#Choose_method)  
  
    3.  [概要](#Summary)  
  
    4.  [データ層アプリケーションの削除](#Delete_datatier_application)  
  
##  <a name="Introduction"></a> [説明] ページ  
 このページでは、データ層アプリケーションを削除する手順について説明します。  
  
 **[次回からこのページを表示しない]** : 今後このページを表示しないようにするには、このチェック ボックスをオンにします。  
  
 **[次へ >]** : **[方法の選択]** ページに進みます。  
  
 **[キャンセル]** : データ層アプリケーションもデータベースも削除することなくウィザードを終了します。  
  
 [データ層アプリケーションの削除ウィザードの使用](#UsingDeleteDACWizard)  
  
##  <a name="Choose_method"></a> [方法の選択] ページ  
 削除する DAC に関連付けられているデータベースの処理オプションを指定するには、このページを使用します。  
  
 **[登録の削除]** : データ層アプリケーションを定義しているメタデータを削除しますが、関連付けられたデータベースはそのまま保持されます。  
  
 **[データベースのデタッチ]** : データ層アプリケーションを定義しているメタデータを削除して、関連付けられたデータベースをデタッチします。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスはデータベースを参照できなくなりますが、データ ファイルとログ ファイルはそのまま保持されます。  
  
 **[データベースの削除]** : DAC を定義しているメタデータと、関連付けられたデータベースを削除します。  
  
 データベースのデータ ファイルとログ ファイルは、完全に削除されます。  
  
 **[< 戻る]** : **[説明]** ページに戻ります。  
  
 **[次へ]** : **[概要]** ページに進みます。  
  
 **[キャンセル]** : DAC もデータベースも削除することなくウィザードを終了します。  
  
 [データ層アプリケーションの削除ウィザードの使用](#UsingDeleteDACWizard)  
  
##  <a name="Summary"></a> [概要] ページ  
 このページでは、DAC インスタンスの削除時にウィザードが行うアクションを確認します。  
  
 **[選択内容の概要の確認]** : ボックスに表示されている DAC、データベース、および削除方法を確認します。 情報が正しい場合は、 **[次へ]** または **[完了]** をクリックして DAC を削除します。 DAC とデータベースの情報が正しくない場合は、 **[キャンセル]** をクリックしてから正しい DAC を選択します。 削除方法が正しくない場合は、 **[戻る]** をクリックして **[方法の選択]** ページに戻り、別の方法を選択します。  
  
 **[< 戻る]** : **[方法の選択]** ページに戻り、別の削除方法を選択します。  
  
 **[次へ >]** : 前のページで選択した方法で DAC インスタンスを削除して、 **[データ層アプリケーションの削除]** ページに進みます。  
  
 **[キャンセル]** : DAC インスタンスを削除することなくウィザードを終了します。  
  
 [データ層アプリケーションの削除ウィザードの使用](#UsingDeleteDACWizard)  
  
##  <a name="Delete_datatier_application"></a> [データ層アプリケーションの削除] ページ  
 このページには、削除操作の成功または失敗が表示されます。  
  
 **[DAC の削除]** : DAC インスタンスを削除するために行った各アクションの成功または失敗が表示されます。 内容を確認して、各アクションの成功または失敗を判断します。 エラーが発生したアクションには、 **[結果]** 列にリンクが表示されます。 そのアクションのエラーのレポートを表示するには、リンクをクリックします。  
  
 **[レポートの保存]** : 削除レポートを HTML ファイルに保存します。 ファイルには、アクションで発生したすべてのエラーを含む、各アクションのステータスが報告されます。 既定のフォルダーは、Windows アカウントの Documents フォルダーにある SQL Server Management Studio\DAC Packages フォルダーです。  
  
 **[完了]** : ウィザードを終了します。  
  
 [データ層アプリケーションの削除ウィザードの使用](#UsingDeleteDACWizard)  
  
##  <a name="DeleteDACPowerShell"></a> PowerShell の使用  

1. SMO サーバー オブジェクトを作成し、削除する DAC を含んだインスタンスに設定します。  
  
1. **ServerConnection** オブジェクトを開いて、同じインスタンスに接続します。  
  
1. `add_DacActionStarted` および `add_DacActionFinished` を使用して、DAC アップグレード イベントをサブスクライブします。  
  
1. 削除する DAC を指定します。  
  
1. どの削除オプションが適切かに応じて、3 つの例のいずれかを使用します。  
  
   - DAC 登録を削除し、データベースをそのままにするには、`Unmanage` メソッドを使用します。  
   - DAC 登録を削除し、データベースをデタッチするには、`Uninstall` メソッドを使用し、`DetachDatabase` を指定します。  
   - DAC 登録を削除し、データベースを削除するには、`Uninstall` メソッドを使用し、`DropDatabase` を指定します。
  
### <a name="delete-the-dac-and-leave-the-database"></a>DAC を削除してデータベースを終了する

次の例では、`Unmanage` メソッドを使用して `<myApplication>` という名前の DAC を削除します。これにより、DAC は削除されますが、データベースはそのまま残ります。  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$server = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverConnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($server.ConnectionContext.SqlConnectionObject)  
$serverConnection.Connect()  
$dacStore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverConnection)  
  
## Subscribe to the DAC delete events.  
$dacStore.add_DacActionStarted({Write-Host `n`nStarting at $(Get-Date) :: $_.Description})  
$dacStore.add_DacActionFinished({Write-Host Completed at $(Get-Date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "<myApplication>"  
  
## Only delete the DAC definition from msdb, the associated database remains active.  
$dacStore.Unmanage($dacName)  
```
  
### <a name="delete-the-dac-and-detach-the-database"></a>DAC を削除し、データベースをデタッチする

次の例では、`Uninstall` メソッドを使用して `<myApplication>` という名前の DAC を削除します。これにより、DAC は削除され、データベースはデタッチされます。  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$server = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverConnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($server.ConnectionContext.SqlConnectionObject)  
$serverConnection.Connect()  
$dacStore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverConnection)  
  
## Subscribe to the DAC delete events.  
$dacStore.add_DacActionStarted({Write-Host `n`nStarting at $(Get-Date) :: $_.Description})  
$dacStore.add_DacActionFinished({Write-Host Completed at $(Get-Date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "<myApplication>"  
  
## Delete the DAC definition from msdb and detach the associated database.  
$dacStore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DetachDatabase)  
```
  
### <a name="delete-the-dac-and-drop-the-database"></a>DAC を削除し、データベースをドロップする

次の例では、`Uninstall` メソッドを使用して `<myApplication>` という名前の DAC を削除します。これにより、DAC は削除され、データベースはドロップされます。  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$server = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverConnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($server.ConnectionContext.SqlConnectionObject)  
$serverConnection.Connect()  
$dacStore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverConnection)  
  
## Subscribe to the DAC delete events.  
$dacStore.add_DacActionStarted({Write-Host `n`nStarting at $(Get-Date) :: $_.Description})  
$dacStore.add_DacActionFinished({Write-Host Completed at $(Get-Date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "<myApplication>"  
  
## Delete the DAC definition from msdb and drop the associated database.  
$dacStore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DropDatabase)  
```
  
## <a name="see-also"></a>参照  
 [[データ層アプリケーション]](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [[データ層アプリケーション]](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [データ層アプリケーションの配置](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [データベースを DAC として登録する方法](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)   
 [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
