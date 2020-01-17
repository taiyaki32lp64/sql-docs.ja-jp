---
title: CurveToLineWithTolerance (geometry データ型) | Microsoft Docs
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
- CurveToLineWithTolerance method (geometry)
ms.assetid: 96871075-1998-4cd9-86b1-3fc55577aee4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 95893aac0b6ca62b60b12f9d35daf15e77e565f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929300"
---
# <a name="curvetolinewithtolerance-geometry-data-type"></a>CurveToLineWithTolerance (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

円弧を含む **geometry** インスタンスの多角形近似を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.CurveToLineWithTolerance ( tolerance, relative )  
```  
  
## <a name="arguments"></a>引数  
 *tolerance*  
 元の円弧とその線形近似の間の最大誤差を定義する **double** 式です。  
  
 *relative*  
 偏差に相対最大値を使用するかどうかを示す **bool** 式です。 relative を false (0) に設定すると、線形近似で許容される偏差に絶対最大値が設定されます。 relative を true (1) に設定すると、tolerance は tolerance パラメーターと空間オブジェクトに外接する四角形の直径の積として計算されます。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
## <a name="exceptions"></a>例外  
 tolerance <= 0 に設定すると、`ArgumentOutOfRange` 例外がスローされます。  
  
## <a name="remarks"></a>Remarks  
 このメソッドを使用すると、結果として得られる **LineString** の許容誤差量を指定できます。  
  
 次の表には、さまざまな種類の `CurveToLineWithTolerance()` によって返されるインスタンスの種類を示しています。  
  
|呼び出し元のインスタンスの種類|返される空間の種類|  
|----------------------------|---------------------------|  
|空の geometry インスタンス|空の **GeometryCollection** インスタンス|  
|**Point** と **MultiPoint**|**Point** インスタンス|  
|**MultiPoint**|**Point** または **MultiPoint** インスタンス|  
|**CircularString**、**CompoundCurve**、または **LineString**|**LineString** インスタンス|  
|**MultiLineString**|**LineString** または **MultiLineString** インスタンス|  
|**CurvePolygon** と **Polygon**|**Polygon** インスタンス|  
|**MultiPolygon**|**Polygon** または **MultiPolygon** インスタンス|  
|円弧を含まないインスタンスを 1 つ持つ **GeometryCollection**|**GeometryCollection** に含まれているインスタンスによって、返されるインスタンスの型が決まります。|  
|1 次元の円弧セグメント インスタンス (**CircularString**、**CompoundCurve**) を 1 つ持つ **GeometryCollection**|**LineString** インスタンス|  
|2 次元の円弧セグメント インスタンス (**CurvePolygon**) を 1 つ持つ **GeometryCollection**|**Polygon** インスタンス|  
|1 次元インスタンスを複数持つ **GeometryCollection**|**MultiLineString** インスタンス|  
|2 次元のインスタンスを複数持つ **GeometryCollection**|**MultiPolygon** インスタンス|  
|次元の異なるインスタンスを複数持つ **GeometryCollection**|**GeometryCollection** インスタンス|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. CircularString インスタンスに対して異なる tolerance 値を使用する  
 次の例では、許容値の設定によって、`CircularString` から返される `LineString` インスタンスが変化するしくみを確認できます。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
 ```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. 1 つの LineString を含む MultiLineString インスタンスに対してこのメソッドを使用する  
 次の例では、`MultiLineString` インスタンスを 1 つだけ含む `LineString` インスタンスから返される結果を示します。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. 複数の LineString を含む MultiLineString インスタンスに対してこのメソッドを使用する  
 次の例では、複数の `MultiLineString` インスタンスを含む `LineString` インスタンスから返される結果を示します。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9),(4 4, 9 18))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. 呼び出し元の CurvePolygon インスタンスに対して relative を true に設定する  
 次の例では、`CurvePolygon` インスタンスを使用し、*relative* を true に設定して `CurveToLineWithTolerance()` を呼び出します。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
### <a name="e-using-the-method-on-a-geometrycollection-instance"></a>E. GeometryCollection インスタンスに対してメソッドを使用する  
 次の例では、2 次元の `CurvePolygon` インスタンスと 1 次元の `CircularString` インスタンスを含む `GeometryCollection` に対して `CurveToLineWithTolerance()` を呼び出します。 `CurveToLineWithTolerance()` により、両方の円弧型が線分型に変換され、`GeometryCollection` 型で返されます。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('GEOMETRYCOLLECTION(CURVEPOLYGON( COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))), CIRCULARSTRING(4 4, 8 6, 9 5))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.1, 0).ToString();
 ```  
  
## <a name="see-also"></a>参照  
 [CurveToLineWithTolerance &#40;geography データ型&#41;](../../t-sql/spatial-geography/curvetolinewithtolerance-geography-data-type.md)   
 [STCurveToLine &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stcurvetoline-geometry-data-type.md)  
  
  

