---
title: STPointN (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 12ae393f99510df743b5a5ec0bf777f7b982d570
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120819"
---
# <a name="stpointn-geography-data-type"></a>STPointN (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** インスタンス内の指定した地点を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 1 から **geography** インスタンス内の地点の数までの **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
 Open Geospatial Consortium (OGC) の型:**Point**  
  
## <a name="remarks"></a>Remarks  
 ユーザーが作成した **geography** インスタンスの場合、STPointN() は、最初に入力した順序で地点を並べ替えることで、*expression* で指定された地点を返します。  
  
 システムによって作成された **geography** インスタンスの場合、STPointN() は、出力する順序ですべての地点を並べ替えることで、*式*で指定された地点を返します。出力する順序にするには、**geography** インスタンス、インスタンス内のリング (必要な場合)、リング内の地点の順に並べ替えます。 この順序は決定的です。  
  
 1 未満の値を指定してこのメソッドを呼び出すと、**ArgumentOutOfRangeException** がスローされます。  
  
 インスタンス内の地点の数より大きい値を指定してこのメソッドを呼び出すと、メソッドは NULL を返します。  
  
## <a name="examples"></a>使用例  
 `LineString` インスタンスを作成し、`STPointN()` を使用して、このインスタンスの記述に含まれる 2 番目の地点を取得する例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
