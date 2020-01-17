---
title: ユーティリティ ダッシュ ボード (SQL Server ユーティリティ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 999eb741-4a60-43f6-ab37-2df7dce845c1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f0eb497499eafe16756becfb9607b925add08e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773814"
---
# <a name="utility-dashboard-sql-server-utility"></a>ユーティリティ ダッシュボード (SQL Server ユーティリティ)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティ ダッシュボードにデータを表示するには、ユーティリティ エクスプローラーのツリーで最上位ノード "Utility<UCP 名>\\(ComputerName\UCP)" を選択します。 ダッシュボードには、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のすべてのマネージド インスタンス、および [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティのすべてのデータ層アプリケーションに関する概要データと詳細データが表示されます。 ダッシュボードのデータを更新するには、ユーティリティ エクスプローラーのツリーで最上位ノードを右クリックし、 **[更新]** をクリックします。  
  
 ユーティリティ コントロール ポイントの作成方法については、「 [SQL Server ユーティリティ コントロール ポイントの作成 &#40;SQL Server ユーティリティ&#41;](../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)をクリックします。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティに追加する方法については、「[Enroll an Instance of SQL Server &#40;SQL Server Utility&#41; (SQL Server のインスタンスの登録 &#40;SQL Server ユーティリティ&#41;)](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)」を参照してください。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 マネージド インスタンスの正常性  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスの正常性状態は、ユーティリティ エクスプローラーのコンテンツ ペインの左側に表示されます。  
  
 マネージド インスタンスの正常性パラメーターは次のとおりです。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]インスタンスの CPU 使用率  
  
-   データベース ファイルの使用率  
  
-   記憶域ボリュームの領域使用率  
  
-   コンピューターの CPU 使用率  
  
-   各パラメーターの状態は、次の 3 つのカテゴリに分類されます。  
  
-   適正使用 - リソース使用率のポリシーに違反していない、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスの数  
  
-   過小使用 - リソースの過小使用ポリシーに違反しているマネージド リソースの数  
  
-   過大使用 - リソースの過大使用ポリシーに違反しているマネージド リソースの数  
  
-   利用可能データなし - SQL Server のマネージド インスタンスによって利用できるデータがありません。SQL Server のインスタンスが登録された直後であるため最初のデータ収集操作が完了していないか、またはデータの収集と UCP へのアップロードの際に SQL Server のマネージド インスタンスで問題が発生したことが原因です。  
  
 各正常性パラメーターの詳細な状態は、スライド式インジケーターに一覧表示されます。 スライド式インジケーターの右側にある部分は、何個のマネージド インスタンスが各状態カテゴリに存在するかを示します。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスまたはデータ層アプリケーションについてフィルターを適用したビューを作成するには、ユーティリティ ダッシュボードのスライド式インジケーターの横にある使用率カテゴリのリンクをクリックします。 たとえば、 **ユーティリティ エクスプローラーのコンテンツ** ペインで **[使用率が高いインスタンス CPU]** をクリックすると、SSMS では、現在のポリシー設定に基づいてフィルターが適用され、CPU 使用率の高い [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスについてのリスト ビューが作成されます。  
  
 使用率カテゴリのリンクをクリックすると、ユーティリティ エクスプローラー ナビゲーション ウィンドウの対応するノードに **(フィルター選択)** と表示されます。つまり、 **[マネージド インスタンス]** のラベルが **[マネージド インスタンス (フィルター選択)]** になります。 フィルターの設定を表示するには、ナビゲーション ウィンドウでノードを右クリックし、 **[フィルター]** 、 **[フィルターの設定]** の順にクリックします。 フィルターの設定をクリアするには、ナビゲーション ウィンドウでノードを右クリックし、 **[フィルター]** 、 **[フィルターの削除]** の順にクリックします。  
  
 個々の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスの正常性状態の表示と、ポリシー構成設定の表示または変更の詳細については、「[マネージド インスタンスの詳細 &#40;SQL Server ユーティリティ &#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)」を参照してください。  
  
 ユーティリティの概要  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスの数と、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティによって管理されるデータ層アプリケーションの数を表示します。  
  
 データ層アプリケーションの正常性  
 データ層アプリケーションの正常性状態は、ユーティリティ エクスプローラーのコンテンツ ペインの右側に表示されます。  
  
 データ層アプリケーションの正常性パラメーターは次のとおりです。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]インスタンスの CPU 使用率  
  
-   データベース ファイルの使用率  
  
-   記憶域ボリュームの領域使用率  
  
-   コンピューターの CPU 使用率  
  
 各パラメーターの状態は、次の 3 つのカテゴリに分類されます。  
  
-   適正使用 - リソース使用率のポリシーに違反していないデータ層アプリケーションの数  
  
-   過大使用 - リソースの過大使用ポリシーに違反しているデータ層アプリケーションの数  
  
-   過小使用 - リソースの過小使用ポリシーに違反しているデータ層アプリケーションの数  
  
-   利用可能データなし - データ層アプリケーションによって利用できるデータがありません。データ層アプリケーションを含む SQL Server のマネージド インスタンスがデータを報告していないことが原因です。  
  
 各正常性パラメーターの詳細な状態は、スライド式インジケーターに一覧表示されます。 スライド式インジケーターの右側にある部分は、何個のデータ層アプリケーションが各状態カテゴリに存在するかを示します。 個々のデータ層アプリケーションの正常性状態の表示と、ポリシー構成設定の表示または変更の詳細については、「[配置済みのデータ層アプリケーションの詳細 &#40;SQL Server ユーティリティ&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)」を参照してください。  
  
 ユーティリティの記憶域使用率の履歴  
 使用率の履歴は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティ ダッシュボードの下部にある時間グラフに表示されます。 時間データとして、UCP のローカル日時が datetime データ型で表示されることに注意してください。 詳細については、SQL Server オンライン ブックの「 [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 」を参照してください。 ユーティリティ オブジェクト モデルを使用する場合は、SSMS で datetimeoffset データ型が使用されることに注意してください。 詳細については、SQL Server オンライン ブックの「 [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 」を参照してください。  
  
 表示領域の左側にあるオプション ボタンを使用して、グラフ表示の対象期間を変更できます。  
  
 対象期間のオプションは次のとおりです。  
  
-   [1 日] : 15 分間隔で表示されます。  
  
-   [1 週間] : 1 日間隔で表示されます。  
  
-   [1 か月] : 1 週間間隔で表示されます。  
  
-   [1 年] : 1 か月間隔で表示されます。  
  
 レポート間隔を変更すると、データが自動的に更新されます。  
  
 ユーティリティの記憶域使用率  
 ダッシュボードの右下には、記憶域の使用率を示す円グラフが表示されます。このグラフでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンスを含むコンピューターにあるボリュームについて、使用済み領域と空き領域の比率を確認できます。 ここに表示されるデータは、15 分ごとに更新されます。  
  
## <a name="see-also"></a>参照  
 [ユーティリティ エクスプローラーを使用した SQL Server ユーティリティの管理](../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [SQL Server のインスタンスの登録&#40;SQL Server ユーティリティ&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)   
 [リソース正常性ポリシーの定義の変更 &#40;SQL Server Utility&#41;](../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)  
  
  
