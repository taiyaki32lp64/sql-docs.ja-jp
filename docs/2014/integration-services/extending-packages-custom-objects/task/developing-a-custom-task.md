---
title: カスタム タスクの開発 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom tasks [Integration Services], about custom tasks
- Task class
- custom tasks [Integration Services]
- SSIS custom tasks
- SSIS custom tasks, about custom tasks
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- tasks [Integration Services], custom
- TaskHost object
ms.assetid: dcbd8615-fa6d-4ddb-b8a5-0b19dddd6239
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7f597ee3a063da534267f7d4674a024a8fcc02f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896143"
---
# <a name="developing-a-custom-task"></a>カスタム タスクの開発
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] は、作業単位を実行するタスクを使用して、データの抽出、変換、および読み込みをサポートします。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、SQL ステートメントの実行から、FTP サイトからのファイルのダウンロードまで、頻繁に使用される操作を実行するためのさまざまなタスクが用意されています。 用意されているタスクとサポートされている操作が、要件を完全には満たない場合は、カスタム タスクを作成できます。  
  
 カスタム タスクを作成するには、<xref:Microsoft.SqlServer.Dts.Runtime.Task> 基本クラスを継承するクラスを作成し、新しいクラスに <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 属性を適用して、<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> メソッドなど、基本クラスの重要なメソッドとプロパティをオーバーライドする必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 ここでは、カスタム タスクとそのオプションのカスタム ユーザー インターフェイスを作成、構成、およびコーディングする方法について説明します。  
  
 [カスタム タスクの作成](creating-a-custom-task.md)  
 カスタム タスクを作成する最初の手順について説明します。  
  
 [カスタム タスクのコーディング](coding-a-custom-task.md)  
 カスタム タスクの主なメソッドのコードを記述する方法について説明します。  
  
 [カスタム タスクでのデータ ソースへの接続](connecting-to-data-sources-in-a-custom-task.md)  
 カスタム タスクをデータ ソースに接続する方法について説明します。  
  
 [カスタム タスクでのイベントの発生と定義](raising-and-defining-events-in-a-custom-task.md)  
 カスタム タスクからカスタム イベントを発生させ、定義する方法について説明します。  
  
 [カスタム タスクにおけるデバッグのサポートの追加](adding-support-for-debugging-in-a-custom-task.md)  
 カスタム タスクでのブレークポイント ターゲットの作成方法について説明します。  
  
 [カスタム タスク用ユーザー インターフェイスの開発](developing-a-user-interface-for-a-custom-task.md)  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーに表示され、カスタム タスクのプロパティを構成するユーザー インターフェイスの作成方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
  
### <a name="information-common-to-all-custom-objects"></a>すべてのカスタム オブジェクトに共通の情報  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で作成可能なカスタム オブジェクトのすべての種類に共通の情報については、次のトピックを参照してください。  
  
 [Integration Services 用のカスタム オブジェクトの開発](../developing-custom-objects-for-integration-services.md)  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のすべての種類のカスタム オブジェクトを実装する基本手順について説明します。  
  
 [カスタム オブジェクトの永続化](../persisting-custom-objects.md)  
 カスタムの永続性と、それが必要な場合について説明します。  
  
 [カスタム オブジェクトのビルド、配置、デバッグ](../building-deploying-and-debugging-custom-objects.md)  
 カスタム オブジェクトをビルド、署名、配置、およびデバッグする方法について説明します。  
  
### <a name="information-about-other-custom-objects"></a>その他のカスタム オブジェクトに関する情報  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で作成可能なその他の種類のカスタム オブジェクトについては、次のトピックを参照してください。  
  
 [カスタム接続マネージャーの開発](../connection-manager/developing-a-custom-connection-manager.md)  
 カスタム接続マネージャーのプログラム方法について説明します。  
  
 [カスタム ログ プロバイダーの開発](../log-provider/developing-a-custom-log-provider.md)  
 カスタム ログ プロバイダーのプログラム方法について説明します。  
  
 [カスタム ForEach 列挙子の開発](../foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 カスタム列挙子のプログラム方法について説明します。  
  
 [カスタム データ フロー コンポーネントの開発](../data-flow/developing-a-custom-data-flow-component.md)  
 カスタム データ フローの変換元、変換、変換先のプログラム方法について説明します。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [スクリプト タスクによるパッケージの拡張](../../extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [スクリプティング ソリューションとカスタム オブジェクトとの比較](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
