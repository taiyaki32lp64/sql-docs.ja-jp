---
title: STIsClosed (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed (geography Data Type)
- STIsClosed_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed method
ms.assetid: eba1643f-07c4-4500-8643-b7e90f908147
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: dbc1bd923b0e86acfd0fbae995bd6fdbd16816a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042034"
---
# <a name="stisclosed-geography-data-type"></a>STIsClosed (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定された **geography** インスタンスの始点と終点が同じ場合は 1 を返します。 含まれている各 **geometry** インスタンスが閉じている場合は、**geometrycollection** 型に対して 1 を返します。 インスタンスが閉じていない場合は 0 を返します。  
  
 この **geography** データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型:**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 **geography** インスタンスの任意の図形が地点の場合、またはインスタンスが空の場合、このメソッドは 0 を返します。  
  
 **FullGlobe** インスタンスが **Polygon** などの別の型のインスタンスの場合、このメソッドは true を返します。  
  
 すべての **Polygon** インスタンスは閉じていると見なされます。  
  
## <a name="examples"></a>使用例  
 `Polygon` インスタンスを作成し、`STIsClosed()` を使用して `Polygon` が閉じているかどうかをテストする例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
