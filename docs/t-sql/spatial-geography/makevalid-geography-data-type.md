---
title: MakeValid (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid method (geography)
ms.assetid: f67038e3-4f62-4465-994e-e95ac27d8ada
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d913a0e7bbe29ab6f6f303519c73304238afd7df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127402"
---
# <a name="makevalid-geography-data-type"></a>MakeValid (geography データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  無効な **geography** インスタンスを、有効な Open Geospatial Consortium (OGC) 型の **geography** インスタンスに変換します。  
  
 入力オブジェクトが STIsValid() に対して False を返す場合、`MakeValid()` はこの無効なインスタンスを有効なインスタンスに変換します。  
  
 この geography データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 このメソッドにより、**geography** インスタンスの型が変更されることがあります。 さらに、**geography** インスタンスの地点がわずかに移動することもあります。 いくつかのメソッド (NumPoint() など) の結果が変更されることがあります。  
  
 無効な空間インスタンスが赤道と交差し、EnvelopeAngle() = 180 である場合、**FullGlobe** インスタンスが返されます。 `MakeValid()`**geography** データ型のメソッドは、有効なインスタンスを返すように試みますが、結果が正確であることは保証されません。  
  
> [!NOTE]  
>  無効なオブジェクトをデータベースに格納することができます。 無効なインスタンス (STIsValid() が False を返すインスタンス) で実行可能なメソッドは、有効性を確認するメソッドまたはエクスポートを許可するメソッドであり、それらは次のとおりです。STIsValid()、MakeValid()、STAsText()、STAsBinary()、ToString()、AsTextZM()、AsGml()。  
  
 このメソッドは正確ではありません。  
  
## <a name="examples"></a>使用例  
 最初に、そのインスタンス自体が重なる、無効な `LineString` インスタンスを作成し、`STIsValid()` を使用して、無効なインスタンスであることを確認する例を示します。 `STIsValid()` は、無効なインスタンスに対して値 0 を返します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 4326);  
SELECT @g.STIsValid();  
```  
  
 次に、`MakeValid()` を使用してインスタンスを有効にし、そのインスタンスが実際に有効であるかどうかをテストする例を示します。 `STIsValid()` は、有効なインスタンスに対して値 1 を返します。  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.STIsValid();  
```  
  
 最後に、このインスタンスがどのようにして有効なインスタンスに変換されたかを検証する例を示します。  
  
```  
SELECT @g.ToString();  
```  
  
 この例では、`LineString` インスタンスが選択されると、値は有効な `MultiLineString` インスタンスとして返されます。  
  
```  
MULTILINESTRING ((0 2, 1 1, 2 2), (1 1, 1 0))  
```  
  
## <a name="see-also"></a>参照  
 [STIsValid &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
