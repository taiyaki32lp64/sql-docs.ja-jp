---
title: Parse (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 209186cf3756c0bfb9b572a33ba470a83e0cd493
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051441"
---
# <a name="parse-geography-data-type"></a>Parse (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現を基に **geography** インスタンスを返します。 Parse() は、SRID (spatial reference ID) 4326 をパラメーターとして想定する点を除いて、[STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md) と同じです。 入力には、オプションとして Z (標高) 値と M (メジャー) 値が含まれる場合があります。
  
この **geography** データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。
  
## <a name="syntax"></a>構文  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>引数  
 *geography_tagged_text*  
 返される **geography** インスタンスの WKT 表現です。 *geography_tagged_text* は **nvarchar** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 `Parse()` によって返された **geography** インスタンスの OGC 型は、対応する WKT 入力に設定されます。  
  
 "NULL" 文字列は、**geography** の NULL インスタンスと解釈されます。  
  
 このメソッドは、入力に対蹠点が含まれている場合、**ArgumentException** をスローします。  
  
## <a name="examples"></a>使用例  
 `Parse()` を使用して `geography` インスタンスを作成する例を次に示します。  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>参照  
 [拡張された静的な地理メソッド](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText #40;geography データ型&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
