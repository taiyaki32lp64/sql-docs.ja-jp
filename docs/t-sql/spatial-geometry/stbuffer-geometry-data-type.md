---
title: STBuffer (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBuffer (geometry Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geometry Data Type)
ms.assetid: ca6bf2dc-1d38-4503-b87e-f2ea033d36ba
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 01d7b5277e0711f5297e00d7b08b12e105b7f78b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930367"
---
# <a name="stbuffer-geometry-data-type"></a>STBuffer (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** インスタンスからの距離が指定した値以下となる、すべての地点の和集合を表すジオメトリック オブジェクトを返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>引数  
 *distance*  
 **float** 型 (.NET Framework では **double** 型) の値であり、バッファー計算の対象とする geometry インスタンスからの距離を指定します。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 `STBuffer()` は、*tolerance* = distance \* .001 と *relative* = **false** を指定して [BufferWithTolerance](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md) と同様の方法でバッファーを計算します。  
  
 *distance* > 0 のときは、**Polygon** または **MultiPolygon** インスタンスが返されます。  
  
> [!NOTE]  
>  distance は **float** であるため、非常に小さな値は計算においてゼロと同一視されることがあります。  その場合、呼び出し元の **geometry** インスタンスのコピーが返されます。  「[float と real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)」を参照してください。  
  
 *distance* = 0 のときは、呼び出し元の **geometry** インスタンスのコピーが返されます。  
  
 *distance* < 0 のときは、  
  
-   インスタンスのディメンションが 0 または 1 であれば、空の **GeometryCollection** インスタンスが返されます。  
  
-   インスタンスのディメンションが 2 以上のとき、負の値のバッファーが返されます。  
  
    > [!NOTE]  
    >  負の値のバッファーでは、空の **GeometryCollection** インスタンスが作成されることもあります。  
  
 バッファーに負の値を指定すると、geometry インスタンスの境界から、指定された距離の範囲内にある地点がすべて削除されます。  
  
 理論上のバッファーと計算されたバッファーの間の誤差は、max(tolerance, extents * 1.E-7) です。tolerance は distance \* .001 になります。 エクステントの詳細については、「[geometry データ型メソッド リファレンス](https://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-calling-stbuffer-with-parametervalue--0-on-one-dimensional-geometry-instance"></a>A. 1 次元の geometry インスタンスに対して、パラメーターに 0 を下回る (< 0) 値を指定して、STBuffer() を呼び出す  
 次の例では、空の `GeometryCollection` インスタンスが返されます。  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="b-calling-stbuffer-with-parametervalue--0-on-a-polygon-instance"></a>B. Polygon インスタンスに対して、パラメーターに 0 を下回る (< 0) 値を指定して、STBuffer() を呼び出す  
 次の例では、バッファーが負の値の `Polygon` インスタンスが返されます。  
  
```
 DECLARE @g geometry = 'POLYGON((1 1, 1 5, 5 5, 5 1, 1 1))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="c-calling-stbuffer-with-parametervalue--0-on-a-curvepolygon-instance"></a>C. CurvePolygon インスタンスに対して、パラメーターに 0 を下回る (< 0) 値を指定して、STBuffer() を呼び出す  
 次の例では、`CurvePolygon` インスタンスからバッファーが負の値の `Polygon` インスタンスが返されます。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
> [!NOTE]  
>  `CurvePolygon` インスタンスの代わりに `Polygon` インスタンスが返されます。  `CurvePolygon` インスタンスを返すには、「[BufferWithCurves &#40;geometry Data Type&#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)」を参照してください。  
  
### <a name="d-calling-stbuffer-with-a-negative-parameter-value-that-returns-an-empty-instance"></a>D. 負のパラメーター値を指定して STBuffer() を呼び出し、空のインスタンスを取得する  
 次の例では、前の例で *distance* パラメーターが -2 の場合にどうなるかを示します。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-2).ToString();
 ```  
  
 この **SELECT** ステートメントからは `GEOMETRYCOLLECTION EMPTY.` が返されます。  
  
### <a name="e-calling-stbuffer-with-parametervalue--0"></a>E. パラメーターに 0 を指定して STBuffer() を呼び出す  
 次の例では、呼び出し元の `geometry` インスタンスのコピーが返されます。  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(0).ToString();
 ```  
  
### <a name="f-calling-stbuffer-with-a-non-zero-parameter-value-that-is-extremely-small"></a>F. パラメーターに 0 以外の非常に小さい値を指定して、STBuffer() を呼び出す  
 次の例でも、呼び出し元の `geometry` インスタンスのコピーが返されます。  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.STBuffer(@distance).ToString();
 ```  
  
### <a name="g-calling-stbuffer-with-parametervalue--0"></a>G. パラメーターに 0 を上回る (> 0) 値を指定して STBuffer() を呼び出す  
 次の例では、`Polygon` インスタンスが返されます。  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(2).ToString();
 ```  
  
### <a name="h-calling-stbuffer-with-a-string-parameter-value"></a>H. 文字列のパラメーター値を指定して STBuffer() を呼び出す  
 次の例では、前と同じように `Polygon` インスタンスが返されますが、文字列パラメーターをメソッドに渡します。  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('2').ToString();
 ```  
  
 次の例では、エラーがスローされます。  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('a').ToString();
 ```  
  
> [!NOTE]  
>  前の 2 つの例では、文字列リテラルを `STBuffer()` に渡しています。  最初の方の例は、文字列リテラルを数値に変換できるので機能します。 一方、2 番目の例では `ArgumentException` がスローされます。  
  
### <a name="i-calling-stbuffer-on-a-multipoint-instance"></a>I. MultiPoint インスタンスに対して STBuffer() を呼び出す  
 次の例では、2 つの `MultiPolygon` インスタンスと 1 つの `Polygon` インスタンスが返されます。  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.STBuffer(1).ToString(); 
 SELECT @g.STBuffer(1.5).ToString(); 
 SELECT @g.STBuffer(1.6).ToString();
 ```  
  
 最初の 2 つの **SELECT** ステートメントでは、*distance* が (1 1) と (1 4) の 2 つの地点の距離の 1/2 以下であるため、`MultiPolygon` インスタンスが返されます。 3 番目の **SELECT** ステートメントでは、(1 1) と (1 4) の 2 つの地点のバッファーに格納されたインスタンスが重なるため、`Polygon` インスタンスが返されます。  
  
## <a name="see-also"></a>参照  
 [BufferWithTolerance &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)   
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

