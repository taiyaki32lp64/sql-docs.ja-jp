---
title: STGeomCollFromText (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomCollFromText_TSQL
- STGeomCollFromText (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomCollFromText method
ms.assetid: a5b3c344-1045-43a4-82fa-47f6206a288e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e8669d2d4a04fba9a18f091dabab04fc1284ce03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042250"
---
# <a name="stgeomcollfromtext-geography-data-type"></a>STGeomCollFromText (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現を基に **geography** インスタンスを返します。インスタンスに格納されている Z (標高) 値と M (メジャー) 値で補完されています。
  
## <a name="syntax"></a>構文  
  
```  
  
STGeomCollFromText ( 'geometrycollection_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>引数  
 *geometrycollection_tagged_text*  
 返される **geography** インスタンスの WKT 表現です。 *geometrycollection_tagged_text* は **nvarchar(max)** 式です。  
  
 *SRID*  
 返される **geography** インスタンスの SRID (spatial reference ID) を表す **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 STGeomCollFromText() によって返される **geography** の OGC 型は、対応する WKT 入力に設定されています。  
  
 このメソッドは、入力が無効な場合に、**ArgumentException** をスローします。  
  
## <a name="examples"></a>使用例  
 `STGeomCollFromText()` を使用して `geography` インスタンスを作成する例を次に示します。  
  
```  
DECLARE @g geography;  
DECLARE @g geography;  
SET @g = geography::STGeomCollFromText('GEOMETRYCOLLECTION ( POINT(-122.34900 47.65100), LINESTRING(-122.360 47.656, -122.343 47.656) )', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>参照  
 [OGC の静的な地理メソッド](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
