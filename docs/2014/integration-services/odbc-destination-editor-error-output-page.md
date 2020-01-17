---
title: Odbc 入力先エディター ([エラー出力] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 972357372fe6d0281aedb57d49dd8d50682085b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057200"
---
# <a name="odbc-destination-editor-error-output-page"></a>ODBC 変換先エディター ([エラー出力] ページ)
  **[ODBC 入力先エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択できます。  
  
 ODBC 入力先の詳細については、「 [ODBC Destination](data-flow/odbc-destination.md)」を参照してください。  
  
 **[ODBC 入力先エディター] の [エラー出力] ページを開くには**  
  
## <a name="task-list"></a>タスク一覧  
  
-   [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で、ODBC 入力先を含む [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
-   **[データ フロー]** タブで、ODBC 入力先をダブルクリックします。  
  
-   **[ODBC 入力先エディター]** で、 **[エラー出力]** をクリックします。  
  
## <a name="options"></a>および  
  
### <a name="inputoutput"></a>[入力または出力]  
 データ ソースの名前を表示します。  
  
### <a name="column"></a>[列]  
 使用されていません。  
  
### <a name="error"></a>[エラー]  
 ODBC 入力先でフローのエラーを処理する方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
### <a name="truncation"></a>切り捨て  
 ODBC 入力先でフローの切り捨てを処理する方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
### <a name="description"></a>説明  
 エラーの説明を表示します。  
  
### <a name="set-this-value-to-selected-cells"></a>[選択したセルに設定する値]  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルを ODBC 入力先でどのように処理するか (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
### <a name="apply"></a>[適用]  
 選択したセルにエラー処理オプションを適用します。  
  
## <a name="error-handling-options"></a>エラー処理オプション  
 ODBC 入力先でのエラーと切り捨ての処理方法を構成するには、次のオプションを使用します。  
  
### <a name="fail-component"></a>エラー コンポーネント  
 エラーまたは切り捨てが発生すると、データ フロー タスクは失敗します。 これは既定の動作です。  
  
### <a name="ignore-failure"></a>エラーを無視する  
 エラーまたは切り捨ては無視されます。  
  
### <a name="redirect-flow"></a>[フローのリダイレクト]  
 エラーまたは切り捨てが ODBC 入力先のエラー出力に送られる原因となった行。 詳細については、「ODBC 入力先」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ODBC 変換先エディター &#40;[接続マネージャー] ページ&#41;](../../2014/integration-services/odbc-destination-editor-connection-manager-page.md)   
 [ODBC 変換先エディター ([マッピング] ページ)](../../2014/integration-services/odbc-destination-editor-mappings-page.md)  
  
  
