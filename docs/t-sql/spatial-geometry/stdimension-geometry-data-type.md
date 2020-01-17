---
title: STDimension (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDimension_TSQL
- STDimension (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDimension (geometry Data Type)
ms.assetid: 4fbd27dd-317b-4916-a8ae-4df1b8a6f27c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1feffb9116294c6dc77af5bae2552362fd8e532b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107837"
---
# <a name="stdimension-geometry-data-type"></a>STDimension (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** インスタンスの最大次元数を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STDimension ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **int**  
  
 CLR の戻り値の型:**SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 **geometry** インスタンスが空の場合、`STDimension()` は 1 を返します。  
  
## <a name="examples"></a>使用例  
 **geometry** インスタンスを保持するテーブル変数を作成し、`Point`、`LineString`、`Polygon` を挿入する例を次に示します。  その後、`STDimension()` を使用して各 **geometry** インスタンスの次元を返します。  
  
```  
DECLARE @temp table ([name] varchar(10), [geom] geometry);  
INSERT INTO @temp values ('Point', geometry::STGeomFromText('POINT(3 3)', 0));  
INSERT INTO @temp values ('LineString', geometry::STGeomFromText('LINESTRING(0 0, 3 3)', 0));  
INSERT INTO @temp values ('Polygon', geometry::STGeomFromText('POLYGON((0 0, 3 0, 0 3, 0 0))', 0));  
SELECT [name], [geom].STDimension() as [dim]  
FROM @temp;  
```  
  
 次に、各 `geometry` インスタンスの次元を返す例を示します。  
  
|NAME|dim|  
|----------|---------|  
|ポイント|0|  
|LineString|1|  
|Polygon|2|  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

