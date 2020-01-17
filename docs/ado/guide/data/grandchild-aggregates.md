---
title: 孫の集計 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac0b06479b3ad4feedaa63bdac227d028b7a9e09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925238"
---
# <a name="grandchild-aggregates"></a>孫の集計
Shape コマンドの句の作成」の章の列を指定できます、*章エイリアス名*(通常、AS キーワード) を使用します。 形状の任意の章の任意の列を識別する**レコード セット**列を含む子を識別する完全修飾名。 たとえば、親章、chap1、子の章では、chap2 に含まれる場合 amt、amount 列を持つ、chap1.chap2.amt が修飾名になります。修飾名は、集計関数 (SUM、AVG、MAX、MIN、COUNT、STDEV、またはいずれか) のいずれかの引数として使用できます。  
  
## <a name="see-also"></a>関連項目  
 [データ シェイプの例](../../../ado/guide/data/data-shaping-example.md)
