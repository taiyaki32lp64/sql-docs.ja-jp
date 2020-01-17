---
title: スクリプト コンポーネントでのログ記録 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 52f4c841d2022216480051576bb0b6da7bdb5d34
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71286464"
---
# <a name="logging-in-the-script-component"></a>スクリプト コンポーネントでのログ記録

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージのログ記録を使用すると、実行の進行状況、結果、問題点などに関する詳細な情報を、定義済みのイベントまたはユーザー定義のメッセージとして保存し、後で分析することができます。 スクリプト コンポーネントでユーザー定義のデータをログ記録するには、**ScriptMain** クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> メソッドを使用できます。 ログ記録が有効で、 **[SSIS ログの構成]** ダイアログ ボックスの **[詳細]** タブでログ記録の対象として **[ScriptComponentLogEntry]** イベントが選択されている場合、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> メソッドを 1 回呼び出すと、そのデータ フロー タスク用に設定されているすべてのログ プロバイダーに対し、イベント情報が保存されます。  
  
 ログ記録の簡単な例を次に示します。  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  ログ記録はスクリプト コンポーネントから直接実行できますが、ログ記録ではなくイベントを実装することを検討する必要があります。 イベントを使用すると、イベント メッセージのログ記録を有効にできるだけでなく、既定またはユーザー定義のイベント ハンドラーによってイベントに応答することができます。  
  
 ログ記録の詳細については、「[Integration Services &#40;SSIS&#41; のログ記録](../../../integration-services/performance/integration-services-ssis-logging.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のログ記録](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
