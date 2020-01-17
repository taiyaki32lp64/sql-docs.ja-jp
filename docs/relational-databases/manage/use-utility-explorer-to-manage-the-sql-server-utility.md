---
title: ユーティリティ エクスプローラーを使用した SQL Server ユーティリティの管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 74012c90-b42e-4171-b27a-9c30cf69ff98
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d904d16bb54236ee61dd463ca3c7bf829a46c3e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115319"
---
# <a name="use-utility-explorer-to-manage-the-sql-server-utility"></a>ユーティリティ エクスプローラーを使用した SQL Server ユーティリティの管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ユーティリティ エクスプローラーは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のコンポーネントで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスに接続して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ内のすべてのオブジェクトのツリー ビューを表示します。 ユーティリティ エクスプローラーのコンテンツ ウィンドウには、SQL Server のマネージド インスタンスの正常性状態について、いくつかの方法で概要データと詳細データを表示できます。 ユーティリティ エクスプローラーには、ポリシー定義の表示と管理を行うためのユーザー インターフェイスも用意されています。 ユーティリティ エクスプローラーの機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ内のオブジェクトによって多少異なりますが、一般に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティによって管理されるオブジェクト、データ、およびポリシーが含まれます。 詳細については、「 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)」を参照してください。  
  
## <a name="create-utility-control-point"></a>ユーティリティ コントロール ポイントの作成  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティを使用する前に、ユーティリティ コントロール ポイントを作成する必要があります。 詳細については、「[SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)」または「[SQL Server ユーティリティ コントロール ポイントの作成 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)」を参照してください。  
  
## <a name="enroll-an-instance-of-sql-server-or-a-data-tier-application-from-utility-explorer"></a>ユーティリティ エクスプローラーからの SQL Server インスタンスまたはデータ層アプリケーションの登録  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに簡単に登録することができます。 ユーティリティ エクスプローラーで、 **[マネージド インスタンス]** ノードを右クリックし、 **[マネージド インスタンスの追加]** をクリックします。 操作を完了するには、ウィザードの手順に従います。 詳細については、「[SQL Server のインスタンスの登録 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)」を参照してください。  
  
 データ層アプリケーションを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスに配置するには、 **[オブジェクト エクスプローラー]** タブをクリックし、 **[管理]** ノードを展開して、 **[データ層アプリケーション]** を右クリックします。 右クリックで表示されるメニューで、 **[データ層アプリケーションの配置]** をクリックします。 詳細については、「 [データ層アプリケーションの配置](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)」を参照してください。  
  
## <a name="viewing-utility-explorer"></a>ユーティリティ エクスプローラーの表示  
 ユーティリティ エクスプローラーは、既定では、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 内に表示されません。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ユーザー インターフェイスにユーティリティ エクスプローラーが表示されない場合は、 **[表示]** メニューの **[ユーティリティ エクスプローラー]** をクリックしてください。 ユーティリティ エクスプローラーのコンテンツ ウィンドウを表示するには、 **[表示]** メニューの **[ユーティリティ エクスプローラーのコンテンツ]** をクリックします。  
  
## <a name="viewing-objects-in-utility-explorer"></a>ユーティリティ エクスプローラーでのオブジェクトの表示  
 ユーティリティ エクスプローラーのナビゲーション ウィンドウとユーティリティ エクスプローラーのコンテンツ ウィンドウでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで管理されるデータ、オブジェクト、およびポリシーが表示されます。 ナビゲーション ウィンドウを使用して、ダッシュボードとビューポイントに表示する情報を指定したら、コンテンツ ウィンドウおよび詳細タブを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで管理されているオブジェクトのデータとポリシー情報にアクセスします。  
  
### <a name="sql-server-utility-navigation-pane"></a>SQL Server ユーティリティのナビゲーション ウィンドウ  
 ユーティリティ エクスプローラーのナビゲーション ウィンドウでは、ユーティリティ コントロール ポイント (UCP) でグループ化された、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ オブジェクトのツリー ビューが表示されます。 フォルダーを展開するには、プラス記号 (+) をクリックするか、ユーティリティ エクスプローラーのナビゲーション ウィンドウ内の UCP 名をダブルクリックします。 フォルダーまたはオブジェクトを右クリックすると、一般的なタスクを実行するためのメニューが表示されます。 ツリー ビューのノードは次のとおりです。  
  
-   ツリー ビューの最上位ノードは、ユーティリティ コントロール ポイント (UCP) です。 ノード名は、"Utility_Name"(ComputerName\UCP_instance_name) のように作成されます。 UCP がない場合は、作成する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに接続していない場合は、接続する必要があります。 詳細については、「 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)」を参照してください。 ツリー ビューの UCP 名をクリックし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ エクスプローラーのコンテンツ ウィンドウに、ダッシュボード ビューのデータを読み込みます。 詳細については、「[ユーティリティ ダッシュボード &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/999eb741-4a60-43f6-ab37-2df7dce845c1)」を参照してください。  
  
     UCP ノードを右クリックして、ダッシュボードのデータを更新します。  
  
