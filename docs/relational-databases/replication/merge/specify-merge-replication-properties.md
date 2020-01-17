---
title: マージ レプリケーションのプロパティの指定 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8ae39654a19c73c71c602801b3aa5f594f7d0828
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908157"
---
# <a name="specify-merge-replication-properties"></a>マージ レプリケーションのプロパティの指定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
このトピックでは、マージ レプリケーションのさまざまなプロパティを指定する方法について説明します。 

## <a name="merge-article-is-download-only"></a>マージ アーティクルはダウンロード専用です
ダウンロード専用のアーティクルは、サブスクライバーで更新されないデータを含むアプリケーション用に設計されています。 詳細については、「[ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンス最適化](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)」を参照してください。  
   
###  <a name="considerations"></a>考慮事項   
-   サブスクリプションが初期化された後でアーティクルをダウンロードのみに指定する場合は、そのアーティクルを受信したすべてのクライアント サブスクリプションを再初期化する必要があります。 サーバー サブスクリプションは再初期化する必要はありません。 プロパティ変更の影響の詳細については、「[パブリケーションおよびアーティクルのプロパティの変更](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)」を参照してください。  
  
### <a name="use-sql-server-management-studio"></a>SQL Server Management Studio の使用 [SQL Server]  
  
#### <a name="on-the-articles-page"></a>[アーティクル] ページ
パブリケーションの新規作成ウィザードの **[アーティクル]** ページでテーブルを選択し、 **[反転表示されたテーブルはダウンロードのみである]** チェック ボックスをオンにします。  
  
#### <a name="on-the-properties-tab-of-the-article-properties"></a>[アーティクルのプロパティ] の [プロパティ] タブ  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスでテーブルを選択し、 **[アーティクルのプロパティ]** をクリックします。    
2.  **[反転表示されたテーブル アーティクルのプロパティを設定]** または **[すべてのテーブル アーティクルのプロパティを設定]** をクリックします。  
  
3.  **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブの **[対象オブジェクト]** セクションで、 **[同期の方向]** に対して以下のいずれかの値を指定します。    
    -   **[サブスクライバーへのダウンロードのみを実行し、サブスクライバーの変更を禁止する]**    
    -   **[サブスクライバーへのダウンロードのみを実行し、サブスクライバーの変更を許可する]**    
4.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  

###  <a name="use-transact-sql"></a>Transact-SQL の使用  
  
#### <a name="new-article"></a>新しいアーティクル  
  
1.  パラメーター [@subscriber_upload_options](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) に **1** または **2** を指定し、`@subscriber_upload_options` を使用して、マージ テーブル アーティクルをダウンロード専用に指定する方法について説明します。 各数値は次の動作に対応します。  
  
    -   **0** - 制限なし (既定)。 サブスクライバー側で行われた変更は、パブリッシャーにアップロードされます。    
    -   **1** - サブスクライバーでの変更は許可されますが、パブリッシャーにはアップロードされません。    
    -   **2** - サブスクライバーでの変更は許可されません。  
  
       > [!NOTE]  
       > アーティクルのソース テーブルが別のパブリケーションで既にパブリッシュされている場合、`@subscriber_upload_options` の値は、両方のアーティクルで同じであることが必要です。  
  
#### <a name="existing-article"></a>既存のアーティクル
  
1.  アーティクルがダウンロード専用であるかどうかを判断するには、[sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) を実行して、結果セット内のアーティクルの **upload_options** の値を確認します。 
  
2.  手順 1. で返された値が **0** である場合は、[sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行します。この場合、`@property` に **subscriber_upload_option** の値を、`@force_invalidate_snapshot` および `@force_reinit_subscription` に値 **1** を、`@value` に値 **1** または値 **2** を (この場合、次の値に対応) 指定します。  
  
    -   **1** - サブスクライバーでの変更は許可されますが、パブリッシャーにはアップロードされません。    
    -   **2** - サブスクライバーでの変更は許可されません。  
  
        > [!NOTE]  
        >  アーティクルのソース テーブルが別のパブリケーションで既にパブリッシュされている場合、ダウンロード専用の動作は、両方のアーティクルで同じであることが必要です。  
  
## <a name="interactive-conflict-resolution"></a>Interactive Conflict Resolution 
  
 Microsoft SQL Server レプリケーションには、Microsoft Windows 同期マネージャーでの要求時同期中に、手動で競合を解決できるインタラクティブ競合回避モジュールがあります。 インタラクティブな競合解決を有効にすると、インタラクティブ競合回避モジュールを使用して、同期実行時に競合がインタラクティブに解決されます。 インタラクティブ競合回避モジュールは、Microsoft Windows 同期マネージャーを介して利用できます。 詳細については、「[Windows 同期マネージャーを使用したサブスクリプションの同期 &#40;Windows 同期マネージャー&#41;](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)」をご覧ください。  
  
  
### <a name="Recommendations"></a> 推奨事項  
  
-   同期が Windows 同期マネージャーの外部で (スケジュールされた同期、または SQL Server Management Studio かレプリケーション モニターでの要求時同期として) 実行される場合、アーティクルに指定された既定の競合回避を使用して、ユーザーの介入なしに自動的に競合が解決されます。 詳細については、「 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)」を参照してください。  
  
### <a name="use-sql-server-management-studio"></a>SQL Server Management Studio の使用 [SQL Server]  
  
#### <a name="enable-interactive-conflict-resolution-for-an-article"></a>アーティクルに対するインタラクティブな競合解決の有効化  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、テーブルを選択します。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication.md)」および「[View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。   
2.  **[アーティクルのプロパティ]** をクリックし、次に **[反転表示されたテーブル アーティクルのプロパティを設定]** または **[すべてのテーブル アーティクルのプロパティを設定]** をクリックします。    
3.  **[アーティクルのプロパティ - \<Article>]** または **[アーティクルのプロパティ - \<ArticleType>]** ページで、 **[競合回避モジュール]** タブをクリックします。    
4.  **[要求時同期中にサブスクライバーが対話的に競合を解決することを許可する]** を選択します。    
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]    
6.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  
  
