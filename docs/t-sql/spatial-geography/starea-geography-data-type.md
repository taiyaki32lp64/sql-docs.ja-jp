---
title: STArea (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 817a6325b956f5fc4214597b0b8bc46f6aff49f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042514"
---
# <a name="starea-geography-data-type"></a>STArea (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geography** インスタンスの合計面積を返します。 STArea() の結果は、**geography** インスタンスの空間参照識別子で使用される平方の測定単位です。 たとえば、インスタンスの SRID が 4326 の場合、STArea() は結果を平方メートル単位で返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **float**  
  
CLR の戻り値の型:**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
**geography** インスタンスに含まれるすべての図形が 0 次元または 1 次元の図形の場合、または空である場合、STArea() は 0 を返します。  
  
> [!NOTE]  
>  基準の戻り値を生成する、**geography** データ型のメソッドの結果は、メソッドで使用されるインスタンスの SRID に応じて異なります。 SRID の詳細については、「[&#40;SRIDs&#41; Spatial Reference Identifiers](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
`STArea()` を使用して、`Polygon geography` インスタンスを作成し、多角形の面積を計算する例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>参照  
[Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
