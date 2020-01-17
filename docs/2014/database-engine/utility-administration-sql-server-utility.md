---
title: ユーティリティの管理 (SQL Server ユーティリティ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 3e5a00c3-8905-40f0-9ddc-d924df9c2f0d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6da38b25ca23302c8b683a5c9b54ed2b6f88f6b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773754"
---
# <a name="utility-administration-sql-server-utility"></a>ユーティリティの管理 (SQL Server ユーティリティ)
  ユーティリティの管理の各タブでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティのポリシー設定、セキュリティ設定、およびデータ ウェアハウス設定を管理できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティの概念の詳細については、「 [SQL Server ユーティリティの機能とタスク](../relational-databases/manage/sql-server-utility-features-and-tasks.md)」を参照してください。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 [ポリシー] タブ - このタブでは、グローバル監視ポリシーを表示または指定できます。  
  
 [グローバル データ層アプリケーション監視ポリシーを設定する] : このオプションの値一覧を表示するには、ポリシー名の横にある矢印をクリックするか、ポリシーのタイトルをクリックします。  
 [アプリケーションがプロセッサの能力を使い果たすタイミング] : このポリシー説明の右側にあるコントロールを使用してポリシーを変更し、 **[適用]** をクリックします。 また、画面の下部にあるボタンを使用して、既定値を復元したり変更を破棄したりすることもできます。  
  
-   プロセッサ使用率の既定の最大値は 70% です。  
  
-   プロセッサ使用率の既定の最小値は 0% です。  
  
 [アプリケーションがファイル領域を使い果たすタイミング] : このポリシー説明の右側にあるコントロールを使用して、データ ファイルまたはログ ファイルの領域使用率ポリシーを変更し、 **[適用]** をクリックします。 また、画面の下部にあるボタンを使用して、既定値を復元したり変更を破棄したりすることもできます。  
  
-   ファイル領域使用率の既定の最大値は 70% です。  
  
-   ファイル領域使用率の既定の最小値は 0% です。  
  
 [グローバル SQL Server マネージド インスタンス アプリケーション監視ポリシーを設定する] : このオプションの値一覧を表示するには、ポリシー名の横にある矢印をクリックするか、ポリシーのタイトルをクリックします。  
 [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスがプロセッサの能力を使い果たすタイミング] : このポリシー説明の右側にあるコントロールを使用してポリシーを変更し、 **[適用]** をクリックします。 また、画面の下部にあるボタンを使用して、既定値を復元したり変更を破棄したりすることもできます。  
  
-   インスタンスのプロセッサ使用率の既定の最大値は 70% です。  
  
-   インスタンスのプロセッサ使用率の既定の最小値は 0% です。  
  
 [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンピューターのマネージド インスタンスがプロセッサの能力を使い果たすタイミング] : このポリシー説明の右側にあるコントロールを使用してポリシーを変更し、 **[適用]** をクリックします。 また、画面の下部にあるボタンを使用して、既定値を復元したり変更を破棄したりすることもできます。  
  
-   コンピューターのプロセッサ使用率の既定の最大値は 70% です。  
  
-   コンピューターのプロセッサ使用率の既定の最小値は 0% です。  
  
 [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスがファイル領域を使い果たすタイミング] : このポリシー説明の右側にあるコントロールを使用して、データ ファイルまたはログ ファイルの領域使用率ポリシーを変更し、 **[適用]** をクリックします。 また、画面の下部にあるボタンを使用して、既定値を復元したり変更を破棄したりすることもできます。  
  
-   ファイル領域使用率の既定の最大値は 70% です。  
  
-   ファイル領域使用率の既定の最小値は 0% です。  
  
 [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンピューターのマネージド インスタンスが記憶域ボリュームの領域を使い果たすタイミング] : このポリシー説明の右側にあるコントロールを使用してポリシーを変更し、 **[適用]** をクリックします。 また、画面の下部にあるボタンを使用して、既定値を復元したり変更を破棄したりすることもできます。  
  
-   コンピューターのボリューム領域使用率の既定の最大値は 70% です。  
  
-   コンピューターのボリューム領域使用率の既定の最小値は 0% です。  
  
 [変動の激しいリソースによって生じるポリシー違反ノイズの軽減] : この機能のコントロールを表示するには、画面の右側にある下向き矢印をクリックします。  
 詳細については、「[CPU 使用率のポリシーにおけるノイズの軽減 &#40;SQL Server ユーティリティ&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)」を参照してください。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 [セキュリティ] タブ - UCP の管理または読み取りの権限とログイン名が表示されます。  
  
 [Utility Reader ロールに追加される UCP のログインを選択する]  
 Utility Reader 特権があるユーザー アカウントでは、以下のことが可能です。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティに接続する  
  
-   SSMS のユーティリティ エクスプローラーで、すべてのビューポイントを表示する  
  
-   SSMS のユーティリティ エクスプローラーで、[ユーティリティの管理] ノードの設定を表示する  
  
 ユーティリティ管理者は、SQL Server のインスタンスを SQL Server ユーティリティに登録したり、SQL Server のインスタンスを SQL Server ユーティリティから削除したりできるほか、マネージド インスタンスのポリシーの変更や UCP の管理設定の変更が可能です。  
  
 ユーティリティ管理者になるには、SQL Server のインスタンスに対する sysadmin 特権が必要です。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] UCP のユーザー アカウントを追加または変更するには、SSMS のオブジェクト エクスプローラーを使用して、SQL Server の UCP インスタンスのサーバー ログインにユーザーを追加します。 詳細については、「[sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)」を参照してください。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 [データ ウェアハウス] タブ - ユーティリティ管理データ ウェアハウスの構成の詳細が表示されます。  
  
 [データ保有期間]  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンス用に収集された使用率情報のデータ保有期間を指定します。 既定の期間は 1 年です。 最小値は 1 か月です。 指定可能な最長期間は 2 年です。  
  
 [ユーティリティ データ ウェアハウスの構成情報]  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のこのリリースで構成できない構成設定は次のとおりです。  
  
-   UMDW 名:Sysutility_mdw _\<GUID > _DATA します。  
  
-   コレクション セットのアップロード頻度。15 分ごとにします。  
  
 UMDW ディレクトリは構成できます。\<システム ドライブ >: \Program Files\Microsoft SQL server \mssql10_50. < UCP_Name > \MSSQL\Data\\ここで、\<システム ドライブ > は、通常は、C:\ドライブ。 ログ ファイル UMDW_\<GUID>_LOG は同じディレクトリにあります。  
  
> [!NOTE]  
>  UMDW (sysutility_mdw) ファイルの場所を変更するには、デタッチとアタッチを使用する方法と ALTER DATABASE を使用する方法があります。 ALTER DATABASE の使用をお勧めします。 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)」を参照してください。  
  
 [追加設定なしの既定値に戻す]  
 このタブの設定を既定値にリセットするには、 **[既定値に戻す]** ボタンをクリックし、 **[適用]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [ユーティリティ ダッシュ ボード&#40;SQL Server ユーティリティ&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [配置済みのデータ層アプリケーションの詳細 &#40;SQL Server ユーティリティ&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [マネージド インスタンスの詳細 &#40;SQL Server ユーティリティ&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [SQL Server ユーティリティでの SQL Server のインスタンスの監視](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
  
