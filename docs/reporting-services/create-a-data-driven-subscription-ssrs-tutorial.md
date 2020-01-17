---
title: データ ドリブン サブスクリプションの作成 (SSRS チュートリアル) | Microsoft Docs
ms.date: 05/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: baff01bd8bc02af409a37c5cc1ce193e69663387
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194837"
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>データ ドリブン サブスクリプションの作成 (SSRS チュートリアル)
この [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] チュートリアルでは、データ ドリブン サブスクリプションを作成し、フィルター処理されたレポート出力を生成してファイル共有に保存する簡単な例の手順を示すことで、データ ドリブン サブスクリプションの概念を説明します。 
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のデータ ドリブン サブスクリプションを使用すると、動的なサブスクライバー データに基づいてレポートの配信をカスタマイズおよび自動化できます。 データ ドリブン サブスクリプションには次のような用途があります。  
  
-   配信するたびに宛先メンバーの構成が変更される多人数受信者プールへのレポート配信。 たとえば、月刊レポートを現在の全顧客にメールで送付する場合など。  
  
-   定義済みの条件に基づく特定の受信者グループへのレポート配信。 たとえば、社内のすべての営業責任者に販売実績レポートを送信する場合など。
+ .xlsx や .pdf などのさまざまな形式のレポートの生成の自動化。  
  
## <a name="what-you-will-learn"></a>学習する内容  
このチュートリアルは、次の 3 つのレッスンで構成されています。  

| レッスン | コメント |
| ------ | -------- |
| [レッスン 1: サンプル サブスクライバー データベースを作成する](../reporting-services/lesson-1-creating-a-sample-subscriber-database.md) | このレッスンでは、サブスクライバー情報を格納するテーブル ローカル [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースを作成します。 フィルター処理および出力ファイル形式に使用する情報の注文番号。 |
| [レッスン 2: レポート データ ソースのプロパティを構成する](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md) | このレッスンでは、指定したスケジュールでレポートを自動実行できるようにレポート データ ソースを構成します。 自動処理では保存された資格情報が必要です。 また、レポートのデータセットを変更して、サブスクライバーのデータが提供するパラメーターを含めます。 このパラメーターは、注文番号に基づくレポート データのフィルター処理に使用されます。 |
| [レッスン 3: データ ドリブン サブスクリプションを定義する](../reporting-services/lesson-3-defining-a-data-driven-subscription.md) | このレッスンでは、データ ドリブン サブスクリプションを作成します。 ここでは、データ ドリブン サブスクリプション ウィザードを 1 ページずつ順に実行します。 |

次の図は、チュートリアルの基本的なワークフローです。

| 手順    | [説明] |
| --------|------------ |
| (1)     | サブスクリプションの構成には、ソース レポート、スケジュール、およびサブスクライバー データベースへのフィールド マッピングが記述されています。 |
| (2)     | OrderInfo テーブルには、フィルター処理に使用する 4 つの注文番号が含まれています (ファイルごとに 1 つ)。 テーブルには、生成されるレポートのファイル形式も含まれています。 |
| (3)     | Adventureworks データベースからの情報がフィルタリングされてレポートで返されます。 |
| (4)     | Orderinfo テーブルで指定されたファイル形式でレポートが作成されます。 |



   ![ssrs_tutorial_datadriven_flow](../reporting-services/media/ssrs-tutorial-datadriven-flow.png) 
  
## <a name="requirements"></a>必要条件  
通常、データ ドリブン サブスクリプションはレポート サーバー管理者が作成し、保守します。 データ ドリブン サブスクリプションを作成するには、クエリ作成の専門知識、サブスクライバー データを持つデータ ソースに関する知識、およびレポート サーバーへの高度なアクセス権が必要です。  
  
このチュートリアルでは、チュートリアル「 *基本的なテーブル レポートの作成 (SSRS チュートリアル)* 」で作成した [基本的なテーブル レポートの作成 (SSRS チュートリアル)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) レポートと、サンプル データベース **AdventureWorks2014**のデータを使用します。  
  
このチュートリアルを使用するには、コンピューターに次のコンポーネントがインストールされている必要があります。  
  
-   データ ドリブン サブスクリプションをサポートするエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 詳しくは、[SQL Server 2017 のエディションと機能](../sql-server/editions-and-components-of-sql-server-2017.md)に関するページをご覧ください。  
  
-   レポート サーバー (ネイティブ モードで実行)。 このチュートリアルで説明するユーザー インターフェイスは、ネイティブ モードのレポート サーバーに基づいています。 サブスクリプションは SharePoint モードのレポート サーバーでサポートされていますが、ユーザー インターフェイスはこのチュートリアルで説明されているものとは異なります。  
  
-   SQL Server エージェント サービス (実行された状態)。  
  
-   パラメーターを含むレポート。 このチュートリアルでは、チュートリアル「 `Sales Orders` 基本的なテーブル レポートの作成 (SSRS チュートリアル) [基本的なテーブル レポートの作成 (SSRS チュートリアル)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)のデータを使用します。  
  
-   サンプル レポートにデータを提供する **AdventureWorks2014** サンプル データベース。  
  
-   サンプル レポートでのすべてのサブスクリプションを管理タスクを含む [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ロールの割り当て。 データ ドリブン サブスクリプションを定義するには、この作業が必要です。 コンピューター管理者の場合は、ローカル管理者用の既定のロール割り当てで、データ ドリブン サブスクリプションの作成に必要な権限が与えられます。 詳細については、「 [ネイティブ モードのレポート サーバーに対する権限の許可](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)」をご覧ください。  
  
-   書き込み権限のある共有フォルダー。 共有フォルダーはネットワーク接続経由でアクセス可能になっている必要があります。  
  
**このチュートリアルの推定所要時間:** 30 分。 基本的なレポートのチュートリアルを完了していない場合は追加で 30 分かかります。  
  
## <a name="see-also"></a>参照  
[Data-Driven Subscriptions](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[基本的なテーブル レポートの作成 (SSRS チュートリアル)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)
 

