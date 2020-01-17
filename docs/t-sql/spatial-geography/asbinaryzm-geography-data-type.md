---
title: AsBinaryZM (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsBinaryZM
- AsBinaryZM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsBinaryZM, geography
- AsBinaryZM
ms.assetid: 37246adb-814d-4113-9983-4d336de8182c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c617d4303593588b6e86a5b9b7662a5ec690c577
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948074"
---
# <a name="asbinaryzm-geography-data-type"></a>AsBinaryZM (geography データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  インスタンスに格納されている **Z** (標高) 値と **M** (メジャー) 値で補完された **geometry** インスタンスについて、Open Geospatial Consortium (OGC) Well-Known Binary (WKB) 表現を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **varbinary(max)**  
  
 CLR の戻り値の型:**SqlBytes**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>使用例  
  
```sql  
DECLARE @g1 GEOGRAPHY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40;geography データ型&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40;geography データ型&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
