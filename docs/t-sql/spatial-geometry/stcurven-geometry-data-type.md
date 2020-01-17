---
title: STCurveN (geometry データ型) | Microsoft Docs
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
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9b9e958085af5f70d4dedb1f9a44866c04918343
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930130"
---
# <a name="stcurven-geometry-data-type"></a>STCurveN (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

**LineString**、**CircularString**、**CompoundCurve**、または **MultiLineString** である **geometry** インスタンスから指定された曲線を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STCurveN ( curve_index )  
```  
  
## <a name="arguments"></a>引数  
 *curve_index*  
 1 から **geometry** インスタンス内の曲線の数までの **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
## <a name="exceptions"></a>例外  
 *curve_index* < 1 の場合、`ArgumentOutOfRangeException` がスローされます。  
  
## <a name="remarks"></a>Remarks  
 次のいずれかの場合、**NULL** が返されます。  
  
-   **geometry** インスタンスが宣言されているが、インスタンス化されていない  
  
-   **geometry** インスタンスが空  
  
-   *curve_index* が **geometry** インスタンス内の曲線の数を超えている  
  
-   **geometry** インスタンスが **Point**、**MultiPoint**、**Polygon**、**CurvePolygon**、または **MultiPolygon** である  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>A. CircularString インスタンスに対して STCurveN() を使用する  
 次の例では、`CircularString` インスタンスの 2 番目の曲線が返されます。  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 このトピックの前の例では、次の値が返されます。  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve-instance-with-one-circularstring-instance"></a>B. 1 つの CircularString インスタンスを持つ CompoundCurve インスタンスに対して STCurveN() を使用する  
 次の例では、`CompoundCurve` インスタンスの 2 番目の曲線が返されます。  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 このトピックの前の例では、次の値が返されます。  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-instance-with-three-circularstring-instances"></a>C. 3 つの CircularString インスタンスを持つ CompoundCurve インスタンスに対して STCurveN() を使用する  
 次の例では、3 つの異なる `CompoundCurve` インスタンスを前の例と同じ曲線シーケンスに結合した `CircularString` インスタンスを使用します。  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE (CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246), CIRCULARSTRING(3 6.3246, 0 7, -3 6.3246), CIRCULARSTRING(-3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 このトピックの前の例では、次の値が返されます。  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
 前の 3 つの例の結果が同じであることに注意してください。 同じ曲線シーケンスの入力にどの WKT (Well-known Text) 形式を使用しても、`STCurveN()` インスタンスを使用する場合、`CompoundCurve` によって返される結果は同じです。  
  
### <a name="d-validating-the-parameter-before-calling-stcurven"></a>D. STCurveN() を呼び出す前に、パラメーターを検証する  
 次の例では、`STCurveN()` メソッドを呼び出す前に `@n` が有効であることを確認する方法を示しています。  
  
```
 DECLARE @g geometry;  
 DECLARE @n int;  
 SET @n = 3;  
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
 ```  
  
## <a name="see-also"></a>参照  
 [STNumCurves &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

