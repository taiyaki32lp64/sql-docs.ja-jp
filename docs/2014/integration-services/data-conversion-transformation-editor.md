---
title: データ変換変換エディター |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- Data Conversion Transformation Editor
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5346c808c7d724ae630bb3dd25016a9977af363e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060050"
---
# <a name="data-conversion-transformation-editor"></a>データ変換変換エディター
  **[データ変換変換エディター]** ダイアログ ボックスを使用すると、変換対象の列や列の変換先のデータ型を選択したり、変換属性を設定したりできます。  
  
> [!NOTE]  
>  `FastParse`データ変換の変換の出力列のプロパティでは使用できません、**データ変換変換エディター**を使用して設定できますが、**高度なエディター**します。 このプロパティの詳細については、「 [変換のカスタム プロパティ](data-flow/transformations/transformation-custom-properties.md)」の「データ変換の変換」を参照してください。  
  
 データ変換の変換の詳細については、「 [データ変換の変換](data-flow/transformations/data-conversion-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **使用できる入力列**  
 変換対象の列のチェック ボックスを使用して選択します。 選択した列が入力列として下のテーブルに追加されます。  
  
 **入力列**  
 使用できる入力列の一覧から変換対象の列を選択します。 上記のチェック ボックスに、選択内容が反映されます。  
  
 **[出力の別名]**  
 それぞれの新しい列の別名を入力します。 既定では、入力列の名前の後に "`Copy of`" が追加された別名になりますが、固有のわかりやすい名前を選択することもできます。  
  
 **[データ型]**  
 一覧から利用可能なデータ型を選択します。 詳細については、「 [Integration Services Data Types](data-flow/integration-services-data-types.md)」を参照してください。  
  
 **Length**  
 文字列データの列の長さを設定します。  
  
 **Precision**  
 数値データの有効桁数を設定します。  
  
 **Scale**  
 数値データの小数点以下桁数を設定します。  
  
 **コード ページ**  
 DT_STR 型の列に適したコード ページを選択します。  
  
 **[エラー出力の構成]**  
 [[エラー出力の構成]](../../2014/integration-services/configure-error-output.md) ダイアログ ボックスを使用して、エラーの処理方法を指定します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [データ変換の変換を使用してデータを別のデータ型に変換する](data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  
