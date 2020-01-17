---
title: Long (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs:
- TSQL
helpviewer_keywords:
- Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 20f1521091a295d1293c9f3e06958f36930ba4e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930203"
---
# <a name="long-geography-data-type"></a>Long (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** インスタンスの経度プロパティを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.Long  
```  
  
## <a name="return-value"></a>戻り値  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の型: **float**  
  
 CLR の型:**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 OpenGIS モデルでは、Long は単一地点のデータで構成される **geography** インスタンスにのみ定義されます。 **geography** インスタンスに複数の地点が含まれる場合、このプロパティは NULL を返します。 このプロパティは正確で、読み取り専用です。  
  
## <a name="examples"></a>使用例  
 **Point** インスタンスを作成し、その地点の経度を取得する例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
