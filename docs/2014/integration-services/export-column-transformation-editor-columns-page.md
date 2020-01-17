---
title: 列エクスポート変換エディター ([列] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fileextractortransformation.columns.f1
helpviewer_keywords:
- Export Column Transformation Editor
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0d5e37211471285e971ba29bc3419e759b0c7af7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059007"
---
# <a name="export-column-transformation-editor-columns-page"></a>[列エクスポート変換エディター] ([列] ページ)
  **[列エクスポート変換エディター]** ダイアログ ボックスの **[列]** ページを使用すると、ファイルに抽出するデータ フロー内の列を指定できます。 列エクスポート変換でファイルにデータを追加するか、既存のファイルを上書きするかどうかを指定できます。  
  
 列エクスポート変換の詳細については、「 [Export Column Transformation](data-flow/transformations/export-column-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[列の抽出]**  
 テキストまたは画像データを持つ入力列の一覧から選択します。 すべての行には、 **[列の抽出]** と **[ファイル パス列]** の定義が含まれます。  
  
 **[ファイル パス列]**  
 ファイル パスとファイル名を持つ入力列の一覧から選択します。 すべての行には、 **[列の抽出]** と **[ファイル パス列]** の定義が含まれます。  
  
 **[追加の許可]**  
 変換により、既存のファイルにデータを追加するかどうかを指定します。 既定値は `false` です。  
  
 **[強制的に切り捨て]**  
 変換により、データを書き込む前に既存のファイルの内容を削除するかどうかを指定します。 既定値は `false` です。  
  
 **[バイト順マークの書き込み]**  
 バイト順マーク (BOM) をファイルに書き込むかどうかを指定します。 BOM は、データが `DT_NTEXT` または DT_WSTR のデータ型を持つ場合にのみ書き込まれ、既存のデータ ファイルには追加されません。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[列エクスポート変換エディター] &#40;[エラー出力] ページ&#41;](../../2014/integration-services/export-column-transformation-editor-error-output-page.md)  
  
  
