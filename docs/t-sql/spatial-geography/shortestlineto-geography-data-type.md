---
title: ShortestLineTo (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ShortestLineTo_TSQL
- ShortestLineTo
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geography)
ms.assetid: 9d7c9885-5d1b-49ae-af31-5ef9fb8acaba
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7844f1d38f5d2e6f36f971eb83d8961596483142
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042613"
---
# <a name="shortestlineto-geography-data-type"></a>ShortestLineTo (geography データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  2 つの **geography** インスタンスの間の最短距離を表す 2 つの点を持つ **LineString** インスタンスを返します。 返される **LineString** インスタンスの長さは、2 つの **geography** インスタンスの間の距離です。  
  
## <a name="syntax"></a>構文  
  
```  
  
.ShortestLineTo ( geography_other )  
```  
  
## <a name="arguments"></a>引数  
 *geography_other*  
 呼び出し元の **geography** インスタンスとの最短距離を調べる 2 つ目の **geography** インスタンスを指定します。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 このメソッドでは、比較対象の 2 つの交差しない **geography** インスタンスの境界上にあるエンドポイントを持つ **LineString** インスタンスが返されます。 返される **LineString** インスタンスの長さは、2 つの **geography** インスタンスの間の最短距離です。 2 つの **geography** インスタンスが相互に交差している場合、空の **LineString** インスタンスが返されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. 交差しないインスタンスに対して ShortestLineTo() を呼び出す  
 この例では、`CircularString` インスタンスと `LineString` インスタンスの間の最短距離を調べ、その 2 つの点を結ぶ `LineString` インスタンスを返します。  
  
 ```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography = 'LINESTRING(-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. 交差するインスタンスに対して ShortestLineTo() を呼び出す  
 次の例では、`LineString` インスタンスが `LineString` インスタンスと交差しているため、空の `CircularString` インスタンスが返されます。  
  
 ```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography = 'LINESTRING(-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.348 47.649, -122.681 47.655)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
``` 
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
