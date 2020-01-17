---
title: Reporting Services のモバイル レポートでシミュレートされたデータを使用する | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 6baabc36-58fb-4a98-bb9c-c42bafb16d0f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 15c2ebe8c7084e10e4b7ff1ad556ed465d91c799
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62474871"
---
# <a name="work-with-simulated-data-in-reporting-services-mobile-reports"></a>Reporting Services のモバイル レポートでシミュレートされたデータを使用する
デザイン サーフェイスにギャラリー要素を配置すると、 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] は、その要素のシミュレートされたデータを即座に生成します。 このデータは、モバイル レポートを作成するときにさまざまな目的を果たします。   
  
![SS_MRP_SimDataTreeMapProps](../../reporting-services/mobile-reports/media/ss-mrp-simdatatreemapprops.png)  
  
シミュレートされたデータは、デザイン ベースのアプローチでモバイル レポートを作成する際に役立ちます。 シミュレートされたデータを要素に最初に入力しておくと、特定のデータ要件に対応することなく、モバイル レポート プロトタイプをすばやく作成できます。 その後、これらのモバイル レポートの全体的な外観と有効性を評価できます。  
  
## <a name="create-an-excel-file-with-simulated-data-as-a-template"></a>シミュレートされたデータを含む Excel ファイルをテンプレートとして作成する  
  
シミュレートされたデータは、特定のモバイル レポート デザインのデータ要件を正確に表すテンプレートとしても機能します。   
  
-  データ ビューの右上隅にある **[すべてのデータのエクスポート]** をクリックします。   
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] は、シミュレートされたデータを含む Excel ドキュメントを生成します。これらのデータを実際のデータにすばやく置き換えて、インポートする準備を整えることができます。   
  
## <a name="how-simulated-data-behaves"></a>シミュレートされたデータの動作  
  
シミュレートされたデータは、作成するモバイル レポートに合わせて生成されます。 デザイン サーフェイスにさらに要素を配置していくと、関連付けられているシミュレートされたデータが増加および変化して、実際のデータを除いた最適なエクスペリエンスを提供します。 この進化により、グラフの視覚エフェクトに追加の系列を追加するか、1 つまたは複数のモバイル レポート要素のスコープを別の方法で拡張する場合に、追加のフィールドとフィルターを使用できます。  
  
前述のように、シミュレートされたデータを Excel ファイルにエクスポートして、関連付けられているモバイル レポート用の完全なデータ テンプレートを作成できます。 この Excel ファイルのデータを実際のデータで置き換えて、 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]にインポートできます。   
  
実際のデータにすべてのコントロールがバインドされたら、使用されなくなったシミュレートされたテーブルはモバイル レポートから自動的に削除されます。 デザイン サーフェイス上の要素によって参照されているシミュレートされたテーブルは削除できません。  
  
>**注**: シミュレートされたデータによって、モバイル レポートの全体的なサイズは増加しません。これは、これらのデータはモバイル レポートでシリアル化されず、実行時にその場で生成されるからです。  
  
### <a name="see-also"></a>参照  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (SQL Server Mobile Report Publisher でモバイル レポートを作成し発行する)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [iPad アプリ (Power BI for iOS) で SQL Server モバイル レポートと KPI を表示する](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  
-  [iPhone アプリ (Power BI for iOS) で SQL Server モバイル レポートと KPI を表示する](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports)  
  
  
  
  
  

