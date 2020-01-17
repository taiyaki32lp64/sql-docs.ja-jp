---
title: チュートリアルの前提条件 (レポート ビルダー) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 450a490e5c4f54f9fec2e88c1c73bfbf8502869a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66499992"
---
# <a name="prerequisites-for-tutorials-report-builder"></a>チュートリアルの前提条件 (レポート ビルダー)

レポート ビルダー チュートリアルを実行するには、レポート サーバー上、またはレポート サーバーと統合されている SharePoint サイト上で、 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] のページ分割されたレポートを表示および保存できる必要があります。 すべてのチュートリアルでは、データを取得するために、SQL Server のインスタンスで処理される必要があるリテラル クエリを使用します。  
  
レポート サーバーやサイト、またはデータ ソースにアクセスできない場合は、オフラインのレポートを作成することによってレポート ビルダーについて学習できます。 「[チュートリアル: オフラインでのクイック グラフ レポートの作成 &#40;レポート ビルダー&#41;](../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)」を参照してください。  

## <a name="requirements"></a>必要条件

レポート ビルダーのチュートリアルを完了するには、次の条件を満たしている必要があります。  
  
-   レポート ビルダーへのアクセス。 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] レポート サーバーまたは SharePoint 統合モードの [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] レポート サーバーから、レポート ビルダーを実行できます。 これらの異なるサーバーでは、最初の手順であるレポート ビルダーを開く方法のみが異なります。  
  
    レポート サーバーで、 **[新規]**  >  **[ページ分割されたレポート]** を選択します。
  
    SharePoint 統合モードのレポート サーバーで、 **[ドキュメント]** タブの **[新しいドキュメント]** を選択し、ドロップ ダウン リストから **[レポート ビルダー レポート]** を選択します。 たとえば、 `https://<servername>/sites/mySite/reports`のようにします。 SharePoint 管理者は、各ドキュメント ライブラリのレポート ビルダー レポート機能を有効にする必要があります。  
  
-   [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] レポート サーバー、または [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] レポート サーバーと統合されている SharePoint サイトの URL。 レポート、共有データ ソース、共有データセット、レポート パーツ、およびモデルを保存および表示する権限が必要です。 既定では、レポート サーバーの URL は `https://<servername>/reportserver`です。 既定では、SharePoint サイトの URL は `https://<sitename>` または `https://<server>/site`です。  
  
-   SQL Server インスタンスの名前と任意のデータベースへの読み取り専用アクセスに必要な資格情報。 チュートリアルのデータセット クエリでは、リテラル データを使用します。ただし、各クエリは、レポート データセットに必要なメタデータを返すように、SQL Server インスタンスで処理される必要があります。 たとえば、 `data source=<servername>`という接続文字列では、サーバーしか指定されていません。 この場合は、そのサーバーにアクセスする権限を付与したシステム管理者によって割り当てられた既定のデータベースに対する読み取りアクセス権が必要です。 `data source=<servername>;initial catalog=<database>`という接続文字列のように、データベースを指定することもできます。  
  
-   「[チュートリアル: マップ レポート (レポート ビルダー)](Tutorial:%20Map%20Report%20\(Report%20Builder\).md)」では、レポート サーバーが Bing Maps を背景としてサポートするように構成されている必要があります。 詳細については、「 [マップ レポートのサポートを計画する](https://msdn.microsoft.com/5ddc97a7-7ee5-475d-bc49-3b814dce7e19)」を参照してください。   

-   「[チュートリアル: 詳細レポートとメイン レポートの作成 (レポート ビルダー)](Tutorial:%20Creating%20Drillthrough%20and%20Main%20Reports%20\(Report%20Builder\).md)」チュートリアルでは、Contoso Sales キューブへのアクセスが必要です。 詳細については、チュートリアルを参照してください。 
  
レポート サーバー管理者は、レポート サーバーに対する必要な権限の許可、 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] のフォルダーの場所の構成、およびレポート ビルダーの既定のオプションの構成を行う必要があります。 詳細については、「 [Install Report Builder](install-windows/install-report-builder.md)」を参照してください。  

## <a name="next-steps"></a>次の手順

[レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
