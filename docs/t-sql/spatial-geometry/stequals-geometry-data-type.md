---
title: STEquals (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STEquals (geometry Data Type)
- STEquals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STEquals (geometry Data Type)
ms.assetid: 808f0e25-9e68-4ba7-9329-07ec950698f3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 8880c5287d65e91ccca3c223d93c7b7b070a8df3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107752"
---
# <a name="stequals-geometry-data-type"></a>STEquals (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** インスタンスが別の **geometry** インスタンスと同一地点を表している場合は 1 を返します。 そうでない場合は 0 を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STEquals ( other_geometry )  
```  
  
## <a name="arguments"></a>引数  
 *other_geometry*  
 `STEquals()` を呼び出したインスタンスと比較される、別の **geometry** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型:**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 **geometry** インスタンスの SRID (spatial reference ID) が一致しない場合、このメソッドは常に null を返します。  
  
## <a name="examples"></a>使用例  
 `STGeomFromText()` を含むほぼ同じ `geometry` インスタンスを 2 つ作成し、`STEquals()` を使用して 2 つのインスタンスが同一であるかどうかをテストする例を次に示します。  
  
```  
DECLARE @g geometry  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('MULTILINESTRING((4 2, 2 0), (0 2, 2 0))', 0);  
SELECT @g.STEquals(@h);  
```  
  
## <a name="see-also"></a>参照  
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

