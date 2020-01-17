---
title: 参照変換エディター ([列] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.columns.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: 690ffef5-fd59-4e95-a27d-4fcf0d6b1c0b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e1a32dcbcee6704cb4fecef7b58cbff8354b910a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057894"
---
# <a name="lookup-transformation-editor-columns-page"></a>[参照変換エディター] ([列] ページ)
  **[参照変換エディター]** ダイアログ ボックスの **[列]** ページを使用すると、元のテーブルと参照テーブルの間に結合を指定したり、参照テーブルから参照列を選択したりできます。  
  
 参照変換の詳細については、「 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。 入力列とは、データ フロー内の接続されているソースからの列です。 入力列と参照列のデータ型は一致している必要があります。  
  
 ドラッグ アンド ドロップ操作により、使用できる入力列を参照列にマップします。  
  
 キーボードを使用して、 **[使用できる入力列]** テーブル内の列を強調表示し、アプリケーション キーを押して、 **[マッピングの編集]** をクリックすることで、入力列を参照列にマップすることもできます。  
  
 **使用できる参照列**  
 参照列の一覧を表示します。 参照列とは、入力列に一致する値の参照先の参照テーブルにある列です。  
  
 ドラッグ アンド ドロップ操作により、使用できる参照列を入力列にマップします。  
  
 チェック ボックスを使用して、参照操作を実行する参照テーブル内の参照列を選択します。  
  
 キーボードを使用して、 **[使用できる参照列]** テーブル内の列を強調表示し、アプリケーション キーを押して、 **[マッピングの編集]** をクリックすることで、参照列を入力列にマップすることもできます。  
  
 **参照列**  
 選択した参照列を表示します。 選択内容は、 **[使用できる参照列]** テーブルのチェック ボックスの状態に反映されます。  
  
 **[参照操作]**  
 一覧から、参照列で実行する参照操作を選択します。  
  
 **[出力の別名]**  
 各参照列の出力の別名を入力します。 既定では参照列の名前が使用されますが、一意なわかりやすい名前を自由に付けることができます。  
  
## <a name="see-also"></a>関連項目  
 [[参照変換エディター] &#40;[全般] ページ&#41;](general-page-of-integration-services-designers-options.md)   
 [参照変換エディター ([接続] ページ)](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [参照変換エディター ([詳細設定] ページ)](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [[参照変換エディター] &#40;[エラー出力] ページ&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [あいまい参照変換](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
