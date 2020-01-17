---
title: DQS 管理
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- dqs administration
- administration
- dqs,adminstration
ms.assetid: 9940ef5d-f6f6-4dec-9414-1077a4d7f12b
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 065a8869eff0e88cee5bf0bb110a948f709743d7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251664"
---
# <a name="dqs-administration"></a>DQS 管理

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) では、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]で実行されるさまざまな DQS アクティビティを管理し、DQS アクティビティに関連するサーバー レベルのプロパティを構成し、参照データ サービスの設定を構成し、DQS ログの設定を構成できます。 これらの作業は、 **の** 管理 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]機能を使用して行います。 DQS でのセキュリティ アクセス (ロール) に基づいて、特定の管理機能へのアクセスが許可/禁止されます。  
  
 これらの管理機能とは別に、このトピックでは、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]を使用して実行しない管理アクティビティである DQS データベースのバックアップと復元についても説明します。  
  
 
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] での管理機能には次のような利点があります。  
  
-   データ スチュワードは、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] から [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]でのさまざまな DQS アクティビティを監視できます。  
  
-   DQS 管理者は、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] から [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]での DQS アクティビティを監視でき、必要に応じて、実行中のアクティビティを *終了* させたり、アクティビティ内で実行中のプロセスを *停止* させたりできます。  
  
-   Azure Marketplace との接続の設定や、ダイレクトサードパーティ参照データサービスプロバイダーの管理など、参照データサービスの設定を構成します。  
  
-   クレンジングおよび照合アクティビティのしきい値を構成します。  
  
-   
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]での通知を有効または無効にします。  
  
-   イベントの重大度レベルに基づくログを構成します。  
  
##  <a name="AdminUsingClent"></a>Data Quality Client を使用した管理アクティビティ  
 以下のアクティビティは、 **の** 管理 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]機能を使用して行います。  
  
### <a name="activity-monitoring"></a>[アクティビティ監視]  
 
  **の** [アクティビティ監視] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 画面には、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]で実行されている各アクティビティについての詳細な情報が表示されます。 この画面は、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] アプリケーションが接続されている [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 上で実行されているすべてのアクティビティに関する高レベルの監視を実行するために主にデータ スチュワードによって使用されます。 この画面では、システム レベルの監視は提供されません。 また、この画面を使用すると、DQS 管理者は、必要に応じて、実行中のアクティビティを終了したり、アクティビティ内で実行中のプロセスを停止したりして、アクティビティまたはアクティビティ内のプロセスを制御できます。 ナレッジの検出、ドメインの管理、照合ポリシー、クレンジング、照合、および SQL Server Integration Services (SSIS) ベースのクレンジングに関するデータが表示されます。  
  
### <a name="configuration"></a>構成  
 
  **の** [構成] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 画面では、DQS 管理者は次のことを行うことができます。  
  
-   **参照データ**: 参照データサービスプロバイダーを構成する: Azure Marketplace またはダイレクト参照データサービスプロバイダー。 参照データ サービス プロバイダーを設定した後は、ナレッジ ベースでのドメイン管理アクティビティの間にドメイン/複合ドメインと参照データをマップし、データ品質プロジェクトでのクレンジング アクティビティに同じナレッジ ベースを使用できます。 また、Azure Marketplace を使用するためにインターネットに接続するためのプロキシ設定を指定することもできます。  
  
-   **全般設定**: データクレンジングとデータ照合のしきい値を指定し、で[!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]プロファイリングの通知を有効にするかどうかを指定します。 これらのしきい値は、データ品質プロジェクトでのコンピューター支援型のクレンジングおよび照合アクティビティの間に、DQS によって使用されます。  
  
-   **ログの設定**: dqs のログファイルには dqs で実行されたアクティビティが記録されます。これは、メンテナンスおよびトラブルシューティングの間に運用上の問題を追跡する場合に役立ちます。 さまざまな DQS 機能 (ドメイン管理、ナレッジ検出、クレンジング、照合、参照データ サービス) および DQS モジュールに関してログに記録するメッセージを、イベントの重大度レベルに基づいてフィルターできます。  
  
> [!NOTE]  
>  
  **[構成]** 画面は、DQS_MAIN データベースの dqs_administrator ロールを持つユーザーのみ使用できます。  
  
##  <a name="AdminOutsideClient"></a>Data Quality Client の外部の管理アクティビティ  
 アクティビティは Data Quality Client の外部で実行されます。  
  
-   **Dqs データベースのバックアップと復元**: dqs データベースのバックアップと復元は、SQL Server データベースのバックアップと復元と同じですが、dqs に固有の考慮事項がいくつかあります。  
  
-   **Dqs データベース**のデタッチとアタッチ: dqs データベースをデタッチおよびアタッチする手順は、SQL Server データベースのデタッチとアタッチと同じですが、dqs に固有の考慮事項がいくつかあります。  
  
 詳細については、「 [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|DQS のアクティビティを監視する方法について説明します。|[DQS アクティビティの監視](../data-quality-services/monitor-dqs-activities.md)|  
|DQS で参照データの設定を構成する方法について説明します。|[参照データを使用する DQS の構成](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|クレンジングおよび照合アクティビティのしきい値を構成する方法について説明します。|[クレンジングと照合のしきい値の構成](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|DQS で通知を有効または無効にする方法について説明します。|[DQS のプロファイル通知の有効化または無効化](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
|イベントの重大度レベルに基づいて DQS のログを構成する方法について説明します。|[DQS ログ ファイルの重大度レベルの構成](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|DQS ログの詳細設定を構成する方法について説明します。|[DQS ログ ファイルの詳細設定の構成](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
|DQS データベースのバックアップと復元の方法について説明します。|[DQS データベースのバックアップと復元](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|DQS データベースをデタッチおよびアタッチする方法について説明します。|[DQS データベースのデタッチとアタッチ](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>参照  
 [DQS での Data Services の参照](../data-quality-services/reference-data-services-in-dqs.md)   
 [DQS ログファイルの管理](../data-quality-services/manage-dqs-log-files.md)   
 [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md)  
  
  
