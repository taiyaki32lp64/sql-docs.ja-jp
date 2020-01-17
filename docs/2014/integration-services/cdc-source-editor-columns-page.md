---
title: CDC ソース エディター (列 ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.columns.f1
ms.assetid: bcf3030e-98d8-4445-967c-33c3f8ecb4fc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 980b9cf22e2c50cd1de3eb90a06e6496c01cc093
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061031"
---
# <a name="cdc-source-editor-columns-page"></a>[CDC ソース エディター] ([列] ページ)
  **[CDC ソース エディター]** ダイアログ ボックスの **[列]** ページを使用すると、出力列をそれぞれの外部 (ソース) 列にマップできます。  
  
 CDC ソースの詳細については、「 [CDC Source](data-flow/cdc-source.md)」を参照してください。  
  
## <a name="task-list"></a>タスク一覧  
 **[CDC ソース エディター] の [列] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で、CDC ソースを含む [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、CDC ソースをダブルクリックします。  
  
3.  **[CDC ソース エディター]** で、 **[列]** をクリックします。  
  
## <a name="options"></a>および  
 **使用できる外部列**  
 データ ソース内の使用できる外部列の一覧です。 このテーブルを使用して列を追加または削除することはできません。 ソースで使用する列を選択します。 選択した列は、選択した順序で **[外部列]** の一覧に追加されます。  
  
 **[外部列]**  
 外部 (ソース) 列のビューです。CDC ソースのデータを使用するコンポーネントを構成するときの表示順になります。 この順序を変更するには、まず **[使用できる外部列]** の一覧で選択した列を消去してから、別の順序で一覧から外部列を選択します。 選択した列は、選択した順序で **[外部列]** の一覧に追加されます。  
  
 **出力列**  
 各出力列の一意の名前を入力します。 既定では選択された外部 (ソース) 列の名前になりますが、一意でわかりやすい名前を付けることもできます。 入力した名前は、SSIS デザイナーで表示されます。  
  
## <a name="see-also"></a>参照  
 [CDC ソース エディター &#40;[接続マネージャー] ページ&#41;](../../2014/integration-services/cdc-source-editor-connection-manager-page.md)   
 [CDC ソース エディター &#40;[エラー出力] ページ&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  
