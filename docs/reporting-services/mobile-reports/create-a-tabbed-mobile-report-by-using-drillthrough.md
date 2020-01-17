---
title: ドリルスルーを使用してタブ付きモバイル レポートを作成する | Reporting Services のモバイル レポート | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d01f9f1bef4d13cbce3f3e736cbef2f838c680ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061820"
---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>ドリルスルーを使用してタブ付きモバイル レポートを作成する
ドリルスルーとパラメーターを使用して、タブ付きレポートのような外観と動作の [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] モバイル レポートを作成する方法について説明します。

たとえば、このレポートでは、上部にあるゲージはタブのように動作します。 輸送ゲージをクリックすると、他のグラフのデータがフィルターされ、輸送データのみが表示されます。

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

実際には、これは 5 つの独立したレポートのセットであり、それぞれがレポート上部で選択されたゲージと一致するようにレポートをフィルター処理する異なるパラメーターを備えています。 最初に 5 つのレポートをすべて作成した後、それぞれについて、他の 4 つのゲージで他の 4 つのレポートにドリルスルーできるようにします。

この例の手順を次に示します。

## <a name="create-the-basic-report"></a>基本的なレポートの作成

1. 次の5 つのゲージを持つ売上という名前のレポートを作成します。

    * 売上
    * 輸送
    * 燃料
    * ストレージ
    * その他諸経費

   ![01-Sales-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. レポートの他の部分よりも目立つように (この例では黒地に白)、売上ゲージの **[アクセント]** を **[オン]** に設定します。

    ![01a-Sales-Accent-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] レポート サーバーに保存します。

## <a name="make-copies-of-the-report"></a>レポートのコピーを作成する

1. 売上レポートのコピーを 4 部作成し、次のように名前を付けます。 

    * 輸送
    * 燃料
    * ストレージ
    * その他諸経費

3. レポートを [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] レポート サーバーに保存します。

## <a name="set-the-gauge-as-a-drillthrough"></a>ゲージをドリルスルーとして設定する

このセクションでは、各ゲージ (売上ゲージ以外) をその対応するレポートへのドリルスルーとして設定します。

1. 売上レポートで輸送ゲージを選択します。

    ![02-Sales-Create-DrillThrough-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. **[レイアウト]** タブを選択した状態で、 **[ビジュアルのプロパティ]** ウィンドウの **[ドリルスルー ターゲット]** を選択します。

3. **[モバイル レポート]** を選択します。

4. ドリルスルー対象のレポートを探して選択します。この例では、"金融 - 輸送" です。

    ![03-Sales-Select-Dashboard-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. **[ターゲット レポートの構成]** でレポートをフィルター処理するパラメーターを選択し、 **[適用]** を選択します。

   ![04-Sales-Apply-Parameters-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. 売上レポートの他の各ゲージについてこれらの手順を繰り返します。 

## <a name="set-the-gauges-for-the-other-reports"></a>他のレポートのゲージを設定する

1.  輸送レポートを開き、売上ゲージを売上レポートへのドリルスルーとして、また他の 3 つのゲージをそれぞれのレポートへのドリルスルーとして設定します。

2. 輸送レポートを開いたままで、輸送ゲージの **[アクセント]** を **[オン]** に設定して、レポートの他の部分よりも目立つようにします。

3. 燃料、ストレージ、その他諸経費の各レポートについてこれらの手順を繰り返します。 

## <a name="view-the-report-in-the-web-portal"></a>Web ポータルでレポートを確認する

1. [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] レポート サーバーに移動し、レポートのいずれかを開きます。 

2. 各ゲージの右上にドリルスルー アイコンが表示される点に注目してください。

    ![Web-Viewer-drillthrough-icon-mobile-report-builder](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. ゲージのいずれかを選択すると、そのゲージのデータに絞り込まれたレポートが表示されます。

   ![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>参照
    
* [モバイル レポートにパラメーターを追加する](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [モバイル レポートから他のモバイル レポートまたは URL にドリルスルーを追加する](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  

