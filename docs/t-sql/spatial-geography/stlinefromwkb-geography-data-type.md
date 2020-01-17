---
title: STLineFromWKB (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLineFromWKB (geography Data Type)
- STLineFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromWKB method
ms.assetid: 8ac2b772-6673-4ba1-a7ab-3b4b5841560b
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2d24050e9344c3dd351f852e624e6a1453432ebc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952242"
---
# <a name="stlinefromwkb-geography-data-type"></a>STLineFromWKB (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Open Geospatial Consortium (OGC) の Well-Known Binary (WKB) 表現を基に **LineString geography** インスタンスを返します。
  
## <a name="syntax"></a>構文  
  
```  
  
STLineFromWKB ( 'WKB_linestring' , SRID )  
```  
  
## <a name="arguments"></a>引数  
 *WKB_linestring*  
 返される **LineString geography** インスタンスの WKB 表現です。 *WKB_linestring* は、**varbinary (max)** 式です。  
  
 *SRID*  
 返される **LineString geography** インスタンスの SRID (spatial reference ID) を表す **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
 OGC の型:**LineString**  
  
## <a name="remarks"></a>Remarks  
 このメソッドでは、入力が整形式でない場合に、**FormatException** がスローされます。  
  
## <a name="examples"></a>使用例  
 次の例では、`STLineFromWKB()` を使用して `geography` インスタンスを作成します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STLineFromWKB(0x010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>参照  
 [OGC の静的な地理メソッド](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
