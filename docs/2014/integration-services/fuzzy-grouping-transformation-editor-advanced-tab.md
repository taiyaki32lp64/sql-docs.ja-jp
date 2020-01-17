---
title: あいまいグループ化変換エディター (詳細 タブ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: dd820d75-b8a7-4515-aea4-3553ba5b442e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dcebe499eb80fbe01b9aa36a4e07785846eaf621
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058366"
---
# <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>[あいまいグループ化変換エディター] ([詳細設定] タブ)
  **[あいまいグループ化変換エディター]** ダイアログ ボックスの **[詳細設定]** タブを使用すると、入力列と出力列の指定、類似性のしきい値の設定、区切り記号の定義ができます。  
  
> [!NOTE]  
>  `Exhaustive`と`MaxMemoryUsage`、あいまいグループ化変換のプロパティが表示されない、**あいまいグループ化変換エディター**を使用して設定することが、**高度なエディター**. これらのプロパティの詳細については、「 [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md)」の「あいまいグループ化変換」を参照してください。  
  
 あいまいグループ化変換の詳細については、「 [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[入力キー列名]**  
 各入力行の一意の識別子を含む、出力列の名前を指定します。 [`_key_in`] 列は各行を一意に識別する値を持ちます。  
  
 **[出力キー列名]**  
 重複する行グループの正規行の一意識別子を含む、出力列の名前を指定します。 [`_key_out`] 列は、正規データ行の `_key_in` 値に対応します。  
  
 **[類似性スコアの列名]**  
 類似性スコアを含む列の名前を指定します。 類似性スコアは、正規行に対する入力行の類似性を示す、0 ～ 1 の間の値です。 スコアが 1 に近いほど、その行と正規行との類似性が高いことを示しています。  
  
 **[類似性のしきい値]**  
 スライダーを使用して類似性のしきい値を設定します。 しきい値が 1 に近づくと、より類似性が高い行どうしのみが重複として扱われるようになります。 しきい値を増加させると候補レコードとして処理対象になる数が少なくなるため、一致処理の速度が向上します。  
  
 **[トークン区切り記号]**  
 変換により、トークンにするデータの区切り記号の既定のセットが提供されます。必要に応じて、一覧を編集して区切り記号の追加や削除を行うことができます。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [あいまいグループ化変換を使用して類似のデータ行を識別する](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
