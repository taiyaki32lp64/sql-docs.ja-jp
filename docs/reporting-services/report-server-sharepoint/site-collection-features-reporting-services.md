---
title: Reporting Services サイト コレクション機能 | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e13654a38738c84095cc284a24fb723aa2b05327
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580500"
---
# <a name="reporting-services-site-collection-features"></a>Reporting Services サイト コレクション機能

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Reporting Services SharePoint モードには、SharePoint サイト コレクションの 3 つの機能が用意されています。 これらの機能は、一般的な Reporting Services SharePoint モードのレポート環境、[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、SQL Server 2016 Reporting Services アドインの機能、SharePoint サーバーの全体管理の Reporting Services の管理操作をサポートします。

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
## <a name="site-collection-features"></a>サイト コレクションの機能

 次の表に、Reporting Services のサイト コレクションの機能を示します。  
  
|機能|[説明]|  
|-------------|-----------------|  
|**レポート サーバーの全体管理機能**|Reporting Services レポート サーバーとの統合を管理する機能を有効にします。 この機能は、SharePoint サーバーの全体管理のサイト コレクション内でのみインストールおよび使用されます。<br /><br /> レポート サーバーの統合機能は、SharePoint 製品用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] アドインをインストールすると自動的に SharePoint サーバーの全体管理のサイト コレクションでアクティブ化されます。 場合によっては、この機能を手動でアクティブ化する必要があります。 レポート サーバー機能をアクティブ化するには、SharePoint サーバーの全体管理の [サイトの設定] ページ内の Reporting Services ページを使用します。<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Reporting Services 以降のバージョンの SharePoint 製品用アドインをインストールすると、既存のすべてのサイト コレクションのレポート サーバーの統合機能がアクティブ化されます。 また、この機能は、新しいサイト コレクションに対して自動的にアクティブ化されます。|  
|**レポート サーバーの統合機能**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Reporting Services による豊富なレポート機能を有効にする<br /><br /> この機能は、既定でアクティブになっています。|  
|**Power View の統合機能**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックおよび Analysis Services の表形式のデータベースに対する対話形式のデータ探索と視覚的な表示を有効にします。<br /><br /> この機能には、次のデータ ソースのコンテキスト メニューからアクセスできます。<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> **.bism** 接続ファイル<br /><br /> <br /><br /> [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] がコンテキスト メニューに表示されない場合は、 **Power View の統合機能** がアクティブになっていることを確認してください。<br /><br /> この機能は、既定で非アクティブになっています。|  

## <a name="next-steps"></a>次の手順

[SharePoint でのレポート サーバーと Power View の統合機能のアクティブ化](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Reporting Services のサイト設定とサイト機能 &#40;SharePoint モード&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[SharePoint サーバーの全体管理でレポート サーバーのファイル同期機能をアクティブにする](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
