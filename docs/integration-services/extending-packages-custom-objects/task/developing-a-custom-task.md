---
title: カスタム タスクの開発 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 671c49e0b36107682994fdc2192a11db0b40d9d1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297114"
---
# <a name="developing-a-custom-task"></a>カスタム タスクの開発

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] は、作業単位を実行するタスクを使用して、データの抽出、変換、および読み込みをサポートします。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、SQL ステートメントの実行から、FTP サイトからのファイルのダウンロードまで、頻繁に使用される操作を実行するためのさまざまなタスクが用意されています。 用意されているタスクとサポートされている操作が、要件を完全には満たない場合は、カスタム タスクを作成できます。  
  
 カスタム タスクを作成するには、<xref:Microsoft.SqlServer.Dts.Runtime.Task> 基本クラスを継承するクラスを作成し、新しいクラスに <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 属性を適用して、<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> メソッドなど、基本クラスの重要なメソッドとプロパティをオーバーライドする必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 ここでは、カスタム タスクとそのオプションのカスタム ユーザー インターフェイスを作成、構成、およびコーディングする方法について説明します。  
  
 [カスタム タスクの作成](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)  
 カスタム タスクを作成する最初の手順について説明します。  
  
 [カスタム タスクのコーディング](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)  
 カスタム タスクの主なメソッドのコードを記述する方法について説明します。  
  
 [カスタム タスクでのデータ ソースへの接続](../../../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
 カスタム タスクをデータ ソースに接続する方法について説明します。  
  
 [カスタム タスクでのイベントの発生と定義](../../../integration-services/extending-packages-custom-objects/task/raising-and-defining-events-in-a-custom-task.md)  
 カスタム タスクからカスタム イベントを発生させ、定義する方法について説明します。  
  
 [カスタム タスクにおけるデバッグのサポートの追加](../../../integration-services/extending-packages-custom-objects/task/adding-support-for-debugging-in-a-custom-task.md)  
 カスタム タスクでのブレークポイント ターゲットの作成方法について説明します。  
  
 [カスタム タスク用ユーザー インターフェイスの開発](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーに表示され、カスタム タスクのプロパティを構成するユーザー インターフェイスの作成方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
  
### <a name="information-common-to-all-custom-objects"></a>すべてのカスタム オブジェクトに共通の情報  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で作成可能なカスタム オブジェクトのすべての種類に共通の情報については、次のトピックを参照してください。  
  
 [Integration Services 用のカスタム オブジェクトの開発](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のすべての種類のカスタム オブジェクトを実装する基本手順について説明します。  
  
 [カスタム オブジェクトの永続化](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 カスタムの永続性と、それが必要な場合について説明します。  
  
 [カスタム オブジェクトのビルド、配置、デバッグ](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 カスタム オブジェクトをビルド、署名、配置、およびデバッグする方法について説明します。  
  
### <a name="information-about-other-custom-objects"></a>その他のカスタム オブジェクトに関する情報  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で作成可能なその他の種類のカスタム オブジェクトについては、次のトピックを参照してください。  
  
 [カスタム接続マネージャーの開発](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 カスタム接続マネージャーのプログラム方法について説明します。  
  
 [カスタム ログ プロバイダーの開発](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 カスタム ログ プロバイダーのプログラム方法について説明します。  
  
 [カスタム ForEach 列挙子の開発](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 カスタム列挙子のプログラム方法について説明します。  
  
 [カスタム データ フロー コンポーネントの開発](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 カスタム データ フローの変換元、変換、変換先のプログラム方法について説明します。  
  
## <a name="see-also"></a>参照  
 [スクリプト タスクによるパッケージの拡張](../../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [スクリプティング ソリューションとカスタム オブジェクトとの比較](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
