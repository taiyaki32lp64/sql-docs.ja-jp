---
title: STLength (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLength_TSQL
- STLength (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STLength (geometry Data Type)
ms.assetid: e34dc620-2a65-4248-b099-fff91830ab98
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2b42f879a238e1c1e9a44c92c8683a91c9021600
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030863"
---
# <a name="stlength-geometry-data-type"></a>STLength (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** インスタンス内の要素の合計長を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **float**  
  
 CLR の戻り値の型:**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 **geometry** インスタンスが閉じられている場合、長さはインスタンスの周囲の合計長として計算されます。多角形の長さとは、周囲の長さです。地点の長さは 0 です。 **geometrycollection** コレクション型の長さは、コレクションに含まれるすべての **geometry** インスタンスの長さの合計として計算されます。  
  
 STLength() は、LineString が有効でも無効でも動作します。 通常、LineString が無効になるのは、線分の重複のためです。これは、不正確な GPS のトレースなどの異常によって起きる場合があります。 STLength() は、重複する線分や無効な線分を削除しません。 返される長さの値には、重複する線分や無効な線分が含まれています。 MakeValid() メソッドは、LineString から重複する線分を削除できます。  
  
## <a name="examples"></a>使用例  
 `LineString` インスタンスを作成し、`STLength()` を使用して、インスタンスの長さを取得する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

