---
title: カスタム接続マネージャーの開発 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7e8810b9f6aa5b167ff45607821d304af81123c2
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71287747"
---
# <a name="developing-a-custom-connection-manager"></a>カスタム接続マネージャーの開発

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] では、接続マネージャーを使用して、外部データ ソースに接続するために必要な情報をカプセル化します。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、エンタープライズ データベースからテキスト ファイルや Excel ワークシートまで、よく使用されるデータ ソースへの接続をサポートする、さまざまな接続マネージャーが用意されています。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] でサポートされている接続マネージャーと外部データ ソースが、要件を必ずしも満たさない場合は、カスタム接続マネージャーを作成できます。  
  
 カスタム接続マネージャーを作成するには、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> 基本クラスを継承するクラスを作成し、新しいクラスに <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> 属性を適用し、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> プロパティや <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> メソッドなど、基本クラスの重要なメソッドとプロパティをオーバーライドする必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] に組み込まれているタスク、変換元、および変換先の多くは、組み込みの接続マネージャーの特定の種類でのみ機能します。 組み込みのタスクやコンポーネントで使用するカスタム接続マネージャーを開発する前に、それらのコンポーネントで使用できる接続マネージャーが、特定の種類に限定されるかどうかを確認してください。 ソリューションがカスタム接続マネージャーを必要とする場合は、その接続マネージャーで機能するカスタムのタスク、変換元、および変換先も開発する必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 ここでは、カスタム接続マネージャーとそのオプションのカスタム ユーザー インターフェイスを作成、構成、およびコーディングする方法について説明します。 このセクション内のコード スニペットは、Sql Server Custom Connection Manager のサンプルに含まれています。  
  
 [カスタム接続マネージャーの作成](../../../integration-services/extending-packages-custom-objects/connection-manager/creating-a-custom-connection-manager.md)  
 カスタム接続マネージャー プロジェクト用のクラスの作成方法について説明します。  
  
 [カスタム接続マネージャーのコーディング](../../../integration-services/extending-packages-custom-objects/connection-manager/coding-a-custom-connection-manager.md)  
 基本クラスのメソッドとプロパティのオーバーライドによる、カスタム接続マネージャーの実装方法について説明します。  
  
 [カスタム接続マネージャー用ユーザー インターフェイスの開発](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md)  
 ユーザー インターフェイス クラスと、カスタム接続マネージャーの構成に使用するフォームの実装方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
  
### <a name="information-common-to-all-custom-objects"></a>すべてのカスタム オブジェクトに共通の情報  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で作成可能なカスタム オブジェクトのすべての種類に共通の情報については、次のトピックを参照してください。  
  
 [Integration Services 用のカスタム オブジェクトの開発](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のすべての型のカスタム オブジェクトを実装する基本手順について説明します。  
  
 [カスタム オブジェクトの永続化](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 カスタムの永続性と、それが必要な場合について説明します。  
  
 [カスタム オブジェクトのビルド、配置、デバッグ](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 カスタム オブジェクトをビルド、署名、配置、およびデバッグする方法について説明します。  
  
### <a name="information-about-other-custom-objects"></a>その他のカスタム オブジェクトに関する情報  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で作成可能なその他の種類のカスタム オブジェクトについては、次のトピックを参照してください。  
  
 [カスタム タスクの開発](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 カスタム タスクのプログラム方法について説明します。  
  
 [カスタム ログ プロバイダーの開発](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 カスタム ログ プロバイダーのプログラム方法について説明します。  
  
 [カスタム ForEach 列挙子の開発](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 カスタム列挙子のプログラム方法について説明します。  
  
 [カスタム データ フロー コンポーネントの開発](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 カスタム データ フローの変換元、変換、変換先のプログラム方法について説明します。  
  
