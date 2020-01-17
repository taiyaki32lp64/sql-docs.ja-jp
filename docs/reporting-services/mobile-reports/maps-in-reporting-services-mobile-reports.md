---
title: Reporting Services モバイル レポート内のマップ | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 50658295-a71c-441e-8eba-e1ef066629c0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5b09c8aec100d877256f0d8d9b4b97530ecdf5c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62683696"
---
# <a name="maps-in-reporting-services-mobile-reports"></a>Maps in Reporting Services mobile reports
マップは、地理的データを視覚化するための優れた方法です。 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] は、3 種類のマップの視覚エフェクト、および大陸と多数の個々の国の組み込みのマップを提供します。 [カスタム マップをアップロードして使用する](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)こともできます。   
  
## <a name="types-of-maps"></a>マップの種類  
  
SQL Server モバイル レポートでは、さまざまな状況に役立つ、3 種類のマップを用意しています。  
  
![SSMRP_MapsGallery](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
**グラデーション ヒート マップ** 値プロパティ内のフィールドが、マップ内の各領域を塗りつぶす 1 色の網掛けで表示されます。 **[値の方向]** ボックスで、高い値と低い値のどちらを濃くするかを設定できます。  
  
**バブル マップ** 値プロパティによって、関連付けられている領域に表示されるバブル視覚エフェクトの半径を決定します。 すべてのバブルを同じ色にするか、またはすべて違う色にするかを設定できます。   
  
**範囲停止ヒート マップ** ターゲットに相対的に値を表示します。 **ターゲット** プロパティは [比較] フィールドと [値] フィールド間のデルタを決定します。 結果のデルタによって、緑から黄色と赤までのマップの関連領域を塗りつぶす色が決まります。 **[値の方向]** ボックスで、高い値と低い値のどちらを緑色にするかを設定できます。  
  
## <a name="select-the-map-type-and-region"></a>マップの種類と領域の選択  
  
1. **[レイアウト]** タブで、マップの種類を選択して、それをデザイン画面にドラッグし、必要なサイズにします。  
  
2. **[レイアウト]** ビュー、 **[表示プロパティ]** パネル、 **[マップ]** の順に選択し、必要な特定のマップ領域を選択します。  
  
   ![SSMRP_SelectMap](../../reporting-services/mobile-reports/media/ssmrp-selectmaps.png)  
  
3. 放射ヒート マップと範囲停止ヒート マップの場合、高い値と低い値のどちらが優れているかを、 **[表示プロパティ]** の下の **[値の方向]** ボックスで設定します。  
  
7. バブル マップの場合、 **[表示プロパティ]** で、 **[異なる色を使う]** を **[オン]** または **[オフ]** にして、バブルをすべて同じ色にするか、すべて異なる色にします。  
  
## <a name="select-the-map-data"></a>マップ データの選択  
最初にレポートにマップを追加すると、 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] によって、シミュレート済みの地理データが入力されます。  
  
![SSMRP_MapsData](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
マップに実際のデータを表示するには、少なくとも 2 つのマップのデータ プロパティの値を設定する必要があります。   
* **[キー]** プロパティは、データを特定のマップ領域 (たとえば、米国の州やアフリカの国) に接続します。  
* **[値]** プロパティは、選択されたキー フィールドと同じテーブル内の数値フィールドです。 これらの値は、マップごとに異なる方法で表示されます。 **グラデーション マップ** では、これらの値が、値の範囲に基づいたさまざまな網掛けで各領域に色を付けるために使われます。 **バブル マップ** では、各地域のバブル視覚エフェクトのサイズが値プロパティに基づきます。   
* 範囲停止ヒート マップの場合は、 **[ターゲット]** プロパティも設定する必要があります。  
  
### <a name="set-map-data-properties"></a>マップ データ プロパティの設定  
  
1. 左上隅にある **[データ]** タブを選択します。  
  
2. **[データの追加]** を選択し、次に **ローカル Excel** または **[SSRS サーバー]** を選択します。  
  
   > **ヒント**: データが [モバイル レポートに適した形式](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)であることを確認してください。  
  
3. 目的のワークシートを選択し、 **[インポート]** を選択します。  
   [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]でデータを確認します。  
  
4. この **[データ]** ビュー、 **[データのプロパティ]** パネル、 **[キー]** の順に移動して、左のボックスからマップ データを含むテーブルを選択し、右のボックスから、マップ内の領域に一致するキー フィールドを選択します。  
  
5. **[値]** の下で、同じテーブルが既に左のボックスにあります。 マップに表示する値を持つ数値フィールドを選択します。   
  
6. これが範囲停止ヒート マップである場合は、 **[ターゲット]** ボックスの下の左のボックスに同じテーブルがあります。 右のボックスで、ターゲットにする値を持つ数値フィールドを選択します。   
  
   ![SSMRP_MapRangeHeatData](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatdata.png)  
  
7. 左上隅の **[プレビュー]** を選択します。  
  
   ![SSMRP_MapRangeHeatPreview](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatpreview.png)  
     
8. 左上隅の **[保存]** アイコンを選択して、コンピューターに **[ローカルに保存]** するか、または **[サーバーに保存]** します。  
  
### <a name="see-also"></a>参照  
-  [Reporting Services モバイル レポートのカスタム マップ](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (SQL Server Mobile Report Publisher でモバイル レポートを作成し発行する)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  
