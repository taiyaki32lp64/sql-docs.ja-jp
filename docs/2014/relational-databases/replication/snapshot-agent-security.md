---
title: '[スナップショット エージェントのセキュリティ] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.SSA.f1
helpviewer_keywords:
- Snapshot Agent Security dialog box
ms.assetid: 64e84c67-acc6-4906-98d4-3451767363fe
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1e63cee642738036933b0a1e2a9da6b48192fba9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62676638"
---
# <a name="snapshot-agent-security"></a>[スナップショット エージェントのセキュリティ]
  **[スナップショット エージェントのセキュリティ]** ダイアログ ボックスを使用すると、次の項目を指定できます。  
  
-   ディストリビューターでスナップショット エージェントを実行するときに使用される [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウント。 エージェント プロセスがこのアカウントで実行されるため、Windows アカウントは *プロセス アカウント*とも呼ばれます。  
  
-   スナップショット エージェントから [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリッシャーへの接続に使用されるコンテキスト。 接続は、Windows アカウントを借用して作成されるか、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントのコンテキストで作成されます。  
  
    > [!NOTE]  
    >  パブリッシャーとディストリビューターが同じコンピューターに置かれている場合でも、スナップショット エージェントからパブリッシャーへの接続が作成されます。 スナップショット エージェントからディストリビューターへの接続も作成されます。これらの接続は常に、エージェントの実行に使用される Windows アカウントを借用して作成されます。  
  
     Oracle パブリッシャーの場合、スナップショット エージェントからパブリッシャーへの接続に使用されるコンテキストを **[パブリッシャーのプロパティ]** ダイアログ ボックス ( **[ディストリビューターのプロパティ]** ダイアログ ボックスから開きます) で指定します。 詳細については、「 [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md)」を参照してください。  
  
 各アカウントに正しいパスワードが指定され、すべてのアカウントが有効である必要があります。 アカウントとパスワードは、エージェントが実行されるまで検証されません。  
  
## <a name="options"></a>および  
 **Process account**  
 ディストリビューターでスナップショット エージェントを実行するときに使用される  Windows アカウントを入力します。 指定する Windows アカウントは、次の条件を満たしている必要があります。  
  
-   最低でも、ディストリビューション データベースで **db_owner** 固定データベース ロールのメンバーである。  
  
-   スナップショット共有に対する書き込み権限がある。  
  
 **[パスワード]** と **[パスワードの確認入力]**  
 Windows アカウントのパスワードを入力します。  
  
 **[パブリッシャーに接続]**  
 **[プロセス アカウント]** テキスト ボックスで指定されたアカウントを借用するか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントを使用して、スナップショット エージェントからパブリッシャーへの接続を作成するかどうかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントの使用を選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインとパスワードを入力します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントの使用ではなく、Windows アカウントの借用を選択することをお勧めします。  
  
 接続に使用される Windows アカウントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントは、少なくとも、パブリケーション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーションのログインとパスワードの管理](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [レプリケーション エージェントのセキュリティ モデル](security/replication-agent-security-model.md)   
 [レプリケーション エージェントの概要](agents/replication-agents-overview.md)   
 [レプリケーション セキュリティの推奨事項](security/replication-security-best-practices.md)  
  
  