#### <a name="specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>サブスクリプションでのインタラクティブな競合解決の使用の指定  
  
1.  **[サブスクリプションのプロパティ - \<Subscriber>:\<SubscriptionDatabase>]** ダイアログ ボックスで、 **[競合を対話的に解決]** オプションに **[True]** の値を指定します。 このダイアログ ボックスへのアクセスの詳細については、「 [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 」および「 [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)」を参照してください。   
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="use-transact-sql"></a>Transact-SQL の使用  
 マージ パブリケーションに対するプル サブスクリプションが作成されるときに、サブスクライバーがこのグラフィカル インターフェイスを使用してアーティクルの競合を回避するように、プログラムで指定できます。 このオプションをサポートするアーティクル内の競合のみが、インタラクティブ競合回避モジュールに表示されます。  
  
#### <a name="create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>インタラクティブ競合回避モジュールを使用するマージ プル サブスクリプションの作成  
  
1.  パブリッシャー側のパブリケーション データベースに対し、`@publication` を指定して [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) を実行します。 インタラクティブ競合回避モジュールが使用される結果セット内の各アーティクルに対する **allow_interactive_resolver** の値を確認します。   
    -   この値が **1**の場合、インタラクティブ競合回避モジュールが使用されます。    
    -   この値が **0**の場合は、最初に、各アーティクルに対してインタラクティブ競合回避モジュールを有効にする必要があります。 そのためには、[sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行します。このとき、`@publication` および `@article` を指定し、さらに `@property` に **allow_interactive_resolver** の値を指定し、`@value` に値 **true** を指定します。    
2.  サブスクライバー側のサブスクリプション データベースに対して、 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)を実行します。 詳細については、「 [プル サブスクリプションの作成](../../../relational-databases/replication/create-a-pull-subscription.md)」をご覧ください。    
3.  サブスクライバー側のサブスクリプション データベースに対し、次のパラメーターを指定して [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)を実行します。    
    -   `@publisher`、`@publisher_db` (パブリッシュされるデータベース)、および `@publication`。    
    -   `@enabled_for_syncmgr` には値 **true**。    
    -   `@use_interactive_resolver` には値 **true**。    
    -   マージ エージェントが必要とするセキュリティ アカウント情報。 詳細については、「 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)」を参照してください。    
4.  パブリッシャー側のパブリケーション データベースに対し、 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)を実行します。  
  
#### <a name="define-an-article-that-supports-the-interactive-resolver"></a>インタラクティブ競合回避モジュールをサポートするアーティクルの定義  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)を実行します。 アーティクルが属しているパブリケーションの名前を `@publication` に、アーティクルの名前を `@article` に、パブリッシュされるデータベース オブジェクトを `@source_object` に、値 **true** を `@allow_interactive_resolver` に指定します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
 
## <a name="conflict-tracking-and-resolution-level-for-merge-articles"></a>マージ アーティクルの競合追跡と競合解決のレベル
このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、マージ アーティクルの競合追跡と回避のレベルを指定する方法について説明します。  
  
 マージ パブリケーションへのサブスクリプションを同期する際、パブリッシャーとサブスクライバーの同じデータに加えられた変更によって、競合が発生していないかどうかがレプリケーション時に確認されます。 競合を行レベルで検出するか (行に加えられたすべての変更が競合と見なされます)、列レベルで検出するか (同じ行と列に対する変更のみが競合と見なされます) を指定できます。 アーティクルの競合解決は行レベルで実行されます。 論理レコードが使用される場合の競合の検出と解決の詳細については、「 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)」を参照してください。  
 
