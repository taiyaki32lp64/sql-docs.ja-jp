---
title: データ ドリブン サブスクリプションの作成 (SSRS チュートリアル) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b905b7127d10be80d9c30ec7c594fbaedc7d9c00
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109689"
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>データ ドリブン サブスクリプションの作成 (SSRS チュートリアル)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] が提供するデータ ドリブン サブスクリプションにより、動的なサブスクライバー データに基づいてレポートの配信をカスタマイズできます。 データ ドリブン サブスクリプションには次のような用途があります。  
  
-   配信するたびに宛先メンバーの構成が変更される多人数受信者プールへのレポート配信。 たとえば、月刊レポートを現在の全顧客に配信する場合など。  
  
-   定義済みの条件に基づく特定の受信者グループへのレポート配信。 たとえば、社内の上位 10 名の営業責任者に販売実績レポートを送信する場合など。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルでは、簡単な例で概念を確認しながら、データ ドリブン サブスクリプションの使用方法を学習します。  
  
 このチュートリアルは、次の 3 つのレッスンで構成されています。  
  
 [レッスン 1:サンプル サブスクライバー データベースの作成](lesson-1-creating-a-sample-subscriber-database.md)  
 このレッスンでは、サブスクライバー情報を格納するローカル [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースを作成する方法を学習します。  
  
 [レッスン 2:レポート データ ソースのプロパティの変更](lesson-2-modifying-the-report-data-source-properties.md)」を参照してください  
 このレッスンでは、レポート データ ソースのプロパティを変更し、レポートを自動実行できるようにする方法を学習します。 自動処理では保存された資格情報が必要です。 また、レポートのデータセットを変更して、サブスクライバーのデータが提供するパラメーターを含めます。  
  
 [レッスン 3:データ ドリブン サブスクリプションを定義します。](lesson-3-defining-a-data-driven-subscription.md)  
 このレッスンでは、データ ドリブン サブスクリプションを定義する方法を学習します。 ここでは、データ ドリブン サブスクリプション ウィザードを 1 ページずつ順に実行します。  
  
## <a name="requirements"></a>必要条件  
 通常、データ ドリブン サブスクリプションはレポート サーバー管理者が作成し、保守します。 データ ドリブン サブスクリプションを作成するには、クエリ作成の専門知識、サブスクライバー データを持つデータ ソースに関する知識、およびレポート サーバーへの高度なアクセス権が必要です。  
  
 チュートリアルでは、このチュートリアルで作成したレポートを使用します[基本的な表レポートの作成&#40;SSRS チュートリアル&#41;](create-a-basic-table-report-ssrs-tutorial.md)とからのデータ。 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]  
  
 このチュートリアルを使用するには、システムに以下のコンポーネントがインストールされている必要があります。  
  
-   データ ドリブン サブスクリプションをサポートするエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 詳細については、次を参照してください。[エディションと SQL Server 2014 のコンポーネントの](../sql-server/editions-and-components-of-sql-server-2016.md)します。  
  
-   レポート サーバー (ネイティブ モードで実行)。 このチュートリアルで説明するユーザー インターフェイスは、ネイティブ モードのレポート サーバーに基づいています。 サブスクリプションは SharePoint モードのレポート サーバーでサポートされていますが、ユーザー インターフェイスはこのチュートリアルで説明されているものとは異なります。  
  
-   SQL Server エージェント サービス (実行された状態)。  
  
-   パラメーターを含むレポート。 このチュートリアルでは、チュートリアル「 `Sales Orders` 基本的なテーブル レポートの作成 (SSRS チュートリアル) [基本的なテーブル レポートの作成 (SSRS チュートリアル)](create-a-basic-table-report-ssrs-tutorial.md)のデータを使用します。  
  
-   サンプル レポートにデータを提供する [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] サンプル データベース。  
  
-   サンプル レポートで、すべてのサブスクリプション タスクを管理するためのロールの割り当て。 データ ドリブン サブスクリプションを定義するには、この作業が必要です。 コンピューター管理者の場合は、ローカル管理者用の既定のロール割り当てで、データ ドリブン サブスクリプションの作成に必要な権限が与えられます。 詳細については、「 [ネイティブ モードのレポート サーバーに対する権限の許可](security/granting-permissions-on-a-native-mode-report-server.md)」をご覧ください。  
  
-   書き込み権限のある共有フォルダー。 共有フォルダーはネットワーク接続経由でアクセス可能になっている必要があります。  
  
 **このチュートリアルの推定所要時間:** 30 分。 基本的なレポートのチュートリアルを完了していない場合は追加で 30 分かかります。  
  
## <a name="see-also"></a>参照  
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [基本的なテーブル レポートの作成 (SSRS チュートリアル)](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
