---
title: BufferWithCurves (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geometry)
ms.assetid: 8ffaba3f-d2dd-4e57-9f41-3ced9f14b600
author: MladjoA
ms.author: mlandzic
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 608b6cc3ee887a8d17b30a027a7669d51c8822ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929313"
---
# <a name="bufferwithcurves-geometry-data-type"></a>BufferWithCurves (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  呼び出し元の **geometry** インスタンスからの距離が *distance* パラメーターの値以下となる、すべての地点のセットを表す **geometry** インスタンスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>引数  
 *distance*  
 バッファーを形成するポイントの、**geometry** インスタンスからの最大距離を示す **float** を指定します。  
  
## <a name="return-types"></a>戻り値の型  
SQL Server 戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
## <a name="exceptions"></a>例外  
 次の条件を満たす場合、**ArgumentException** がスローされます。  
  
-   パラメーター (`@g.BufferWithCurves()` など) は、このメソッドに渡されません。  
  
-   数値以外のパラメーター (`@g.BufferWithCurves('a')` など) がこのメソッドに渡されます。  
  
-   `@g.BufferWithCurves(NULL)` のように、**NULL** がメソッドに渡された。  
  
## <a name="remarks"></a>Remarks  
 次の図には、このメソッドによって返される geometry インスタンスの例を示しています。  
  
 ![BufferedCurve](../../t-sql/spatial-geometry/media/bufferedcurve.gif)
  
 次の表に、さまざまな distance 値に対して返される結果を示します。  
  
|distance 値|型ディメンション|返される空間の種類|  
|--------------------|---------------------|---------------------------|  
|distance < 0|0 または 1|空の **GeometryCollection** インスタンス|  
|distance < 0|2 以上|負のバッファーを持つ **CurvePolygon** または **GeometryCollection** インスタンス **注:** 負の値のバッファーでは、空の **GeometryCollection** が作成されることがあります|  
|distance = 0|すべてのディメンション|呼び出し元の **geography** インスタンスのコピー|  
|distance > 0|すべてのディメンション|**CurvePolygon** または **GeometryCollection** インスタンス|  
  
> [!NOTE]  
>  *distance* は **float** であるため、非常に小さな値は計算においてゼロと同一視されることがあります。 その場合、呼び出し元のコピー **geometry** インスタンスが返されます。 「[float と real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)」を参照してください。  
  
 バッファーに負の値を指定すると、geometry インスタンスの境界から、指定された距離の範囲内にある地点がすべて削除されます。 次の図には、負の値のバッファーを薄い網掛けがある円の領域として示しています。 点線は元の多角形の境界を示しており、実線は結果として得られる多角形の境界を示しています。  
  
 **string** パラメーターをこのメソッドに渡すと、**float** に変換されるか、`ArgumentException` がスローされます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geometry-instance"></a>A. 1 次元の geometry インスタンスに対して、パラメーターに 0 を下回る値を指定して、BufferWithCurves() を呼び出す  
 次の例では、空の `GeometryCollection` インスタンスが返されます。  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(-1).ToString(); 
 ```
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geometry-instance"></a>B. 2 次元の geometry インスタンスに対して、パラメーターに 0 を下回る値を指定して、BufferWithCurves() を呼び出す  
 次の例では、バッファーが負の値の `CurvePolygon` インスタンスが返されます。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. パラメーターに 0 を下回る (< 0) 値を指定して、BufferWithCurves() を呼び出し、空の GeometryCollection を返す  
 次の例では、*distance* パラメーターが -2 の場合にどうなるかを示します。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 この **SELECT** ステートメントからは `GEOMETRYCOLLECTION EMPTY` が返されます。  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. パラメーター値に 0 を指定して、BufferWithCurves() を呼び出す  
 次の例では、呼び出し元の **geometry** インスタンスのコピーが返されます。  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. パラメーターに 0 以外の非常に小さい値を指定して、BufferWithCurves() を呼び出す  
 次の例では、呼び出し元の **geometry** インスタンスのコピーも返されます。  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 DECLARE @distance float = 1e-20; 
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. パラメーターに 0 を上回る (> 0) 値を指定して、BufferWithCurves() を呼び出す  
 次の例では、`CurvePolygon` インスタンスが返されます。  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
  
### <a name="g-passing-a-valid-string-parameter"></a>G. 有効な文字列パラメーターを渡す  
 次の例では、前と同じように `CurvePolygon` インスタンスが返されますが、文字列パラメーターをメソッドに渡します。  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves('2').ToString();
 ```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. 無効な文字列パラメーターを渡す  
 次の例では、エラーがスローされます。  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)' 
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 前の 2 つの例では、文字列リテラルを `BufferWithCurves()` メソッドに渡しています。 最初の方の例は、文字列リテラルを数値に変換できるので機能します。 一方、2 番目の例では `ArgumentException` がスローされます。  
  
### <a name="i-calling-bufferwithcurves-on-multipoint-instance"></a>I. MultiPoint インスタンスに対して BufferWithCurves() を呼び出す  
 次の例では、2 つの `GeometryCollection` インスタンスと 1 つの `CurvePolygon` インスタンスが返されます。  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.BufferWithCurves(1).ToString(); 
 SELECT @g.BufferWithCurves(1.5).ToString(); 
 SELECT @g.BufferWithCurves(1.6).ToString();
 ```  
  
 最初の 2 つの **SELECT** ステートメントでは、*distance* が (1 1) と (1 4) の 2 つの地点の距離の 1/2 以下であるため、`GeometryCollection` インスタンスが返されます。 3 番目の **SELECT** ステートメントでは、(1 1) と (1 4) の 2 つの地点のバッファーに格納されたインスタンスが重なるため、`CurvePolygon` インスタンスが返されます。  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの拡張メソッド](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
 
