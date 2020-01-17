---
title: Windows 同期マネージャー (Windows Synchronization Manager) を使用してサブスクリプションの同期 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], Windows Synchronization Manager
- Windows Synchronization Manager
ms.assetid: 80f15dd6-e84d-4f96-9866-5b34ea531f1e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 04b1c5322408f66ab2a4023e3d215cc7e669eab6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745761"
---
# <a name="synchronize-a-subscription-using-windows-synchronization-manager-windows-synchronization-manager"></a>Windows 同期マネージャーを使用したサブスクリプションの同期 (Windows 同期マネージャー)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 同期マネージャーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が同期マネージャーと同じコンピューターで実行されている場合には、サブスクリプションを Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリケーションに同期させるためだけに使用できます (オフライン ファイルや Web ページを同期するためにも使用できます)。 同期マネージャーを使用するには、以下の手順を実行します。  
  
1.  **[サブスクリプションのプロパティ - \<サブスクライバー>: \<SubscriptionDatabase>]** ダイアログ ボックスで、Windows 同期マネージャーを使用したプル サブスクリプションの同期を有効にします。 このダイアログ ボックスへのアクセスの詳細については、「[プル サブスクリプションのプロパティの表示または変更](view-and-modify-pull-subscription-properties.md)」を参照してください。  
  
2.  Windows の **[スタート]** メニューから、同期マネージャーにアクセスします。  
  
 同期マネージャーでは、マージ サブスクリプションでインタラクティブ競合回避モジュールを使用できます。 一般に、同期の際に検出された競合は自動的に回避されますが、対話型の競合回避が有効になっていると、同期の際にユーザーが競合を回避することができます。 同期が Windows 同期マネージャーの外部で (スケジュールされた同期、または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] かレプリケーション モニターでの要求時同期として) 実行される場合、競合は、アーティクルに指定された競合回避モジュールに従って、ユーザーの介入なしに自動的に解決されます。  
  
> [!NOTE]  
>  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] および [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]以降では、Windows 同期マネージャーの 64 ビット版は 32 ビット サブスクリプションを検出することはできません。  
  
### <a name="to-enable-the-synchronization-of-pull-subscriptions-with-windows-synchronization-manager"></a>Windows 同期マネージャーを使用したプル サブスクリプションの同期を有効化するには  
  
1.  **[サブスクリプションのプロパティ - \<サブスクライバー>:\<SubscriptionDatabase>]** ダイアログ ボックスの [全般] ページで、 **[Windows 同期マネージャーを使用]** オプションの値として **[有効化]** を選択します。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-synchronize-a-pull-subscription-with-synchronization-manager"></a>同期マネージャーを使用してプル サブスクリプションを同期するには  
  
1.  次の方法のいずれかを使用して、同期マネージャーを起動します。  
  
    -   Internet Explorer で、 **[ツール]** メニューの **[同期]** をクリックします。  
  
    -   **[スタート]** ボタンをクリックし、 **[プログラム]** または **[すべてのプログラム]** をポイントします。 **[アクセサリ]** をポイントし、 **[同期]** をクリックします。  
  
    -   **[スタート]** メニューの **[ファイル名を指定して実行]** **実行**ダイアログ ボックスに「`mobsync.exe`で、**オープン**フィールドをクリックしてして **[ok]** 。  
  
2.  **[同期する項目]** ダイアログ ボックスで、同期するサブスクリプションを選択します。 サブスクリプションは、そのコンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの下に表示されます。  
  
3.  **[同期]** をクリックします。  
  
### <a name="to-reinitialize-a-pull-subscription-with-synchronization-manager"></a>同期マネージャーを使用してプル サブスクリプションを再初期化するには  
  
1.  **[同期する項目]** ダイアログ ボックスでサブスクリプションを選択し、次に **[プロパティ]** をクリックします。  
  
