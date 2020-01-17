---
title: カスタム ログ プロバイダーの開発 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SSIS packages, log providers
- custom log providers [Integration Services]
- SQL Server Integration Services packages, log providers
- log providers [Integration Services]
- packages [Integration Services], logs
- Integration Services packages, log providers
ms.assetid: 3f715b95-7074-4f5c-8ae2-246998052e78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 25531ce8e4a405b1e52a0f1f8d81fb536087cff7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768608"
---
# <a name="developing-a-custom-log-provider"></a>カスタム ログ プロバイダーの開発
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、パッケージの実行中に発生したイベントをキャプチャできるようにする広範なログ記録機能があります。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] では、さまざまなログ プロバイダーを使用でき、ログを作成して XML、テキスト、データベースなどの形式で保存したり、Windows イベント ログに格納したりできます。 提供されるログ プロバイダーと出力形式が、要件を必ずしも満たさない場合は、カスタム ログ プロバイダーを作成できます。  
  
 カスタム ログ プロバイダーを作成するには、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 基本クラスを継承するクラスを作成し、新しいクラスに <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 属性を適用し、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> プロパティや <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> メソッドなど、基本クラスの重要なメソッドとプロパティをオーバーライドする必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 ここでは、カスタム ログ プロバイダーを作成、構成、およびコーディングする方法について説明します。  
  
 [カスタム ログ プロバイダーの作成](creating-a-custom-log-provider.md)  
 カスタム ログ プロバイダー プロジェクト用のクラスの作成方法について説明します。  
  
 [カスタム ログ プロバイダーのコーディング](coding-a-custom-log-provider.md)  
 基本クラスのメソッドとプロパティのオーバーライドによる、カスタム ログ プロバイダーの実装方法について説明します。  
  
 [カスタム ログ プロバイダー用ユーザー インターフェイスの開発](developing-a-user-interface-for-a-custom-log-provider.md)  
 カスタム ログ プロバイダー用のカスタム ユーザー インターフェイスは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ではサポートされません。  
  
## <a name="related-topics"></a>関連トピック  
  
### <a name="information-common-to-all-custom-objects"></a>すべてのカスタム オブジェクトに共通の情報  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で作成可能なカスタム オブジェクトのすべての種類に共通の情報については、次のトピックを参照してください。  
  
 [Integration Services 用のカスタム オブジェクトの開発](../developing-custom-objects-for-integration-services.md)  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のすべての型のカスタム オブジェクトを実装する基本手順について説明します。  
  
 [カスタム オブジェクトの永続化](../persisting-custom-objects.md)  
 カスタムの永続性と、それが必要な場合について説明します。  
  
 [カスタム オブジェクトのビルド、配置、デバッグ](../building-deploying-and-debugging-custom-objects.md)  
 カスタム オブジェクトをビルド、署名、配置、およびデバッグする方法について説明します。  
  
### <a name="information-about-other-custom-objects"></a>その他のカスタム オブジェクトに関する情報  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で作成可能なその他の種類のカスタム オブジェクトについては、次のトピックを参照してください。  
  
 [カスタム タスクの開発](../task/developing-a-custom-task.md)  
 カスタム タスクのプログラム方法について説明します。  
  
 [カスタム接続マネージャーの開発](../connection-manager/developing-a-custom-connection-manager.md)  
 カスタム接続マネージャーのプログラム方法について説明します。  
  
 [カスタム ForEach 列挙子の開発](../foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 カスタム列挙子のプログラム方法について説明します。  
  
 [カスタム データ フロー コンポーネントの開発](../data-flow/developing-a-custom-data-flow-component.md)  
 カスタム データ フローの変換元、変換、変換先のプログラム方法について説明します。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
  
