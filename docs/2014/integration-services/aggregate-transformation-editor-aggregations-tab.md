---
title: 集計変換エディター ([集計] タブ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregationtransformation.aggregations.f1
helpviewer_keywords:
- Aggregate Transformation Editor
ms.assetid: a01cb124-ec79-4673-b1a1-bf4d60ee1b45
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 698e3757a32d9a2a9db95df495e33903dbdfed1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061578"
---
# <a name="aggregate-transformation-editor-aggregations-tab"></a>[集計変換エディター] ([集計] タブ)
  **[集計変換エディター]** ダイアログ ボックスの **[集計]** タブを使用すると、集計列および集計プロパティを指定できます。 複数の集計を適用することができます。 この変換ではエラー出力を生成しません。  
  
> [!NOTE]  
>  キーの数、キー スケール、個別のキーの数、個別のキー スケールのオプションは、 **[詳細設定]** タブで指定した場合はコンポーネント レベル、 **[集計]** タブの [詳細設定] 画面で指定した場合は出力レベル、 **[集計]** タブの下部にある列の一覧で指定した場合は列レベルで適用されます。  
>   
>  集計変換では、 **[キー]** および **[キー スケール]** は、 **グループ化** 操作の結果として予想されるグループの数を示します。 **[個別カウント キー数]** および **[個別カウント スケール]** は、 **個別のカウント** 操作の結果として予想される個別の値の数を示します。  
  
 集計変換の詳細については、「 [集計変換](data-flow/transformations/aggregate-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[詳細設定]/[基本]**  
 複数の出力用に複数の集計を構成するオプションを表示したり非表示にしたりします。 既定では、[詳細設定] オプションは非表示です。  
  
 **[集計名]**  
 [詳細設定] 画面で、集計の表示名を入力します。  
  
 **[グループ化列]**  
 [詳細設定] 画面で、後で説明するように、 **[使用できる入力列]** リストを使用してグループ化する列を選択します。  
  
 **[キー スケール]**  
 [詳細設定] 画面で、集計によって書き込むことのできるキーの概数をオプションで指定します。 既定では、このオプションの値は **[未指定]** です。 **[キー スケール]** プロパティと **[キー]** プロパティの両方が設定されている場合、 **[キー]** の値が優先されます。  
  
|値|説明|  
|-----------|-----------------|  
|[未指定]|[キー スケール] プロパティは使用されません。|  
|Low|集計では約 500,000 キーを書き込むことができます。|  
|Medium|集計では約 5,000,000 キーを書き込むことができます。|  
|High|集計では 25,000,000 を超えるキーを書き込むことができます。|  
  
 **[キー]**  
 [詳細設定] 画面で、集計によって書き込むことのできる正確なキーの数をオプションで指定します。 **[キー スケール]** と **[キー]** の両方が指定されている場合、 **[キー]** が優先されます。  
  
 **[使用できる入力列]**  
 このテーブルのチェック ボックスを使用して、使用できる入力列の一覧から選択します。  
  
 **入力列**  
 使用できる入力列の一覧から選択します。  
  
 **[出力の別名]**  
 各列に対して別名を入力します。 既定は入力列の名前です。一意のわかりやすい名前を付けることもできます。  
  
 **操作**  
 使用可能な操作の一覧から選択します。次の表を指針として使用できます。  
  
|操作|説明|  
|---------------|-----------------|  
|**GroupBy**|データセットをグループに分割します。 どのようなデータ型を持つ列でもグループ化に使用できます。 詳細については、「GROUP BY」を参照してください。|  
|**Sum**|列内の値を合計します。 numeric データ型を持つ列のみ、合計することができます。 詳細については、「SUM」を参照してください。|  
|**平均**|列内の列値の平均を返します。 numeric データ型を持つ列のみ、平均値を計算することができます。 詳細については、「AVG」を参照してください。|  
|**Count**|グループ内のアイテムの数を返します。 詳細については、「COUNT」を参照してください。|  
|**CountDistinct**|グループ内の NULL でない一意の値の数を返します。 詳細については、「COUNT」および「DISTINCT」を参照してください。|  
|**最小**|グループ内の最小値を返します。 numeric データ型に制限されます。|  
|**[最大]**|グループ内の最大値を返します。 numeric データ型に制限されます。|  
  
 **[比較フラグ]**  
 **[グループ化]** を選択する場合、チェック ボックスを使用して、変換により比較がどのように実行されるかを制御します。 文字列比較オプションについては、「 [文字列データの比較](data-flow/comparing-string-data.md)」を参照してください。  
  
 **Count Distinct Scale**  
 集計で書き込むことのできる個別の値の概数をオプションで指定します。 既定では、このオプションの値は **[未指定]** です。 両方`CountDistinctScale`と**CountDistinctKeys**が指定されて**CountDistinctKeys**が優先されます。  
  
|値|説明|  
|-----------|-----------------|  
|[未指定]|`CountDistinctScale` プロパティは使用されません。|  
|Low|集計では約 500,000 の個別の値を書き込むことができます。|  
|Medium|集計では約 5,000,000 の個別の値を書き込むことができます。|  
|高|集計では 25,000,000 を超える個別の値を書き込むことができます。|  
  
 **Count Distinct Keys**  
 集計によって書き込むことのできる個別の値の正確な数をオプションで指定します。 両方`CountDistinctScale`と**CountDistinctKeys**が指定されて**CountDistinctKeys**が優先されます。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[集計変換エディター] &#40;[詳細設定] タブ&#41;](../../2014/integration-services/aggregate-transformation-editor-advanced-tab.md)   
 [集計変換を使用してデータセットの値を集計する](data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  
