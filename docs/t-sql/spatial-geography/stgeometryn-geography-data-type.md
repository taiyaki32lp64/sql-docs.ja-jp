---
title: STGeometryN (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 249639ef13d9200d1d6cedc189044c30ba8ff7ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042263"
---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **GeometryCollection** またはそのサブタイプのいずれかに含まれる、指定した **geography** 要素を返します。 **MultiPoint** や **MultiLineString** のように、STGeometryN() が **GeometryCollection** のサブタイプで使用されるとき、このメソッドは N=1 で呼び出された場合、**geography** インスタンスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STGeometryN ( expression )  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 1 から **GeometryCollection** に含まれる **geography** インスタンスの数までの数値を表す **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 パラメーターが [STNumGeometries()](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md) の結果よりも大きい場合、このメソッドは null を返します。*expression* パラメーターが 1 より小さい場合は、**ArgumentOutOfRangeException** をスローします。  
  
## <a name="examples"></a>使用例  
 `MultiPoint``geography` インスタンスを作成し、`STGeometryN()` を使用して **GeometryCollection** の 2 番目の `geography` インスタンスを見つける例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
