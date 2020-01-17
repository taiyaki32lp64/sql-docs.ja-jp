---
title: 手順 1:配置バンドルのコピー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b6ef1e56-d278-4a24-afd3-68d8e0595cbb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1d28a85e4dccaa6165d96046848513879998136f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891711"
---
# <a name="step-1-copying-the-deployment-bundle"></a>手順 1:配置バンドルのコピー
  このタスクでは、配置先コンピューターに配置バンドルをコピーします。  
  
 配置先コンピューターに配置バンドルをコピーするには、まず配置先コンピューターにパブリック共有を作成し、ドライブをパブリック共有にマッピングして、配置バンドルを共有にコピーするのが最も簡単な方法です。 パブリック フォルダーを作成して構成する方法や、ドライブのマッピング方法がわからない場合は、Windows のドキュメントを参照してください。  
  
### <a name="to-copy-the-deployment-bundle"></a>配置バンドルをコピーするには  
  
1.  コンピューターで配置バンドルを探します。  
  
     既定の場所を使用した場合、配置バンドルは Deployment Tutorial フォルダーの Bin\Deployment フォルダーにあります。  
  
2.  Deployment フォルダーを右クリックし、 **[コピー]** をクリックします。  
  
3.  ターゲット コンピューターで、フォルダーをコピーするパブリック共有を探し、 **[貼り付け]** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [手順 2:パッケージ インストール ウィザードの実行](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
![Integration Services のアイコン (小)](media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
  
