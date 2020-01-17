---
title: STCurveToLine (geography データベース型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCurveToLine_TSQL
- STCurveToLine
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geography)
ms.assetid: 2f863a85-6168-465a-b32f-bb5e3de58dee
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d6c68aa9859fbe7e1066ad392377d6b50289fd0a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042392"
---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  円弧を含む **geography** インスタンスの多角形近似を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STCurveToLine()  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 **CircularString** または **CompoundCurve** インスタンスに対して **LineString** インスタンスを返します。  
  
 **CurvePolygon** インスタンスに対して **Polygon** インスタンスを返します。  
  
 **CircularString**、**CompoundCurve**、または **CurvePolygon** インスタンスを含まない **geography** インスタンスのコピーを返します。  
  
 SQL MM 仕様とは異なり、このメソッドは多角形近似の計算に z 座標値を使用しません。 呼び出し元の **geography** インスタンスに含まれているすべての z-coordinate 値は無視されます。  
  
## <a name="examples"></a>使用例  
 次の例は、`LineString` インスタンスの多角形近似である `CircularString` インスタンスを返します。  
  
```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography;  
 SET @g2 = @g1.STCurveToLine();  
 SELECT @g1.STNumPoints() AS G1, @g2.STNumPoints() AS G2;
 ```  
  
## <a name="see-also"></a>参照  
 [STLength &#40;geography データ型&#41;](../../t-sql/spatial-geography/stlength-geography-data-type.md)   
 [STNumPoints &#40;geography データ型&#41;](../../t-sql/spatial-geography/stnumpoints-geography-data-type.md)   
 [空間データ型の概要](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
