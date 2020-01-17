---
title: STLength (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLength (geography Data Type)
- STLength_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLength method
ms.assetid: 774560ab-4a4a-4058-b043-1e67cf6fb9eb
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 61487b976322f8725f9398e54f8292919ff0ca58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139107"
---
# <a name="stlength-geography-data-type"></a>STLength (geography データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  **geography** インスタンス、または **GeometryCollection** 内の複数の **geography** インスタンス内の要素の合計長を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **float**  
  
 CLR の戻り値の型:**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 **geography** インスタンスが閉じられている場合、長さはインスタンスの周囲の合計長として計算されます。多角形の長さとは、周囲の長さです。地点の長さは 0 です。 **GeometryCollection** の長さは、コレクションに含まれるすべての **geography** インスタンスの合計長として計算されます。  
  
 STLength() は、LineString が有効でも無効でも動作します。 通常、LineString が無効になるのは、線分の重複のためです。これは、不正確な GPS のトレースなどの異常によって起きる場合があります。 STLength() は、重複する線分や無効な線分を削除しません。 返される長さの値には、重複する線分や無効な線分が含まれています。 MakeValid() メソッドは、LineString から重複する線分を削除できます。  
  
## <a name="examples"></a>使用例  
 `LineString` インスタンスを作成し、`STLength()` を使用して、インスタンスの長さを取得する例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