-   ツリー ビューの **[配置済みのデータ層アプリケーション]** ノードをクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのコンテンツ ペイン内のリスト ビューのデータにアクセスします。 コンテンツ ウィンドウの下部にある詳細タブでは、CPU 使用率および記憶域使用率に関するデータが表示されるだけでなく、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティにある個々のデータ層アプリケーションに関するポリシーの定義やプロパティの詳細へのアクセスが可能になります。 詳細については、「[配置済みのデータ層アプリケーションの詳細 &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)」を参照してください。  
  
     ツリー ビューの **[配置済みのデータ層アプリケーション]** ノードを右クリックして、フィルターの設定にアクセスしたり、リスト ビューのデータを更新したりします。  
  
-   ツリー ビューの **[マネージド インスタンス]** ノードをクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのコンテンツ ウィンドウ内のリスト ビューのデータにアクセスします。 コンテンツ ウィンドウの下部にある詳細タブでは、CPU 使用率および記憶域ボリューム使用率に関するデータが表示されるだけでなく、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティにある個々の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージド インスタンスに関するポリシーの定義やプロパティの詳細へのアクセスが可能になります。 詳細については、「[マネージド インスタンスの詳細 &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)」を参照してください。  
  
     ツリー ビューの **[マネージド インスタンス]** ノードを右クリックして、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティへの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスの追加、フィルター設定へのアクセス、またはリスト ビューのデータの更新を行います。  
  
-   ツリー ビューの **[ユーティリティ管理]** ノードをクリックして、すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスのグローバル ポリシー定義、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの配置済みのデータ層アプリケーションのグローバル ポリシー定義にアクセスします。また、UCP の管理者情報を表示したり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ管理データ ウェアハウスの構成設定にアクセスしたりすることも可能です。 詳細については、「[ユーティリティの管理 &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)」を参照してください。 **[ポリシー]** タブのコントロールを使用して、ポリシー違反の報告の感度を変更することもできます。 詳細については、「[CPU 使用率のポリシーにおけるノイズの軽減 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)」を参照してください。  
  
     ツリー ビューの **[ユーティリティ管理]** ノードを右クリックして、コンテンツ ペインのデータを更新します。  
  
### <a name="sql-server-utility-dashboard"></a>SQL Server ユーティリティ ダッシュボード  
 ユーティリティ エクスプローラーのツリー ビューで UCP ノードを選択すると、ユーティリティ エクスプローラーのコンテンツ ウィンドウに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ ダッシュボードが設定されます。 ダッシュボードでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ内のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージド インスタンスとデータ層アプリケーションの状態、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで管理されるオブジェクトの全体的な記憶域使用率の概要がひとめでわかるように表示されます。 詳細については、「[ユーティリティ ダッシュボード &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/999eb741-4a60-43f6-ab37-2df7dce845c1)」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを登録または削除するには、「[SQL Server のインスタンスの登録 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)」、「[データ層アプリケーションの配置](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)」、または「[SQL Server ユーティリティからの SQL Server のインスタンスの削除](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)」を参照してください。  
  
### <a name="filtering-the-list-of-objects-in-utility-explorer-contents"></a>ユーティリティ エクスプローラー内のオブジェクトの一覧に対するフィルター処理  
 1 つのノードに多数のオブジェクトが含まれていると、対象のオブジェクトを見つけるのが難しくなります。 そのような場合は、ユーティリティ エクスプローラーのフィルター機能を使用して、一覧のサイズを小さく絞り込みます。 たとえば、特定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスや、ファイル領域の使用率の低いコンピューターだけを見つけるとします。 フィルター処理を行うフォルダーを右クリックし、[フィルター] ボタンをクリックして、 **[フィルターの設定]** をクリックして [ユーティリティ エクスプローラーのフィルターの設定] ダイアログ ボックスを開きます。 名前、コンピューターの CPU、インスタンスの CPU、ファイル領域、ボリューム領域、ポリシーのオーバーライド設定、または最終報告日時で、一覧をフィルター処理できます。 **[演算子]** 列および **[値]** 列のボックスの一覧には、追加のフィルター演算子が表示されます。  
  
### <a name="starting-powershell"></a>PowerShell の起動  
 PowerShell セッションを起動するには、オブジェクト エクスプローラー ツリーで、一部を除くいずれかのフォルダーまたはオブジェクトを右クリックし、 **[Powershell の起動]** をクリックします。 これにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell サポートが有効になった Powershell セッションが起動し、パスがオブジェクト エクスプローラーで右クリックしたオブジェクトに設定されます。 これで、対話型の Powershell 環境で Powershell コマンドを入力できます。 詳細については、「 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)」を参照してください。  
  
 PowerShell には F1 ヘルプがありませんが、 **Get-Help** コマンドレットで PowerShell の使用に関する情報を参照することができます。 詳細については、「 [Get Help SQL Server PowerShell](../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [正常性ポリシーの構成 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)   
 [[オブジェクト エクスプローラー]](../../ssms/object/object-explorer.md)  
  
  
