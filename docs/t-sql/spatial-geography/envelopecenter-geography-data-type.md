---
title: EnvelopeCenter (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: da1c2fd6f1e6732f28f79196b433b8e46a595a85
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066433"
---
# <a name="envelopecenter-geography-data-type"></a>EnvelopeCenter (geography データ型 )
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geography** インスタンスの外接する円の中心として使用できる点を返します。  
  
インスタンス内の各点は、ベクトルとして記述されます。 外接する円を割り出すには、ベクトルを地球の中心から地球の表面の点に延長します。 外接する円の中心点は、すべてのベクトルの平均として計算されます。 **Polygon** インスタンスまたは **LineString** インスタンスの閉じたループの場合、最初と最後の点は一度しか使用されません。  
  
この **geography** データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>戻り値の型  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
CLR の戻り値の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
このメソッドは、**地点**を返します。 `EnvelopeAngle()` と共に使用した場合、`EnvelopeCenter()` は、**geography** インスタンスの外接する円を返します。  
  
> [!NOTE]  
>  `EnvelopeCenter()` は **geography** インスタンスの外接する円を返しますが、結果が最小の外接する円になることは保証されません。 一方、**geometry** データ型のメソッド `STEnvelope()` は、**geometry** インスタンスに適用した場合に最小の境界ボックスを返します。  
  
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、このインスタンスのエンベロープを表す円の中心は**地点**として返されます。 `EnvelopeAngle()` = 180 で定義されているすべてのラージ オブジェクトでは、`EnvelopeCenter()` は (90,0) を返します。  
  
このメソッドは正確ではありません。  
  
## <a name="examples"></a>使用例  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>参照  
[Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
[EnvelopeAngle &#40;geography データ型&#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
