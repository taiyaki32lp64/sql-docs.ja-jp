---
title: STWithin (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STWithin_TSQL
- STWithin (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STWithin (geometry Data Type)
ms.assetid: f845d28c-8029-4e2b-bcf0-71c52a592501
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1ca7e74743773fb42a85300a37cc6b8aaa9d8f39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066261"
---
# <a name="stwithin-geometry-data-type"></a>STWithin (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** インスタンスが別の **geometry** インスタンスに完全に含まれている場合は 1 を返します。それ以外の場合は 0 を返します。 `STWithin` コマンドでは大文字と小文字が区別されます。
  
## <a name="syntax"></a>構文  
  
```  
  
.STWithin ( other_geometry )  
```  
  
## <a name="arguments"></a>引数  
 *other_geometry*  
 `STWithin()` を呼び出したインスタンスと比較される、別の **geometry** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型:**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 **geometry** インスタンスの SRID (spatial reference ID) が一致しない場合、このメソッドは常に null を返します。
  
## <a name="examples"></a>使用例  
 `STWithin()` を使用して、2 つの `geometry` インスタンスの一方のインスタンスがもう一方のインスタンスを完全に含むかどうかをテストする例を次に示します。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STWithin(@h);  
```  
  
## <a name="see-also"></a>参照  
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

