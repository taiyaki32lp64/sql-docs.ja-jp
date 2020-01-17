---
title: Reporting Services の SharePoint サービスとサービス アプリケーション | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 1dfe62ba964b05f069009b51ddf62f376c12c906
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580533"
---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Reporting Services の SharePoint サービスとサービス アプリケーション

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Reporting Services SharePoint モードは、SharePoint サービス アーキテクチャ上に構築されており、SharePoint サービスと一対多のサービス アプリケーションを利用します。 サービス アプリケーションを作成すると、サービスが使用可能になり、サービス アプリケーション データベースが生成されます。 複数の Reporting Services サービス アプリケーションを作成することができますが、ほとんどの配置シナリオではサービス アプリケーションは 1 つで十分です。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
## <a name="creating-a-reporting-services-service-application"></a>Reporting Services サービス アプリケーションの作成

 SharePoint サーバーの全体管理または PowerShell スクリプトを使用して、Reporting Services サービス アプリケーションを作成できます。 SharePoint サーバーの全体管理を使用する方法の詳細については、「[SharePoint 2010 用 Reporting Services の SharePoint モードのインストール](https://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)」の「Reporting Services サービス アプリケーションの作成」セクションを参照してください。 サービス アプリケーションを作成するための PowerShell スクリプトの例は、このトピックの後半の PowerShell のセクションを参照してください。  
  
## <a name="modify-the-associations-of-the-service-application-with-a-proxy-group"></a>プロキシ グループを使用したサービス アプリケーションの関連付けの変更

 サービス アプリケーションを作成するための [新規作成] ページには、 **[Web アプリケーションの関連付け]** セクションがあります。 このセクションでは、サービス アプリケーションの作成時に関連付けを行うことができます。 関連付けを変更してカスタム構成をサービス アプリケーションに割り当てるには、次の手順を使用します。 同じ一般的なプロセスは、サービス アプリケーションとカスタム グループとの関連付けを変更せずに、プロキシを既定のグループに追加する場合にも使用できます。  
  
1.  SharePoint サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの関連付けの構成]** をクリックします。  
  
2.  [サービス アプリケーションの関連付け] ページで、ビューを **[サービス アプリケーション]** に変更します。  
  
3.  新しい Reporting Services サービス アプリケーションの名前を探してクリックします。 アプリケーション プロキシ グループ名 **[既定]** をクリックして、次の手順を完了せずに、プロキシを既定のグループに追加することもできます。  
  
4.  **[編集する接続グループ]** 選択ボックスで、 **[カスタム]** をクリックします。  
  
5.  プロキシのチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
## <a name="edit-service-application-properties"></a>サービス アプリケーションのプロパティの編集

 サービス アプリケーションのプロパティ ページを開き直してプロパティを変更することができます。  
  
1.  SharePoint サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  サービス アプリケーションを選択するには、型列をクリックして行全体を選択します。 アプリケーションの名前をクリックすると、サービス アプリケーションのプロパティが開く代わりに、サービスの管理オプション ページが開きます。  
  
3.  [サービス アプリケーション] リボンで、 **[プロパティ]** をクリックします。  
  
## <a name="create-a-reporting-services-service-application-using-powershell"></a>PowerShell を使用して Reporting Services サービス アプリケーションを作成する

 PowerShell を使用して Service アプリケーションとプロキシを作成することができます。 次のサンプルでは、使用するサービス アプリケーションをどのアプリケーション プールに構成するかがわかっていることを前提としています。  
  
1.  アプリケーション プール名のアプリケーション プール オブジェクトを、New アクションに渡される変数に追加します。  
  
    ```  
    $appPoolName = get-spserviceapplicationpool "<application pool name>"  
    ```  
  
2.  指定した名前とアプリケーション プール名を使用してサービス アプリケーションを作成します。  
  
    ```  
    New-SPRSServiceApplication -Name 'MyServiceApplication' -ApplicationPool $appPoolName -DatabaseName 'MyServiceApplicationDatabase' -DatabaseServer '<Server Name>'  
    ```  
  
3.  新しいサービス アプリケーション オブジェクトを取得し、新しいプロキシ コマンドレットにオブジェクトをパイプします。  
  
    ```  
    Get-SPRSServiceApplication -name MyServiceApplication | New-SPRSServiceApplicationProxy "MyServiceApplicationProxy"  
    ```  
  
## <a name="related-tasks"></a>関連タスク
  
|タスク|リンク|  
|----------|----------|  
|サービス アプリケーションの設定を管理する|[Reporting Services SharePoint サービス アプリケーションの管理](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)|  
|サービス アプリケーションと関連コンポーネント (暗号化キーやプロキシなど) をバックアップおよび復元する|[Reporting Services SharePoint サービス アプリケーションのバックアップと復元](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
