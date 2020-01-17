---
title: ディメンション処理変換先エディター ([接続マネージャー] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimprocessingtransformation.connection.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 44aab631-d62d-4895-8fc7-7f1f3b1b68ce
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2259b19cec6674cdb1f5f4a0064334f78aa5300f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059435"
---
# <a name="dimension-processing-destination-editor-connection-manager-page"></a>[ディメンション処理変換先エディター] ([接続マネージャー] ページ)
   **[ディメンション処理変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトまたは [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のインスタンスへの接続を指定できます。  
  
 ディメンション処理変換先の詳細については、「 [Dimension Processing Destination](data-flow/dimension-processing-destination.md)」を参照してください。  
  
## <a name="options"></a>および  
 **Connection manager**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[Analysis Services 接続マネージャーの追加]** ダイアログ ボックスを使用して、新しい接続を作成します。  
  
 **利用可能なディメンションの一覧**  
 処理するディメンションを選択します。  
  
 **[処理方法]**  
 一覧で選択したディメンションに適用する処理方法を選択します。 このオプションの既定値は **[完全]** です。  
  
|値|説明|  
|-----------|-----------------|  
|**[追加 (増分)]**|ディメンションの増分処理を実行します。|  
|**[完全]**|ディメンションの完全処理を実行します。|  
|**Update**|ディメンションの更新処理を実行します。|  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [ディメンション処理変換先エディター ([マッピング] ページ)](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)   
 [ディメンション処理変換先エディター ([詳細設定] ページ)](../../2014/integration-services/dimension-processing-destination-editor-advanced-page.md)  
  
  
