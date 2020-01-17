---
title: 空間データ (SQL Server) | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7bd529f67f9184f86d4a9ec704e9cf7af972f3f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014056"
---
# <a name="spatial-data-sql-server"></a>空間データ (SQL Server)
  空間データは、幾何オブジェクトの物理的な位置と形状に関する情報を表します。 それらのオブジェクトは、点の位置である場合もあれば、国、道、湖などのより複雑なオブジェクトである場合もあります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、`geometry` と `geography` の 2 つの空間データ型がサポートされています。  
  
-   `geometry` 型は、ユークリッド (平面) 座標系のデータを表します。  
  
-   `geography` 型は、球体地球座標系のデータを表します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、どちらのデータ型も .NET 共通言語ランタイム (CLR) のデータ型として実装されています。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]で導入された空間機能の詳細な説明とサンプルについては、ホワイト ペーパー「 [New Spatial Features in SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407)」 (SQL Server 2012 の新しい空間機能) をダウンロードして参照してください。  
  
##  <a name="reltasks"></a> 関連タスク  
 [geometry インスタンスの作成、構築、およびクエリ](create-construct-and-query-geometry-instances.md)  
 geometry データ型のインスタンスで使用できるメソッドについて説明します。  
  
 [geography インスタンスの作成、構築、およびクエリ](create-construct-and-query-geography-instances.md)  
 geography データ型のインスタンスで使用できるメソッドについて説明します。  
  
 [空間データに対するニアレスト ネイバーのクエリ](query-spatial-data-for-nearest-neighbor.md)  
 特定の空間オブジェクトに最も近い空間オブジェクトを検索するための一般的なクエリ パターンについて説明します。  
  
 [空間インデックスの作成、変更、および削除](create-modify-and-drop-spatial-indexes.md)  
 空間インデックスの作成、変更、および削除に関する情報を提供します。  
  
## <a name="related-content"></a>関連コンテンツ  
 [空間データ型の概要](spatial-data-types-overview.md)  
 空間データ型について説明します。  
  
-   [ポイント](point.md)  
  
-   [LineString](linestring.md)  
  
-   [CircularString](circularstring.md)  
  
-   [CompoundCurve](compoundcurve.md)  
  
-   [多角形](polygon.md)  
  
-   [CurvePolygon](curvepolygon.md)  
  
-   [MultiPoint](multipoint.md)  
  
-   [MultiLineString](multilinestring.md)  
  
-   [MultiPolygon](multipolygon.md)  
  
-   [GeometryCollection](geometrycollection.md)  
  
 [空間インデックスの概要](spatial-indexes-overview.md)  
 空間インデックス、テセレーション、テセレーション スキームについて説明します。  
  
  
