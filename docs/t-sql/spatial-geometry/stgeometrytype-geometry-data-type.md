---
title: STGeometryType (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryType_TSQL
- STGeometryType (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryType (geometry Data Type)
ms.assetid: 224cdc83-aa83-4ad4-bb82-b7481031e910
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7aa87371bda53f1c329b0b30a490450cd7d9cba5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950182"
---
# <a name="stgeometrytype-geometry-data-type"></a>STGeometryType (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** インスタンスで表される Open Geospatial Consortium (OGC) の型名を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STGeometryType ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **nvarchar(4000)**  
  
 CLR の戻り値の型:**SqlString**  
  
## <a name="remarks"></a>Remarks  
 `STGeometryType()` によって返される OGC の型名は、**Point**、**LineString**、**CircularString**、**CompoundCurve**、**Polygon、CurvePolygon**、**GeometryCollection**、**MultiPoint**、**MultiLineString** および **MultiPolygon** です。  
  
## <a name="examples"></a>使用例  
 `Polygon` インスタンスを作成し、`STGeometryType()` を使用してこれが多角形であることを確認する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0))', 0);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

