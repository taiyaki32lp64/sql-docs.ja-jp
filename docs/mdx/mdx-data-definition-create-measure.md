---
title: CREATE MEASURE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 02c6d29bbebcc794e72f4ca960e3d9259de7205b
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892142"
---
# <a name="mdx-data-definition---create-measure"></a>MDX データ操作 - CREATE MEASURE


  テーブル モデルでメジャーを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE MEASURE Table_Name[Measure_Name] = DAX_Expression  
[; CREATE MEASURE ...n]  
  
```  
  
## <a name="arguments"></a>引数  
 *Table_Name*  
 メジャーを作成するテーブルの名前を指定する有効な文字列リテラルです。  
  
 *Measure_Name*  
 メジャー名を指定する有効な文字列リテラルです。  
  
 *DAX_Expression*  
 1 つのスカラー値を返す有効な DAX 式を入力します。  
  
## <a name="remarks"></a>コメント  
 *Measure_Name*は、角かっこで囲む必要があります。  
  
 CREATE MEASURE ステートメントは、MDX スクリプト定義内でのみ使用できます。「 [MdxScript 要素&#40;assl&#41;](https://docs.microsoft.com/bi-reference/assl/objects/mdxscript-element-assl)」を参照してください。  
  
 1 つのクエリだけで使用する計算されるメンバーを定義することも可能です。 1 つのクエリに限定される計算されるメンバーを定義するには、SELECT ステートメントで WITH 句を使用します。 詳細については、「 [MDX でのメジャーの作成](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-building-measures)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Mdx データ定義ステートメント&#40;mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
