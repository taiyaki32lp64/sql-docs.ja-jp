---
title: STDimension (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDimension (geography Data Type)
- STDimension_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STDimension method
ms.assetid: 4368b0f6-0678-4ade-87dc-b43d8b2e8d92
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ac39de3b0fe0d85aa65ef59661a512988acd4a36
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042332"
---
# <a name="stdimension-geography-data-type"></a>STDimension (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** インスタンスの最大次元数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STDimension ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **int**  
  
 CLR の戻り値の型:**SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 STDimension() では、**geography** インスタンスが空の場合、-1 を返します。  
  
## <a name="examples"></a>使用例  
 `STDimension()` を使用して、`geography` インスタンスを保持するテーブル変数を作成し、`Point`、`LineString`、および `Polygon` を挿入する例を次に示します。  
  
```  
DECLARE @temp table ([name] varchar(10), [geom] geography);  
  
INSERT INTO @temp values ('Point', geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326));  
INSERT INTO @temp values ('LineString', geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326));  
INSERT INTO @temp values ('Polygon', geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
  
SELECT [name], [geom].STDimension() as [dim]  
FROM @temp;  
```  
  
 次に、各 `geography` インスタンスの次元を返す例を示します。  
  
|NAME|dim|  
|----------|---------|  
|ポイント|0|  
|LineString|1|  
|Polygon|2|  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
