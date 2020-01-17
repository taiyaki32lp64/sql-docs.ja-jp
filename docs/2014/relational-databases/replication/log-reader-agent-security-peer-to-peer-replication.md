---
title: '[ログ リーダー エージェントのセキュリティ] (ピア ツー ピア レプリケーション) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.LRA.f1
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d6bcf7d78fd550404f81f9cc303414303ad82504
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63000359"
---
# <a name="log-reader-agent-security-peer-to-peer-replication"></a>[ログ リーダー エージェントのセキュリティ] \(ピア ツー ピア レプリケーション)
  **[ログ リーダー エージェントのセキュリティ]** ページを使用すると、各ピアでログ リーダー エージェントが実行され、接続するときに使用されるアカウントを指定できます。 エージェントで必要とされる権限と、レプリケーション セキュリティの推奨事項については、「[レプリケーション エージェントのセキュリティ モデル](security/replication-agent-security-model.md)」および「[レプリケーション セキュリティの推奨事項](security/replication-security-best-practices.md)」を参照してください。  
  
> [!NOTE]  
>  トランザクション レプリケーションを使用してパブリッシュされるデータベースには、それぞれ 1 つのログ リーダー エージェントが存在します。 データベースにログ リーダー エージェントが既に設定されている場合 (このウィザードを以前に実行したときのパブリケーション、または同じデータベースにある他のトランザクション パブリケーションで)、使用されている資格情報をこのウィザードで変更することはできません。 新しい資格情報を指定した場合は無視されます。 資格情報を変更するには、 **[パブリケーションのプロパティ]** ダイアログ ボックスを使用します。 詳細については、「 [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md)」を参照してください。  
  
## <a name="options"></a>および  
 各ピアの行にあるプロパティ ボタン ( **[...]** ) をクリックすると、 **[ログ リーダー エージェントのセキュリティ]** ダイアログ ボックスが開きます。 エージェントで使用されるアカウントに必要な権限の詳細については、 **[ログ リーダー エージェントのセキュリティ]** ダイアログ ボックスを開いて **[ヘルプ]** をクリックしてください。  
  
 このダイアログ ボックスに設定値を入力すると、サブスクライバーへの接続情報がグリッドに表示されます。  
  
 **[パブリッシャーのエージェント]**  
 各ピア サーバー インスタンスの名前です。  
  
 **[ピア データベース]**  
 各ピアでパブリケーション データベースおよびサブスクリプション データベースとして機能するデータベースです。  
  
 **[ディストリビューターへの接続]**  
 ディストリビューターに接続するコンテキストを作成します。 ディストリビューターへのローカル接続は常に、エージェントの実行に使用される [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントのコンテキストを使用して作成されます。そのため、このフィールドには常に **['\<Domain>\\<Login\>' の権限を借用する]** または **['\<Computer>\\<Login\>' の権限を借用する]** と表示されます。  
  
 **[パブリッシャーへの接続]**  
 パブリッシャーへの接続が作成されるときのコンテキストです。 パブリッシャーへの接続は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン、またはエージェントが実行される Windows アカウントのコンテキストを使用して作成できます。 このフィールドには、次のいずれかが表示されます。 **[ログイン '\<Login>' を使用する]** 、 **['\<ドメイン>\\<ログイン\>' の権限を借用する]** 、 **['\<コンピューター>\\<ログイン\>' の権限を借用する]** 。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、Windows アカウントのコンテキストを使用して、すべての接続を作成することをお勧めします。  
  
## <a name="see-also"></a>参照  
 [ピア ツー ピア トポロジの管理 &#40;レプリケーション Transact-SQL プログラミング&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [@loopback_detection](transactional/peer-to-peer-transactional-replication.md)  
  
  
