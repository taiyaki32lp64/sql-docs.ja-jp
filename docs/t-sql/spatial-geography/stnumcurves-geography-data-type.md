---
title: STNumCurves (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumCurves
- STNumCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geography)
ms.assetid: e98a56c2-8496-4dfd-9b37-7f3c4ca9b2b5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f7a525dedd8f5cbfbf881da63b7bb40f461bc802
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120932"
---
# <a name="stnumcurves-geography-data-type"></a>STNumCurves (geography データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  1 次元の **geography** インスタンスに含まれる曲線の数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 1 次元の空間データ型には、**LineString**、**CircularString**、**CompoundCurve** があります。 空の 1 次元 **geography** インスタンスは 0 を返します。す。  
  
 `STNumCurves`() は単純型に対してのみ機能し、**MultiLineString** のような **geography** コレクションでは機能しません。 **geography** インスタンスが 1 次元のデータ型ではない場合、**NULL** が返されます。  
  
 初期化されていない **geography** インスタンスに対しては **Null** が返されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. CircularString インスタンスに対して STNumCurves() を使用する  
 次の例では、`CircularString` インスタンスに含まれる曲線の数を取得する方法を示します。  
  
```
 DECLARE @g geography; 
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. CompoundCurve インスタンスに対して STNumCurves() を使用する  
 次の例では、`STNumCurves()` を使用して、`CompoundCurve` インスタンスに含まれる曲線の数を返します。  
  
```
 DECLARE @g geography;  
 SET @g = geography::Parse('COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>参照  
 [空間データ型の概要](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
