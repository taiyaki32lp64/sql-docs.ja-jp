---
title: マイニング モデルからの列の除外 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70049092909b625a1f304f16f153bf4287d5bcdf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084556"
---
# <a name="exclude-a-column-from-a-mining-model"></a>マイニング モデルからの列の除外
  新しいマイニング モデルを作成するとき、基となるマイニング構造に存在するすべての列を使用しないことがあります。 たとえば、ドリルスルー、顧客名列を追加した可能性がありますが、モデリングに使用する必要はありません。 または、列の複数のコピーをそれぞれ異なる分離で作成して、各モデルで 1 つのコピーのみ使用し、残りは無視する場合があります。 複数の異なるモデルで入力列を選択的に追加して、追加した変数が出力列に与える影響を確認することもできます。  
  
 列の組み合わせごとに新しいマイニング構造を作成する必要はありません。代わりに、特定のモデルで使用されていないことを示すフラグを列に設定できます。  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>マイニング モデルから列を除外するには  
  
1.  **のデータ マイニング デザイナーの** [マイニング モデル] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]タブにある適切なマイニング モデルで、除外する列に対応するセルを選択します。  
  
2.  ドロップダウン リスト ボックスから **[無視]** を選択します。  
  
## <a name="see-also"></a>参照  
 [マイニング モデル タスクと操作方法](mining-model-tasks-and-how-tos.md)  
  
  
