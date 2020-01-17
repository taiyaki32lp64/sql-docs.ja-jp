---
title: STPointFromText (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointFromText_TSQL
- STPointFromText (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromText (geometry Data Type)
ms.assetid: 1d71dfd8-9d80-44c3-b6e1-64e99cde1fa0
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a198292700fdda1e5dc092afc4a5bb1948e7192a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075051"
---
# <a name="stpointfromtext-geometry-data-type"></a>STPointFromText (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

インスタンスに格納されている Z (標高) 値と M (メジャー) 値で補完された、Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現を基に **geometry** インスタンスを返します。
  
## <a name="syntax"></a>構文  
  
```  
  
STPointFromText ( 'point_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>引数  
 *point_tagged_text*  
 返される **geometryPoint** インスタンスの WKT 表現です。 *point_tagged_text* は **nvarchar(max)** 式です。  
  
 *SRID*  
 返される **geometryPoint** インスタンスの SRID (spatial reference ID) を表す **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
 OGC の型:**Point**  
  
## <a name="remarks"></a>Remarks  
 このメソッドでは、入力が正しい形式でない場合に、**FormatException** をスローします。  
  
## <a name="examples"></a>使用例  
 `STPointFromText()` を使用して `geometry` インスタンスを作成する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STPointFromText('POINT (100 100)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>参照  
 [OGC の静的なジオメトリ メソッド](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

