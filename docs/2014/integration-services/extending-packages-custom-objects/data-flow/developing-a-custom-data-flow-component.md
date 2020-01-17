---
title: カスタム データ フロー コンポーネントの開発 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6c174fe5cdf1ebe1dbc9b0350a01fb6e8027effa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768968"
---
# <a name="developing-a-custom-data-flow-component"></a>カスタム データ フロー コンポーネントの開発
  データ フロー タスクは、さまざまなデータ ソースに接続し、そのデータを高速で変換およびルーティングするコンポーネントで構成されています。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] では、拡張可能なオブジェクト モデルが用意されており、開発者はそのオブジェクト モデルを使用して、[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] や配置されたパッケージで使用できるカスタム変換元、カスタム変換、およびカスタム変換先を作成できます。 ここでは、カスタム データ フロー コンポーネントの開発に役立つトピックを紹介します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [カスタム データ フロー コンポーネントの作成](creating-a-custom-data-flow-component.md)  
 カスタム データ フロー コンポーネントを作成するための初期手順について説明します。  
  
 [データ フロー コンポーネントのデザイン時のメソッド](design-time-methods-of-a-data-flow-component.md)  
 カスタム データ フロー コンポーネントに実装する、デザイン時のメソッドについて説明します。  
  
 [データ フロー コンポーネントの実行時のメソッド](run-time-methods-of-a-data-flow-component.md)  
 カスタム データ フロー コンポーネントに実装する、実行時のメソッドについて説明します。  
  
 [実行プランおよびバッファーの割り当て](execution-plan-and-buffer-allocation.md)  
 データ フローの実行プラン、およびデータ バッファーの割り当てについて説明します。  
  
 [データ フロー内のデータ型の処理](working-with-data-types-in-the-data-flow.md)  
 データ フローが [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] データ型をどのように .NET Framework マネージド データ型にマップするかについて説明します。  
  
 [データ フロー コンポーネントの検証](validating-a-data-flow-component.md)  
 コンポーネントの構成の検証、およびコンポーネントのメタデータの再構成に使用するメソッドについて説明します。  
  
 [外部メタデータの実装](implementing-external-metadata.md)  
 データ検証用の外部メタデータ列の使用方法について説明します。  
  
 [データ フロー コンポーネントのイベントの発生と定義](raising-and-defining-events-in-a-data-flow-component.md)  
 定義済みのイベントおよびカスタム イベントの起動方法について説明します。  
  
 [データ フロー コンポーネントのログ エントリの記録と定義](logging-and-defining-log-entries-in-a-data-flow-component.md)  
 カスタム ログ エントリの作成方法およびカスタム ログ エントリへの書き込み方法について説明します。  
  
 [データ フロー コンポーネントでのエラー出力の使用](using-error-outputs-in-a-data-flow-component.md)  
 エラー行を別の出力にリダイレクトする方法について説明します。  
  
 [データ フロー コンポーネントのバージョンのアップグレード](upgrading-the-version-of-a-data-flow-component.md)  
 新しいバージョンのコンポーネントが最初に使用されるときに、保存されたコンポーネント メタデータを更新する方法について説明します。  
  
 [データ フロー コンポーネント用ユーザー インターフェイスの開発](developing-a-user-interface-for-a-data-flow-component.md)  
 コンポーネント用のカスタム エディターの実装方法について説明します。  
  
 [特定の種類のデータ フロー コンポーネントの開発](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
 変換元、変換、および変換先の、3 種類のデータ フロー コンポーネントの開発に関する情報が含まれています。  
  
## <a name="reference"></a>リファレンス  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 カスタム データ フロー コンポーネントを作成するために使用するクラスやインターフェイスが含まれています。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 データ フロー タスクのオブジェクト モデルを構成するクラスおよびインターフェイスが含まれており、これを使用するとカスタム データ フロー コンポーネントを作成したり、データ フロー タスクを構築できます。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>  
 データ フロー コンポーネント用のユーザー インターフェイスの作成に使用する、クラスおよびインターフェイスが含まれています。  
  
 [Integration Services のエラーとメッセージのリファレンス](../../integration-services-error-and-message-reference.md)  
 事前に定義されている [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] エラー コードと、そのシンボル名および説明の一覧を示します。  
  
## <a name="related-sections"></a>関連項目  
  
### <a name="information-common-to-all-custom-objects"></a>すべてのカスタム オブジェクトに共通の情報  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で作成可能なカスタム オブジェクトのすべての種類に共通の情報については、次のトピックを参照してください。  
  
 [Integration Services 用のカスタム オブジェクトの開発](../../extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のすべての型のカスタム オブジェクトを実装する基本手順について説明します。  
  
 [カスタム オブジェクトの永続化](../../extending-packages-custom-objects/persisting-custom-objects.md)  
 カスタムの永続性と、それが必要な場合について説明します。  
  
 [カスタム オブジェクトのビルド、配置、デバッグ](../../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 カスタム オブジェクトをビルド、署名、配置、およびデバッグする方法について説明します。  
  
### <a name="information-about-other-custom-objects"></a>その他のカスタム オブジェクトに関する情報  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で作成可能なその他の種類のカスタム オブジェクトについては、次のトピックを参照してください。  
  
 [カスタム タスクの開発](../../extending-packages-custom-objects/task/developing-a-custom-task.md)  
 カスタム タスクのプログラム方法について説明します。  
  
 [カスタム接続マネージャーの開発](../../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 カスタム接続マネージャーのプログラム方法について説明します。  
  
 [カスタム ログ プロバイダーの開発](../../extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 カスタム ログ プロバイダーのプログラム方法について説明します。  
  
 [カスタム ForEach 列挙子の開発](../../extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 カスタム列挙子のプログラム方法について説明します。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [スクリプト コンポーネントによるデータ フローの拡張](../../extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md   
 [スクリプティング ソリューションとカスタム オブジェクトとの比較](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
