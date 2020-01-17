---
title: 'チェックリスト: PowerShell を使用して PowerPivot for SharePoint | を確認するMicrosoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 73a13f05-3450-411f-95f9-4b6167cc7607
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26d88f2123d87d462ff7f83d0736c182885bf250
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75225353"
---
# <a name="checklist-use-powershell-to-verify-powerpivot-for-sharepoint"></a>チェック リスト: PowerShell を使用して PowerPivot for SharePoint を確認する
  
  [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] のインストール操作や復旧操作を完了するには、信頼性の高い検証テストに合格する必要があります。このテストでは、サービスとデータが操作可能であるかどうかが確認されます。 この記事では、Windows PowerShell を使用してこのテストの手順を実行する方法について説明します。 各手順は個別のセクションで説明されています。これにより、特定のタスクを直接参照することもできます。 たとえば、メンテナンスやバックアップでサービス アプリケーションとコンテンツ データベースの名前の確認をスケジュールする必要がある場合は、このトピックの「 [データベース](#bkmk_databases) 」セクションのスクリプトを実行し、これらの名前を確認することができます。  
  
|||  
|-|-|  
|![PowerShell 関連コンテンツ](../../../reporting-services/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ")|完全な PowerShell スクリプトは、トピックの最後に記載されています。 
  [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] の完全な配置を監査するためのカスタム スクリプトを構築するには、完全なスクリプトをひな形として使用します。|  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** Sharepoint 2013 &#124; sharepoint 2010|  
  
 **このトピックの**内容: 次の表に示すアルファベット順の項目は、図の領域に対応しています。 ダイアグラムでは、次を説明します。  
  
|||  
|-|-|  
|[PowerShell 環境を準備する](#bkmk_prerequisites)<br /><br /> [現象と推奨される操作](#bkmk_symptoms)<br /><br /> **(A)** [Analysis Services Windows サービス](#bkmk_windows_service)<br /><br /> **(B)** [get-powerpivotsystemservice と get-powerpivotengineservice](#bkmk_engine_and_system_service)<br /><br /> **(C)** [PowerPivot サービスアプリケーションとプロキシ](#bkmk_powerpivot_service_application)<br /><br /> **(D)** [データベース](#bkmk_databases)<br /><br /> [SharePoint の機能](#bkmk_features)<br /><br /> [タイマージョブ](#bkmk_timer_jobs)<br /><br /> [正常性ルール](#bkmk_health_rules)<br /><br /> **(E)** [Windows と ULS のログ](#bkmk_logs)<br /><br /> [MSOLAP プロバイダー](#bkmk_msolap)<br /><br /> [ADOMD.Net クライアントライブラリ](#bkmk_adomd)<br /><br /> [正常性データの収集ルール](#bkmk_health_collection)<br /><br /> ['83'5c](#bkmk_solutions)<br /><br /> [手動による検証手順](#bkmk_manual)<br /><br /> [その他のリソース](#bkmk_more_resources)<br /><br /> [完全な PowerShell スクリプト](#bkmk_full_script)|![PowerPivot の PowerShell による検証](../../../sql-server/install/media/ssas-powershell-component-verification.png "PowerPivot の PowerShell による検証")|  
  
##  <a name="bkmk_prerequisites"></a>PowerShell 環境を準備する  
 このセクションの手順では、PowerShell 環境を準備します。 この手順は必須ではありませんが、スクリプト環境が現在どのように構成されているかに応じて必要になります。  
  
 **PowerShell のアクセス許可**  
  
 
  **管理者特権**を使用して、PowerShell ウィンドウまたは PowerShell ISE (Integrated Scripting Environment) を開きます。 コマンドの実行時に管理者特権がないと、次のようなエラー メッセージが表示されます。  
  
 Get-SPLogEvent: このコマンドレットを実行するには、コンピューター **管理者の権限** が必要です。  
  
 **SharePoint と[!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] **第  
  
 SharePoint 関連のコマンドレットを実行したときに次のようなエラー メッセージが表示された場合は、Add-PSSnapin コマンドを実行します。  
  
 用語 'Get-PowerPivotSystemService' **は、コマンドレット**、関数、スクリプト ファイル、または操作可能なプログラムの名前として認識されません。 名前が正しく記述されていることを確認し、パスが含まれている場合はそのパスが正しいことを確認してから、再試行してください。  
  
```  
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0  
```  
  
 **Windows PowerShell**  
  
 PowerShell ISE の詳細については、「 [Windows PowerShell ISE の概要](https://technet.microsoft.com/library/dd315244.aspx) 」と「 [Windows Powershell を使用して SharePoint 2013 を管理する](https://technet.microsoft.com/library/ee806878\(v=office.15\).aspx)」を参照してください。  
  
|||  
|-|-|  
|![SharePoint アプリケーションの全般設定での PowerPivot](../../../sql-server/install/media/ssas-powerpivot-logo.png "SharePoint アプリケーションの全般設定での PowerPivot")|
  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 管理ダッシュボードを使用することで、サーバーの全体管理の大半のコンポーネントを必要に応じて確認できます。 サーバーの全体管理でダッシュボードを開くには、 **[アプリケーションの全般設定]** をクリックし、 **[PowerPivot]** の **[管理ダッシュボード]** をクリックします。 ダッシュボードの詳細については、「 [PowerPivot Management Dashboard and Usage Data](../../power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)」を参照してください。|  
  
##  <a name="bkmk_symptoms"></a>現象と推奨される操作  
 次の表は、現象や問題、および問題解決に役立つこのトピックの推奨されるセクションを示しています。  
  
|症状|参照セクション|  
|-------------|-----------------|  
|データ更新が実行されていない|「 [Timer Jobs](#bkmk_timer_jobs) 」のセクションを参照して、 **"Online PowerPivot Data Refresh Timer Job"** がオンラインになっていることを確認します。|  
|管理ダッシュボードのデータが古くなっている|「 [タイマー ジョブ](#bkmk_timer_jobs) 」のセクションを参照して、 **"Management Dashboard Processing Timer Job"** がオンラインになっていることを確認します。|  
|管理ダッシュボードの一部の機能に関する問題|(Excel Services または PowerPivot for SharePoint のない) サーバーの全体管理のトポロジを持つファームに PowerPivot for SharePoint をインストールする場合に、PowerPivot 管理ダッシュボードの組み込みレポートへのフル アクセスが必要なときは、Microsoft ADOMD.NET クライアント ライブラリをダウンロードしてインストールする必要があります。 ダッシュボードの一部のレポートでは、ADOMD.NET を使用して、ファームの PowerPivot クエリ処理およびサーバーの状態に関するレポート データを提供する内部データにアクセスします。 セクション「 [ADOMD.Net クライアント ライブラリ](#bkmk_adomd) 」およびトピック「 [サーバーの全体管理を実行している Web フロントエンド サーバーに ADOMD.NET をインストールする方法](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)」を参照してください。|  
|\<今後のコンテンツ>||  
  
##  <a name="bkmk_windows_service"></a>Windows サービスの Analysis Services  
 このセクションのスクリプトでは、SharePoint モードの [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のインスタンスを検証します。 サービスが**実行**されていることを確認します。  
  
```powershell
Get-Service | Select name, displayname, status | Where {$_.Name -eq "msolap`$powerpivot"} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
Name              DisplayName                                Status  
----              -----------                                ------  
MSOLAP$POWERPIVOT SQL Server Analysis Services (POWERPIVOT) Running  
```  
  
##  <a name="bkmk_engine_and_system_service"></a>Get-powerpivotsystemservice と Get-powerpivotengineservice  
 このセクションのスクリプトでは、 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] System サービスを確認します。 SharePoint 2013 の配置では 1 つのシステム サービスが存在し、SharePoint 2010 の配置では 2 つサービスが存在します。  
  
 **Get-powerpivotsystemservice**  
  
 状態が**オンライン**であることを確認します。  
  
```powershell
Get-PowerPivotSystemService | Select typename, status, applications, farm | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
TypeName                                  Status Applications                             Farm  
--------                                  ------ ------------                             ----  
SQL Server PowerPivot Service Application Online {Default PowerPivot Service Application} SPFarm Name=SharePoint_Config_77d8ab0744a34e8aa27c806a2b8c760c  
```  
  
 **Get-powerpivotengineservice**  
  
> [!NOTE]  
>  SharePoint 2013 を使用して**いる場合は、このスクリプトをスキップ**します。 PowerPivotEngineService は、SharePoint 2013 の配置には含まれません。 SharePoint 2013 で Get PowerPivot**Engine**Service コマンドレットを実行すると、次のようなエラーメッセージが表示されます。 このエラー メッセージは、このトピックの前提条件に関するセクションで説明されている Add-PSSnapin コマンドを実行した場合でも返されます。  
>   
>  用語 'Get-PowerPivotEngineService' は、コマンドレットの名前として認識されません  
  
 SharePoint 2010 の配置では、状態が **オンライン**であることを確認します。  
  
```powershell
Get-PowerPivotEngineService | Select typename, status, name, instances, farm | Format-Table -Property * -AutoSize | Out-Default
```
  
```Output  
TypeName  : SQL Server Analysis Services  
Status    : Online  
Name      : MSOLAP$POWERPIVOT  
Instances : {POWERPIVOT}  
Farm      : SPFarm Name=SharePoint_Config  
```  
  
##  <a name="bkmk_powerpivot_service_application"></a>PowerPivot サービスアプリケーションとプロキシ  
 状態が **オンライン**であることを確認します。 Excel Services アプリケーションはサービス アプリケーション データベースを使用しないため、コマンドレットはデータベース名を返しません。 このトピックのデータベースに関するセクションでデータベースがオンラインであることを確認できるように、 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービス アプリケーションで使用されているデータベースを把握しておいてください。  
  
 **PowerPivot サービス アプリケーションと Excel サービス アプリケーション**  
  
 SharePoint 2010 の配置では、状態が **オンライン**であることを確認します。  
  
```powershell
Get-PowerPivotServiceApplication | Select typename,name, status, unattendedaccount, applicationpool, farm, database  
Get-SPExcelServiceApplication | Select typename, DisplayName, status  
```
  
```Output  
TypeName          : PowerPivot Service Application  
Name              : PowerPivotServiceApplication1  
Status            : Online  
UnattendedAccount : PowerPivotUnattendedAccount  
ApplicationPool   : SPIisWebServiceApplicationPool Name=sqlbi_serviceapp  
Farm              : SPFarm Name=SharePoint_Config  
Database          : GeminiServiceDatabase Name=PowerPivotServiceApplication1_19648f3f2c944e27acdc6c20aab8487a  
  
TypeName    : Excel Services Application Web Service Application  
DisplayName : Excel Services Application  
Status      : Online  
```  
  
 **サービスアプリケーションプール**  
  
> [!NOTE]  
>  次のコード サンプルでは、最初に既定の [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] サービス アプリケーションの applicationpool プロパティを返します。 文字列から名前が解析され、その名前を使用して、アプリケーション プール オブジェクトの状態が取得されます。  
>   
>  状態が**オンライン**であることを確認します。 状態がオンラインでない場合、またはサイトを[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]参照するときに "http エラー" が表示される場合は、IIS アプリケーションプールの id 資格情報が正しいことを確認してください。 IIS のプール名は、Get-SPServiceApplicationPool コマンドによって返された ID プロパティの値になります。  
  
```powershell
$poolname = [string](Get-PowerPivotServiceApplication | Select -Property applicationpool)  
$position = $poolname.lastindexof("=")  
$poolname = $poolname.substring($position+1)  
$poolname = $poolname.substring(0,$poolname.length-1)

Get-SPServiceApplicationPool | Select name, status, processaccountname, id | Where {$_.Name -eq $poolname} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
Name                           Status ProcessAccountName Id  
----                           ------ ------------------ -------   
SharePoint Web Services System Online DOMAIN\account     89b50ec3-49e3-4de7-881a-2cec4b8b73ea  
```  
  
 ![メモ](../../../reporting-services/media/rs-fyinote.png "note")アプリケーションプールは、サーバーの全体管理ページで [**サービスアプリケーションの管理**] で確認することもできます。 サービス アプリケーションの名前をクリックし、リボンで **[プロパティ]** をクリックします。  
  
 **PowerPivot サービス アプリケーションと Excel サービス アプリケーションのプロキシ**  
  
 状態が**オンライン**であることを確認します。  
  
```powershell
Get-SPServiceApplicationProxy | Select typename, status, unattendedaccount, displayname | Where {$_.TypeName -Like "*powerpivot*" -Or $_.TypeName -Like "*excel services*"} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
TypeName                                                 Status UnattendedAccount           DisplayName  
--------                                                 ------ -----------------           -----------  
PowerPivot Service Application Proxy                     Online PowerPivotUnattendedAccount PowerPivotServiceApplication1  
Excel Services Application Web Service Application Proxy Online                             Excel Services Application  
```  
  
##  <a name="bkmk_databases"></a>データベース  
 次のスクリプトは、サービス アプリケーション データベースとすべてのコンテンツ データベースの状態を返します。 状態が **オンライン**であることを確認します。  
  
```powershell
Get-SPDatabase | Select name, status, server, typename | Where {$_.TypeName -eq "content database" -Or $_.TypeName -Like "*Gemini*"} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
Name                                                                       Status Server                  TypeName   
----                                                                       ------ ------                  --------   
DefaultPowerPivotServiceApplicationDB-38422181-2b68-4ab2-b2bb-9c00c39e5a5e Online SPServer Name=TESTSERVER Microsoft.AnalysisServices.SPAddin.GeminiServiceDatabase  
DefaultWebApplicationDB-f0db1a8e-4c22-408c-b9b9-153bd74b0312               Online TESTSERVER\POWERPIVOT    Content Database   
SharePoint_Admin_3cadf0b098bf49e0bb15abd487f5c684                          Online TESTSERVER\POWERPIVOT    Content Database  
```  
  
##  <a name="bkmk_features"></a>SharePoint の機能  
 サイト、Web、ファームの各機能がオンラインであることを確認します。  
  
```powershell
Get-SPFeature | Select displayname, status, scope, farm | Where {$_.displayName -Like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
DisplayName     Status Scope Farm                           
-----------     ------ ----- ----                           
PowerPivotSite  Online  Site SPFarm Name=SharePoint_Config  
PowerPivotAdmin Online   Web SPFarm Name=SharePoint_Config  
PowerPivot      Online  Farm SPFarm Name=SharePoint_Config  
```  
  
##  <a name="bkmk_timer_jobs"></a>タイマージョブ  
 タイマー ジョブが **オンライン**であることを確認します。 
  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] EngineService は SharePoint 2013 にはインストールされないので、スクリプトを使用しても、SharePoint 2013 の配置における EngineService タイマー ジョブは表示されません。  
  
```powershell
Get-SPTimerJob | Where {$_.service -Like "*power*" -Or $_.service -Like "*mid*"} | Select status, displayname, LastRunTime, service | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
      Status DisplayName                                                                          LastRunTime          Service                               
------ -----------                                                                          -----------          -------                               
Online Health Analysis Job (Daily, SQL Server Analysis Services, All Servers)               4/9/2014 12:00:01 AM EngineService Name=MSOLAP$POWERPIVOT  
Online Health Analysis Job (Hourly, SQL Server Analysis Services, All Servers)              4/9/2014 1:00:01 PM  EngineService Name=MSOLAP$POWERPIVOT  
Online Health Analysis Job (Weekly, SQL Server Analysis Services, All Servers)              4/6/2014 12:00:10 AM EngineService Name=MSOLAP$POWERPIVOT  
Online PowerPivot Management Dashboard Processing Timer Job                                 4/8/2014 3:45:38 AM  MidTierService  
Online PowerPivot Health Statistics Collector Timer Job                                     4/9/2014 1:00:12 PM  MidTierService  
Online PowerPivot Data Refresh Timer Job                                                    4/9/2014 1:09:36 PM  MidTierService  
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, All Servers)  4/9/2014 12:00:00 AM MidTierService  
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, Any Server)   4/9/2014 12:00:00 AM MidTierService  
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, All Servers) 4/6/2014 12:00:03 AM MidTierService  
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, Any Server)  4/6/2014 12:00:03 AM MidTierService  
Online PowerPivot Setup Extension Timer Job                                                 4/1/2014 1:40:31 AM  MidTierService  
```  
  
##  <a name="bkmk_health_rules"></a>正常性ルール  
 SharePoint 2013 の配置では、ルールの数が少なくなっています。 各 SharePoint 環境のルールの完全な一覧と、ルールの使用方法の説明については、「 [PowerPivot の正常性ルール-構成](../../power-pivot-sharepoint/configure-power-pivot-health-rules.md)」を参照してください。  
  
```powershell
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -Like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
Name                          Enabled Summary  
----                          ------- -------           
SecondaryLogonHealthRule         True PowerPivot:  Secondary Logon service (seclogon) is disabled  
DataRefreshTimerJobHealthRule    True PowerPivot: The PowerPivot Data Refresh timer job is disabled.  
ASUsageLoadHealthRule            True PowerPivot: The ratio of load events to connections is too high.  
ASMiniDumpHealthRule             True PowerPivot: One or more minidump files were found in the Logs directory, indicating a program crash  
ASUsageCubeRule                  True PowerPivot: Usage data is not getting updated at the expected frequency.  
ASADOMDNETHealthRule             True PowerPivot: ADOMD.NET is not installed on a standalone WFE that is configured for central admin  
MidTierAcctReadPermissionRule    True PowerPivot: MidTier process account should have 'Full Read' permission on all associated SPWebApplications.  
```  
  
##  <a name="bkmk_logs"></a>Windows と ULS のログ  
 **Windows イベントログ**  
  
 次のコマンドは、SharePoint モードの [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のインスタンスに関連するイベントの Windows イベント ログを検索します。 イベントの無効化やイベントレベルの変更の詳細については、「 [SharePoint ログファイルと診断ログの構成と表示」 &#40;PowerPivot for SharePoint&#41;](../../power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)を参照してください。  
  
 **サービス名:** MSOLAP $ POWERPIVOT  
  
 **Windows サービスの表示名:** SQL Server Analysis Services (POWERPIVOT)  
  
```powershell
Get-EventLog "application" | Where-Object {$_.source -Like "msolap`$powerpivot*"}  | Select timegenerated, entrytype , source, message | Format-Table -property * -AutoSize | Out-Default  
```
  
```Output
TimeGenerated           EntryType Source            Message  
-------------           --------- ------            -------  
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.  
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Service started. Microsoft SQL Server Analysis Services 64 Bit Evaluation (x64) RTM 12.0.1997.5.  
4/16/2014 1:45:18 PM  Information MSOLAP$POWERPIVOT The flight recorder was started.  
4/14/2014 6:45:37 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.  
```  
  
 **SharePoint ULS ログ、過去48時間**  
  
 次のコマンドは、過去 48 時間に作成された ULS ログから [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] メッセージを返します。 addhours パラメーターは必要に応じて調整してください。  
  
```powershell
Get-SPLogEvent -StartTime(Get-Date).AddHours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | Select timestamp, area, category, eventid,level, message | Format-Table -Property * -AutoSize | Out-Default  
```  
  
 次のコマンドのバリエーションは、 **データ更新** カテゴリのログ イベントのみを返します。  
  
```powershell
Get-SPLogEvent -starttime(Get-Date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | Select timestamp, area, category, eventid, level, correlation, message  
```
  
```Output
Timestamp   : 4/14/2014 7:15:01 PM  
Area        : PowerPivot Service  
Category    : Data Refresh  
EventID     : 43  
Level       : High  
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77  
Message     : The following error occured when working with the service application, Default PowerPivot Service Application. Skipping the service application..  
  
Timestamp   : 4/14/2014 7:15:02 PM  
Area        : PowerPivot Service  
Category    : Data Refresh  
EventID     : 99  
Level       : High  
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77  
Message     : EXCEPTION: System.TimeoutException: The request channel timed out while waiting for a reply after 00:00:47.0625313. Increase the timeout value passed to   
              the call to Request or increase the SendTimeout value on the Binding. The time allotted to this operation may have been a portion of a longer timeout.   
              ---> System.TimeoutException: The HTTP request to 'http://localhost:32843/SecurityTokenServiceApplication/securitytoken.svc/actas' has exceeded the   
              allotted timeout of 00:00:54.5930000. The time allotted to this operation may have been a portion of a longer timeout. ---> System.Net.WebException: The   
              operation has timed out     at System.Net.HttpWebRequest.GetResponse()     at   
              System.ServiceModel.Channels.HttpChannelFactory`1.HttpRequestChannel.HttpChannelRequest.WaitForReply(TimeSpan timeout...  
```  
  
##  <a name="bkmk_msolap"></a>MSOLAP プロバイダー  
 プロバイダーが MSOLAP プロバイダーであることを確認します。 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]および[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]には MSOLAP. 5 が必要です。  
  
```powershell
$excelApp = Get-SPExcelServiceApplication  
Get-SPExcelDataProvider -ExcelServiceApplication $excelApp | Select providerid, providertype, description | Where {$_.providerid -like "msolap*" } | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
ProviderId ProviderType Description  
---------- ------------ -----------  
MSOLAP     Oledb        Microsoft OLE DB Provider for OLAP Services       
MSOLAP.3   Oledb        Microsoft OLE DB Provider for OLAP Services 9.0   
MSOLAP.4   Oledb        Microsoft OLE DB Provider for OLAP Services 10.0  
MSOLAP.5   Oledb        Microsoft OLE DB Provider for OLAP Services 11.0  
```  
  
 詳細については、「 [SharePoint サーバーへの Analysis Services OLE DB プロバイダーのインストール](../../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) 」および「 [Excel Services で信頼できるデータ プロバイダーとして MSOLAP.5 を追加](https://technet.microsoft.com/library/hh758436.aspx)」を参照してください。  
  
##  <a name="bkmk_adomd"></a>ADOMD.Net クライアントライブラリ  
  
```powershell
Get-WMIObject -Class win32_product | Where-Object {$_.name -Like "*ado*"} | Select name, version, vendor | Format-Table -Property * -AutoSize | out-default  
```
  
```Output
name                                                  version      vendor  
----                                                  -------      ------  
Microsoft SQL Server 2008 Analysis Services ADOMD.NET 10.1.2531.0  Microsoft Corporation  
Microsoft SQL Server 2005 Analysis Services ADOMD.NET 9.00.1399.06 Microsoft Corporation  
```  
  
 詳細については、「 [サーバーの全体管理を実行している Web フロントエンド サーバーに ADOMD.NET をインストールする方法](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)」を参照してください。  
  
##  <a name="bkmk_health_collection"></a>正常性データの収集ルール  
 
  **"Status"** がオンラインであり、 **"Enabled"** が True であることを確認します。  
  
```powershell
Get-SPUsageDefinition | Select name, status, enabled, tablename, DaysToKeepDetailedData | Where {$_.name -Like "powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
Name                         Status Enabled TableName                   DaysToKeepDetailedData  
----                         ------ ------- ---------                   ----------------------  
PowerPivot Connections       OnlineTrue AnalysisServicesConnections  14  
PowerPivot Load Data Usage   Online    True AnalysisServicesLoads                           14  
PowerPivot Query Usage       Online    True AnalysisServicesRequests                        14  
PowerPivot Unload Data Usage Online    True AnalysisServicesUnloads                         14  
```  
  
 詳細については、「 [PowerPivot Usage Data Collection](../../power-pivot-sharepoint/power-pivot-usage-data-collection.md)」を参照してください。  
  
##  <a name="bkmk_solutions"></a>'83'5c  
 他のコンポーネントがオンラインになっている場合は、ソリューションの確認をスキップできます。 ただし正常性ルールがない場合は、2 つのソリューションが存在し表示されることを確認します。また、2 つの PowerPivot ソリューションが **オンライン** になっており、 **配置済み**であることを確認します。  
  
```powershell
Get-SPSolution | Select name, status, deployed, DeploymentState, DeployedServers | Where {$_.Name -Like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
```  
  
SharePoint 2013:
  
```Output
Name                                 Status Deployed        DeploymentState DeployedServers  
----                                 ------ --------        --------------- ---------------  
powerpivotfarm14solution.wsp         Online     True         GlobalDeployed {UETESTA00}  
powerpivotfarmsolution.wsp           Online     True         GlobalDeployed {UETESTA00}  
powerpivotwebapplicationsolution.wsp Online     True WebApplicationDeployed {UETESTA00}  
```  
  
SharePoint 2010:
  
```Output
Name                 Status Deployed        DeploymentState DeployedServers   
----                 ------ --------        --------------- ---------------   
powerpivotfarm.wsp   Online     True         GlobalDeployed {uesql11spoint2}  
powerpivotwebapp.wsp Online     True WebApplicationDeployed {uesql11spoint2}  
```  
  
 SharePoint ソリューションを配置する方法については、「 [ソリューション パッケージを展開する (SharePoint Server 2010)](https://technet.microsoft.com/library/cc262995\(v=office.14\).aspx)」を参照してください。  
  
##  <a name="bkmk_manual"></a>手動による検証手順  
 このセクションでは、PowerShell コマンドレットでは実行できない検証手順について説明します。  
  
 **定期データ更新:**[更新スケジュールを構成する (ブックの更新**も可能な限り早く更新**する)。  詳細については、「[データ更新のスケジュール」と「Windows 認証をサポートしていないデータソース &#40;PowerPivot for SharePoint&#41;](../../power-pivot-sharepoint/schedule-data-refresh-and-data-sources-no-windows-authentication.md)」の「データ更新の検証」セクションを参照してください。  
  
##  <a name="bkmk_more_resources"></a>その他のリソース  
 [Windows PowerShell の Web サーバー (IIS) 管理コマンドレット](https://technet.microsoft.com/library/ee790599.aspx)。  
  
 [SharePoint でサービス、IIS サイト、アプリケーションプールの状態を確認するための PowerShell](https://gallery.technet.microsoft.com/office/PowerShell-to-check-a6ed72a0)。  
  
 [Windows PowerShell for SharePoint 2013 リファレンス](https://technet.microsoft.com/library/ee890108\(v=office.15\).aspx)  
  
 [Windows PowerShell for SharePoint Foundation 2010 リファレンス](https://technet.microsoft.com/library/ee890105\(v=office.14\).aspx)  
  
 [Windows PowerShell を使用した Excel Services の管理 (SharePoint Server 2010)](https://technet.microsoft.com/library/ff191201\(v=office.14\).aspx)  
  
 [SQL Server セットアップログファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
 [Get EvenLog コマンドレットを使用する](https://technet.microsoft.com/library/ee176846.aspx)  
  
##  <a name="bkmk_full_script"></a>完全な PowerShell スクリプト  
 次のスクリプトには、上記の各セクションのコマンドがすべて含まれています。 スクリプトでは、このトピックに示した順序でコマンドが実行されます。 またスクリプトには、このトピックで説明したコマンドのバリエーションが含まれています。追加のフィルターが必要になった場合に、状況に応じて使用してください。 バリエーションは、コメント文字 (#) によって無効になっています。 スクリプトには、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の SharePoint モードを確認するためのステートメントも含まれています。 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ステートメントは、コメント文字 (#) によって無効になっています。  
  
```powershell
# This script audits services related to PowerPivot for SharePoint  
$starttime = Get-Date  
write-host -foregroundcolor DarkGray StartTime $starttime
  
Write-Host  "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0  
  
Write-Host -ForegroundColor Green "Analysis Services Windows Service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-Service | Select name, displayname, status | Where {$_.Name -eq "msolap`$powerpivot"} | Format-Table -Property * -AutoSize | Out-Default  
  
Write-Host -ForegroundColor Green "PowerPivotEngineService and PowerPivotSystemService"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
Get-PowerPivotSystemService | Select typename, status, applications, farm | Format-Table -property * -AutoSize | Out-Default  
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section  
#Get-PowerPivotSystemService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default  
  
Get-PowerPivotEngineService | Select typename, status, name, instances, farm | Format-Table -property * -AutoSize | Out-Default  
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section  
#Get-PowerPivotEngineService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default  

#Write-Host -ForegroundColor Green "Service Instances - optional if you want to associate services with the server"  
#Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#Get-SPServiceInstance | select typename, status, server, service, instance | where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*excel*" -or $_.TypeName -like "*Analysis Services*"} | format-table -property * -autosize | out-default  
#Get-PowerPivotEngineServiceInstance  | select typename, ASServername, status, server, service, instance  
#Get-PowerPivotSystemServiceInstance  | select typename, ASSServerName, status, server, service, instance  

Write-Host -ForegroundColor Green "PowerPivot And Excel Service Applications"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-PowerPivotServiceApplication | Select typename,name, status, unattendedaccount, applicationpool, farm, database
Get-SPExcelServiceApplication | Select typename,  DisplayName, status
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivot Service Application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
# the following assumes there is only 1 PowerPivot Service Application, and returns that applicaitons pool name.  if you have more than one, use the 2nd version  
$poolname = [string](Get-PowerPivotServiceApplication | Select -Property applicationpool)  
$position = $poolname.lastindexof("=")  
$poolname = $poolname.substring($position+1)  
$poolname = $poolname.substring(0,$poolname.length-1)  
Get-SPServiceApplicationPool | Select name, status, processaccountname, id | Where {$_.Name -eq $poolname} | Format-Table -Property * -AutoSize | Out-Default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivot and Excel Service Application Proxy"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPServiceApplicationProxy |  Select typename, status, unattendedaccount, displayname | Where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*excel services*"} | Format-Table -Property * -AutoSize | Out-Default  
#Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*Reporting Services*" -or $_.TypeName -like "*excel services*"} | format-table -property * -autosize | out-default  

Write-Host -ForegroundColor Green "DATABASES"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPDatabase | Select name, status, server, typename | Where {$_.TypeName -eq "content database" -or $_.TypeName -like "*Gemini*"} | Format-Table -Property * -AutoSize | Out-Default  
#Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq "content database" -or $_.TypeName -like "*Gemini*" -or $_.TypeName -like "*ReportingServices*"}

Write-Host -ForegroundColor Green "features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPFeature | Select displayname, status, scope, farm | Where {$_.displayName -like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
#Get-SPFeature | select displayname, status, scope, farm | where {$_.displayName -like "*powerpivot*" -or $_.displayName -like "*ReportServer*"}  | format-table -property * -autosize | out-default  

Write-Host -ForegroundColor Green "Timer Jobs (Job Definitions) -- list is the same as seen in the 'Review timer job definitions' section of the management dashboard"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPTimerJob | Where {$_.service -like "*power*" -or $_.service -like "*mid*"} | Select status, displayname, LastRunTime, service | Format-Table -Property * -AutoSize | Out-Default  

Write-Host -ForegroundColor Green "health rules"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -Like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default  
  
$time = Get-Date  
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time  

Write-Host -ForegroundColor Green "Windows Event Log data MSSQL$POWERPIVOT and "  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*"}  | Select timegenerated, entrytype , source, message | Format-Table -Property * -autosize | Out-Default  
#The following is the same command but with the Inforamtion events filtered out.  
#Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*" -and ($_.entrytype -match "error" -or $_.entrytype -match "critical" -or $_.entrytype -match "warning")}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "ULS Log data"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPLogEvent -StartTime(Get-Date).AddHours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | Select timestamp, area, category, eventid, level, correlation, message | Format-Table -Property * -AutoSize | Out-Default  
#the following example filters for the category 'data refresh'  
#Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | select timestamp, area, category, eventid, level, correlation, message  
  
$time = Get-Date  
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time  

Write-Host -ForegroundColor Green "MSOLAP data provider for Excel Servivces, service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
$excelApp = Get-SPExcelServiceApplication  
Get-SPExcelDataProvider -ExcelServiceApplication $excelApp | Select providerid, providertype, description | Where {$_.providerid -like "msolap*" } | Format-Table -Property * -AutoSize | Out-Default  
  
Write-Host -ForegroundColor Green "ADOMD.net client library"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-WMIObject -Class win32_product | Where-Object {$_.name -like "*ado*"} | Select name, version, vendor | Format-Table -Property * -AutoSize | Out-Default  
  
Write-Host -ForegroundColor Green "Usage Data Rules"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPUsageDefinition | Select name, status, enabled, tablename, DaysToKeepDetailedData | Where {$_.name -like "powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
  
Write-Host -ForegroundColor Green "Solutions"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPSolution | Select name, status, deployed, DeploymentState, DeployedServers | Where {$_.Name -like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
  
$time = Get-Date  
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time
