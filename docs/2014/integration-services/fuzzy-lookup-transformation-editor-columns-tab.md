---
title: あいまい参照変換エディター ([列] タブ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.columns.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: aaf45327-79e9-4760-9b4d-546ace91b5b4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 063248c6b91aebf6198323487aa30ddd1c9cb6ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058327"
---
# <a name="fuzzy-lookup-transformation-editor-columns-tab"></a>[あいまい参照変換エディター] ([列] タブ)
  **[あいまい参照変換エディター]** ダイアログ ボックスの **[列]** タブを使用すると、入力列および出力列のプロパティを設定できます。  
  
 あいまい参照変換の詳細については、「 [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **使用できる入力列**  
 入力列をドラッグして、使用できる参照列に接続します。 これらの列は、サポートされているデータ型と一致する必要があります。 マッピングする行を選択して右クリックし、 [[リレーションシップの作成]](data-flow/transformations/create-relationships.md) ダイアログ ボックスでマッピングを編集します。  
  
 **名前**  
 使用可能な入力列の名前が表示されます。  
  
 **[パススルー]**  
 変換先の出力に入力列を含めるかどうかを指定します。  
  
 **使用できる参照列**  
 チェック ボックスを使用して、あいまい参照操作を実行する列を選択します。  
  
 **参照列**  
 使用できる参照テーブル列の一覧から参照列を選択します。 選択内容が **[使用できる参照列]** テーブルのチェック ボックスに反映されます。 **[使用できる参照列]** テーブルの列を選択すると、返される一致行ごとに参照テーブル列の値を含む出力列が作成されます。  
  
 **[出力の別名]**  
 各参照列の出力の別名を入力します。 既定では、参照列の名前に数値のインデックス値が追加されます。一意のわかりやすい名前を付けることもできます。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [あいまい参照変換エディター &#40;[参照テーブル] タブ&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [[あいまい参照変換エディター] &#40;[詳細設定] タブ&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
