---
title: EnvelopeAngle (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e3289956dd79c852eef6534ad1f72623ad4dcaa6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066463"
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  `EnvelopeCenter()` で返される地点と **geography** インスタンスの地点との間の最大角度 (度数) を返します。  
  
 この **geography** データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **float**  
  
 CLR の戻り値の型:**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 このメソッドは **geography** インスタンスの地点を度数で返します。 EnvelopeCenter() と共に使用した場合、`EnvelopeAngle()` は、**geography** インスタンスの外接する円を返します。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、このメソッドは **FullGlobe** インスタンスに拡張されました。  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] で `EnvelopeAngle()` に適用された半球に関する制限はなくなりました。 ただし、90 度を超える角度のインスタンスの場合、180 度が返されます。 `EnvelopeAngle()` は、複数の半球にまたがる **geography** インスタンスに関しては正確ではありません。  
  
## <a name="examples"></a>使用例  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter &#40;geography データ型&#41;](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  
