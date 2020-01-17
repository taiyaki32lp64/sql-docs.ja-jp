---
title: レポート パラメーターの追加、変更、または削除 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d44a8e0a-10cf-4502-9391-09743ffc9bad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eb0d29f62a3751f0b8b6acd1c33c7b7f7eb10ff2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65582070"
---
# <a name="add-change-or-delete-a-report-parameter-report-builder-and-ssrs"></a>レポート パラメーターの追加、変更、または削除 (レポート ビルダーおよび SSRS)
  レポート パラメーターは、レポート データの選択、他のレポートとの関連付け、レポートの表示方法の変更などの用途に使用されます。 既定値や使用可能な値のリストを指定できるほか、ユーザーに選択内容を変更させることもできます。  
  
 レポートをパブリッシュした後、レポート サーバーから、レポート パラメーターの各種プロパティ (既定値や使用可能な値など) を変更できます。 リンク レポートを作成して、既定のパラメーター値の複数のセットを指定できます。 詳細については、「 [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
 この記事では、 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] または [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のレポート デザイナーで改ページされたレポートにレポート パラメーターを追加する方法について説明します。 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]でモバイル レポートにレポート パラメーターを追加することもできます。 詳細については、「 [Create mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 」をご覧ください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-or-edit-a-report-parameter"></a>レポート パラメーターを追加または編集するには  
  
1.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] または [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のレポート デザイナーの **レポート データ** ペインで、 **[パラメーター]** ノードを右クリックし、 **[パラメーターの追加]** をクリックします。 **[レポート パラメーターのプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[名前]** にパラメーターの名前を入力するか、既定の名前をそのまま使用します。  
  
3.  **[表示名]** に、レポートの実行時にパラメーター テキスト ボックスの隣に表示する文字列を入力します。  
  
4.  **[データ型]** で、パラメーター値のデータ型を選択します。  
  
5.  空白の値を含めることができる場合は、 **[空白の値を許可]** をオンにします。  
  
6.  パラメーターに NULL 値を含めることができる場合は、 **[NULL 値を許可]** をオンにします。  
  
7.  パラメーターに複数の値を選択できるようにする場合は、 **[複数の値を許可]** を選択します。  
  
8.  表示オプションを設定します。  
  
    -   パラメーターをレポート上部のツール バーに表示する場合は、 **[表示]** を選択します。  
  
    -   パラメーターがツール バーに表示されないようにする場合は、 **[非表示]** を選択します。  
  
    -   レポートのパブリッシュ後はパラメーターを非表示にし、レポート サーバーで変更できないよう保護する場合は、 **[内部]** を選択します。 レポート パラメーターは、レポート定義でのみ参照できます。 このオプションを選択した場合は、既定値を設定するか、パラメーターで Null 値を許可するように設定する必要があります。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-report-parameter"></a>レポート パラメーターを削除するには  
  
1.  **レポート データ** ペインで **[パラメーター]** ノードを展開します。  
  
2.  レポート パラメーターを右クリックし、 **[削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レポート パラメーターの値の追加、変更、または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md)   
 [レポート パラメーターの既定値の追加、変更、または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [レポート パラメーターの順序の変更 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [カスケード型パラメーターのレポートへの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [チュートリアル: レポートへのパラメーターの追加 &#40;レポート ビルダー&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Parameters コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [複数の値を持つパラメーターのレポートへの追加](../../reporting-services/report-design/add-a-multi-value-parameter-to-a-report.md)  
  
  
