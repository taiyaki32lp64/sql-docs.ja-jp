---
title: '[ログ リーダー エージェントのセキュリティ] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.LRA.f1
helpviewer_keywords:
- Log Reader Agent Security dialog box
ms.assetid: d6981e74-ddb8-41b8-9ea1-56c2ece63b8a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c55292aff126d1955c438c9417ce0651cc6afc94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162233"
---
# <a name="log-reader-agent-security"></a>[ログ リーダー エージェントのセキュリティ]
  **[ログ リーダー エージェントのセキュリティ]** ダイアログ ボックスを使用すると、次の指定ができます。  
  
-   ログ リーダー エージェントをディストリビューターで実行する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウント。 エージェント プロセスがこのアカウントで実行されるため、Windows アカウントは *プロセス アカウント*とも呼ばれます。  
  
-   ログ リーダー エージェントが [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリッシャーへの接続を作成するコンテキスト。 接続は、Windows アカウントを借用して作成されるか、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントのコンテキストで作成されます。  
  
    > [!NOTE]  
    >  パブリッシャーおよびディストリビューターが同じコンピューター上にある場合でも、ログ リーダー エージェントはパブリッシャーへの接続を作成します。 ログ リーダー エージェントはディストリビューターへの接続も作成します。これらの接続は必ず、エージェントが実行される Windows アカウントを借用して作成されます。  
  
     Oracle パブリッシャーの場合、ログ リーダー エージェントがパブリッシャーに接続するコンテキストを **[パブリッシャーのプロパティ]** ダイアログ ボックス ( **[ディストリビューターのプロパティ]** ダイアログ ボックスから使用可能) で指定します。 詳細については、「 [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md)」を参照してください。  
  
 各アカウントに正しいパスワードが指定され、すべてのアカウントが有効である必要があります。 アカウントとパスワードは、エージェントが実行されるまで検証されません。  
  
## <a name="options"></a>および  
 **[プロセス アカウント]**  
 ログ リーダー エージェントをディストリビューターで実行する Windows アカウントを入力します。 指定した Windows アカウントは少なくともディストリビューション データベースで **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
 **[パスワード]** と **[パスワードの確認入力]**  
 Windows アカウントのパスワードを入力します。  
  
 **[パブリッシャーに接続]**  
 ログ リーダー エージェントがパブリッシャーに接続するのに **[プロセス アカウント]** テキスト ボックスで指定されたアカウントを借用する必要があるか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントを使用する必要があるかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントの使用を選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインとパスワードを入力します。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアカウントの使用ではなく、Windows アカウントの借用を選択することをお勧めします。  
  
 接続に使用される Windows アカウントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントは、少なくとも、パブリケーション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
## <a name="see-also"></a>参照  
 [レプリケーションのログインとパスワードの管理](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [レプリケーション エージェントのセキュリティ モデル](security/replication-agent-security-model.md)   
 [レプリケーション エージェントの概要](agents/replication-agents-overview.md)   
 [レプリケーション セキュリティの推奨事項](security/replication-security-best-practices.md)  
  
  
