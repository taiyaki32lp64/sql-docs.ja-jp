---
title: Filter (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 3d629a39-157e-4159-a3ca-a3c2e0ed4160
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 701110865f4cda286c647ef887dba2e29cc5fb42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081165"
---
# <a name="filter-geometry-data-type"></a>Filter (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

インデックスが使用可能である場合に、**geometry** インスタンスが別の **geometry** インスタンスと交差するかどうかを判断する、高速のインデックス専用積集合メソッドを提供するメソッドです。
  
**geometry** インスタンスが別の **geometry** インスタンスと交差する可能性がある場合、1 を返します。 このメソッドは偽陽性の戻り値を生成する場合があり、正確な結果はプランによって異なります。 **geometry** インスタンスの交差が見つからない場合は、正確な 0 値 (真陰性の戻り値) を返します。
  
インデックスが使用できない場合、または使用されていない場合、このメソッドは、同じパラメーターを使用して呼び出した場合の **STIntersects()** と同じ値を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.Filter ( other_geometry )  
```  
  
## <a name="arguments"></a>引数  
 *other_geometry*  
 Filter() を呼び出したインスタンスと比較される、別の **geometry** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型:**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 このメソッドは決定的でなく、正確ではありません。  
  
## <a name="examples"></a>使用例  
 `Filter()` を使用して 2 つの `geometry` インスタンスが相互に交差しているかどうかを調べる例を次に示します。  
  
```  
CREATE TABLE sample (id int primary key, g geometry);  
GO  
INSERT INTO sample VALUES  
   (0, geometry::Point(0, 0, 0)),  
   (1, geometry::Point(0, 1, 0)),  
   (2, geometry::Point(0, 2, 0)),  
   (3, geometry::Point(0, 3, 0)),  
   (4, geometry::Point(0, 4, 0));  
  
CREATE SPATIAL INDEX sample_idx ON sample(g)  
WITH (bounding_box = (-8000, -8000, 8000, 8000));  
GO  
SELECT id  
FROM sample   
WHERE g.Filter(geometry::Parse('POLYGON((-1 -1, 1 -1, 1 1, -1 1, -1 -1))')) = 1;  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの拡張メソッド](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [STIntersects &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
  

