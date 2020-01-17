---
title: Reduce (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0713ba46d6d99a8ed325d37d11396b46618f92ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101770"
---
# <a name="reduce-geography-data-type-"></a>Reduce (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定した **geography** インスタンスを簡略化したものを返します。これは、指定された許容範囲で、特定のインスタンスに対して Douglas-Peucker アルゴリズムを実行することにより生成されます。  
  
 この **geography** データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>引数  
  
|||  
|-|-|  
|項目|定義|  
|*tolerance*|**float** 型の値です。 *tolerance* は、Douglas-Peucker アルゴリズムに入力する許容範囲です。 *tolerance* には正の数値を指定する必要があります。|  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 コレクション型の場合、このアルゴリズムはインスタンスに含まれている **geography** ごとに個別に実行されます。 このアルゴリズムによって、**Point** インスタンスが変更されることはありません。  
  
 このメソッドでは、**LineString** インスタンスのエンドポイントを保持しようとしますが、有効な結果を保持する目的でそれに失敗する場合があります。  
  
 負の値を指定して `Reduce()` が呼び出された場合、このメソッドでは **ArgumentException** が発生します。 `Reduce()` で使用される許容範囲は正の数値である必要があります。  
  
 Douglas-Peucker アルゴリズムでは、開始点と終了点以外のすべての点を取り除くことで、**geography** インスタンス内の各曲線またはリングを処理します。 その後、取り除かれた各点が、最も遠くの範囲外の点から始めて、結果から *tolerance* を超える点がなくなるまで戻されます。 有効な結果が保証されるように、必要に応じて結果が有効になります。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、このメソッドは **FullGlobe** インスタンスに拡張されました。  
  
 このメソッドは正確ではありません。  
  
## <a name="examples"></a>使用例  
 `LineString` インスタンスを作成し、`Reduce()` を使用してそのインスタンスを簡略化する例を次に示します。  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
