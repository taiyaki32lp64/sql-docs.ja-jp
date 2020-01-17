---
title: Reporting Services モバイル レポートのカスタム マップ | Microsoft Docs
description: SQL Server Mobile Report Publisher の ESRI シェープファイルと呼ばれる形式で定義された地理的マップについて学習します。
ms.date: 12/06/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 17975defea6029e4077acbe45fd3f8b0d7495267
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62759646"
---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Reporting Services モバイル レポートのカスタム マップ
SQL Server Mobile Report Publisher の地理的マップは、*ESRI シェープファイル*と呼ばれる形式で定義されます。  
  
この形式は、もともとは一企業によって設計されたものですが、広く普及した準オープン形式として GIS アプリケーションの大部分で使用されるようになりました。 この形式に従い、Mobile Report Publisher でマップを定義するときは、次の 2 つのファイルを提供する必要があります。  
  
- 図形ジオメトリ用の .SHP ファイル  
- メタデータ用の .DBF ファイル  
  
ベース ファイル名は一致する必要があります (例: *canada.shp* と *canada.dbf*)。 メタデータには、マップにデータを設定するときに使用する対応する図形の名前 (キー) を値として含む *NAME* フィールドを含める必要があります。  

SHP と DBF の 2 つのマップ ファイルのサイズの合計は、512 KB 以下である必要があります。 マップ ファイルが大きすぎる場合は、[https://mapshaper.org/](https://mapshaper.org/) などのツールを使用してサイズを小さくします。  
  
[モバイル レポートにカスタムのマップを追加](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md)する方法を確認してください。  
  
## <a name="technical-information"></a>技術情報  
  
- 公式の仕様: [https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- Wikipedia のシェープファイルの記事: [https://en.wikipedia.org/wiki/Shapefile](https://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>マップ ジオメトリの作成および編集  
  
シェープファイルの作成と編集プロセスは複雑であり、このドキュメントの範囲外です。 役に立つリソースとアプリケーションを次に示します。  
  
- ArcGIS: [https://www.arcgis.com/](https://www.arcgis.com/)  
- Adobe Illustrator 用 MAPublisher プラグイン: [https://www.avenza.com/mapublisher](https://www.avenza.com/mapublisher)  
- QuantumGIS (無料): [https://www.qgis.org/](https://www.qgis.org/)  

## <a name="existing-shapefiles"></a>既存のシェープファイル  
  
Diva-GIS ([https://www.diva-gis.org/Data](https://www.diva-gis.org/Data)) のような Web サイトから既存のシェープファイルを多数ダウンロードできます。  

## <a name="see-also"></a>参照  
- [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (SQL Server Mobile Report Publisher でモバイル レポートを作成し発行する)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
