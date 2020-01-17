---
title: Reduce (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5725b95df233f46e9e003f6c2af155ae943ba2b1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101041"
---
# <a name="reduce-geometry-data-type"></a>Reduce (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

指定された **geometry** インスタンスの近似を返します。 近似は、指定された許容範囲で、特定のインスタンスに対して Douglas-Peucker アルゴリズムの拡張を実行することにより生成されます。
  
## <a name="syntax"></a>構文  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>引数  
 *tolerance*  
 **float** 型の値です。 *tolerance* は、近似アルゴリズムに入力する許容範囲です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 コレクションの場合、このアルゴリズムは個別に各 **geometry** インスタンスに含まれています。  
  
 このアルゴリズムによって、**Point** インスタンスが変更されることはありません。  
  
 **LineString**、**CircularString**、**CompoundCurve** のインスタンスでは、近似アルゴリズムによってインスタンスの元の始点と終点が維持されます。 次に、アルゴリズムでは、結果から最も離れた元のインスタンスの点が繰り返し追加されます。 この処理は、指定された許容範囲より大きく外れた点がなくなるまで続けられます。  
  
 `Reduce()` は、**CircularString** インスタンスに対して **LineString**、**CircularString**、**CompoundCurve** インスタンスを返します。  `Reduce()` は、**CompoundCurve** インスタンスに対して **CompoundCurve** または **LineString** インスタンスを返します。  
  
 **Polygon** インスタンスでは、近似アルゴリズムが各リングに個別に適用されます。 返された **Polygon** インスタンスが無効な場合、メソッドは `FormatException` を生成します。たとえば、インスタンス内の各リングを簡略化するために `Reduce()` が適用され、その結果リングが重なる場合、無効な **MultiPolygon** が作成されます。  外部リングがあり、内部リングがない **CurvePolygon** インスタンスでは、`Reduce()` は **CurvePolygon**、**LineString**、**Point** インスタンスを返します。  **CurvePolygon** に内部リングがある場合、**CurvePolygon** または **MultiPoint** インスタンスが返されます。  
  
 円弧が検出されると、指定された許容範囲の半分以内で弦によって円弧を近似できるかどうかが近似アルゴリズムによってチェックされます。 弦がこの条件を満たす場合、円弧は計算において弦で置き換えられます。 弦がこの条件を満たしていない場合は、円弧が保持され、近似アルゴリズムが残りのセグメントに適用されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-reduce-to-simplify-a-linestring"></a>A. Reduce() を使用して LineString を簡略化する  
 `LineString` インスタンスを作成し、`Reduce()` を使用してそのインスタンスを簡略化する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0, 2 1, 3 0, 4 1)', 0);  
SELECT @g.Reduce(.75).ToString();  
```  
  
### <a name="b-using-reduce-with-varying-tolerance-levels-on-a-circularstring"></a>B. CircularString に対し許容レベルを変えて Reduce() を使用する  
 次の例では、**CircularString** インスタンスに対して 3 つの許容レベルを適用して `Reduce()` を使用します。  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0)'; 
 SELECT @g.Reduce(5).ToString(); 
 SELECT @g.Reduce(15).ToString(); 
 SELECT @g.Reduce(16).ToString();
 ```  
  
 この例の結果は、次のようになります。  
  
 ```
 CIRCULARSTRING (0 0, 8 8, 16 0, 20 -4, 24 0) 
 COMPOUNDCURVE (CIRCULARSTRING (0 0, 8 8, 16 0), (16 0, 24 0)) 
 LINESTRING (0 0, 24 0)
 ```  
  
 返されるそれぞれのインスタンスには、終点 (0 0) と (24 0) が含まれます。  
  
### <a name="c-using-reduce-with-varying-tolerance-levels-on-a-compoundcurve"></a>C. CompoundCurve に対し許容レベルを変えて Reduce() を使用する  
 次の例では、**CompoundCurve** インスタンスに対して 2 つの許容レベルを適用して `Reduce()` を使用します。  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 この例では、2 番目の **SELECT** ステートメントによって **LineString** インスタンス (`LineString(0 0, 16 0)`) が返されます。  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>元の始点と終点が失われる例を示す  
 次の例では、元の始点と終点が結果のインスタンスで保持されない状況を示します。 このような動作は、元の始点と終点を保持した結果、**LineString** インスタンスが無効となった場合に発生します。  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>参照  
 [拡張された静的なジオメトリ メソッド](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
