---
title: STCrosses (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCrosses (geometry Data Type)
- STCrosses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCrosses (geometry Data Type)
ms.assetid: 3e3fc065-555a-4bee-8b71-e92f3dc62a4f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0320cbd20242f19bab7c7990f4bad13458e403e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930146"
---
# <a name="stcrosses-geometry-data-type"></a>STCrosses (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

**geometry** インスタンスが別の **geometry** インスタンスと重なり合う場合、1 を返します。 そうでない場合は 0 を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STCrosses ( other_geometry )  
```  
  
## <a name="arguments"></a>引数  
 *other_geometry*  
 `STCrosses()` を呼び出したインスタンスと比較される、別の **geometry** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型:**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 次の条件が両方とも該当する場合、2 つの **geometry** インスタンスは交差します。  
  
-   2 つの **geometry** インスタンスが交差すると、ジオメトリの次元は、基になる **geometry** インスタンスの最大次元数よりも小さくなります。  
  
-   交差集合は、基になる **geometry** インスタンスの両方に含まれる部分です。  
  
 **geometry** インスタンスの SRID (spatial reference ID) が一致しない場合、このメソッドは常に null を返します。  
  
## <a name="examples"></a>使用例  
 `STCrosses()` を使用して 2 つの `geometry` インスタンスが交差かどうかをテストする例を次に示します。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0)', 0);  
SET @h = geometry::STGeomFromText('LINESTRING(0 0, 2 2)', 0);  
SELECT @g.STCrosses(@h);  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

