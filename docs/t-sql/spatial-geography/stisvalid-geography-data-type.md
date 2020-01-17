---
title: STIsValid (geography データ型) | Microsoft Docs
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
- STIsValid method (geography)
ms.assetid: 1bfe787f-ddf0-4fc7-af6a-570a58faab23
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7c8b190e1678ff53d29e31dde55069739c2ce76f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079891"
---
# <a name="stisvalid-geography-data-type"></a>STIsValid (geography データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  **geography** インスタンスが整形式であり、Open Geospatial Consortium (OGC) 型に基づいて有効な geography オブジェクトとして認識されている場合に、true を返します。 **geography** インスタンスが整形式になっていない場合は false を返します。 このメソッドは正確です。  
  
 この geography データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型:**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 **geography** インスタンスの OGC 型は、[STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md) を呼び出すことによって判別できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、有効な **geography** インスタンスのみを生成しますが、無効なインスタンスの取得と格納が可能です。 無効なインスタンスと同じ地点のセットを表す有効なインスタンスは、`MakeValid()` メソッドを使用して取得できます。  
  
## <a name="examples"></a>使用例  
 `geography` インスタンスを作成し、`STIsValid()` を使用してこのインスタンスが有効かどうかをテストする例を次に示します。  
  
```  
DECLARE @g geography = geography::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 4326);  
SELECT @g.STIsValid();  
DECLARE @g geography  
```  
  
## <a name="see-also"></a>参照  
 [STGeometryType &#40;geography データ型&#41;](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)   
 [MakeValid &#40;geography データ型&#41;](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
