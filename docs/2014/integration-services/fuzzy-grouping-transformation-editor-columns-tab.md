---
title: あいまいグループ化変換エディター ([列] タブ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.columns.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 24f4539f-2a9f-4acd-acc7-06228a07f7df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a97225797380294968f1af595f1299e478d548d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058357"
---
# <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>[あいまいグループ化変換エディター] ([列] タブ)
  **[あいまいグループ化変換エディター]** ダイアログ ボックスの **[列]** タブを使用すると、重複する値を持つ行をグループ化するための列を指定できます。  
  
 あいまいグループ化変換の詳細については、「 [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **使用できる入力列**  
 重複する値を持つ行をグループ化するために使用する入力列を、この一覧から選択します。  
  
 **名前**  
 使用できる入力列の名前を表示します。  
  
 **[パススルー]**  
 入力列を変換の出力に含めるかどうかを選択します。 グループ化に使用されるすべての列は、自動的に出力にコピーされます。 この列を選択することによって、追加の列を含めることができます。  
  
 **入力列**  
 **[使用できる入力列]** の一覧で選択されている入力列の 1 つを選択します。  
  
 **[出力の別名]**  
 対応する出力列に付けるわかりやすい名前を入力します。 既定では、出力列名は入力列名と同じになります。  
  
 **[グループ出力の別名]**  
 グループ化された重複の標準の値を含む列に付けるわかりやすい名前を入力します。 この出力列の既定の名前は、入力列名に _clean を付けた名前です。  
  
 **[一致の種類]**  
 あいまい一致と完全一致のどちらかを指定します。 あいまい一致の場合、行は、すべての列にわたって行が十分に類似している場合に重複していると見なされます。 さらに、特定の列に対して完全一致を指定した場合、完全一致列内で同一の値を含む行だけが、重複の可能性があると見なされます。 したがって、特定の列にエラーや矛盾がないことがわかっている場合は、その列に対して完全一致を指定して、他の列でのあいまい一致の精度を高めることができます。  
  
 **[最小類似]**  
 スライダーを使用して、類似のしきい値を結合レベルで設定します。 値を 1 に近づけるほど、参照元の値と参照先の値との類似性が高くなければ一致しないと見なされます。 しきい値を大きくすると、照合の対象となるレコードが少なくなるため、照合の速度が向上します。  
  
 **[類似出力の別名]**  
 選択された結合の類似スコアを格納する、新しい出力列に付ける名前を指定します。 この値を空にした場合、出力列は作成されません。  
  
 **[数字]**  
 列データを比較する際の先頭および末尾の数字の有意性を指定します。 たとえば、先頭の数字が有意である場合、"123 Main Street" は "456 Main Street" と同じグループとは見なされません。  
  
|値|説明|  
|-----------|-----------------|  
|**[Neither]**|先頭および末尾の数字は考慮されません。|  
|**[Leading]**|先頭の数字のみが考慮されます。|  
|**[Trailing]**|末尾の数字のみが考慮されます。|  
|**[Leading and Trailing]**|先頭および末尾の両方の数字が考慮されます。|  
  
 **[比較フラグ]**  
 文字列比較オプションについては、「 [文字列データの比較](data-flow/comparing-string-data.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [あいまいグループ化変換を使用して類似のデータ行を識別する](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
