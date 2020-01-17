---
title: Parameters コレクションの参照 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c4b47e15-0484-4c13-9182-898db825f01f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c3c9452a9be55c71431a0ed3012769b1f5f6d8eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106410"
---
# <a name="parameters-collection-references-report-builder-and-ssrs"></a>Parameters コレクションの参照 (レポート ビルダーおよび SSRS)
  レポート パラメーターは、式から参照できる組み込みコレクションの 1 つです。 パラメーターを式に含めると、レポートのデータと外観をユーザーの選択に基づいてカスタマイズできます。 式は、(*Fx*) オプションまたは [\<**式**>] オプションを利用できる、すべてのレポート アイテム プロパティやテキスト ボックス プロパティで使用できます。 式は、他の方法でレポートの内容と外観を制御する場合にも使用されます。 詳細については、「[式の例 &#40;レポート ビルダーおよび SSRS&#41;](expression-examples-report-builder-and-ssrs.md)」を参照してください。  
  
 実行時にパラメーター値をデータセットのフィールド値と比較する場合は、比較する 2 つのアイテムのデータ型が同じである必要があります。 レポート パラメーターに使用できるデータ型は次のいずれかです:Boolean、DateTime、Integer、Float、または Text (これは基になるデータ型 String を表します)。 必要に応じて、パラメーター値のデータ型をデータセットの値に一致するように変換することが必要になる場合もあります。 詳細については、「 [式で使用されるデータ型 (レポート ビルダーおよび SSRS)](expressions-report-builder-and-ssrs.md)など、先頭に &amp; (アンパサンド) が付いた状態で表示されます。  
  
 パラメーター参照を式に含めるには、パラメーター参照に適切な構文を指定する方法を理解する必要があります。これは、パラメーターが単独値パラメーターと複数の値を持つパラメーターのどちらであるかによって異なります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Single"></a> 式での単独値パラメーターの使用  
 次の表は、任意のデータ型の単独値パラメーターへの参照を式に含めるときに使用する構文の例を示しています。  
  
|例|説明|  
|-------------|-----------------|  
|`=Parameters!` *\<ParameterName>* `.IsMultiValue`|`False` を返します。<br /><br /> パラメーターが複数値であるかどうかを確認します。 場合`True`パラメーターが複数値、オブジェクトのコレクションです。 場合`False`のパラメーターは単一値、1 つのオブジェクト。|  
|`=Parameters!` *\<ParameterName>* `.Count`|整数値 1 が返されます。 単一値パラメーターの場合、カウントは常に 1 です。|  
|`=Parameters!` *\<ParameterName>* `.Label`|パラメーター ラベルが返されます。パラメーター ラベルは通常、使用可能な値のドロップダウン リストの表示名として使用されます。|  
|`=Parameters!` *\<ParameterName>* `.Value`|パラメーターの値が返されます。 Label プロパティが設定されていない場合、この値は使用可能な値のボックスの一覧に表示されます。|  
|`=CStr(Parameters!`  *\<ParameterName>* `.Value)`|パラメーターの値が文字列として返されます。|  
|`=Fields(Parameters!` *\<ParameterName>* `.Value).Value`|パラメーターと同じ名前のフィールドの値が返されます。|  
  
 フィルターでのパラメーターの使用の詳細については、｢[データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 &#40;レポート ビルダーおよび SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)」を参照してください。  
  
##  <a name="Multi"></a> 式での複数値パラメーターの使用  
 次の表は、任意のデータ型の複数の値を持つパラメーターへの参照を式に含めるときに使用する構文の例を示しています。  
  
|例|説明|  
|-------------|-----------------|  
|`=Parameters!` *\<MultivalueParameterName>* `.IsMultiValue`|`True` または `False` が返されます。<br /><br /> パラメーターが複数値であるかどうかを確認します。 `True` の場合、パラメーターは複数値でオブジェクトのコレクションです。 `False` の場合、パラメーターは単一値で 1 つのオブジェクトです。|  
|`=Parameters!` *\<MultivalueParameterName>* `.Count`|整数値が返されます。<br /><br /> 値の数を表します。 単一値パラメーターの場合、カウントは常に 1 です。 複数値パラメーターの場合、カウントは 0 以上です。|  
|`=Parameters!` *\<MultivalueParameterName>* `.Value(0)`|複数値パラメーターの最初の値が返されます。|  
|`=Parameters!` *\<MultivalueParameterName>* `.Value(Parameters!` *\<MultivalueParameterName>* `.Count-1)`|複数値パラメーターの最後の値が返されます。|  
|`=Split("Value1,Value2,Value3",",")`|値の配列が返されます。<br /><br /> 複数の値を持つ `String` 型のパラメーターに基づいて、値の配列を作成します。 Split の 2 番目のパラメーターでは、任意の区切り記号を使用できます。 この式は、複数値パラメーターの既定値を設定したり、サブレポートや詳細レポートに送信する複数値パラメーターを作成する場合に使用できます。|  
|`=Join(Parameters!` *\<MultivalueParameterName>* `.Value,", ")`|複数の値を持つパラメーターの値をコンマで区切ったリストで構成される `String` が返されます。 Join の 2 番目のパラメーターでは、任意の区切り記号を使用できます。|  
  
 フィルターでのパラメーターの使用の詳細については、「[レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [式 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [一般的に使用されるフィルター &#40;レポート ビルダーおよび SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md)   
 [レポート パラメーターの追加、変更、または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [チュートリアル: レポートへのパラメーターの追加 &#40;レポート ビルダー&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [チュートリアル&#40;レポート ビルダー&#41;](../report-builder-tutorials.md)   
 [式で使用される組み込みコレクション &#40;レポート ビルダーおよび SSRS&#41;](built-in-collections-in-expressions-report-builder.md)  
  
  