### <a name="limitations-and-restrictions"></a>制限事項と制約事項  
  
-   サブスクリプションを初期化した後で追跡レベルを変更した場合は、サブスクリプションを再初期化する必要があります。 プロパティ変更の影響の詳細については、「[パブリケーションおよびアーティクルのプロパティの変更](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)」を参照してください。   
-   行レベルおよび列レベルの追跡では、行レベルでの競合回避は常に実行されます。優先されなかった行が優先された行で上書きされます。 マージ レプリケーションでは、論理レコード レベルでの競合の追跡と回避も指定できますが、このオプションは [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]にはありません。 レプリケーション ストアド プロシージャからこのオプションを設定する方法については、「 [マージ テーブル アーティクル間に論理レコード リレーションシップを定義する](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)」を参照してください。  
  
### <a name="use-sql-server-management-studio"></a>SQL Server Management Studio の使用 [SQL Server]  
 **[アーティクルのプロパティ]** ダイアログ ボックスの **[プロパティ]** タブで、マージ アーティクルに対する行レベルまたは列レベルの追跡を指定します。このダイアログ ボックスは、パブリケーションの新規作成ウィザードおよび **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで使用できます。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication.md)」および「[View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
#### <a name="specify-row--or-column-level-tracking"></a>行レベルまたは列レベルの追跡の指定  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、テーブルを選択します。  
2.  **[アーティクルのプロパティ]** をクリックし、次に **[反転表示されたテーブル アーティクルのプロパティを設定]** または **[すべてのテーブル アーティクルのプロパティを設定]** をクリックします。   
3.  **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブで、 **[追跡レベル]** プロパティの値として **[行レベルの追跡]** または **[列レベルの追跡]** のいずれかを選択します。   
4.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  
  
### <a name="use-transact-sql"></a>Transact-SQL の使用  
  
#### <a name="to-specify-conflict-tracking-options-for-a-new-merge-article"></a>新しいマージ アーティクルの競合追跡オプションを指定するには  
  
1.  パブリッシャーのパブリケーション データベースに対して、[sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行し、次のいずれかの値を `@column_tracking` に指定します。  
  
    -   **true** - アーティクルに対して列レベルの追跡を使用します。    
    -   **false** - 既定の行レベルの追跡を使用します。  
  
#### <a name="change-conflict-tracking-options-for-a-merge-article"></a>マージ アーティクルの競合追跡オプションの変更  
  
1.  マージ アーティクルの競合追跡オプションを定義するには、 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)を実行します。 アーティクルの結果セットの **column_tracking** オプションの値を調べます。 値 **1** は、列レベルの追跡が使用されていることを示します。値 **0** は、行レベルの追跡が使用されていることを示します。    
2.  パブリッシャー側のパブリケーション データベースに対して、 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)を実行します。 `@property` に **column_tracking** の値を指定し、`@value` に次のいずれかの値を指定します。  
  
    -   **true** - アーティクルに対して列レベルの追跡を使用します。    
    -   **false** - 既定の行レベルの追跡を使用します。  
  
     `@force_invalidate_snapshot` と `@force_reinit_subscription` の両方に値 **1** を指定します。 

## <a name="manage-tracking--deletes"></a>削除の追跡を管理する
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 既定では、マージ レプリケーションではパブリッシャーとサブスクライバーの DELETE コマンドが同期されます。 マージ レプリケーションを使用すると、行がパブリケーションから削除されても、サブスクリプション データベースでその行を保持できます。その逆の操作も可能です。 新しいアーティクルを作成するときに DELETE コマンドを無視するようにプログラムで指定したり、レプリケーション ストアド プロシージャを使用してこの機能を後で有効にすることができます。  
  
> [!IMPORTANT]  
>  この機能を有効にすると、データが収束しなくなります。つまり、サブスクライバーに存在するデータにパブリッシャーのデータが正確に反映されなくなります。 削除された行を手動で削除するためのメカニズムを独自に実装する必要があります。  
  
### <a name="specify-that-deletes-be-ignored-for-a-new-merge-article"></a>新しいマージ アーティクルで削除を無視する指定  
  
