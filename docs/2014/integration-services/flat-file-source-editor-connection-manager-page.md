---
title: '[フラット ファイル ソース エディター] ([接続マネージャー] ページ) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesourceadapter.connection.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: 2efd6baa-ed75-4f3f-b667-514024cebdb8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3c729faa93cf445e7e0aff46fa94258bc7ea7a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058692"
---
# <a name="flat-file-source-editor-connection-manager-page"></a>[フラット ファイル ソース エディター]\ ([接続マネージャー] ページ)
  **[フラット ファイル ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、フラット ファイル ソースが使用する接続マネージャーを選択できます。 フラット ファイル ソースは、区切り形式、固定幅形式、または区切りと固定幅が混在した形式のテキスト ファイルからデータを読み取ります。  
  
 フラット ファイル ソースは、次のいずれかの種類の接続マネージャーを使用できます。  
  
-   ソースが単一のフラット ファイルの場合は、フラット ファイル接続マネージャー。 詳しくは、「 [フラット ファイル接続マネージャー](connection-manager/file-connection-manager.md)」をご覧ください。  
  
-   ソースが複数フラット ファイルで、データ フロー タスクが For ループ コンテナーなどのループ コンテナーの内部にある場合は、複数フラット ファイル接続マネージャー。 コンテナーの各ループで、フラット ファイル ソースは、複数フラット ファイル接続マネージャーが提供する次のファイル名からデータを読み込みます。 詳細については、「 [複数フラット ファイル接続マネージャー](connection-manager/multiple-flat-files-connection-manager.md)」を参照してください。  
  
 フラット ファイル ソースの詳細については、「 [Flat File Source](data-flow/flat-file-source.md)」を参照してください。  
  
## <a name="options"></a>および  
 **Flat file connection manager**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続マネージャーを作成します。  
  
 **[新規作成]**  
 新しい接続マネージャーを作成するには、 **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスを使用します。  
  
 **[データ ソースの NULL 値をデータ フローで NULL 値として保持する]**  
 データが抽出されたときに NULL 値を保持するかどうかを指定します。 このプロパティの既定値は **false**です。 この値が `alse` である場合、フラット ファイル変換元は変換元データの NULL 値を各列の適切な既定値で置き換えます。たとえば、文字列型の列の場合は空の文字列、数値型の列の場合は 0 です。  
  
 **プレビュー**  
 **[データ ビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [フラット ファイル ソース エディター ([列] ページ)](../../2014/integration-services/flat-file-source-editor-columns-page.md)   
 [フラット ファイル ソース エディター ([エラー出力] ページ)](../../2014/integration-services/flat-file-source-editor-error-output-page.md)   
 [フラット ファイル接続マネージャー](connection-manager/file-connection-manager.md)  
  
  
