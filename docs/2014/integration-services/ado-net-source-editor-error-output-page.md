---
title: ADO net 変換元エディター ([エラー出力] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.erroroutput.f1
ms.assetid: 4dd9d129-a95c-4d3a-bbbf-e84a39089950
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8543f1a7bd14db09873aaefb58b74efae0f3cf34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061636"
---
# <a name="ado-net-source-editor-error-output-page"></a>[ADO NET 変換元エディター] ([エラー出力] ページ)
  **[ADO NET 変換元エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択したり、エラー出力列のプロパティを設定したりできます。  
  
 ADO NET 変換元の詳細については、「 [ADO NET Source](data-flow/ado-net-source.md)」を参照してください。  
  
 **[エラー出力] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、ADO NET 変換元を含む [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ADO NET 変換元をダブルクリックします。  
  
3.  **[ADO NET 変換元エディター]** で、 **[エラー出力]** をクリックします。  
  
## <a name="options"></a>および  
 **[入力または出力]**  
 データ ソースの名前を表示します。  
  
 **列**  
 **[ADO NET 変換元エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで選択した外部 (変換元) 列を表示します。  
  
 **Error**  
 エラーが発生した場合に、障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **関連項目:** [データのエラー処理](data-flow/error-handling-in-data.md)  
  
 **切り捨て**  
 切り捨てが発生したときの処理方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を指定します。  
  
 **[説明]**  
 エラーの説明を表示します。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルに対して障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
## <a name="see-also"></a>参照  
 [[ADO NET 変換元エディター] ([接続マネージャー] ページ)](../../2014/integration-services/ado-net-source-editor-connection-manager-page.md)   
 [[ADO NET 変換元エディター] ([列] ページ)](../../2014/integration-services/ado-net-source-editor-columns-page.md)   
 [ADO.NET 接続マネージャー](connection-manager/ado-net-connection-manager.md)  
  
  
