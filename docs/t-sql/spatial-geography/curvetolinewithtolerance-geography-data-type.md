---
title: CurveToLineWithTolerance (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CurveToLineWithTolerance_TSQL
- CurveToLineWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geography)
ms.assetid: 74369c76-2cf6-42ae-b9cc-e7a051db2767
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6f81b5ba7ba6de057dd82090775013db55e4275b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066493"
---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance (geography データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

円弧を含む **geography** インスタンスの多角形近似を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
## <a name="arguments"></a>引数  
_tolerance_  
元の円弧とその線形近似の間の最大誤差を定義する **double** 式です。  
  
_relative_  
偏差に相対最大値を使用するかどうかを示す **bool** 式です。 relative が false (0) の場合、線形近似で許容される偏差に絶対最大値が設定されます。 relative が true (1) の場合、tolerance は tolerance パラメーターと空間オブジェクトに外接する四角形の直径の積として計算されます。  
  
## <a name="return-types"></a>戻り値の型  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
CLR の戻り値の型:**SqlGeography**  
  
## <a name="exceptions"></a>例外  
tolerance <= 0 を設定すると、**ArgumentOutOfRange** 例外がスローされます。  
  
## <a name="remarks"></a>Remarks  
このメソッドでは、結果として得られる **LineString** に許容誤差量を指定できます。  
  
**CurveToLineWithTolerance** メソッドでは、**CircularString** または **CompoundCurve** インスタンスに **LineString** インスタンスが返され、**CurvePolygon** インスタンスに **Polygon** インスタンスが返されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. CircularString インスタンスに対して異なる tolerance 値を使用する  
次の例では、許容値の設定によって、`CircularString` から返される `LineString` インスタンスが変化するしくみを確認できます。  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. 1 つの LineString を含む MultiLineString インスタンスに対してこのメソッドを使用する  
次の例では、`MultiLineString` インスタンスを 1 つだけ含む `LineString` インスタンスから返される結果を示します。  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649))');  
SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. 複数の LineString を含む MultiLineString インスタンスに対してこのメソッドを使用する  
次の例では、複数の `MultiLineString` インスタンスを含む `LineString` インスタンスから返される結果を示します。  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649),(-123.358 47.653, -123.348 47.649))');  
SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. 呼び出し元の CurvePolygon インスタンスに対して relative を true に設定する  
次の例では、`CurvePolygon` インスタンスを使用し、*relative* を true に設定して `CurveToLineWithTolerance()` を呼び出します。  
  
```
DECLARE @g geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658), (-122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
```  
  
## <a name="see-also"></a>参照  
[Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
