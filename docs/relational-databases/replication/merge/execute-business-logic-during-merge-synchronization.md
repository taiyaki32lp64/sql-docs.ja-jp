---
title: マージ同期中のビジネス ロジック
description: マージ レプリケーションの同期に使用するビジネス ロジックのマネージド アセンブリ コードを記述する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom error resolution [SQL Server replication]
- custom change handling [SQL Server replication]
- errors [SQL Server replication], business logic handlers
- merge replication business logic handlers [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
- business logic handlers [SQL Server replication]
ms.assetid: 9d4da2ef-c17f-4a31-a1f6-5c3b7ca85f71
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a3f1e7f07b95c71eeddc65fed6db3f10cc31ee32
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321490"
---
# <a name="execute-business-logic-during-merge-synchronization"></a>マージ同期中のビジネス ロジックの実行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ビジネス ロジック ハンドラー フレームワークを使用すると、マネージド コードのアセンブリを記述して、マージ同期処理中に呼び出すことができます。 このアセンブリには、データの変更、競合、およびエラーなど、同期中に発生するさまざまな状況に対処するためのビジネス ロジックを記述できます。 ビジネス ロジック ハンドラー フレームワークには単純なプログラミング モデルが用意されており、マージ処理によってアセンブリに提供されるデータは ADO.NET データセットの形式になっています。このため、専用インターフェイスについての知識ではなく ADO.NET についての知識を活用できます。 ビジネス ロジック ハンドラーのプログラミングの詳細については、以下のトピックを参照してください。  
  
-   アプリケーション プログラミング インターフェイス (API) リファレンス : <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>  
  
-   ビジネス ロジック ハンドラーの実装方法についての説明: [マージ アーティクルのビジネス ロジック ハンドラーの実装](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
## <a name="uses-for-business-logic-handlers"></a>ビジネス ロジック ハンドラーの用途  
 マージ同期処理では、ビジネス ロジック ハンドラーを呼び出して、以下の操作を実行できます。  
  
-   カスタム変更処理  
  
-   カスタム競合解決  
  
-   カスタム エラー解決  
  
> [!NOTE]  
>  指定するビジネス ロジック ハンドラーは、同期されるすべての行に対して実行されます。 その他のアプリケーションまたはネットワーク サービスに対する複雑なロジックおよび呼び出しは、パフォーマンスに影響を与える可能性があります。  
  
### <a name="custom-change-handling"></a>カスタム変更処理  
 ビジネス ロジック ハンドラーは、競合していないデータの変更処理中に呼び出すことができ、次の 3 つの操作のいずれかを実行できます。  
  
-   データの拒否  
  
     特定のサブスクライバーからの変更または特定のサブスクライバーへの変更を反映したくないアプリケーションに役立ちます。 たとえば、管理者は、サブスクライバーのパーティション内に属さない挿入をフィルター処理によって拒否したり、場合によってはサブスクライバーで実行された削除を拒否することができます。 別の例としては、在庫が不足している場合に、サブスクライバーで入力された注文をアプリケーションが拒否できます。  
  
-   データの受け入れ  
  
     これは、パブリッシャーまたはサブスクライバーで行われたデータの変更を反映する前に確認を行う必要があるアプリケーションに役立ちます。 たとえば、中間層アプリケーションでは、フィールドから送られてきた新しい注文を検証し、中間層で調達ワークフロー プロセスと統合することができます。  
  
-   カスタム データの適用  
  
     これは、特定のデータの値または操作をオーバーライドする必要があるアプリケーションに役立ちます。 たとえば、アプリケーションでは、行の削除を、その行の **status** 列を "削除" の値に設定するという特殊な更新方法に変更して、その削除を実行するクライアントの ID を追跡することができます。 これは、監査やワークフローにも役立ちます。  
  
### <a name="custom-conflict-resolution"></a>カスタム競合解決  
 マージ レプリケーションには、競合の検出機能と解決機能が用意されており、既定の解決方法を受け入れるか、競合に対するカスタム解決方法を選択することができます。 詳細については、「 [マージ レプリケーションの競合検出および解決の詳細](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。 ビジネス ロジック ハンドラーは、競合しているデータの変更処理中に呼び出すことができ、次の 2 つの操作のいずれかを実行できます。  
  
-   既定の解決の受け入れ  
  
     これは、競合の確認や追加アクションの実行、場合によってはカスタム競合ログ メッセージのログ記録などを行う必要があるアプリケーションに役立ちます。  
  
-   カスタム解決の実行  
  
     これは、ビジネス ロジックに固有のデータ値を選択し、このカスタム データセットを使用した同期処理を提供する必要があるアプリケーションに役立ちます。 たとえば、アプリケーションで、パブリッシャーとサブスクライバーのデータセットの値を組み合わせることにより、優先される行の新しいバージョンを提供することができます。  
  
### <a name="custom-error-resolution"></a>カスタム エラー解決  
 カスタム ロジックは、結果的にエラーが発生する変更の反映中に呼び出すことができます。 このロジックは、次の 2 つの操作のいずれかを実行できます。  
  
-   既定のエラー解決の受け入れ  
  
     これは、エラーの確認や追加アクションの実行、場合によってはカスタム エラー ログ メッセージのログ記録などを行う必要があるアプリケーションに役立ちます。  
  
-   カスタム エラー解決の受け入れ  
  
     これは、ビジネス ロジックに固有のデータ値を選択し、このカスタム データセットを使用した同期処理を提供する必要があるアプリケーションに役立ちます。 たとえば、レプリケーション処理で重複キー違反が発生した場合、ビジネス ロジック ハンドラーによって、キーの競合がなくなる新しいバージョンのデータ変更を提供することができます。 パブリッシャーとサブスクライバーで行われた変更は、データベースで保持することができます。レプリケーション プロセスは、失敗した挿入に対して削除による補正を行う必要はありません。  
  
## <a name="deployment-scenarios-for-business-logic-handlers"></a>ビジネス ロジック ハンドラーの配置シナリオ  
 ビジネス ロジック ハンドラーは、以下の場所に配置できます。  
  
-   ディストリビューター。 ディストリビューターでビジネス ロジックが実行されるように、プッシュ サブスクリプションを使用します。  
  
-   サブスクライバー。 サブスクライバーでビジネス ロジックが実行されるように、プル サブスクリプションを使用します。  
  
-   インターネット インフォメーション サービス (IIS) サーバー (Web 同期を使用する場合)。 Web 同期を使用して同期されたプル サブスクリプションを使用します。ビジネス ロジック ハンドラーが IIS サーバーで実行されます。  
  
## <a name="see-also"></a>参照  
 [マージ レプリケーション](../../../relational-databases/replication/merge/merge-replication.md)   
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)   
 [データの同期](../../../relational-databases/replication/synchronize-data.md)   
 [マージ レプリケーションの Web 同期](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
