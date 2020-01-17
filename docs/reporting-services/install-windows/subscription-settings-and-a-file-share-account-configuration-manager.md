---
title: サブスクリプション設定とファイル共有アカウント (構成マネージャー) | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
f1_keywords:
- SQL13.rsconfigtool.subscriptionsettings.F1
ms.assetid: fefa7bdb-b5f2-4db7-b91c-b58869279f3c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9e8dfea342f4545313035869f8c2e12367e62aed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651970"
---
# <a name="subscription-settings-and-a-file-share-account-configuration-manager"></a>サブスクリプション設定とファイル共有アカウント (構成マネージャー)
  **構成マネージャーの** [サブスクリプションの設定] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ページを使用すると、ネイティブ モードのレポート サーバーとファイル共有のサブスクリプションのファイル共有アカウントを構成できます。 ファイル共有アカウントでは、複数のサブスクリプションで 1 つの資格情報のセットを使用し、ファイル共有にレポートを配信することができます。 資格情報の変更が必要なときは、ファイル共有アカウントの変更を構成します。個々のサブスクリプションは更新しません。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のファイル共有サブスクリプションには、2 つのワークフローがあります。  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] リリースから、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理者が構成した 1 つのファイル共有アカウントから、1 つ以上 (多数も可能) のサブスクリプションを使用することが可能になりました。 **[ファイル共有アカウントの指定]** を構成し、個々のサブスクリプションの構成ページで、ユーザーが **[ファイル共有アカウントを使用]** を選択します。  
  
-   個々のサブスクリプションに、宛先のファイル共有の資格情報を具体的に構成します。  
  
-   一部のファイル共有のサブスクリプションでは中枢のファイル共有アカウントを使用し、他のサブスクリプションでは特定の資格情報を使用する、2 つの方法を混在させることも可能です。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード。  
  
## <a name="specify-a-file-share-account"></a>[ファイル共有アカウントの指定]  
 このオプションが選択されている場合、レポート サーバーからファイル共有にアクセスするために使用するアカウントを提供できます。 ファイル共有アカウントを構成すると、ファイル共有にレポートを配信するよう構成されているすべてのサブスクリプションから、すべてのユーザーがアカウントを選択できます。 このオプションが選択されていない場合、どのサブスクリプションでもファイル共有アカウントを使用 **できません** 。  
  
 ファイル共有アカウントとして構成するアカウントには、ファイル共有の配信にユーザーが使用するすべてのファイル共有への読み取りおよび書き込みアクセス許可があることを確認する必要があることに注意してください。  
  
 次は、ファイル共有の配信が構成されているサブスクリプションでユーザーに表示されるものの画像です。 ファイル共有アカウントが構成されていない場合、 **[ファイル共有アカウントを使用]** は無効です。  
  
 ![構成マネージャーのファイル共有アカウント](../../reporting-services/install-windows/media/ssrs-fileshare-account.png "構成マネージャーのファイル共有アカウント")  
  
## <a name="prevent-privilege-escalation-or-elevated-privileges"></a>権限の昇格や昇格された権限の回避  
  
> [!IMPORTANT]
> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アカウントはサブスクリプションの配信を制御したり、ファイル共有サブスクリプションに使用するアカウントと通信したりします。 Windows のセキュリティ機能では、1) [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アカウントと 2) ファイル共有アカウントに使用されるアカウントの組み合わせを制限します。 たとえば、ビルトイン オペレーティング システム アカウントが、ファイル共有アカウントに使用される場合、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アカウントは偽装アクセス許可を持つ別のサービス アカウントである必要があります。 ファイル共有アカウントとパスワードが明示的に構成されている場合、ファイル共有アカウントには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスを実行しているコンピューターにログオンする権限が必要です。 ファイル共有アカウントに必要なアクセス許可がない場合、次のようなエラー メッセージでファイル共有アカウントを使用しているサブスクリプションは失敗します。  
>   
>  `"Failure writing file {file} : An impersonation error occurred using the security context of the current user."`  
  
## <a name="powershell-sample-to-audit-use-of-the-file-share-account"></a>ファイル共有アカウントの使用の監査を実行する PowerShell のサンプル  
 次の Windows PowerShell スクリプトを実行すると、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ファイル共有アカウント **を使用するよう構成されている**のサブスクリプションがすべて列挙されます。 レポート サーバーに適切した値に、 `SERVERNAME` を更新します。  
  
```  
# get all file share subscriptions using the default file share account  
$extensionNameMatch = "Report Server FileShare"  
$extensionSettingMatch = "DEFAULTCREDENTIALS"  
$valueMatch = "True"  
  
# filter for subscriptions that have a given extension setting  
filter script:extensionSettingFilter  
{  
    # subscription must match the extension name  
    if($_.DeliverySettings.Extension -eq $extensionNameMatch)  
    {  
        # locate the extension parameter of interest  
        ForEach($extensionParameter in $_.DeliverySettings.ParameterValues)  
        {  
            # if the setting has the desired value, return the subscription  
            if($extensionParameter.Name -eq $extensionSettingMatch -and $extensionParameter.Value -eq $valueMatch)  
            {  
                $_  
                break  
            }  
        }  
    }  
}  
  
$rs2010 = New-WebServiceProxy -Uri "https:// SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
  
Write-Host "----- File share subscriptions using the default file share account ----";  
Write-Host "-------------------------------------------------------------------------- ";  
$subscriptions | extensionSettingFilter | select report, owner, status, lastexecuted, description, subscriptionid | format-table -auto  
  
```  
  
 スクリプトの出力は、次のようになります。  
  
 `----- File share subscriptions using the default file share account ----`  
  
 `-----------------------------------------------------------------------------------------------------`  
  
 `Report                    Owner          Status   LastExecuted         SubscriptionID`  
  
 `------------------------  -------------- -------- -------------------- ------------------------------------`  
  
 `Aworks_sales_by_territory DOMAIN\UserName Disabled 10/5/2014 1:04:04 PM e843bc2b-023e-45a3-ba23-22f9dc9a0934`  
  
## <a name="see-also"></a>参照  
 [Reporting Services でのファイル共有の配信](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)   
 [ネイティブ モード レポート サーバーのサブスクリプションの作成と管理](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)
  
  
