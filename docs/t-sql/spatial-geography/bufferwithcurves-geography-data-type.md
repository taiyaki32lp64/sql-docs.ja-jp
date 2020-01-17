---
title: BufferWithCurves (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6f0e5927216d6bc0ff1acbb2146d7f23c31012ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066549"
---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves (geography データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  呼び出し元の **geography** インスタンスからの距離が *distance* パラメーターの値以下となる、すべての地点のセットを表す **geography** インスタンスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>引数  
 *distance*  
 バッファーを形成するポイントの、geography インスタンスからの最大距離を示す **float** を指定します。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="exceptions"></a>例外  
 次の条件を満たす場合、**ArgumentException** がスローされます。  
  
-   パラメーター (`@g.BufferWithCurves()` など) がこのメソッドに渡されない。  
  
-   `@g.BufferWithCurves('a')` のように、数値以外のパラメーターがメソッドに渡された。  
  
-   `@g.BufferWithCurves(NULL)` のように、**NULL** がメソッドに渡された。  
  
## <a name="remarks"></a>Remarks  
 次の表に、さまざまな distance 値に対して返される結果を示します。  
  
|distance 値|型ディメンション|返される空間の種類|  
|--------------------|---------------------|---------------------------|  
|distance < 0|0 または 1|空の **GeometryCollection** インスタンス|  
|distance \< 0|2 以上|負のバッファーを持つ **CurvePolygon** または **GeometryCollection** インスタンス<br /><br /> 注:負の値のバッファーでは、空の **GeometryCollection** が作成されることがあります|
|distance = 0|すべてのディメンション|呼び出し元の **geography** インスタンスのコピー|  
|distance > 0|すべてのディメンション|**CurvePolygon** または **GeometryCollection** インスタンス|  
  
> [!NOTE]  
>  *distance* は **float** であるため、非常に小さな値は計算においてゼロと同一視されることがあります。  その場合、呼び出し元の **geography** インスタンスのコピーが返されます。  
  
 **string** パラメーターをこのメソッドに渡すと、**float** に変換されるか、`ArgumentException` がスローされます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geography-instance"></a>A. 1 次元の geography インスタンスに対して、パラメーターに 0 を下回る (< 0) 値を指定して、BufferWithCurves() を呼び出す  
 次の例では、空の `GeometryCollection` インスタンスが返されます。  
  
 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(-1).ToString();
``` 
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geography-instance"></a>B. 2 次元の geography インスタンスに対して、パラメーターに 0 を下回る (< 0) 値を指定して、BufferWithCurves() を呼び出す  
 次の例では、バッファーが負の値の `CurvePolygon` インスタンスが返されます。  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. パラメーターに 0 を下回る (< 0) 値を指定して、BufferWithCurves() を呼び出し、空の GeometryCollection を返す  
 次の例では、*distance* パラメーターが -2 の場合にどうなるかを示します。  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 この **SELECT** ステートメントからは `GEOMETRYCOLLECTION EMPTY` が返されます。  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. パラメーター値に 0 を指定して、BufferWithCurves() を呼び出す  
 次の例では、呼び出し元の **geography** インスタンスのコピーが返されます。  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. パラメーターに 0 以外の非常に小さい値を指定して、BufferWithCurves() を呼び出す  
 次の例では、呼び出し元の **geography** インスタンスのコピーも返されます。  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. パラメーターに 0 を上回る (> 0) 値を指定して、BufferWithCurves() を呼び出す  
 次の例では、`CurvePolygon` インスタンスが返されます。  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
### <a name="g-passing-a-valid-string-parameter"></a>G. 有効な文字列パラメーターを渡す  
 次の例では、前と同じように `CurvePolygon` インスタンスが返されますが、文字列パラメーターをメソッドに渡します。  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves('2').ToString();
```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. 無効な文字列パラメーターを渡す  
 次の例では、エラーがスローされます。  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)'  
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 前の 2 つの例では、文字列リテラルを `BufferWithCurves()` メソッドに渡しています。 最初の方の例は、文字列リテラルを数値に変換できるので機能します。 一方、2 番目の例では `ArgumentException` がスローされます。  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  
