---
title: SharePoint でのレポート サーバーと Power View の統合機能のアクティブ化 | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: dce33b0f267dadd8454378fccb72112970553a96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580503"
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>SharePoint でのレポート サーバーと Power View の統合機能のアクティブ化

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Reporting Services のサイト コレクション機能は、SharePoint 製品用の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] アドインをインストールすると、既定でアクティブ化されます。 場合によっては、この機能を手動でアクティブ化する必要があります。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

 SharePoint 製品のインストール後に SharePoint 2010 製品用の Reporting Services アドインをインストールした場合、レポート サーバーの統合機能と Power View の統合機能はルート サイト コレクションでのみアクティブ化されます。 他のサイト コレクションについては、この機能を手動でアクティブ化する必要があります。 たとえば、**https://[my server name]/sites/[site collection name]** というサイト コレクションが存在する場合は、Reporting Services のサイト コレクション機能を手動でアクティブ化する必要があります。  
  
 ルート サイト コレクションがない場合は、Reporting Services アドインによって、次のようなメッセージがログに記録されます。  
  
 "SharePoint Web アプリケーション 80 にはルート サイト コレクションがありません"  
  
 このメッセージは "RS_SP_#.log" (# は増加する値) という名前のアドイン インストール ログにあります。 このログ ファイルは、現在のユーザーの Temp フォルダー (例: C:\Users\\[user name]\AppData\Local\Temp) にあります。アドインのインストール方法の詳細については、「 [SharePoint 用 Reporting Services アドインのインストールまたはアンインストール](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)」を参照してください。  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>レポート サーバーと Power View の統合サイト コレクション機能をアクティブ化する
  
1.  ブラウザーで、Reporting Services の機能をアクティブ化するサイトを開きます。  
  
2.  **[サイトの操作]** をクリックします。  
  
3.  **[サイトの設定]** をクリックします。  
  
4.  [サイト コレクションの管理] グループで **[サイト コレクションの機能]** をクリックします。  
  
5.  一覧で **[レポート サーバーの統合機能]** または **[Power View 統合機能]** を見つけます。  
  
6.  **[アクティブ化]** をクリックします。  
  
 機能を非アクティブ化するには、 **[アクティブ化]** ではなく **[非アクティブ化]** をクリックする点を除き、同じ手順を実行します。  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>Reporting Services の全体管理のサイト コレクション機能をアクティブ化または非アクティブ化する
  
1.  ブラウザーで SharePoint サーバーの全体管理を開きます。  
  
2.  **[サイトの操作]** をクリックします。  
  
3.  **[サイトの設定]** をクリックします。  
  
4.  [サイト コレクションの管理] グループで **[サイト コレクションの機能]** をクリックします。  
  
5.  一覧で **[レポート サーバーの全体管理機能]** を見つけます。  
  
6.  **[アクティブ化]** をクリックします。  
  
 機能を非アクティブ化するには、 **[アクティブ化]** ではなく **[非アクティブ化]** をクリックする点を除き、同じ手順を実行します。  
  
## <a name="next-steps"></a>次の手順

機能をアクティブ化した後、サーバーの統合を続行できます。

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
