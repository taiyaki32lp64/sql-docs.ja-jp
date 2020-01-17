---
title: 文字マップ変換エディター |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- Character Map Transformation Editor
ms.assetid: 3f1dbcf9-9cca-4606-bdcc-7ea6ad48cdf3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76f2c5e517ca81ae667df3efa6ccd2f49384f090
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060980"
---
# <a name="character-map-transformation-editor"></a>文字マップ変換エディター
  **[文字マップ変換エディター]** ダイアログ ボックスを使用すると、列のデータに適用する文字列関数を選択し、マッピングが埋め込み先の変更か新しい列として追加されるかを指定できます。  
  
 文字マップ変換の詳細については、「 [Character Map Transformation](data-flow/transformations/character-map-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **使用できる入力列**  
 チェック ボックスを使用し、文字列関数を使用して変換する列を選択します。 選択は下の表に表示されます。  
  
 **入力列**  
 上の表で選択された入力列が表示されます。 使用できる入力列の一覧を使用して、選択した列を変更したり、削除したりできます。  
  
 **変換先**  
 文字列処理の結果を、既定の列を使用して所定の場所に保存するか、変更されたデータを新しい列として保存するかを指定します。  
  
|値|説明|  
|-----------|-----------------|  
|[新しい列]|データを新しい列に保存します。 **[出力の別名]** で、列名を割り当てます。|  
|[埋め込み先変更]|変更されたデータを既存の列に保存します。|  
  
 **操作**  
 列のデータに適用する文字列関数を一覧から選択します。  
  
|値|説明|  
|-----------|-----------------|  
|小文字|小文字に変換します。|  
|大文字|大文字に変換します。|  
|バイトの反転|バイト順序を反転します。|  
|ひらがな|カタカナをひらがなに変換します。|  
|カタカナ|ひらがなをカタカナに変換します。|  
|半角|全角文字を半角文字に変換します。|  
|全角|半角文字を全角文字に変換します。|  
|言語の文字種|システムのルールではなく、言語の文字種による規則 (チュルク語などのロケールにおける Unicode の文字種の単純な割り当て) を適用します。|  
|簡体中国語|繁体中国語の文字を簡体中国語に変換します。|  
|繁体字中国語|簡体中国語の文字を繁体中国語に変換します。|  
  
 **[出力の別名]**  
 各出力列の別名を入力します。 既定では、入力列の名前の後に " **のコピー** " が追加された別名になりますが、固有のわかりやすい名前を選択することもできます。  
  
 **エラー出力の構成**  
 [[エラー出力の構成]](../../2014/integration-services/configure-error-output.md) ダイアログ ボックスを使用して、この変換のエラー処理オプションを指定します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
