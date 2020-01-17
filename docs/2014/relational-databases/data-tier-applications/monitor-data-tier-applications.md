---
title: データ層アプリケーションの監視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- monitoring [SQL Server], data-tier applications
- monitoring server performance [SQL Server], DACs
- data-tier application [SQL Server], monitor
ms.assetid: d2765828-2385-4019-aef2-1de3ab7d1b26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8fe96b7d84a2e363166238c3e840cac383f443dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918130"
---
# <a name="monitor-data-tier-applications"></a>データ層アプリケーションの監視
  データ層アプリケーション (DAC) は、システム ビューおよびシステム テーブルと共に **(SSMS) で** ユーティリティ エクスプローラー **および** オブジェクト エクスプローラー [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] から監視できます。 さらに、DAC に含まれるデータベース内のオブジェクトもすべて、データベースと [!INCLUDE[ssDE](../../includes/ssde-md.md)] の標準的な監視方法を使用して監視できます。  
  
## <a name="before-you-begin"></a>はじめに  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のマネージド インスタンスに DAC を配置した場合、その配置した DAC の情報は、次回ユーティリティ コレクション セットがインスタンスからユーティリティ コントロール ポイントへと送信されるときに SQL Server ユーティリティに組み込まれます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **ユーティリティ エクスプローラー**を使用すると、DAC に関する基本的な正常性の情報を表示できます。  
  
 SSMS **オブジェクト エクスプローラー** では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスが SQL Server ユーティリティに管理されているかどうかにかかわらず、インスタンスに配置された各 DAC についての基本的な構成情報が表示されます。 また、データベースの監視と同じ手順で、配置された DAC に関連付けられたデータベースを監視することもできます。  
  
## <a name="using-the-sql-server-utility"></a>SQL Server ユーティリティの使用  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]**ユーティリティ エクスプローラー**の **[配置済みのデータ層アプリケーション]** 詳細ページにダッシュボードが表示されます。このダッシュボードに[!INCLUDE[ssDE](../../includes/ssde-md.md)]のマネージド インスタンスに配置済みのすべての DAC に関するリソース使用状況が報告されます。 詳細ページの上部ペインには、配置済みの各 DAC が視覚インジケーターと共に表示されます。視覚インジケーターは、CPU およびファイル リソースの使用状況が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのために定義されたポリシーに適合しているかどうかを示します。 リスト ビュー内の任意の DAC を選択すると、さらに詳細な情報がページの下部ペインにあるタブに表示されます。 詳細ページに示される情報の詳細については、「[配置済みのデータ層アプリケーションの詳細 &#40;SQL Server ユーティリティ&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)」を参照してください。  
  
 **[配置済みのデータ層アプリケーション]** の詳細ページを使用すると、ハードウェア リソースを十分に活用していない DAC や、ハードウェア リソースに負荷を生じている DAC を迅速に特定でき、問題に対処するための計画を立てることができます。 現在のハードウェア リソースを十分に活用していない DAC が複数ある場合には、1 台のサーバーに統合して、一部のサーバーを別の用途のために解放することもできます。 現在のサーバー上のリソースに負荷を生じている DAC がある場合は、その DAC を規模の大きいサーバーに移動することも、現在のサーバーにリソースを追加することもできます。  
  
 リソース使用率の制限の最小値と最大値は、アプリケーション監視ポリシーによって定義されます。このポリシーは、 **[ユーティリティ管理]** 詳細ページで定義されます。 データベース管理者は、所属する組織で規定されている制限値に適合するようポリシーを調整できます。 たとえば、ある企業では DAC の最大 CPU 使用率を 75% に設定し、別の企業では 80% に設定する場合もあります。 アプリケーション監視ポリシーの設定の詳細については、「[ユーティリティの管理 &#40;SQL Server ユーティリティ&#41;](../../database-engine/utility-administration-sql-server-utility.md)」を参照してください。  
  
 **[配置済みのデータ層アプリケーション]** 詳細ページを表示するには  
  
1.  **[表示]** メニューの [ユーティリティ エクスプローラー] をクリックします。  
  
2.  **ユーティリティ エクスプローラー** をユーティリティ コントロール ポイント (UCP) に接続します。  
  
3.  **[表示]** メニューの [ユーティリティ エクスプローラーの詳細] をクリックします。  
  
4.  **ユーティリティ エクスプローラー** で **[配置済みのデータ層アプリケーション]** ノードをクリックします。  
  
 **[配置済みのデータ層アプリケーション]** 詳細ページに表示される情報は、ユーティリティ管理データ ウェアハウスのデータから取得されます。データ ウェアハウスは、既定で 15 分ごとにデータを収集します。 この間隔も **[ユーティリティ管理]** 詳細ページで調整できます。  
  
## <a name="using-object-explorer"></a>オブジェクト エクスプローラーの使用  
 SSMS **オブジェクト エクスプローラー** には、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに配置された各 DAC についての基本的な構成情報が表示されます。 これには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録済みのマネージド インスタンスと、 **ユーティリティ エクスプローラー**では表示できないスタンドアロン インスタンスの両方が含まれます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに配置された DAC の詳細を表示するには  
  
1.  **[表示]** メニューの [オブジェクト エクスプローラー] をクリックします。  
  
2.  [オブジェクト エクスプローラー] ペインから [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
3.  **[表示]** メニューの [オブジェクト エクスプローラーの詳細] をクリックします。  
  
4.  **オブジェクト エクスプローラー** でインスタンスにマップしているサーバー ノードを選択して、 **[管理]** 、[データ層アプリケーション] の順に移動します。  
  
5.  詳細ページの上部ペインにあるリスト ビューに、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに配置された各 DAC が一覧表示されます。 ページ下部にある詳細ペインに情報を表示する DAC を選択します。  
  
 **[データ層アプリケーション]** ノードの右クリック メニューを使用して、新しい DAC を配置したり、既存の DAC を削除することもできます。  
  
## <a name="using-the-dac-system-views-and-tables"></a>DAC のシステム ビューとシステム テーブルの使用  
 msdb.dbo.sysdac_history_internal システム テーブルは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンス上で実行されるすべての DAC 管理アクションの成功または失敗を記録します。 このテーブルには、各アクションの発生時刻とアクションを開始したログインが記録されます。 詳細については、「[sysdac_history_internal &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/data-tier-application-tables-sysdac-history-internal)」を参照してください。  
  
 DAC システム ビューは、基本的なカタログ情報を報告します。 詳細については、「[データ層アプリケーションのビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances)」を参照してください。  
  
## <a name="monitoring-dac-databases"></a>DAC データベースの監視  
 DAC が正常に配置されると、DAC に含まれるデータベースは、他のデータベースと同様に動作します。 データベースに関するパフォーマンス、ログ、イベント、およびリソース使用状況は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の標準的なテクニックとツールを使用して監視できます。  
  
## <a name="see-also"></a>関連項目  
 [[データ層アプリケーション]](data-tier-applications.md)   
 [データ層アプリケーションの配置](deploy-a-data-tier-application.md)  
  
  
