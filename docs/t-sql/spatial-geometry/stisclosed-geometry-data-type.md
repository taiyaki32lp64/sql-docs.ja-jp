---
title: STIsClosed (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed_TSQL
- STIsClosed (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed (geometry Data Type)
ms.assetid: 14edbb22-df7b-4b8a-b16c-ac477a5d32c1
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 46ed6c4f4d01b6c4ce1851c24a678617967560a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950052"
---
# <a name="stisclosed-geometry-data-type"></a>STIsClosed (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

指定された **geometry** インスタンスの始点と終点が同じ場合は 1 を返します。 含まれている各 **geometry** インスタンスが閉じている場合は、**geometrycollection** 型に対して 1 を返します。 インスタンスが閉じていない場合は 0 を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型:**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 **geometry** インスタンスの任意の図形が地点の場合、またはインスタンスが空の場合、このメソッドは 0 を返します。  
  
 すべての **Polygon** インスタンスは閉じていると見なされます。  
  
## <a name="examples"></a>使用例  
 `LineString` インスタンスを作成し、`STIsClosed()` を使用して `LineString` が閉じているかどうかをテストする例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

