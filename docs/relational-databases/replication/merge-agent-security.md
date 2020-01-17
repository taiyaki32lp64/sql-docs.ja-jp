---
title: マージ エージェント セキュリティ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.MA.f1
helpviewer_keywords:
- Merge Agent Security dialog box
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 45cc5e8c2ca3e311704ffd4eb6577d2e934d484a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140724"
---
# <a name="merge-agent-security"></a>[マージ エージェント セキュリティ]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[マージ エージェント セキュリティ]** ダイアログ ボックスを使用すると、マージ エージェントの実行に使用する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントを指定できます。 マージ エージェントは、プッシュ サブスクリプションの場合はディストリビューターで実行され、プル サブスクリプションの場合はサブスクライバーで実行されます。 エージェント プロセスがこのアカウントで実行されるため、Windows アカウントは *プロセス アカウント*とも呼ばれます。 ダイアログ ボックスで使用できる追加オプションは、次に示すアクセスの方法によって異なります。  
  
-   サブスクリプションの新規作成ウィザードからダイアログ ボックスを開いた場合は、マージ エージェントがプッシュ サブスクリプション用にサブスクライバーへの接続を作成するコンテキスト、またはプル サブスクリプション用にパブリッシャーおよびディストリビューターへの接続を作成するコンテキストを指定できます。 Windows アカウントを使用するか、指定した [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントのコンテキストにより、接続を作成できます。  
  
-   **[サブスクリプションのプロパティ]** ダイアログ ボックスから開いた場合は、 **[サブスクライバー接続]** 行または **[パブリッシャー接続]** 行のプロパティ ボタン ( **[...]** ) をクリックして、マージ エージェントによる接続の作成のコンテキストを指定します。 **[サブスクリプションのプロパティ]** ダイアログ ボックスへのアクセスの詳細については、「[プッシュ サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)」および「[プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)」を参照してください。  
  
 各アカウントに正しいパスワードが指定され、すべてのアカウントが有効である必要があります。 アカウントとパスワードは、エージェントが実行されるまで検証されません。  
  
## <a name="options"></a>オプション  
 **Process Account**  
 マージ エージェントの実行に使用する Windows アカウントを入力します。  
  
-   プッシュ サブスクリプションでは、アカウントには次のことが必要です。  
  
    -   最低でも、ディストリビューション データベースで **db_owner** 固定データベース ロールのメンバーである。  
  
    -   PAL のメンバーである。  
  
    -   パブリケーション データベースのユーザーに関連付けられたログインである。  
  
    -   スナップショット共有の読み取り権限を持っている。  
  
-   プル サブスクリプションでは、アカウントは少なくとも、サブスクリプション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
 接続を作成するときにプロセス アカウントを借用する場合、追加の権限が必要です。 **[パブリッシャーおよびディストリビューターに接続]** および **[サブスクライバーに接続]** を参照してください。  
  
 マージ エージェントは [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] のインスタンスで動作しないので、 **[プロセス アカウント]** は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] に対するプル サブスクリプションに指定できません。  
  
 **[パスワード]** と **[パスワードの確認入力]**  
 Windows アカウントのパスワードを入力します。  
  
 **[パブリッシャーおよびディストリビューターに接続]**  
 プッシュ サブスクリプションの場合、パブリッシャーおよびディストリビューターへの接続は、常に **[プロセス アカウント]** テキスト ボックスで指定されたアカウントを借用することによって行われます。  
  
 プル サブスクリプションの場合、マージ エージェントでパブリケーションおよびディストリビューターへの接続を作成するには、 **[プロセス アカウント]** テキスト ボックスで指定されたアカウントを借用するか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントを使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントの使用を選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインとパスワードを入力します。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアカウントの使用ではなく、Windows アカウントの借用を選択することをお勧めします。  
  
 接続に使用する Windows アカウントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントには次のことが必要です。  
  
-   PAL のメンバーである。  
  
-   パブリケーション データベースのユーザーに関連付けられたログインである。  
  
-   ディストリビューション データベースのユーザー (ゲスト ユーザーでも可) に関連付けられたログインである。  
  
-   スナップショット共有の読み取り権限を持っている。  
  
 **[サブスクライバーに接続]**  
 プル サブスクリプションでは、サブスクライバーへの接続は常に **[プロセス アカウント]** テキスト ボックスに指定されたアカウントを借用することによって作成されます。  
  
 プッシュ サブスクリプションの場合、マージ エージェントでパブリケーションおよびディストリビューターへの接続を作成するには、 **[プロセス アカウント]** テキスト ボックスで指定されたアカウントを借用するか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントを使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントの使用を選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインとパスワードを入力します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントの使用ではなく、Windows アカウントの借用を選択することをお勧めします。  
  
 サブスクライバーへの接続に使用される Windows アカウントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントは、少なくとも、サブスクリプション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
## <a name="see-also"></a>参照  
 [レプリケーションのログインとパスワードの管理](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [レプリケーション エージェントのセキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
