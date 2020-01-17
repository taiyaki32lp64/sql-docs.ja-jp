---
title: Reporting Services のモバイル レポートを作成するときにデザインとデータのどちらを優先するか | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: a7b355fa-312b-4074-bc9b-776269d4fb51
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cf9afd8c4aa916d87929a8e7d73347cc33456252
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63066644"
---
# <a name="design-first-or-data-first-when-creating-in-reporting-services-mobile-reports"></a>Reporting Services のモバイル レポートを作成するときにデザインとデータのどちらを優先するか
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)]を使用すると、調整可能なグリッド行とグリッド列、柔軟なモバイル レポート要素を備えたデザイン画面で、任意の画面サイズに対応するモバイル レポートをすばやく作成できます。   
  
モバイル レポートを作成する際の基本的なアプローチとして、データ優先とデザイン優先の 2 とおりがあります。 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] では、両方をサポートしています。   
  
## <a name="design-first"></a>デザイン優先  
  
次の図は、 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] の [レイアウト] ビューのコンポーネントを示しています。   
  
![SS_MRP_LayoutTab](../../reporting-services/mobile-reports/media/ss-mrp-layouttab.png)  
  
デザイン優先のアプローチでは、最初に、データをインポートせずにモバイル レポートのレイアウトを作成します。 これは、データが正しく書式設定されているかどうかが不明な場合に、モバイル レポートを作成するのに適した方法です。 実際のデータがない場合、ギャラリー要素は、シミュレートされた生成データに自動的にバインドされます。この生成データは、必要なデータを記述するためのテンプレートとしてエクスポートして使用できます。  
  
## <a name="data-first"></a>データ優先  
データ優先のアプローチでは、最初に必要なデータをすべてインポートしてから、モバイル レポートをデザインし、モバイル レポート要素のデータ プロパティを設定します。 このアプローチには、要素をレイアウトに追加する際に、各要素を実際のデータに接続できるという利点があります。 データ優先のアプローチを使用する場合は、実際のデータが [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)]で使用できるように正しく書式設定されていることを確認してください。   
  
 次の図は、 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] の [データ] ビューのすべてのコンポーネントを示しています。  
  
![SS_MRP_DataTab](../../reporting-services/mobile-reports/media/ss-mrp-datatab.png)  
  
### <a name="see-also"></a>参照  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (SQL Server Mobile Report Publisher でモバイル レポートを作成し発行する)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [iPad アプリ (Power BI for iOS) で SQL Server モバイル レポートと KPI を表示する](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  
-  [iPhone アプリ (Power BI for iOS) で SQL Server モバイル レポートと KPI を表示する](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports)  
  
  
  
  

