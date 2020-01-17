---
title: 管理データ ウェアハウスの構成 (SSMS)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.datacollection.wizard_completecfg.f1
- sql13.swb.dc.datacollection.wizard_config.f1
- sql13.swb.dc.datacollection.wizard_finish.f1
- sql13.swb.dc.datacollection.wizard_maploginuser.f1
- sql13.swb.dc.datacollection.wizard_choosemdw.f1
- sql13.swb.dc.datacollection.wizard_welcome.f1
- sql13.swb.dc.datacollection.wizard_createmdw.f1
helpviewer_keywords:
- data warehouse [SQL Server], multiple instances
- data warehouse [SQL Server], configuring
- Configure Management Data Warehouse Wizard
- management data warehouse, configuring
ms.assetid: 23a584f3-c5e1-414c-9afe-73cd7efbda4b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 54badd0404ee5360aef4a7bc095c236e5b31f79d
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056476"
---
# <a name="configure-the-management-data-warehouse-sql-server-management-studio"></a>管理データ ウェアハウスの構成 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、データ コレクターを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 1 つまたは複数のインスタンスのデータ ストレージをサポートするように管理データ ウェアハウスを構成する方法について説明します。 対象のインスタンスは、同じサーバーまたは別々のサーバーのどちらに配置されていてもかまいません。 このトピックでは、 [管理データ ウェアハウス構成ウィザード](#Wizard) のユーザー インターフェイスについても説明します。 データ コレクターの構成の詳細については、「 [Configure Properties of a Data Collector](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md)」を参照してください。  
  
> [!NOTE]  
>  システム サービス アカウント (ローカル システム、ネットワーク サービス、またはローカル サービス) を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを実行するように構成している場合に、管理データ ウェアハウスをデータ コレクターとは別のインスタンス上に作成するときは、プロキシを使用して管理データ ウェアハウスにデータをアップロードするようにコレクション セットを構成する必要があります。  
  
### <a name="configure-the-management-data-warehouse-on-a-single-instance-or-multiple-instances-of-includessnoversionincludesssnoversion-mdmd"></a>の 1 つまたは複数のインスタンスの管理データ ウェアハウスの構成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されていることを確認します。  
  
2.  オブジェクト エクスプローラーで、 **[管理]** ノードを展開します。  
  
3.  **[データ コレクション]** を右クリックし、 **[タスク]** を展開して **[管理データ ウェアハウスの構成]** をクリックします。  
  
4.  [管理データ ウェアハウス構成ウィザード](#Wizard) で、管理データ ウェアハウスを作成し、ログインを構成します。次に、データ コレクションを有効化し、 **システム データ コレクション セット**を開始します。  
  
     複数のインスタンスを構成するには、手順 5 に進みます。  
  
    > [!NOTE]  
    >  同じ管理データ ウェアハウスを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスにデータ コレクターがインストールされている配置では、プロキシを使用することをお勧めします。  
  
5.  別のインスタンスで [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、次のいずれかの操作を実行します。  
  
    -   管理データ ウェアハウス構成ウィザードを使用して、既存の管理データ ウェアハウス用にデータ コレクションを構成します。  
  
    -   **[データ コレクション]** を右クリックし、 **[プロパティ]** をクリックします。 **[全般]** タブで、既存の管理データ ウェアハウス、およびそれがインストールされたサーバーを指定します。  
  
6.  データ コレクターを使用するすべてのデータベース インスタンスが共有管理データ ウェアハウスにデータをアップロードするように構成されるまで、手順 5. を繰り返します。  

####  <a name="Wizard"></a> 管理データ ウェアハウス構成ウィザード  
 **[ようこそ] ページ**  
  
 ようこそページは、データ コレクション構成ウィザードの開始ページです。 このページを表示するかどうかは任意です。  
  
 **[次回からこの開始ページを表示しない]**  
 データ コレクション構成ウィザードを次回起動したときにこのページを表示しない場合にオンにします。  
  
 **[管理データ ウェアハウス ストレージの構成] ページ**  
  
 このページを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース サーバーと管理データ ウェアハウスを選択します。 管理データ ウェアハウスは、収集したデータを格納するリレーショナル データベースです。  
  
> [!NOTE]  
>  サーバー上に管理データ ウェアハウスを作成するには、適切なレベルのアクセス許可を持っている必要があります。 詳細については、「[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)」を参照してください。 また、管理データ ウェアハウス ロール用のログインを作成するための、適切なレベルのアクセス許可も必要です。  
  
 **サーバー名**  
 管理データ ウェアハウスをホストするサーバーの名前を指定します。  
  
 管理データ ウェアハウスを構成する場合は常に、 **[サーバー名]** がローカル サーバー名になり、この名前を変更することはできません。  
  
 **データベース名**  
 収集したデータを格納するリレーショナル データベースを指定します。 一覧を使用して既存のデータベースを選択するか、 **[新規作成]** をクリックし、 **[新しいデータベース]** ダイアログ ボックスを使用して新しい接続を作成します。  
  
 **[新規作成]** オプションはデータ コレクション セットを構成する場合にのみ使用できます。  
  
 **[ログインとユーザーのマップ] ページ**  
  
 このページを使用すると、管理データ ウェアハウスのデータベース ユーザー ロールにログインをマップできます。  
  
 **[このログインにマップされたユーザー]**  
 管理データ ウェアハウスをホストするサーバーの既存のログインを表示します。 各行には、編集可能な **[マップ]** チェック ボックス、 **[ログイン]** 名、およびログインの **[種類]** が含まれます。  
  
 ログインの **[マップ]** チェック ボックスをオンにしてログインを指定します。  
  
 *\<data warehouse name>* の**データベース ロール メンバーシップ**  
 次のオプションの 1 つ以上についてチェック ボックスをオンにし、ログインがマップされる管理データ ウェアハウス ロールを選択します。  
  
-   **mdw_admin**  
  
-   **mdw_reader**  
  
-   **mdw_writer**  
  
 **[新しいログイン]**  
 **[ログイン - 新規作成]** ダイアログ ボックスを開いて、管理データ ウェアハウスの新しいログインを作成します。  
  
 **[ウィザードの完了] ページ**  
  
 このページを使用すると、データ コレクションの構成を確認して完了できます。 表示ウィンドウに表示されるツリーは、適用される構成と、 **[完了]** をクリックしたときに実行されるアクションを示します。  
  
 **[データ コレクション構成ウィザードの進行状況] ページ**  
  
 このページを使用すると、各構成手順の結果を表示できます。  
  
 **詳細**  
 各構成手順を **[詳細]** グリッド内の行として表示します。 各行には、手順について説明する **[アクション]** 列と、手順の成功または失敗を示す **[状態]** 列があります。 エラーが発生した場合は、 **[メッセージ]** 列にメッセージが表示されます。  
  
 **[停止]**  
 ウィザードの処理を停止します。  
  
 **レポート**  
 データ コレクション構成のレポートを表示します。 次のレポート オプションが用意されています。  
  
-   [レポートの表示]  
  
-   [レポートをファイルに保存]  
  
-   [レポートをクリップボードにコピー]  
  
-   [レポートを電子メールとして送信]  
  
 **[閉じる]**  
 ウィザードを閉じます。  
  
## <a name="see-also"></a>参照  
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [データ コレクションの管理](../../relational-databases/data-collection/manage-data-collection.md)  
  
  
