---
title: STPointFromWKB (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointFromWKB (geometry Data Type)
- STPointFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromWKB (geometry Data Type)
ms.assetid: 1157c172-2dc7-4393-bae6-b85406171a34
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 985fb4f48363a1cb3f8411b80365705ee2392498
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066421"
---
# <a name="stpointfromwkb-geometry-data-type"></a>STPointFromWKB (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Open Geospatial Consortium (OGC) Well-Known Binary (WKB) 表現を基に **geometryPoint** インスタンスを返します。
  
## <a name="syntax"></a>構文  
  
```  
  
STPointFromWKB ( 'WKB_point' , SRID )  
```  
  
## <a name="arguments"></a>引数  
 *WKB_point*  
 返される **geometryPoint** インスタンスの WKB 表現です。 *WKB_point* は、**varbinary(max)** 式です。  
  
 *SRID*  
 返される **geometryPoint** インスタンスの SRID (spatial reference ID) を表す **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
 OGC の型:**Point**  
  
## <a name="remarks"></a>Remarks  
 このメソッドでは、入力が正しい形式でない場合に、**FormatException** をスローします。  
  
## <a name="examples"></a>使用例  
 `STPointFromWKB()` を使用して `geometry` インスタンスを作成する例を次に示します。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STPointFromWKB(0x010100000000000000000059400000000000005940, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>参照  
 [OGC の静的なジオメトリ メソッド](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

