---
title: 詳細レポート (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 938a6450-67c1-4eef-80b4-8fdaefeed584
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ccc5c2950baf10cad0e7f9495b446286576b27bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579345"
---
# <a name="drillthrough-reports-report-builder-and-ssrs"></a>詳細レポート (レポート ビルダーおよび SSRS)
  詳細レポートは、ユーザーが別のレポート内のリンクをクリックすることで開かれるレポートのことです。 詳細レポートには、通常、元の要約レポートに含まれるアイテムについての詳細が含まれています。 たとえば、次の図では、売り上げ要約レポートに販売注文と合計の一覧が含まれています。 この要約一覧で任意の注文番号をクリックすると、この注文に関する詳細が含まれた別のレポートが開きます。  
  
 ![rs_DrillThru](../../reporting-services/report-design/media/rs-drillthru.gif "rs_DrillThru")  
  
 詳細レポートのデータは、詳細レポートを開くメイン レポート内のリンクをクリックするまで、取得されません。 メイン レポートと詳細レポートのデータを同時に取得する必要がある場合は、サブレポートの使用を検討してください。 詳細については、「[サブレポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  レポート ビルダーで作業しているときに、メイン レポートのドリルスルー リンクをクリックしたときに開く詳細レポートを表示するには、レポート サーバーに接続している必要があります。  
  
 今すぐ詳細レポートを表示するには、「[チュートリアル: 詳細レポートとメイン レポートの作成 &#40;レポート ビルダー&#41;](../../reporting-services/tutorial-creating-drillthrough-and-main-reports-report-builder.md)」を参照してください。 
   
## <a name="parameters-in-drillthrough-reports"></a>詳細レポートのパラメーター  
 詳細レポートには、通常、要約レポートから渡されるパラメーターが含まれています。 売り上げ要約レポートの例では、要約レポートには、テーブル セルのテキスト ボックス内のフィールド [OrderNumber] が含まれます。 詳細レポートには注文番号 (Order Number) を値として受け取るパラメーターが含まれています。 [OrderNumber] のテキスト ボックスに詳細レポート リンクを設定するとき、対象のレポートのパラメーターも [OrderNumber] に設定します。 ユーザーが要約レポート内の注文番号をクリックすると、対象の詳細レポートが開き、その注文番号の情報が表示されます。 パラメーターの値に基づいて詳細レポートをカスタマイズする方法については、「[レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)」と「[InScope 関数 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-builder-functions-inscope-function.md)」を参照してください。  
  
## <a name="designing-the-drillthrough-report"></a>詳細レポートのデザイン  
 詳細レポートを作成するには、メイン レポートにドリルスルー アクションを作成する前に、まず詳細レポートをデザインする必要があります。  
  
 詳細レポートには、任意のレポートを指定できます。 通常、詳細レポートは、メイン レポートからのリンクに基づいて、表示するデータを指定する 1 つ以上のパラメーターを受け取ります。 たとえば、メイン レポートのリンクが販売注文に対して定義されたものである場合は、販売注文番号が詳細レポートに渡されます。  
  
## <a name="creating-a-drillthrough-action-in-the-main-report"></a>メイン レポートのドリルスルー アクションの作成  
 テキスト ボックス (テーブルまたはマトリックスのセル内のテキストを含む)、画像、グラフ、ゲージなど、Action プロパティ ページがあるレポート アイテムにドリルスルー リンクを追加できます。 詳細については、「[レポートへのドリルスルー アクションの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)」を参照してください。  
  
 メイン レポートのドリルスルー アクションは、レポート アクションまたは URL アクションとして作成できます。 レポート アクションの場合、詳細レポートはメイン レポートと同じレポート サーバーに存在する必要があります。 URL アクションの場合、レポートは完全修飾 URL の場所に存在する必要があります。 レポート サーバーとレポート サーバーに統合されている SharePoint サイトとでは、レポートの指定方法が異なる場合があります。 レポート サーバーが SharePoint 統合モードで構成されている場合は、URL アクションのみがサポートされます。  
  
 詳細については、「[レポートへのドリルスルー アクションの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)」と「[外部アイテムへのパスの指定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="viewing-a-drillthrough-report"></a>詳細レポートの表示  
 ドリルスルー リンクを含むレポートをパブリッシュした後に表示するには、要約レポートと同じレポート サーバー上に詳細レポートを配置する必要があります。 どの場合でも、ユーザーは詳細レポートを表示する権限を持つ必要があります。  
  
## <a name="see-also"></a>参照  
 [ドリルスルー、ドリルダウン、サブレポート、および入れ子になったデータ領域 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  
