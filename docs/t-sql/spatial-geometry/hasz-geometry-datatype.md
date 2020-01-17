---
title: HasZ (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- HasZ geometry
ms.assetid: aa378943-252a-4079-848b-6c59344fcfce
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: cba3487b17828ffaf4f7bd092b83542de639fcfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101251"
---
# <a name="hasz-geometry-datatype"></a>HasZ (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  空間オブジェクトに少なくとも 1 つの Z 値が含まれている場合は 1 (true)、それ以外の場合は 0 (false) を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.HasZ  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型:**Boolean**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>使用例  
  
```sql  
DECLARE @p GEOMETRY = 'Point(1 1 1 1)'  
SELECT @p.HasZ   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの拡張メソッド](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  
