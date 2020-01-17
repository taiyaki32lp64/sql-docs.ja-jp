---
title: データ品質プロジェクト (DQS)
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a43fc9c0-19b6-414a-8661-4c7c55e0c03e
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 22a92035ea26a4341d4f912c3e6b5cdfaef75efa
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251708"
---
# <a name="data-quality-projects-dqs"></a>データ品質プロジェクト (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) のデータ品質プロジェクトは、ナレッジ ベースを使用してソース データの品質を改善する手段になります。 *データ クレンジング* アクティビティおよび *データ照合* アクティビティを実行して、その結果データを SQL Server データベースや .csv ファイルにエクスポートします。 データ品質プロジェクトをクレンジング プロジェクトまたは照合プロジェクトとして作成し、それぞれのアクティビティを実行できます。 データ クレンジングと照合のナレッジは同じナレッジ ベースに組み込むことができるため、クレンジング プロジェクトと照合プロジェクトは同じナレッジ ベースを使用して実行できます。  
  
 データ品質プロジェクトには次の利点があります。  
  
-   DQS ナレッジ ベースのナレッジを使用してソース データのデータ クレンジングを実行できます。  
  
-   ナレッジ ベースの照合ポリシーを使用してソース データのデータ照合を実行できます。  
  
-   クレンジング アクティビティや照合アクティビティの実施をガイドするウィザードが提供されているほか、データを必要により SQL Server データベースや .csv ファイルにエクスポートできます。 データ スチュワードはデータ品質プロジェクトを使用して、コンピューター支援型の、またはインタクラティブなクレンジングやデータ照合手順を実行および制御できます。  
  
##  <a name="Cleansing"></a>データ品質プロジェクト: クレンジングアクティビティ  
 クレンジング データ品質プロジェクトでは、ナレッジ ベースに基づいてソース データのクレンジングを行うことができます。 DQS のデータ クレンジング アクティビティは、2 段階のプロセスから成ります。  
  
1.  
  *コンピューター支援型の* データ クレンジング プロセス。ナレッジ ベース内のナレッジと照らし合わせてソース データを分析し、変更を提示します。 処理後のデータは DQS によって分類 (提案、新規、無効、修正済み、および修正) されたうえでユーザーに表示され、さらに処理が行われます。  
  
2.  
  *インタラクティブな* クレンジング プロセス。データ スチュワードがコンピューター支援型のデータ クレンジング プロセスによって提案されたデータを承認、拒否、または変更します。  
  
 データ品質プロジェクトのクレンジング アクティビティの詳細については、「 [Data Cleansing](../data-quality-services/data-cleansing.md)」を参照してください。  
  
##  <a name="Matching"></a>データ品質プロジェクト: 照合アクティビティ  
 データ品質プロジェクトの照合では、ナレッジ ベース内の照合ポリシーに基づいて照合アクティビティを実行します。完全一致やあいまい一致を特定することによってデータの重複を防ぎ、重複データをユーザーが削除できます。 データをクレンジングしてから照合を実行することをお勧めします。 そのためには、次の操作を実行します。  
  
1.  データ品質プロジェクトを作成し、 **[クレンジング]** アクティビティを選択してソース データのデータ クレンジング アクティビティを完了し、その後 SQL Server データベースのテーブルにエクスポートします。  
  
2.  照合ポリシーを含んだナレッジ ベースを使用して別のデータ品質プロジェクトを作成し、 **[照合]** アクティビティを選択し、手順 1. でクレンジングしたデータをエクスポートしたデータベースとテーブルを **[マップ]** ページで選択します。  
  
3.  クレンジングされたデータに対して照合アクティビティを完了させます。  
  
 データ品質プロジェクトの照合アクティビティの詳細については、「 [Data Matching](../data-quality-services/data-matching.md)」を参照してください。  
  
##  <a name="ProfilingNotification"></a>データプロファイルと通知  
 データ品質プロジェクトでクレンジングおよび照合アクティビティを実行しながら、DQS で処理中のデータに関する統計と情報をリアルタイムに表示できます。 クレンジングおよび照合プロセスの有効性を評価したり、データ クレンジングまたは照合によりデータ品質がどの程度向上したかを計測したりするのに、データ プロファイルが役立ちます。 DQS プロファイルでは、 *完全性* (データがどの程度存在するか) と *正確性* (データがどの程度意図されたとおりに使用できるか) の 2 つのデータ品質ディメンションを提供します。 さらに、データ プロファイル情報に基づいて、データ クレンジングおよびデータ照合操作を向上させるために取ることができるアクションをユーザーに通知します。 データ プロファイルと通知の詳細については、「 [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|データ品質プロジェクトの作成方法について説明します。|[データ品質プロジェクトの作成](../data-quality-services/create-a-data-quality-project.md)|  
|データ品質プロジェクトを開く、ロック解除する、名前を変更する、および削除する方法について説明します。|[データ品質プロジェクトを開く、ロックを解除する、名前を変更する、削除する](open-unlock-rename-and-delete-a-data-quality-project.md)|  
|
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]で Integration Services プロジェクトを開く方法について説明します。|[Data Quality Client で Integration Services プロジェクトを開く](../data-quality-services/open-integration-services-projects-in-data-quality-client.md)|  
  
## <a name="see-also"></a>参照  
 [DQS のナレッジベースとドメイン](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
