---
title: PowerShell を使用して Reporting Services サブスクリプションの所有者を変更および一覧表示し、サブスクリプションを実行する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0fa6cb36-68fc-4fb8-b1dc-ae4f12bf6ff0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ebb20180e96302ba2ee90e9ab90cb79be19b7e1b
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72796380"
---
# <a name="use-powershell-to-change-and-list-reporting-services-subscription-owners-and-run-a-subscription"></a>Use PowerShell to Change and List Reporting Services Subscription Owners and Run a subscription
  [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 以降では、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サブスクリプションの所有権をプログラムによってユーザー間で譲渡できます。 このトピックでは、サブスクリプションの所有権を変更または単純に一覧表示するために使用可能な、いくつかの Windows PowerShell スクリプトを説明します。 各サンプルには、ネイティブ モードと SharePoint モードの両方のサンプル構文が含まれています。 サブスクリプションの所有者を変更した後で、サブスクリプションは新しい所有者のセキュリティ コンテキストで実行され、レポート内の User!UserID フィールドには新しい所有者の値が表示されます。 PowerShell のサンプルが呼び出すオブジェクト モデルの詳細については、「 <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 ![PowerShell 関連コンテンツ](../media/rs-powershellicon.jpg "PowerShell 関連コンテンツ")  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ネイティブ モード &#124; [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint モード|  
  
 **このトピックの内容:**  
  
-   [スクリプトの使用方法](#bkmk_how_to)  
  
-   [スクリプト: すべてのサブスクリプションの所有権の一覧表示](#bkmk_list_ownership_all)  
  
-   [スクリプト: 特定のユーザーが所有するすべてのサブスクリプションの一覧表示](#bkmk_list_all_one_user)  
  
-   [スクリプト: 特定のユーザーが所有するすべてのサブスクリプションの所有権変更](#bkmk_change_all)  
  
-   [スクリプト: 特定のレポートに関連付けられたすべてのサブスクリプションの一覧表示](#bkmk_list_for_1_report)  
  
-   [スクリプト: 特定のサブスクリプションの所有権変更](#bkmk_change_all_1_subscription)  
  
-   [スクリプト： 単一のサブスクリプションの実行 (起動)](#bkmk_run_1_subscription)  
  
##  <a name="bkmk_how_to"></a> スクリプトの使用方法  
  
### <a name="permissions"></a>Permissions  
 このセクションでは、ネイティブ モードと SharePoint モードの [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]向けの各メソッドを使用するのに必要な権限レベルを要約します。 このトピック内のスクリプトは次の [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] メソッドを使用します。  
  
-   [ReportingService2010.ListSubscriptions メソッド](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.listsubscriptions.aspx)  
  
-   [ReportingService2010.ChangeSubscriptionOwner メソッド](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.changesubscriptionowner.aspx)  
  
-   [ReportingService2010.ListChildren](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.listchildren.aspx)  
  
-   [ReportingService2010.FireEvent](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.fireevent.aspx) メソッドは、特定のサブスクリプションをトリガーして実行するために、最後のスクリプトでのみ使用されます。 そのスクリプトを使用する計画がない場合、FireEvent メソッドの権限要件を無視できます。  
  
 **ネイティブ モード:**  
  
-   サブスクリプションの一覧表示: (HYPERLINK "https://technet.microsoft.com/library/microsoft.reportingservices.interfaces.reportoperation.aspx" ReadSubscription on report、ユーザーはサブスクリプションの所有者) または ReadAnySubscription  
  
-   サブスクリプションの変更: ユーザーは、BUILTIN\Administrators グループのメンバーである必要があります。  
  
-   子の一覧表示: アイテムの ReadProperties  
  
-   イベントの開始: GenerateEvents (システム)  
  
 **SharePoint モード:**  
  
-   サブスクリプションの一覧表示: ManageAlerts または (HYPERLINK "https://technet.microsoft.com/library/microsoft.sharepoint.spbasepermissions.aspx" レポートの CreateAlerts、ユーザーはサブスクリプションの所有者で、サブスクリプションは時間指定のサブスクリプション)。  
  
-   サブスクリプションの変更: ManageWeb  
  
-   子の一覧表示: ViewListItems  
  
-   イベントの起動: ManageWeb  
  
 詳しくは、「 [Reporting Services のロールおよびタスクと SharePoint のグループおよび権限の比較](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)」をご覧ください。  
  
### <a name="script-usage"></a>スクリプトの使用法  
 **スクリプトファイル (.ps1) の作成**  
  
1.  **c:\scripts**という名前のフォルダーを作成します。 異なるフォルダーを選択する場合、例のコマンド ライン構文ステートメントで使用されているフォルダー名を変更します。  
  
2.  各スクリプトに対してテキスト ファイルを作成し、ファイルを c:\scripts フォルダーに保存します。 .ps1 ファイルを作成する際、各例のコマンド ライン構文の名前を使用します。  
  
3.  管理者特権を使用してコマンド プロンプトを開きます。  
  
4.  各例に示されているサンプルのコマンド ライン構文を使用して、各スクリプト ファイルを実行します。  
  
 **テスト済みの環境**  
  
 このトピックのスクリプトは PowerShell バージョン 3 および以下のバージョンの [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]を使用してテスト済みです。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]  
  
##  <a name="bkmk_list_ownership_all"></a> スクリプト: すべてのサブスクリプションの所有権の一覧表示  
 このスクリプトはサイト上のすべてのサブスクリプションを一覧表示します。 このスクリプトを使用して、接続のテストまたは他のスクリプトで使用するためのレポート パスとサブスクリプション ID の検証を実施できます。 これは存在するサブスクリプションの内容と所有者を単に監査するのにも役立つスクリプトです。  
  
### <a name="native-mode-syntax"></a>ネイティブモードの構文
  
```cmd
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/reportserver" "/"  
```  
  
### <a name="sharepoint-mode-syntax"></a>SharePoint モードの構文
  
```cmd
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/_vti_bin/reportserver" "http://[server]"  
```  
  
### <a name="script"></a>[スクリプト]
  
```powershell
# Parameters  
#    server   - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
  
Param(  
    [string]$server,  
    [string]$site  
   )  
  
$rs2010 += New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site); # use "/" for default native mode site  
  
Write-Host " "  
Write-Host "----- $server's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted, Status  
```  
  
> [!TIP]  
>  SharePoint モードのサイト URLS を検証するには、SharePoint コマンドレット **Get-SPSite**を使用します。 詳細については、「 [Get-SPSite](https://technet.microsoft.com/library/ff607950\(v=office.15\).aspx)」を参照してください。  
  
##  <a name="bkmk_list_all_one_user"></a> スクリプト: 特定のユーザーが所有するすべてのサブスクリプションの一覧表示  
 このスクリプトは特定のユーザーが所有するすべてのサブスクリプションを一覧表示します。 このスクリプトを使用して、接続のテストまたは他のスクリプトで使用するためのレポート パスとサブスクリプション ID の検証を実施できます。 このスクリプトは、組織内のだれかが離任したときに、所有していたサブスクリプションを検証して、所有者を変更したり、サブスクリプションを削除したりする場合に役立ちます。  
  
### <a name="native-mode-syntax"></a>ネイティブモードの構文
  
```cmd
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]" "[server]/reportserver" "/"  
```  
  
### <a name="sharepoint-mode-syntax"></a>SharePoint モードの構文
  
```cmd
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]"  "[server]/_vti_bin/reportserver" "http://[server]"  
```  
  
### <a name="script"></a>[スクリプト]  
  
```powershell
# Parameters:  
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change  
#    server        - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site        - use "/" for default native mode site  
Param(  
    [string]$currentOwner,  
    [string]$server,  
    [string]$site  
)  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site);  
  
Write-Host " "  
Write-Host " "  
Write-Host "----- $currentOwner's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.owner -eq $currentOwner}  
```  
  
##  <a name="bkmk_change_all"></a> スクリプト: 特定のユーザーが所有するすべてのサブスクリプションの所有権変更  
 このスクリプトは、特定のユーザーが所有するすべてのサブスクリプションの所有権を新しい所有者のパラメーターに変更します。  
  
### <a name="native-mode-syntax"></a>ネイティブモードの構文
  
```cmd
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\current owner]" "[Domain]\[new owner]" "[server]/reportserver"  
```  
  
### <a name="sharepoint-mode-syntax"></a>SharePoint モードの構文
  
```cmd
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\{current owner]" "[Domain]\[new owner]" "[server]/_vti_bin/reportserver"  
```  
  
### <a name="script"></a>[スクリプト]
  
```powershell
# Parameters:  
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change  
#    newOwner      - DOMAIN\USER that will own the subscriptions you wish to change  
#    server        - server and instance name (e.g. myserver/reportserver, myserver/reportserver_db2, myserver/_vti_bin/reportserver)  
  
Param(  
    [string]$currentOwner,  
    [string]$newOwner,  
    [string]$server  
)  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$items = $rs2010.ListChildren("/", $true);  
  
$subscriptions = @();  
  
ForEach ($item in $items)  
{  
    if ($item.TypeName -eq "Report")  
    {  
        $curRepSubs = $rs2010.ListSubscriptions($item.Path);  
        ForEach ($curRepSub in $curRepSubs)  
        {  
            if ($curRepSub.Owner -eq $currentOwner)  
            {  
                $subscriptions += $curRepSub;  
            }  
        }  
    }  
}  
  
Write-Host " "  
Write-Host " "  
Write-Host -foregroundcolor "green" "-----  $currentOwner's Subscriptions changing ownership to $newOwner : "  
$subscriptions | select SubscriptionID, Owner, Path, Description,  Status  | format-table -AutoSize  
  
ForEach ($sub in $subscriptions)  
{  
    $rs2010.ChangeSubscriptionOwner($sub.SubscriptionID, $newOwner);  
}  
  
$subs2 = @();  
  
ForEach ($item in $items)  
{  
    if ($item.TypeName -eq "Report")  
    {  
        $subs2 += $rs2010.ListSubscriptions($item.Path);  
    }  
}  
```  
  
##  <a name="bkmk_list_for_1_report"></a> スクリプト: 特定のレポートに関連付けられたすべてのサブスクリプションの一覧表示  
 このスクリプトは特定のレポートに関連付けられたすべてのサブスクリプションを一覧表示します。 レポート パス構文は、完全な URL を必要とする、異なる SharePoint モードです。 構文例で使用されているレポート名 "title only" には空白が含まれているため、レポート名を単一引用符で囲む必要があります。  
  
### <a name="native-mode-syntax"></a>ネイティブモードの構文
  
```cmd
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/reportserver" "'/reports/title only'" "/"  
```  
  
### <a name="sharepoint-mode-syntax"></a>SharePoint モードの構文
  
```cmd
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/_vti_bin/reportserver"  "'http://[server]/shared documents/title only.rdl'" "http://[server]"  
```  
  
### <a name="script"></a>[スクリプト]
  
```powershell
# Parameters:  
#    server      - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    reportpath  - path to report in the report server, including report name e.g. /reports/test report >> pass in  "'/reports/title only'"  
#    site        - use "/" for default native mode site  
Param  
(  
      [string]$server,  
      [string]$reportpath,  
      [string]$site  
)  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site);  
  
Write-Host " "  
Write-Host " "  
Write-Host "----- $reportpath 's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.path -eq $reportpath}  
```  
  
##  <a name="bkmk_change_all_1_subscription"></a> スクリプト: 特定のサブスクリプションの所有権変更  
 このスクリプトは特定のサブスクリプションの所有権を変更します。 サブスクリプションは、スクリプトに渡す SubscriptionID によって識別されます。 サブスクリプションを一覧表示するスクリプトのいずれかを使用して、正しい SubscriptionID を判別できます。  
  
### <a name="native-mode-syntax"></a>ネイティブモードの構文
  
```cmd
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/reportserver" "/" "ac5637a1-9982-4d89-9d69-a72a9c3b3150"  
```  
  
### <a name="sharepoint-mode-syntax"></a>SharePoint モードの構文
  
```cmd
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/_vti_bin/reportserver" "http://[server]" "9660674b-f020-453f-b1e3-d9ba37624519"  
```  
  
### <a name="script"></a>[スクリプト]
  
```powershell
# Parameters:  
#    newOwner       - DOMAIN\USER that will own the subscriptions you wish to change  
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site        - use "/" for default native mode site  
#    subscriptionID - guid for the single subscription to change  
  
Param(  
    [string]$newOwner,  
    [string]$server,  
    [string]$site,  
    [string]$subscriptionid  
   )  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscription += $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid};  
  
Write-Host " "  
Write-Host "----- $subscriptionid's Subscription properties: "  
$subscription | select Path, report, Description, SubscriptionID, Owner, Status  
  
$rs2010.ChangeSubscriptionOwner($subscription.SubscriptionID, $newOwner)  
  
#refresh the list  
$subscription = $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid}; # use "/" for default native mode site  
Write-Host "----- $subscriptionid's Subscription properties: "  
$subscription | select Path, report, Description, SubscriptionID, Owner, Status  
```  
  
##  <a name="bkmk_run_1_subscription"></a> スクリプト： 単一のサブスクリプションの実行 (起動)  
 このスクリプトは、FireEvent メソッドを使用して特定のサブスクリプションを実行します。 このスクリプトは、サブスクリプションに対して構成されたスケジュールに関係なく、すぐにサブスクリプションを実行します。 EventType は、レポート サーバー構成ファイル **rsreportserver.config** で定義されている既知のイベントのセットと照合されます。スクリプトは標準サブスクリプションに対する以下のイベントの種類を使用します。  
  
 `<Event>`  
  
 `<Type>TimedSubscription</Type>`  
  
 `</Event>`  
  
 構成ファイルの詳細については、「 [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md)」を参照してください。  
  
 スクリプトには遅延ロジック `Start-Sleep -s 6` が含まれているので、イベントの起動後に時間があり、更新されたステータスが ListSubscription メソッドによって使用可能になります。  
  
### <a name="native-mode-syntax"></a>ネイティブモードの構文
  
```cmd
powershell c:\scripts\FireSubscription.ps1 "[server]/reportserver" $null "70366e82-2d3c-4edd-a216-b97e51e26de9"  
```  
  
### <a name="sharepoint-mode-syntax"></a>SharePoint モードの構文
  
```cmd
powershell c:\scripts\FireSubscription.ps1 "[server]/_vti_bin/reportserver" "http://[server]" "c3425c72-580d-423e-805a-41cf9799fd25"  
```  
  
### <a name="script"></a>[スクリプト]
  
```powershell
# Parameters  
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site           - use $null for a native mode server  
#    subscriptionid - subscription guid  
  
Param(  
  [string]$server,  
  [string]$site,  
  [string]$subscriptionid  
  )  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
#event type is case sensative to what is in the rsreportserver.config  
$rs2010.FireEvent("TimedSubscription",$subscriptionid,$site)  
  
Write-Host " "  
Write-Host "----- Subscription ($subscriptionid) status: "  
#get list of subscriptions and filter to the specific ID to see the Status and LastExecuted  
Start-Sleep -s 6 # slight delay in processing so ListSubscription returns the updated Status and LastExecuted  
$subscriptions = $rs2010.ListSubscriptions($site);   
$subscriptions | select Status, Path, report, Description, Owner, SubscriptionID, EventType, lastexecuted | where {$_.SubscriptionID -eq $subscriptionid}
```  
  
## <a name="see-also"></a>「  
 <xref:ReportService2010.ReportingService2010.ListSubscriptions%2A>   
 <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>   
 <xref:ReportService2010.ReportingService2010.ListChildren%2A>   
 <xref:ReportService2010.ReportingService2010.FireEvent%2A>  
