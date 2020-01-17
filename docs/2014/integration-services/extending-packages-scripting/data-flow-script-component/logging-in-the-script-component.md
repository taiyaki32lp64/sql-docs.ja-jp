---
title: スクリプト コンポーネントでのログ記録 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c4723c0e78b37142d7f0a2ccdc16e37ce0fb78fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768428"
---
# <a name="logging-in-the-script-component"></a>スクリプト コンポーネントでのログ記録
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージのログ記録を使用すると、実行の進行状況、結果、問題点などに関する詳細な情報を、定義済みのイベントまたはユーザー定義のメッセージとして保存し、後で分析することができます。 スクリプト コンポーネントでユーザー定義のデータをログ記録するには、`ScriptMain` クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> メソッドを使用できます。 ログ記録が有効で、 **[SSIS ログの構成]** ダイアログ ボックスの **[詳細]** タブでログ記録の対象として **[ScriptComponentLogEntry]** イベントが選択されている場合、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> メソッドを 1 回呼び出すと、そのデータ フロー タスク用に設定されているすべてのログ プロバイダーに対し、イベント情報が保存されます。  
  
 ログ記録の簡単な例を次に示します。  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  ログ記録はスクリプト コンポーネントから直接実行できますが、ログ記録ではなくイベントを実装することを検討する必要があります。 イベントを使用すると、イベント メッセージのログ記録を有効にできるだけでなく、既定またはユーザー定義のイベント ハンドラーによってイベントに応答することができます。  
  
 ログ記録の詳細については、「[Integration Services &#40;SSIS&#41; のログ記録](../../performance/integration-services-ssis-logging.md)」を参照してください。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のログ記録](../../performance/integration-services-ssis-logging.md)  
  
  