パブリッシャー側のパブリケーション データベースに対して、[sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行します。 `@delete_tracking` には値 **false** を指定します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。
  
    > [!NOTE]  
    >  If the source table for an article is already published in another publication, the value of **delete_tracking** must be the same for both articles.  
  
### <a name="specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>既存のマージ アーティクルで削除を無視する指定  
  
1.  アーティクルでエラー補正が有効になっているかどうかを確認するために、[sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) を実行して、結果セット内の **delete_tracking** の値を確認します。 値が **0**の場合、削除は既に無視されています。  
  
2.  手順 1. で得た値が **1** だった場合、パブリッシャー側のパブリケーション データベースに対して [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行します。 `@property` に `delete_tracking` の値を指定し、`@value` には値 **false** を指定します。  
  
    > [!NOTE]  
    >  アーティクルのソース テーブルが別のパブリケーションで既にパブリッシュされている場合、両方のアーティクルで **delete_tracking** の値を同じにする必要があります。  
  

## <a name="processing-order"></a>処理順序
  マージ レプリケーションでは、同期処理中にアーティクルをマージ エージェントで処理する順序を指定できます。 この順序は、レプリケーションのストアド プロシージャを使用して、アーティクル作成時に各アーティクルに対してプログラムから割り当てることができます。 アーティクルは、最も小さい値から最も大きい値の順序で処理されます。 2 つのアーティクルの値が同じ場合、それらは同時に処理されます。 

### <a name="how-processing-order-is-determined"></a>処理順序を決定する方法  
 マージ同期の際、既定ではアーティクルがオブジェクト間の依存関係で必要な順序で処理されます。依存関係には、ベース テーブルに対して定義されている宣言参照整合性 (DRI) 制約も含まれます。 同期処理では、テーブルに対する変更が列挙された後で、これらの変更が適用されます。 DRI が定義されておらず、テーブル アーティクル間に結合フィルターか論理レコードが存在する場合、フィルターや論理レコードで必要な順序でアーティクルが処理されます。 DRI、結合フィルター、論理レコード、またはその他の依存関係で他のアーティクルと関係付けられていないアーティクルは、システム テーブル [sysmergearticles &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/sysmergearticles-transact-sql.md) 内のアーティクル ニックネームに従って処理されます。  
  
 パブリケーションに **SalesOrderHeader** テーブルと **SalesOrderDetail** テーブルが含まれており、 **SalesOrderHeader** テーブルには主キー列 **SalesOrderID** があり、 **SalesOrderDetail** テーブルには対応する外部キー列 **SalesOrderID** があるとします。 同期の際、マージ レプリケーションでは、新しい行を **SalesOrderHeader** に挿入してから関連する行を **SalesOrderDetail**に挿入することで、外部キーの違反を防ぎます。 同様に、 **SalesOrderDetail** から行を削除した後で、関連する行を **SalesOrderHeader**から削除します。  
  
 ただし、アプリケーションによっては、DRI ではなくデータベース トリガーやアプリケーション レベルで参照整合性が設定されます。 上記のようなパブリケーションでは、DRI ではなく **SalesOrderDetail** テーブルの挿入トリガーによって、挿入を許可する前に、 **SalesOrderHeader** テーブルに関連する行があることを確認できる場合があります。 **SalesOrderHeader** の削除トリガーでは、削除を許可する前に、 **SalesOrderDetail** に関連する行がないことを確認できる場合があります。 マージ レプリケーションでは、アーティクルの処理順序を決定する際にトリガーは考慮されません。トリガーが起動されないとその結果がどのようになるかがわからないためです。 同様に、アプリケーション レベルで定義された制約も考慮されません。  
  
 トリガーやアプリケーション レベルで参照整合性を保つ場合は、アーティクルの処理順序を指定する必要があります。 トリガーの例では、アーティクルの順序が挿入の順序で決まるため、 **SalesOrderHeader** テーブルを **SalesOrderDetail**の前に処理するように指定します。 マージ レプリケーションでは、削除の場合、自動的に順序が逆になります。 アーティクルの順序がなくてもマージ レプリケーションは失敗しません。これは、制約違反が発生してもマージ エージェントで処理が継続され、他のアーティクルの処理を終えた後で操作が再試行されるためです。 アーティクルの順序を指定すると、再試行とそれに付随する追加の処理が不要になります。 誤った順序 (詳細レコードがヘッダー レコードの前に処理されるような順序など) を指定すると、マージ レプリケーションは成功するまで処理を再試行します。   
  
### <a name="new-article"></a>新しいアーティクル
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行します。 `@processing_order` のアーティクルの処理順序を表す整数値を指定します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
    > [!NOTE]  
    >  処理順序を指定してアーティクルを作成する場合は、アーティクルの順序を表す値の間に、ある程度の間隔を設けるようにしてください。 こうすることで、後で、新しい値を設定するときに作業が楽になります。 たとえば、固定された処理順序を指定するアーティクルが 3 つある場合、`@processing_order` の値を 1、2、3 とせずに、それぞれ、10、20、30 のように指定します。  
  
### <a name="existing-article"></a>既存のアーティクル
  
1.  アーティクルの処理順序を指定するには、[sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) を実行し、結果セットの **processing_order** の値を確認します。   
2.  パブリッシャー側のパブリケーション データベースに対して、[sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行します。 `@property` に **processing_order** の値を指定し、`@value` には処理順序を表す整数値を指定します。  


## <a name="see-also"></a>参照  
 [ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンス最適化](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [アーティクルのプロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  
