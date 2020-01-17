---
title: ReorientObject (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ReorientObject
- ReorientObject_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ReorientObject method (geography)
ms.assetid: e2a1a4f1-211b-4e82-abed-03fc7140a83c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9c4660fa212a85f3bba5812d6cc990f9c02c5539
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101751"
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject (geography データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

内部領域と外部領域が入れ替えられた **geography** インスタンスを返します。  
  
この **geography** データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```  
  
.ReorientObject (geography)  
```  
  
## <a name="arguments"></a>引数  
_geography_  
`ReorientObject()` を呼び出したときの別の **geography** インスタンスです。  
  
## <a name="return-value"></a>戻り値  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
CLR の戻り値の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
このメソッドでは、**GeometryCollection** 内のすべての **Polygons** のリングの方向が変更されますが、指定されたコレクション内の **Points** または **Linestrings** はいずれも削除または変更されません。  
  
このメソッドに **GeometryCollection** を渡すと、そのコレクション内の各インスタンスの方向が変更されますが、コレクション全体の方向は変更されません。  
  
## <a name="examples"></a>使用例  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>参照  
[Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
