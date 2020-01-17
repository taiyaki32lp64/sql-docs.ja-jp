---
title: レポート ビューアーでのローカル モードと接続モードのレポート | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: be9653d66ef541ebf27cb31c8092b79c2e1bf612
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579875"
---
# <a name="local-mode-vs-connected-mode-reports-in-the-report-viewer"></a>レポート ビューアーでのローカル モードと接続モードのレポート

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポートは、 *レポート サーバーを使用する、* ローカル モード *または*接続モード [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のいずれかで実行するように構成できます。 代わりに、データ拡張機能でローカル モード レポートがサポートされている場合は、レポート ビューアーを使用して SharePoint から直接レポートを表示できます。 この方法は、 *ローカル モード*と呼ばれます。 以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、レポート ビューアー コントロールでレポートを表示できるように、SharePoint モードで構成されている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーに SharePoint ファームが接続されている必要がありました。 この方法は、 *リモート モード* または *接続モード*と呼ばれます。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

 *ローカル モード* では、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーはありません。 SharePoint 製品用に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをインストールする必要がありますが、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーは必須ではありません。 ローカル モードでは、ユーザーはレポートを表示できますが、サブスクリプションやデータ警告などのサーバー側機能にはアクセスできません。  

## <a name="local-mode-vs-connected-mode-and-supported-extensions"></a>ローカル モードと接続モードおよびサポートされる拡張機能

 **ローカル モード:** ローカル モードをサポートしているデータ拡張機能を使用している場合は、レポート ビューアーによって SharePoint から直接レポートが表示されます。 *ローカル モード* では、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーはありません。 SharePoint 製品用に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをインストールする必要がありますが、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーは必須ではありません。 ローカル モードでは、ユーザーはレポートを表示できますが、サブスクリプションやデータ警告などのサーバー側機能には **アクセスできません** 。  
  
 **接続モード**( *リモート モード* とも呼ばれる) では、レポート ビューアー コントロールでレポートを表示できるように、SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーが SharePoint ファームに接続されている必要があります。  
  
 ローカル モード レポートをサポートしているデータ処理拡張機能の一覧を次に示します。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access 2010 レポート拡張機能。 Access Services の詳細については、「 [Access Services と SQL Reporting Services の併用: SQL Server 2008 R2 Reporting Services アドインのインストール (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=192686)」を参照してください。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint リスト データ拡張機能。 SharePoint リスト データ拡張機能の詳細については、「 [Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
 カスタム データ処理拡張機能を開発して、ローカル モードをサポートすることもできます。 詳細については、「 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)」を参照してください。  
  
 ローカル モードでは、データ ソースが埋め込まれているレポート、または .rsds ファイルの共有データ ソースが含まれているレポートを表示できます。 ただし、レポートまたはその関連データ ソースを管理することはできません。 データ ソースを編集しようとすると、データ ソースの編集はローカル モードではサポートされないというエラーが表示されます。 SharePoint サイトのデータ ソース管理は、接続モードでのみサポートされます。  
  
> [!NOTE]  
>  以前のバージョンと同様に、.rsds ファイルにユーザー名とパスワードを埋め込むことはできません。  
  
## <a name="configure-local-mode-and-access-services-with-sharepoint-2013"></a>SharePoint 2013 でのローカル モードと Access Services の構成

 既存の Access 2010 Web データベースと [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ローカル モードをサポートするように SharePoint 2013 ファームを構成できます。 詳細については、「 [SharePoint Server 2013 での Web データベース用の Access Services 2010 のセットアップと構成](https://technet.microsoft.com/library/ee748653\(office.15\).aspx)」を参照してください。  
  
 SharePoint 2013 用の新しい Access Web データベースを作成することはできません。 Access 2013 では、新しい種類のデータベース (Access で構築される *Access Web App* ) が使用されるので、Web ブラウザーで SharePoint アプリケーションとして使用し、他のユーザーと共有します。  
  
 詳細については、次を参照してください。  
  
-   [Access 2013 の新機能](https://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx) (https://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx) 。  
  
-   [Access アプリの基本的なタスク](https://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500) (https://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500) 。  
  
## <a name="configure-local-mode-reporting-with-sharepoint-2010"></a>SharePoint 2010 でのローカル モード レポートの構成

 ローカル モードには ASP.NET セッション状態が必要です。 Access サービスをインストールすると、ASP.NET セッション状態が有効になります。 PowerShell を使用して有効にすることもできます。  
  
1.  SharePoint 2010 管理シェルを開きます。  
  
2.  次のコマンドを入力します。  
  
    ```  
    - Enable-SPSessionStateService  
    ```  
  
3.  プロンプトが表示されたら、データベースの名前を入力します。  
  
4.  IIS リセットを実行します。  
  
 詳細については、「 [Access Services と SQL Reporting Services の併用: SQL Server 2008 R2 Reporting Services アドインのインストール (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=192686) 」および「 [Enable-SPSessionStateService](https://technet.microsoft.com/library/ff607857\(v=office.15\).aspx)」を参照してください。  
  
## <a name="connected-mode"></a>または

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 接続モードでの ADS 拡張機能の使用に関する最新情報については、「[Access Services Report in SharePoint Site shows error in data extension 'ADS'](https://social.technet.microsoft.com/wiki/contents/articles/25298.access-services-report-in-sharepoint-site-shows-error-in-data-extension-ads.aspx)」 (SharePoint サイトの Access Services レポートでデータ拡張機能 'ADS' のエラーが表示される) を参照してください。  
  
## <a name="see-also"></a>参照

 [Reporting Services でサポートされるデータ ソース](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
