---
title: PowerPivot for SharePoint 2013 | の最小特権構成の例Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c1e09e6c-52d3-48ab-8c70-818d5d775087
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 147664030dd6e52c4bfaf17efd6fa7aea35d53ae
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782779"
---
# <a name="example-of-a-minimum-privilege-configuration-for-powerpivot-for-sharepoint-2013"></a>Power Pivot for SharePoint 2013 向けに最小限の特権を構成する例
  このトピックでは、最小限の特権を使用する PowerPivot for SharePoint 2013 構成の例について説明します。 この構成では、3 種類のコンポーネントごとに個別のアカウントを使用します。各アカウントには最小レベルの特権を指定します。  
  
## <a name="summary-of-accounts"></a>アカウントの概要  
 PowerPivot for SharePoint 2013 では、Analysis Services サービス アカウントに Network Service アカウントを使用できます。 Network Service アカウントは、SharePoint 2010 のシナリオではサポートされません。 サービスアカウントの詳細については、「 [Windows サービスアカウントと権限の構成](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)(https://msdn.microsoft.com/library/ms143504.aspx) 」を参照してください。  
  
 次の表は、最小限の特権の構成の例で使用する 3 種類のアカウントをまとめたものです。  
  
|スコープ|NAME|  
|-----------|----------|  
|SharePoint 管理者アカウント|**SPAdmin**|  
|SharePoint ファーム アカウント|**SPFarm**|  
|Analysis Services サービス アカウント|**SPsvc**|  
  
### <a name="the-sharepoint-administrator-account-spadmin"></a>SharePoint 管理者アカウント (SpAdmin)  
 **SPAdmin** は、ファームのインストールと構成に使用するドメイン アカウントです。 このアカウントは、SharePoint 構成ウィザードと SharePoint 2013 用 PowerPivot 構成ツールの実行に使用されます。 **Spadmin**アカウントは、ローカル管理者権限を必要とする唯一のアカウントです。 PowerPivot 構成ツールを実行する前に、SharePoint によってコンテンツデータベースと構成データベースが作成される SQL Server データベースインスタンスに、 **Spadmin**アカウントの特権を付与します。 最小限の特権のシナリオで SPAdmin アカウントを構成する場合、SPAdmin アカウントは **securityadmin** ロールと **dbcreator**ロールのメンバーにします。  
  
### <a name="the-farm-account-spfarm"></a>ファーム アカウント (SPFarm)  
 **SPFarm** は、SharePoint Timer Service と全体管理用 Web アプリケーションが SharePoint コンテンツ データベースにアクセスするために使用するドメイン アカウントです。 このアカウントは、ローカル管理者である必要はありません。 SharePoint 構成ウィザードでは、バックエンドの SQL Server データベースで必要最小限の特権を付与します。SQL Server の特権の最小限の構成は **securityadmin** ロールと **dbcreator**ロールのメンバーシップです。  
  
### <a name="the-service-account-for-powerpivot-service-spsvc"></a>PowerPivot サービスのサービス アカウント (SPsvc)  
 PowerPivot 構成ツールを実行する前に新しい SharePoint ファームが構成されていない場合、PowerPivot 構成ツールでは既定で以下のものを作成します。  
  
-   PowerPivot サービス アプリケーション。  
  
-   Excel Services アプリケーション。  
  
-   Secure Store アプリケーション。  
  
 PowerPivot 構成ツールは、既定のアプリケーション プールのサービス アプリケーション 3 つすべてを構成します。 このアプリケーション プールは通常、サービス アカウントが不要な多くのリソースにアクセスできる SPFarm アカウントとして実行されるように構成されます。最小限の特権環境にするには、適切なアプリケーション プールおよび Web アプリケーションで使用する新しいドメイン アカウントを構成します。  
  
 **SharePoint Service アカウントとして使用する新しいドメイン アカウント SPsvc を作成するには**  
  
1.  SharePoint サーバーの全体管理で、 **[セキュリティ]** をクリックします。  
  
2.  **[サービスアカウントの構成]** をクリックします。  
  
3.  **[新しい管理アカウントの登録]** をクリックします。  
  
 **SPSvc** アカウントにはローカル管理者権限はなく、SharePoint データベースに関する権限もありません。 SPsvc に必要な唯一の特権は、Analysis Services の PowerPivot インスタンスの管理権限です。  
  
 **SPsvc アカウントを使用する適切なアプリケーション プールを構成するには**  
  
1.  SharePoint サーバーの全体管理で、 **[セキュリティ]** をクリックします。  
  
2.  **[サービスアカウントの構成]** をクリックします。  
  
3.  PowerPivot サービス アプリケーションで使用するサービス アプリケーション プールを選択します。 次に、SPSvc アカウントを選択します。  
  
 **PowerShell で Web アプリケーションへのアクセス権を付与するには**  
  
1.  管理者特権を使用して、SharePoint 2013 管理シェルを実行します。  
  
2.  次の PowerShell コードを実行します。  
  
    ```powershell
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")
    ```  
