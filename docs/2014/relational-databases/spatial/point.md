---
title: ポイント | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Point geometry subtype [SQL Server]
- geometry data type [SQL Server], spatial data
ms.assetid: 2a596ec4-8b2f-4962-bcb4-e5c8f77edad5
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: b5027eb9be355348e00b6f17128b821a2bfc2af4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014150"
---
# <a name="point"></a>ポイント
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 空間データの `Point` は、1 つの場所を表す 0 次元のオブジェクトです。 には、Z (昇格) 値と M (メジャー) 値が含まれる場合もあります。  
  
## <a name="geography-data-type"></a>geography データ型  
 geography データ型の Point 型は、 *Lat* が緯度、 *Long* が経度を表している 1 つの場所を表します。 緯度と経度の値は度数で測定されます。 緯度の値は、常に [-90, 90] の範囲内になります。この範囲外の値が入力されると、例外がスローされます。 経度の値は、常に [-180, 180] の範囲内になります。この範囲外の入力値は、この範囲に収まるように調整されます。 たとえば、経度の値として 190 を入力した場合は、値 -170 に調整されます。 *SRID* は、返される **geography** インスタンスの空間参照 ID を表します。  
  
## <a name="geometry-data-type"></a>geometry データ型  
 geometry データ型の Point 型は、 *X* が生成される Point の X 座標、 *Y* が生成される Point の Y 座標を表している 1 つの場所を表します。 *SRID* は、返される **geometry** インスタンスの空間参照 ID を表します。  
  
## <a name="examples"></a>使用例  
 次の例では、点 (3, 4) を表す `geometry Point`インスタンスを作成します。このインスタンスの SRID は 0 です。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT (3 4)', 0);  
```  
  
 次の例では、SRID が 0 (既定)、Z (昇格) 値が 7、M (メジャー) 値が 2.5 の、点 (3, 4) を表す `geometry``Point` インスタンスを作成します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 7 2.5)');  
```  
  
 最後の例では、 `geometry``Point` インスタンスの X、Y、Z、および M の値を返します。  
  
```  
SELECT @g.STX;  
SELECT @g.STY;  
SELECT @g.Z;  
SELECT @g.M;  
```  
  
 Z と M の値は、次の例のように明示的に NULL として指定することもできます。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 NULL NULL)');  
```  
  
## <a name="see-also"></a>参照  
 [MultiPoint](multipoint.md)   
 [STX &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stx-geometry-data-type)   
 [STY &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/sty-geometry-data-type)   
 [空間データ &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
