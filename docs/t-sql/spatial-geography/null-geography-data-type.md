---
title: Null (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Null (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geography Data Type)
- Null method
ms.assetid: bb464b06-86e0-4b8b-ad78-04bd33b6069c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 775410c9a57d9bf030f34f84640522b766f0cf23
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127378"
---
# <a name="null-geography-data-type"></a>Null (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geography** 型の NULL インスタンスを提供する、読み取り専用プロパティです。
  
## <a name="syntax"></a>構文  
  
```  
  
Null  
```  
  
## <a name="arguments"></a>引数  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型: **geography**  
  
 CLR の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>使用例  
 `geography` 型の NULL インスタンスを取得する例を次に示します。  
  
```  
DECLARE @g geography;   
SET @g = geography::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>参照  
 [拡張された静的な地理メソッド](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
