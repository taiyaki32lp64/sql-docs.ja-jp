---
title: レポート ビューアー Web パーツを Web ページに追加する | Microsoft Docs
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 562c762871db5c29476d10a81ac52dad46f65ad5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579396"
---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>レポート ビューアー Web パーツを Web ページに追加する

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

レポート ビューアー Web パーツを使用することで、SharePoint 統合モード用に構成されているレポート サーバーで実行されるレポートを表示できます。 この Web パーツでは、レポート ビルダーまたはレポート デザイナーで作成してライブラリにアップロードしたレポート定義ファイル (.rdl) を表示できます。

Web ページにレポート ビューアー Web パーツを追加することで、Web ページにレポートを埋め込むことができます。

> [!NOTE]
> この記事は、SharePoint 製品向け Reporting Services アドインと共に出荷される Report Viewer Web パーツのみを対象にしています。 SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

Web パーツを Web ページに追加するには、サイト レベルでの "ページの追加とカスタマイズ" アクセス許可が必要です。 既定のセキュリティ設定を使用する場合、この権限はフル コントロール レベルの権限を持つ **所有者** グループのメンバーに与えられます。

## <a name="to-embed-a-report-in-a-web-page"></a>Web ページにレポートを埋め込むには

1.  Web パーツ ページまたはダッシュボードを開くか、作成します。  
  
2.  **[サイトの操作]** の **[ページの編集]** をクリックします。  
  
3.  **[Web パーツの追加]** をクリックします。  
  
4.  Web パーツ カテゴリの一覧で、 **[その他]** カテゴリをクリックし、 **[SQL Server Reporting Services レポート ビューアー]** をクリックします。  
  
5.  **[追加]** をクリックします。 Web パーツがゾーンの一番上に追加されます。 Web パーツは、ドラッグして、領域内の別の場所に移動できます。  
  
6.  ビューアー内で、 **[ツール ペインを開くにはここをクリックします]** をクリックします。  
  
7.  参照ボタン ( **[...]** ) をクリックして、現在のサイト コレクションの任意のライブラリにあるレポートを選択します。 レポートの URL を入力することもできます。 レポートの URL を調べるには、レポートを右クリックし、 **[プロパティ]** をクリックします。 レポートの横にある下向きの矢印アイコンはクリックしないでください。アイテムの [プロパティの表示] ページでは、レポートの URL は表示されません。 **[プロパティ]** ダイアログ ボックスで URL をコピーし、貼り付ける場合には、URL 内の "%20" をスペースに置き換えてください (たとえば、"Company%20Sales" は "Company Sales" にします)。  
  
    > [!NOTE]  
    >  1 つのレポート ビューアー Web パーツには、1 つのレポートが格納されます。 URL は、現在の SharePoint サイト、または同じ Web アプリケーションやファーム内のサイト上のレポートへの完全修飾パスで指定する必要があります。 この URL は、ドキュメント ライブラリとして解決されるか、ドキュメント ライブラリ内でレポートが格納されるフォルダーとして解決される必要があります。 レポート URL には、ファイル拡張子 .rdl を含める必要があります。 レポートがモデル ファイルまたは共有データ ソース ファイルに依存している場合、URL でそのファイルを指定する必要はありません。 必要なファイルへの参照は、レポートに含まれています。  
  
8.  開いているツール ペインでプロパティを設定し、既定の外観とレイアウトを変更します。  
  
9. ツール ペインの下部で **[適用]** をクリックし、 **[OK]** をクリックしてペインを閉じます。  
  
## <a name="see-also"></a>参照

 [SharePoint サイトのレポート ビューアー Web パーツ](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [レポート ビューアー Web パーツのカスタマイズ](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [SharePoint サイトのレポート サーバー アイテムに対する権限の付与](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [SharePoint 用 Reporting Services アドインのインストールまたはアンインストール](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
