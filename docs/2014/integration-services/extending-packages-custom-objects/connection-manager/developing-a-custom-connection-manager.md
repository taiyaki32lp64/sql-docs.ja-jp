---
title: カスタム接続マネージャーの開発 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- packages [Integration Services], connections
- custom connection managers [Integration Services], about custom connection managers
- connection managers [Integration Services], custom
- Integration Services packages, connection managers
- SSIS packages, connection managers
- SQL Server Integration Services packages, connection managers
- custom connection managers [Integration Services]
ms.assetid: bda0b29e-57f5-4879-b04d-1396dc56daa8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fee544578a24f47e662645a0d5cd576a74fb0496
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768891"
---
# <a name="developing-a-custom-connection-manager"></a>カスタム接続マネージャーの開発
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] では、接続マネージャーを使用して、外部データ ソースに接続するために必要な情報をカプセル化します。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、エンタープライズ データベースからテキスト ファイルや Excel ワークシートまで、よく使用されるデータ ソースへの接続をサポートする、さまざまな接続マネージャーが用意されています。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] でサポートされている接続マネージャーと外部データ ソースが、要件を必ずしも満たさない場合は、カスタム接続マネージャーを作成できます。  
  
 カスタム接続マネージャーを作成するには、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> 基本クラスを継承するクラスを作成し、新しいクラスに <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> 属性を適用し、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> プロパティや <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> メソッドなど、基本クラスの重要なメソッドとプロパティをオーバーライドする必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] に組み込まれているタスク、変換元、および変換先の多くは、組み込みの接続マネージャーの特定の種類でのみ機能します。 組み込みのタスクやコンポーネントで使用するカスタム接続マネージャーを開発する前に、それらのコンポーネントで使用できる接続マネージャーが、特定の種類に限定されるかどうかを確認してください。 ソリューションがカスタム接続マネージャーを必要とする場合は、その接続マネージャーで機能するカスタムのタスク、変換元、および変換先も開発する必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 ここでは、カスタム接続マネージャーとそのオプションのカスタム ユーザー インターフェイスを作成、構成、およびコーディングする方法について説明します。 このセクション内のコード スニペットは、Sql Server Custom Connection Manager のサンプルに含まれています。  
  
 [カスタム接続マネージャーの作成](creating-a-custom-connection-manager.md)  
 カスタム接続マネージャー プロジェクト用のクラスの作成方法について説明します。  
  
 [カスタム接続マネージャーのコーディング](coding-a-custom-connection-manager.md)  
 基本クラスのメソッドとプロパティのオーバーライドによる、カスタム接続マネージャーの実装方法について説明します。  
  
 [カスタム接続マネージャー用ユーザー インターフェイスの開発](developing-a-user-interface-for-a-custom-connection-manager.md)  
 ユーザー インターフェイス クラスと、カスタム接続マネージャーの構成に使用するフォームの実装方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
  
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
  
 [カスタム ログ プロバイダーの開発](../log-provider/developing-a-custom-log-provider.md)  
 カスタム ログ プロバイダーのプログラム方法について説明します。  
  
 [カスタム ForEach 列挙子の開発](../foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 カスタム列挙子のプログラム方法について説明します。  
  
 [カスタム データ フロー コンポーネントの開発](../data-flow/developing-a-custom-data-flow-component.md)  
 カスタム データ フローの変換元、変換、変換先のプログラム方法について説明します。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
  
