---
title: Reporting Services SharePoint モード用の PowerShell コマンドレット | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 3e415fee08a9723419c7d8a4258fc88670c5e262
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892403"
---
# <a name="powershell-cmdlets-for-reporting-services-sharepoint-mode"></a>Reporting Services SharePoint モード用の PowerShell コマンドレット

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server 2016 Reporting Services SharePoint モードをインストールすると、SharePoint モードのレポート サーバーをサポートするために PowerShell コマンドレットがインストールされます。 コマンドレットは 3 つのカテゴリの機能をサポートしています。  
  
-   Reporting Services SharePoint 共有サービスおよびプロキシのインストール。  
  
-   Reporting Services サービス アプリケーションおよび関連付けられたプロキシのプロビジョニングと管理。  
  
-   Reporting Services 機能 (拡張機能や暗号化キーなど) の管理。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

## <a name="cmdlet-summary"></a>コマンドレットの概要

 コマンドレットを実行するには、SharePoint 管理シェルを開く必要があります。 Microsoft Windows に付属しているグラフィカル ユーザー インターフェイス エディター ( **Windows PowerShell Integrated Scripting Environment (ISE)** ) を使用することもできます。 詳細については、「 [Windows Server での Windows PowerShell の開始](https://docs.microsoft.com/powershell/scripting/getting-started/starting-windows-powershell)) を使用することもできます。 次のコマンドレット概要では、サービス アプリケーション "データベース" への参照は、Reporting Services サービス アプリケーションによって作成および使用されたすべてのデータベースを参照します。 これには、構成、警告、および一時データベースが含まれます。  
  
 PowerShell の例を入力すると、次のようなエラー メッセージが表示されます。  
  
-   Install-SPRSService : 用語 'Install-SPRSService' は、  
    コマンドレット、関数、スクリプト ファイル、または操作可能なプログラムの名前として認識されません。 名前が正しく記述されていることを確認し、パスが含まれている場合はそのパスが正しいことを確認してから、再試行してください。  
  
 次のいずれかの問題が発生しています。  
  
-   Reporting Services SharePoint モードがインストールされていないため、Reporting Services コマンドレットがインストールされていません。  
  
-   SharePoint 管理シェルでなく、Windows PowerShell または Windows PowerShell ISE で PowerShell コマンドを実行しました。 SharePoint 管理シェルを使用するか、次のコマンドで SharePoint スナップインを Windows PowerShell ウィンドウに追加します。  
  
    ```  
    Add-PSSnapin Microsoft.SharePoint.PowerShell  
    ```  
  
 詳細については、「 [Windows PowerShell を使用して SharePoint 2013 を管理する](https://technet.microsoft.com/library/ee806878.aspx)) を使用することもできます。  
  
### <a name="open-the-sharepoint-management-shell-and-run-cmdlets"></a>SharePoint 管理シェルを開いてコマンドレットを実行する
  
1.  **[スタート]** ボタンをクリックします。  
  
2.  **[Microsoft SharePoint 製品]** グループをクリックします。  
  
3.  **[SharePoint 管理シェル]** をクリックします。  
  
 コマンドレットのコマンド ライン ヘルプを表示するには、PowerShell のコマンド プロンプトで 'Get-Help' コマンドを使用します。 例:  
  
 `Get-Help Get-SPRSServiceApplicationServers`  
  
##  <a name="shared-service-and-proxy-cmdlets"></a>共有サービスとプロキシ コマンドレット

 次の表に、Reporting Services SharePoint 共有サービス用の PowerShell コマンドレットを示します。  
  
|コマンドレット|[説明]|  
|------------|-----------------|  
|Install-SPRSService|Reporting Services 共有サービスをインストールして登録するか、アンインストールします。 この操作は、SharePoint モードの SQL Server Reporting Services がインストールされているコンピューター上でのみ行うことができます。 インストールの場合は、以下の 2 つの操作が行われます。<br /><br /> \- Reporting Services サービスがファームにインストールされます。<br /><br /> \- Reporting Services サービス インスタンスが現在のコンピューターにインストールされます。<br /><br /> アンインストールの場合は、以下の 2 つの操作が行われます。<br /><br /> \- Reporting Services サービスが現在のコンピューターからアンインストールされます。<br /><br /> \- Reporting Services サービスがファームからアンインストールされます。<br /><br /> <br /><br /> Reporting Services サービスがインストールされているファーム内に他のコンピューターが存在する場合や Reporting Services サービス アプリケーションがファーム内で引き続き実行されている場合は、警告メッセージが表示されます。|  
|Install-SPRSServiceProxy|SharePoint ファーム内で Reporting Services サービス プロキシをインストールして登録するか、アンインストールします。|  
|Get-SPRSProxyUrl|Reporting Services サービスにアクセスするための URL を取得します。|  
|Get-SPRSServiceApplicationServers|Reporting Services 共有サービスのインストールを含む、ローカル SharePoint ファーム内のすべてのサーバーを取得します。 このコマンドレットは、どのサーバーで共有サービスを実行していてアップグレードする必要があるかを調べる目的に適しており、Reporting Services のアップグレードに役立ちます。|  
  
## <a name="service-application-and-proxy-cmdlets"></a>サービス アプリケーションとプロキシ コマンドレット

 次の表には、Reporting Services サービス アプリケーションとそれらに関連付けられたプロキシ用の PowerShell コマンドレットが含まれています。  
  
|コマンドレット|[説明]|  
|------------|-----------------|  
|Get-SPRSServiceApplication|1 つ以上の Reporting Services サービス アプリケーション オブジェクトを取得します。|  
|New-SPRSServiceApplication|新しい Reporting Services サービス アプリケーションと、それに関連付けられたデータベースを作成します。<br /><br /> LogonType パラメーター: レポート サーバーが、レポート サーバー データベースへのアクセスに SSRS Application Pool アカウントと SQL Server ログインのどちらを使用するかを指定します。 有効な値は、<br /><br /> 0 Windows 認証<br /><br /> 1 SQL Server<br /><br /> 2 アプリケーション プール アカウント (既定)|  
|Remove-SPRSServiceApplication|指定した Reporting Services サービス アプリケーションを削除します。 これを実行すると、関連付けられたデータベースも削除されます。|  
|Set-SPRSServiceApplication|既存の Reporting Services サービス アプリケーションのプロパティを編集します。|  
|New-SPRSServiceApplicationProxy|新しい Reporting Services サービス アプリケーション プロキシを作成します。|  
|Get-SPRSServiceApplicationProxy|1 つ以上の Reporting Services サービス アプリケーション プロキシを取得します。|  
|Dismount-SPRSDatabase|Reporting Services サービス アプリケーションのサービス アプリケーション データベースをマウント解除します。|  
|Remove-SPRSDatabase|Reporting Services サービス アプリケーション用のサービス アプリケーション データベースを削除します。|  
|Set-SPRSDatabase|Reporting Services サービス アプリケーションに関連付けられたデータベースのプロパティを設定します。|  
|Mount-SPRSDatabase|Reporting Services サービス アプリケーション用のデータベースをマウントします。|  
|New-SPRSDatabase|指定した Reporting Services サービス アプリケーション用の新しいサービス アプリケーション データベースを作成します。|  
|Get-SPRSDatabaseCreationScript|Reporting Services サービス アプリケーション用に、データベース作成スクリプトを画面に出力します。 その後、SQL Server Management Studio でスクリプトを実行できます。|  
|Get-SPRSDatabase|1 つ以上の Reporting Services サービス アプリケーション データベースを取得します。 Set-SPRSDatabase コマンドレットを使用して `querytimeout`などのプロパティを変更できるように、コマンドを使用してサービス アプリケーション データベースの ID を取得します。 このトピックの例「 [Reporting Service アプリケーション データベースのプロパティの取得と設定](#get-and-set-properties-of-the-reporting-service-application-database)」を参照してください。|  
|Get-SPRSDatabaseRightsScript|Reporting Services サービス アプリケーション用に、データベース権限スクリプトを画面に出力します。 これを実行すると、対象のユーザーとデータベースの入力を求めるプロンプトが表示され、権限を変更するための Transact-SQL が返されます。 その後、SQL Server Management Studio でこのスクリプトを実行できます。|  
|Get-SPRSDatabaseUpgradeScript|データベース アップグレード スクリプトを画面に出力します。 このスクリプトは、Reporting Services サービス アプリケーション データベースを、現在の Reporting Services インストールのデータベース バージョンにアップグレードします。|  
  
## <a name="reporting-services-custom-functionality-cmdlets"></a>Reporting Services カスタム機能コマンドレット
  
|コマンドレット|[説明]|  
|------------|-----------------|  
|Update-SPRSEncryptionKey|指定した Reporting Services サービス アプリケーションの暗号化キーを更新し、そのデータを再暗号化します。|  
|Restore-SPRSEncryptionKey|以前にバックアップした、Reporting Services サービス アプリケーションの暗号化キーを復元します。|  
|Remove-SPRSEncryptedData|指定した Reporting Services サービス アプリケーションの暗号化されたデータを削除します。|  
|Backup-SPRSEncryptionKey|指定した Reporting Services サービス アプリケーションの暗号化キーをバックアップします。|  
|New-SPRSExtension|新しい拡張機能を Reporting Services サービス アプリケーションに登録します。|  
|Set-SPRSExtension|既存の Reporting Services 拡張機能のプロパティを設定します。|  
|Remove-SPRSExtension|Reporting Services サービス アプリケーションから拡張機能を削除します。|  
|Get-SPRSExtension|Reporting Services サービス アプリケーションの 1 つ以上の Reporting Services 拡張機能を取得します。<br /><br /> 有効な値は、<br /><br /> <br /><br /> Delivery<br /><br /> DeliveryUI<br /><br /> Render<br /><br /> data<br /><br /> Security<br /><br /> [認証]<br /><br /> EventProcessing<br /><br /> ReportItems<br /><br /> デザイナー<br /><br /> ReportItemDesigner<br /><br /> ReportItemConverter<br /><br /> ReportDefinitionCustomization|  
|Get-SPRSSite|"ReportingService" 機能が有効になっているかどうかに基づいて SharePoint サイトを取得します。 既定では、"ReportingService" 機能が有効になっているサイトが返されます。|  
  
## <a name="basic-samples"></a>基本的なサンプル

 名前に 'SPRS' を含んでいるコマンドレットの一覧を返します。 これは Reporting Services コマンドレットの完全な一覧になります。  
  
```  
Get-command -noun *SPRS*  
```  
  
 または、より詳細な情報を使用して、commandlist.txt という名前のテキスト ファイルにパイプします。  
  
```  
Get-command -noun *SPRS* | Select name, definition | Format-List | Out-File c:\commandlist.txt  
```  
  
 Reporting Services SharePoint サービスおよびサービス プロキシをインストールします。  
  
```  
Install-SPRSService  
```  
  
```  
Install-SPRSServiceProxy  
```  
  
 Reporting Services サービスの開始  
  
```  
get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
```  
  
 SharePoint 管理シェルから次のコマンドを入力すると、フィルター処理された行のリストがログ ファイルから返されます。 このコマンドを実行すると、"ssrscustomactionerror" を含む行がフィルター処理されます。 この例では、rssharepoint.msi のインストール時に作成されたログ ファイルが検索対象となっています。  
  
```  
Get-content -path C:\Users\testuser\AppData\Local\Temp\rs_sp_0.log | select-string "ssrscustomactionerror"  
```  
  
## <a name="detailed-samples"></a>詳細なサンプル

 次のサンプルに加えて、「[手順 1 - 4 に対応する Windows PowerShell スクリプト](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_full_script)」の「Windows PowerShell スクリプト」を参照してください。  
  
### <a name="create-a-reporting-services-service-application-and-proxy"></a>Reporting Services サービス アプリケーションとプロキシの作成

 このサンプル スクリプトは次のタスクを完了します。  
  
1.  Reporting Services サービス アプリケーションとプロキシを作成する。 このスクリプトは、"My App Pool" というアプリケーション プールが既に存在することを前提としています。  
  
2.  作成したプロキシを既定のプロキシ グループに追加する。  
  
3.  ポート 80 の Web アプリケーションのコンテンツ データベースに、サービス アプリケーション アクセス権を付与する。 このスクリプトは、サイト `https://sitename` が既に存在することを前提としています。  
  
```  
# Create service application and service application proxy  
$appPool = Get-SPServiceApplicationPool "My App Pool"  
$serviceApp = New-SPRSServiceApplication "My RS Service App" -ApplicationPool $appPool  
$serviceAppProxy = New-SPRSServiceApplicationProxy -Name "My RS Service App Proxy" -ServiceApplication $serviceApp  
  
# Add service application proxy to default proxy group.  Any web application that uses the default proxy group will now be able to use this service application.  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $serviceAppProxy  
  
# Grant application pool account access to the port 80 web application's content database.  
$webApp = Get-SPWebApplication "https://sitename"  
$appPoolAccountName = $appPool.ProcessAccount.LookupName()  
$webApp.GrantAccessToProcessIdentity($appPoolAccountName)  
  
```  
  
### <a name="review-and-update-a-reporting-services-delivery-extension"></a>Reporting Services 配信拡張機能の確認と更新

 次の PowerShell スクリプトの例では、 `My RS Service App`という名前のサービス アプリケーションについて、レポート サーバーの電子メール配信拡張機能の構成を更新します。 SMTP サーバー (`<email server name>`) と差出人の電子メール別名 (`<your FROM email address>`) の値を更新します。  
  
```  
$app=get-sprsserviceapplication -Name "My RS Service App"  
$emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
$emailXml = [xml]$emailCfg   
$emailXml.SelectSingleNode("//SMTPServer").InnerText = "<email server name>"  
$emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
$emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
$emailXml.SelectSingleNode("//From").InnerText = '<your FROM email address>'  
Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
```  
  
 上の例で、サービス アプリケーションの正確な名前がわからない場合は、最初のステートメントを書き換えて、サービス アプリケーションを部分名検索に基づいて取得することもできます。 例:  
  
```  
$app=get-sprsserviceapplication | where {$_.name -like " ssrs_testapp *"}  
```  
  
 次のスクリプトは、"Reporting Services Application" という名前のサービス アプリケーションについて、レポート サーバーの電子メール配信拡張機能の現在の構成値を返します。 最初のステップでは、"My RS Service App" という名前のサービス アプリケーションのオブジェクトに、変数 $app の値が設定されます。  
  
 2 番目のステートメントは、変数 $app 内のサービス アプリケーション オブジェクト用の "レポート サーバー電子メール" 配信拡張機能を取得し、configurationXML を選択します。  
  
```  
$app=get-sprsserviceapplication -Name "Reporting Services Application"  
Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
 上の 2 つのステートメントを次のように書き直して 1 つのステートメントにすることもできます。  
  
```  
get-sprsserviceapplication -Name "Reporting Services Application" | Get-SPRSExtension -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
### <a name="get-and-set-properties-of-the-reporting-service-application-database"></a>Reporting Service アプリケーション データベースのプロパティの取得と設定

 次の例では、set コマンドに指定するデータベースの GUID (ID) を確認できるように、最初にデータベースとプロパティの一覧を返します。 プロパティの一覧については、「 `Get-SPRSDatabase | format-list`」を参照してください。  
  
```  
get-SPRSDatabase | select id, querytimeout,connectiontimeout, status, server, ServiceInstance   
```  
  
 出力の例を次に示します。 変更するデータベースの ID を確認し、SET コマンドレットでその ID を使用します。  
  
-   `Id                : 56f8d1bc-cb04-44cf-bd41-a873643c5a14`  
  
     `QueryTimeout      : 120`  
  
     `ConnectionTimeout : 15`  
  
     `Status            : Online`  
  
     `Server            : SPServer Name=uetestb01`  
  
     `ServiceInstance   : SPDatabaseServiceInstance`  
  
```  
Set-SPRSDatabase -identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 -QueryTimeout 300  
```  
  
 値が設定されていることを確認するには、もう一度 GET コマンドレットを実行します。  
  
```  
Get-SPRSDatabase -identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 | select id, querytimeout,connectiontimeout, status, server, ServiceInstance  
```  
  
### <a name="list-reporting-services-data-extensions"></a>Reporting Services データ拡張機能の一覧表示

 次の例では、各 Reporting Services サービス アプリケーションの間をループし、それぞれの現在のデータ拡張機能を一覧表示します。  
  
```  
$apps = Get-SPRSServiceApplication  
foreach ($app in $apps)   
{  
Write-host -ForegroundColor "yellow" Service App Name $app.Name  
Get-SPRSExtension -identity $app -ExtensionType "Data" | select name,extensiontype | Format-Table -AutoSize  
}  
```  
  
 **出力例:**  
  
-   `Name           ExtensionType`  
  
     `----           -------------`  
  
     `SQL                     Data`  
  
     `SQLAZURE                Data`  
  
     `SQLPDW                  Data`  
  
     `OLEDB                   Data`  
  
     `OLEDB-MD                Data`  
  
     `ORACLE                  Data`  
  
     `ODBC                    Data`  
  
     `XML                     Data`  
  
     `SHAREPOINTLIST          Data`  
  
### <a name="change-and-list-reporting-services-subscription-owners"></a>Reporting Services サブスクリプション所有者の変更と一覧表示

 「[PowerShell を使用した Reporting Services サブスクリプション所有者の変更および一覧表示とサブスクリプションの実行](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)」を参照してください。  
  
## <a name="next-steps"></a>次の手順

[PowerShell を使用した Reporting Services サブスクリプション所有者の変更および一覧表示とサブスクリプションの実行](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
[チェック リスト: PowerShell を使用して Power Pivot for SharePoint を確認する](https://docs.microsoft.com/analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint)   
[SQL Server PowerShell のヘルプの参照](../../relational-databases/scripting/get-help-sql-server-powershell.md)   

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
