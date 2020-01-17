---
title: Odbc 入力元エディター ([列] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.columns.f1
ms.assetid: 565984eb-8318-4be7-bebc-262209cf5065
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5bfda61e5a57dabd62289f32d04d6367695b070b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057168"
---
# <a name="odbc-source-editor-columns-page"></a>[ODBC ソース エディター] ([列] ページ)
  **[ODBC ソース エディター]** ダイアログ ボックスの **[列]** ページを使用すると、出力列をそれぞれの外部 (入力元) 列にマップできます。  
  
 ODBC 入力元の詳細については、「 [ODBC Source](data-flow/odbc-source.md)」を参照してください。  
  
## <a name="task-list"></a>タスク一覧  
 **[ODBC 入力元エディター] の [列] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で、ODBC 入力元を含む [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ODBC 入力元をダブルクリックします。  
  
3.  **[ODBC 入力元エディター]** で、 **[列]** をクリックします。  
  
## <a name="options"></a>および  
  
### <a name="available-external-columns"></a>使用できる外部列  
 データ ソース内の使用できる外部列の一覧です。 このテーブルを使用して列を追加または削除することはできません。 入力元から使用する列を選択します。 選択した列は、選択した順序で **[外部列]** の一覧に追加されます。  
  
 **[すべて選択]** チェック ボックスをオンにすると、すべての列が選択されます。  
  
### <a name="external-column"></a>外部列  
 外部 (入力元) 列のビューです。ODBC 入力元のデータを使用するコンポーネントを構成するときの表示順になります。  
  
### <a name="output-column"></a>出力列  
 各出力列の一意の名前を入力します。 既定では選択された外部 (変換元) 列の名前になりますが、一意でわかりやすい名前を付けることもできます。 入力した名前は、SSIS デザイナーで表示されます。  
  
## <a name="see-also"></a>参照  
 [ODBC ソース エディター ([接続マネージャー] ページ)](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [[ODBC ソース エディター] &#40;[エラー出力] ページ&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  