2.  **[SQL Server サブスクリプション プロパティ]** ダイアログ ボックスで、 **[サブスクリプションの再初期化]** をクリックします。  
  
3.  **[はい]** をクリックします。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     次回サブスクリプションを同期すると、既定では新しいスナップショットがサブスクリプション データベースに適用されます。 詳細については、「 [サブスクリプションの再初期化](reinitialize-subscriptions.md)」を参照してください。  
  
> [!NOTE]  
>  マージ レプリケーションでは、スナップショットを適用する前に、未処理の変更をパブリッシャーにアップロードすることができますが、このオプションは同期マネージャーでは利用できません。 変更をアップロードするには、サブスクリプションを再初期化する前に同期します。  
  
### <a name="to-set-properties-for-a-pull-subscription-in-synchronization-manager"></a>同期マネージャーでプル サブスクリプションのプロパティを設定するには  
  
1.  **[同期する項目]** ダイアログ ボックスでサブスクリプションを選択し、次に **[プロパティ]** をクリックします。  
  
2.  以下のタブのプロパティを参照および変更します。  
  
    -   **[識別]**  
  
    -   **[サブスクライバー ログイン]** 、 **[ディストリビューター ログイン]** 、および **[パブリッシャー ログイン]** (マージ レプリケーションの場合のみ)  
  
    -   **[Web サーバー情報]** (SQL Server 2005 以降を実行しているサブスクライバー上のマージ サブスクリプションの場合)  
  
    -   **その他**  
  
     すべての接続で Windows 認証を使用することをお勧めします。 ディストリビューション エージェントおよびマージ エージェントで必要な権限については、「 [Replication Agent Security Model](security/replication-agent-security-model.md)」を参照してください。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-pull-subscription-from-synchronization-manager"></a>同期マネージャーからプル サブスクリプションを削除するには  
  
1.  **[同期する項目]** ダイアログ ボックスでサブスクリプションを選択し、次に **[プロパティ]** をクリックします。  
  
2.  **[SQL Server サブスクリプション プロパティ]** ダイアログ ボックスで、 **[サブスクリプションの削除]** をクリックします。  
  
3.  **[サブスクリプションの削除]** ダイアログ ボックスで、オプションを選択します。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-use-the-interactive-resolver"></a>インタラクティブ競合回避モジュールを使用するには  
  
1.  アーティクルおよびサブスクリプションで、対話型の競合回避を有効にします。 詳細については、「[マージ アーティクルのインタラクティブな競合回避の指定](../../relational-databases/replication/publish/specify-merge-replication-properties.md#interactive-conflict-resolution)」を参照してください。
  
2.  対話型の競合回避が有効になっており、1 つ以上のアーティクルで競合があると、同期マネージャーでサブスクリプションの同期が開始された後、インタラクティブ競合回避モジュールが自動的に起動されます。 インタラクティブ競合回避モジュールは、一度に 1 つずつ、競合および (パブリケーションとサブスクリプションの作成時に指定した回避モジュールに基づく) 推奨の回避方法を表示します。  
  
3.  必要に応じて、インタラクティブ競合回避モジュールに表示された任意の列を編集し、以下のボタンのいずれかをクリックして競合を回避します。  
  
    -   **[推奨設定を優先]**  
  
    -   **[パブリッシャーを優先]**  
  
    -   **[サブスクライバーを優先]**  
  
    -   **[残りの競合を自動的に解決]** (それ以上入力を行わなくても、現在のすべての競合が回避されます)  
  
     選択した行がパブリッシャーやサブスクライバーに適用され、以降の同期の際にトポロジ内の他のノードに反映されます。  
  
> [!NOTE]  
>  編集した内容は、回避を選択した行の一部でなければ適用されません。 たとえば、 **[パブリッシャー]** の下を編集し、 **[サブスクライバーを優先]** をクリックしても、編集内容は破棄されます。  
  
## <a name="see-also"></a>参照  
 [インタラクティブな競合解決](merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
