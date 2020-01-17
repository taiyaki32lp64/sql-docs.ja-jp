---
title: CollectionAggregate (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CollectionAggregate method (geometry)
ms.assetid: b7c85d59-c841-4b7f-9d46-8b4b7f2a3afe
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: bff01341c6d28f38cc1ba18ecf6ac2644b4bb530
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017526"
---
# <a name="collectionaggregate-geometry-data-type"></a>CollectionAggregate (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

**geometry** 型のセットから **GeometryCollection** インスタンスを作成します。
  
## <a name="syntax"></a>構文  
  
```  
  
CollectionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>引数  
 *geometry_operand*  
 **GeometryCollection** インスタンスで列挙される **geometry** オブジェクトのセットを表す **geometry** 型のテーブルの列です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
## <a name="exceptions"></a>例外  
 入力値が無効である場合は、`FormatException` をスローします。 「[STIsValid &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 入力が空である場合または入力の SRID が異なる場合は、**null** が返されます。 「[SRID (Spatial Reference Identifier)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)」を参照してください。  
  
 メソッドでは、**null** 入力は無視されます。  
  
> [!NOTE]  
>  メソッドは、入力された値がすべて **null** の場合、**null** を返します。  
  
## <a name="examples"></a>使用例  
 次の例は、`GeometryCollection` と `CurvePolygon` が含まれる `Polygon` インスタンスを返します。  
  
 ```
 -- Setup table variable for CollectionAggregate example  
 DECLARE @Geom TABLE  
 (  
 shape geometry,  
 shapeType nvarchar(50)  
 )  
 INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),  
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');  
 -- Perform CollectionAggregate on @Geom.shape column  
 SELECT geometry::CollectionAggregate(shape).ToString()  
 FROM @Geom;
 ```  
  
## <a name="see-also"></a>参照  
 [拡張された静的なジオメトリ メソッド](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

