---
title: ShortestLineTo (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 4bb425d07d566f4bb06d18a8f74f493a649fa8b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101023"
---
# <a name="shortestlineto-geometry-data-type"></a>ShortestLineTo (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

2 つの **geometry** インスタンスの間の最短距離を表す 2 つの点を持つ **LineString** インスタンスを返します。 返される **LineString** インスタンスの長さは、2 つの **geometry** インスタンスの間の距離です。
  
## <a name="syntax"></a>構文  
  
```  
  
.ShortestLineTo ( geometry_other )  
```  
  
## <a name="arguments"></a>引数  
 *geometry_other*  
 呼び出し元の **geometry** インスタンスとの最短距離を判別するための 2 つ目の **geometry** インスタンス。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 このメソッドでは、比較対象の 2 つの交差しない **geometry** インスタンスの境界上にあるエンドポイントを持つ **LineString** インスタンスが返されます。 返される **LineString** インスタンスの長さは、2 つの **geometry** インスタンスの間の最短距離です。 2 つの **geometry** インスタンスが相互に交差しているとき、空の **LineString** インスタンスが返されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. 交差しないインスタンスに対して ShortestLineTo() を呼び出す  
 この例では、`CircularString` インスタンスと `LineString` インスタンスの間の最短距離を調べ、その 2 つの点を結ぶ `LineString` インスタンスを返します。  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(-4 7, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. 交差するインスタンスに対して ShortestLineTo() を呼び出す  
 次の例では、`LineString` インスタンスが `LineString` インスタンスと交差しているため、空の `CircularString` インスタンスが返されます。  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(0 5, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
## <a name="see-also"></a>参照  
 [ShortestLineTo &#40;geography データ型&#41;](../../t-sql/spatial-geography/shortestlineto-geography-data-type.md)  
  
  

