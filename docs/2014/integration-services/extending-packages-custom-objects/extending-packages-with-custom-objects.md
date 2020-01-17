---
title: カスタム オブジェクトを使用したパッケージの拡張 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 26616eb8-9e80-434d-b22a-ece1b00f449d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d7384fd52f28f52647c310f7c76eec994b8c8141
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896210"
---
# <a name="extending-packages-with-custom-objects"></a>カスタム オブジェクトを使用したパッケージの拡張
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で提供されるコンポーネントがユーザーの要件を満たさない場合、独自の拡張機能をコーディングすることにより、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の機能を拡張できます。 パッケージを拡張するには 2 つの方法があります。1 つ目は、スクリプト タスクおよびスクリプト コンポーネントによって提供される強力なラッパー内でコードを記述する方法です。2 つ目は、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクト モデルによって提供される基本クラスを基にカスタム [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 拡張機能を最初から作成する方法です。  
  
 ここでは、カスタム オブジェクトを使用してパッケージを拡張する 2 つの方法について詳しく説明します。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カスタム ソリューションで、スクリプト タスクやスクリプト コンポーネントよりさらに柔軟な設定が必要な場合、または複数のパッケージで再利用できるコンポーネントが必要な場合は、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクト モデルを使用すると、カスタム タスク、データ フロー コンポーネント、およびその他のパッケージ オブジェクトを、マネージド コードで最初から作成できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [Integration Services 用のカスタム オブジェクトの開発](developing-custom-objects-for-integration-services.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で作成できるカスタム オブジェクトについて説明し、必要な手順や設定の概要を示します。  
  
 [カスタム オブジェクトの永続化](persisting-custom-objects.md)  
 カスタム オブジェクトの既定の永続性、およびカスタムの永続性の実装プロセスについて説明します。  
  
 [カスタム オブジェクトのビルド、配置、デバッグ](building-deploying-and-debugging-custom-objects.md)  
 さまざまな種類のカスタム オブジェクトの作成、配置、テストの一般的なアプローチについて説明します。  
  
 [カスタム タスクの開発](task/developing-a-custom-task.md)  
 カスタム タスクのコードを記述する手順について説明します。  
  
 [カスタム接続マネージャーの開発](connection-manager/developing-a-custom-connection-manager.md)  
 カスタム接続マネージャーのコードを記述する手順について説明します。  
  
 [カスタム ログ プロバイダーの開発](log-provider/developing-a-custom-log-provider.md)  
 カスタム ログ プロバイダーのコードを記述する手順について説明します。  
  
 [カスタム ForEach 列挙子の開発](foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 カスタム列挙子のコードを記述する手順について説明します。  
  
 [カスタム データ フロー コンポーネントの開発](data-flow/developing-a-custom-data-flow-component.md)  
 カスタム データ フローの変換元、変換、変換先のプログラム方法について説明します。  
  
## <a name="reference"></a>リファレンス  
 [Integration Services のエラーとメッセージのリファレンス](../integration-services-error-and-message-reference.md)  
 事前に定義されている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エラー コードと、そのシンボル名および説明の一覧を示します。  
  
## <a name="related-sections"></a>関連項目  
 [スクリプトによるパッケージの拡張](../extending-packages-scripting/extending-packages-with-scripting.md)  
 スクリプト タスクを使用した制御フローの拡張方法や、スクリプト コンポーネントを使用したデータ フローの拡張方法について説明します。  
  
 [プログラムによるパッケージの作成](../building-packages-programmatically/building-packages-programmatically.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージをプログラムで作成、構成、実行、読み込み、保存、および管理する方法を説明します。  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [スクリプティング ソリューションとカスタム オブジェクトとの比較](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
