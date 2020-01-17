---
title: 用語抽出変換エディター ([除外] タブ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextraction.inclusionexclusion.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 90110d95-fd97-4542-9cda-832c86606130
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b1032a0fc11ab07069309b7053e756d28329b77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055231"
---
# <a name="term-extraction-transformation-editor-exclusion-tab"></a>[用語抽出変換エディター] ([除外] タブ)
  **[用語抽出変換エディター]** ダイアログ ボックスの **[除外]** タブを使用すると、除外テーブルへの接続を設定し、除外用語が含まれている列を指定できます。  
  
 用語抽出変換の詳細については、「 [Term Extraction Transformation](data-flow/transformations/term-extraction-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[除外用語を使用する]**  
 除外用語が含まれている列を指定することにより、用語抽出のときに特定の用語を除外するかどうかを示します。 用語を除外する場合は、次のソース プロパティを指定する必要があります。  
  
 **[キャッシュなし]**  
 既存の OLE DB 接続マネージャーを選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスを使用して、データベースへの新しい接続を作成します。  
  
 **[テーブルまたはビュー]**  
 除外用語が含まれているテーブルまたはビューを選択します。  
  
 **列**  
 除外用語が含まれているテーブルまたはビューの列を選択します。  
  
 **エラー出力の構成**  
 [[エラー出力の構成]](../../2014/integration-services/configure-error-output.md) ダイアログ ボックスは、エラーが発生した行に対するエラー処理を指定するために使用します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[用語抽出変換エディター] &#40;[用語抽出] タブ&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [[用語抽出変換エディター] &#40;[詳細設定] タブ&#41;](../../2014/integration-services/term-extraction-transformation-editor-advanced-tab.md)   
 [用語参照変換](data-flow/transformations/lookup-transformation.md)  
  
  
