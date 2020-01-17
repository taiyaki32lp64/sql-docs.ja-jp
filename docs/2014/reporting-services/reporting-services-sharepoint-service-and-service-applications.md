---
title: SharePoint サービスとサービスアプリケーションの Reporting Services |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 501aa9ee-8c13-458c-bf6f-24e00c82681b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93a8092dc9ed731349a1948a74e3950eb32f4f47
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783158"
---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Reporting Services の SharePoint サービスとサービス アプリケーション
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint モードは、SharePoint サービス アーキテクチャ上に構築されており、SharePoint サービスと一対多のサービス アプリケーションを利用します。 サービス アプリケーションを作成すると、サービスが使用可能になり、サービス アプリケーション データベースが生成されます。 複数の Reporting Services サービス アプリケーションを作成することができますが、ほとんどの配置シナリオではサービス アプリケーションは 1 つで十分です。  
  
 このトピックの内容は次のとおりです。  
  
-   [Reporting Services サービス アプリケーションの作成](#bkmk_createapp)  
  
-   [プロキシ グループを使用したサービス アプリケーションの関連付けの変更](#bkmk_associations)  
  
-   [サービス アプリケーションのプロパティの編集](#bkmk_editserviceapplication)  
  
-   [PowerShell を使用して Reporting Services サービス アプリケーションを作成するには](#bkmk_powershell_create_ssrs_serviceapp)  
  
-   [関連タスク](#bkmk_related)  
  
##  <a name="bkmk_createapp"></a> Reporting Services サービス アプリケーションの作成  
 SharePoint サーバーの全体管理または PowerShell スクリプトを使用して、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] サービス アプリケーションを作成できます。 SharePoint サーバーの全体管理を使用する方法の詳細については、「[SharePoint 2010 用 Reporting Services の SharePoint モードのインストール](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)」の「Reporting Services サービス アプリケーションの作成」セクションを参照してください。 サービス アプリケーションを作成するための PowerShell スクリプトの例は、このトピックの後半の PowerShell のセクションを参照してください。  
  
##  <a name="bkmk_associations"></a> プロキシ グループを使用したサービス アプリケーションの関連付けの変更  
 サービス アプリケーションを作成するための [新規作成] ページには、 **[Web アプリケーションの関連付け]** セクションがあります。 このセクションでは、サービス アプリケーションの作成時に関連付けを行うことができます。 関連付けを変更してカスタム構成をサービス アプリケーションに割り当てるには、次の手順を使用します。 同じ一般的なプロセスは、サービス アプリケーションとカスタム グループとの関連付けを変更せずに、プロキシを既定のグループに追加する場合にも使用できます。  
  
1.  SharePoint サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの関連付けの構成]** をクリックします。  
  
2.  [サービス アプリケーションの関連付け] ページで、ビューを **[サービス アプリケーション]** に変更します。  
  
3.  新しい [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] サービス アプリケーションの名前を探してクリックします。 アプリケーション プロキシ グループ名 **[既定]** をクリックして、次の手順を完了せずに、プロキシを既定のグループに追加することもできます。  
  
4.  **[編集する接続グループ]** 選択ボックスで、 **[カスタム]** をクリックします。  
  
5.  プロキシのチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
##  <a name="bkmk_editserviceapplication"></a> サービス アプリケーションのプロパティの編集  
 サービス アプリケーションのプロパティ ページを開き直してプロパティを変更することができます。  
  
1.  SharePoint サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  サービス アプリケーションを選択するには、型列をクリックして行全体を選択します。 アプリケーションの名前をクリックすると、サービス アプリケーションのプロパティが開く代わりに、サービスの管理オプション ページが開きます。  
  
3.  [サービス アプリケーション] リボンで、 **[プロパティ]** をクリックします。  
  
##  <a name="bkmk_powershell_create_ssrs_serviceapp"></a> PowerShell を使用して Reporting Services サービス アプリケーションを作成するには  
 PowerShell を使用して Service アプリケーションとプロキシを作成することができます。 次のサンプルでは、使用するサービス アプリケーションをどのアプリケーション プールに構成するかがわかっていることを前提としています。  
  
1.  アプリケーション プール名のアプリケーション プール オブジェクトを、New アクションに渡される変数に追加します。  
  
    ```powershell
    $appPoolName = Get-SPServiceApplicationPool "<application pool name>"  
    ```  
  
2.  指定した名前とアプリケーション プール名を使用してサービス アプリケーションを作成します。  
  
    ```powershell
    New-SPRSServiceApplication -Name 'MyServiceApplication' -ApplicationPool $appPoolName -DatabaseName 'MyServiceApplicationDatabase' -DatabaseServer '<Server Name>'  
    ```  
  
3.  新しいサービス アプリケーション オブジェクトを取得し、新しいプロキシ コマンドレットにオブジェクトをパイプします。  
  
    ```powershell
    Get-SPRSServiceApplication -name MyServiceApplication | New-SPRSServiceApplicationProxy "MyServiceApplicationProxy"  
    ```  
  
##  <a name="bkmk_related"></a> 関連タスク  
  
|タスク|リンク|  
|----------|----------|  
|サービス アプリケーションの設定を管理する|[Reporting Services SharePoint サービス アプリケーションの管理](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)|  
|サービス アプリケーションと関連コンポーネント (暗号化キーやプロキシなど) をバックアップおよび復元する|[Reporting Services SharePoint サービス アプリケーションのバックアップと復元](../../2014/reporting-services/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  
