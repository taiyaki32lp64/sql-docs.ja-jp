---
title: 参照変換エディター ([エラー出力] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.erroroutput.f1
ms.assetid: 15d53bb0-8be1-46fb-b459-04a397e75fac
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 12f1a73c1d21986d2089878bfe9d29dd4450f222
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057854"
---
# <a name="lookup-transformation-editor-error-output-page"></a>[参照変換エディター] ([エラー出力] ページ)
  **[参照変換エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを指定できます。  
  
 参照変換の詳細については、「 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[入力または出力]**  
 入力の名前を表示します。  
  
 **列**  
 使用されていません。  
  
 **Error**  
 参照データセットに一致するエントリがない行を処理したときに発生させるエラーの種類を指定します。  
  
-   エラーを無視し、行を出力にダイレクトします。  
  
-   行をエラー出力にリダイレクトします。  
  
-   コンポーネントを失敗させます。  
  
 このオプションは、 **[エントリが一致しない行の処理方法を指定する]** ボックスの一覧で **[一致なしの出力に行をリダイレクトする]** を選択した場合には使用できません。 この一覧は、 **[参照変換エディター]** ダイアログ ボックスの **[全般]** ページにあります。  
  
 **関連トピック:** [データのエラー処理](data-flow/error-handling-in-data.md)  
  
 **切り捨て**  
 データの切り捨てが発生したときの動作を指定します。  
  
-   エラーを無視します。  
  
-   行をリダイレクトします。  
  
-   コンポーネントを失敗させます。  
  
 **[説明]**  
 操作の説明を表示します。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生したときのすべての選択済みセルの動作を指定します。  
  
-   エラーを無視します。  
  
-   行をリダイレクトします。  
  
-   コンポーネントを失敗させます。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
