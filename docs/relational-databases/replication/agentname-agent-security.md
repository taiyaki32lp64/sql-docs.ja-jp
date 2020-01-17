---
title: '&lt;AgentName&gt; エージェント セキュリティ | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.agentnameagentsecurity.f1
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: cc3142dfa4a69b961498696961d9838d56fbc572
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770764"
---
# <a name="ltagentnamegt-agent-security"></a>&lt;AgentName&gt; エージェント セキュリティ
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[\<AgentName> エージェント セキュリティ]** ページを使用すると、ディストリビューション エージェント (トランザクション レプリケーションおよびスナップショット レプリケーションの場合) またはマージ エージェント (マージ レプリケーションの場合) が実行されるアカウントを指定し、レプリケーション トポロジ内のコンピューターへの接続を作成することができます。 エージェントで必要とされる権限と、レプリケーション セキュリティの推奨事項については、「[レプリケーション エージェントのセキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)」と「[レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **[ディストリビューション エージェント セキュリティ]** ダイアログ ボックスまたは **[マージ エージェント セキュリティ]** ダイアログ ボックスにアクセスするには、各サブスクライバーの行でプロパティ ボタン ( **[...]** ) をクリックします。 ダイアログ ボックスの **[ヘルプ]** をクリックすると、エージェントによって使用されるアカウントに必要な権限の詳細を参照できます。  
  
 ダイアログ ボックスの 1 つに設定を入力すると、サブスクライバーの接続情報がグリッドに表示されます。  
  
 **[サブスクライバーのエージェント]**  
 各サブスクライバーの名前です。  
  
 **[ディストリビューターへの接続]**  
 トランザクション レプリケーションおよびスナップショット レプリケーションに表示されます。 ディストリビューターに接続するコンテキストを作成します。 ローカル接続は常に、エージェントを実行する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントのコンテキストを使用して作成されます。  
  
-   プッシュ サブスクリプションの場合、ローカル接続はディストリビューターへの接続であるため、このフィールドには常に次が表示されます。 **['\<ドメイン>\\<ログイン\>' の権限を借用する]** または **['\<コンピューター>\\<ログイン\>' の権限を借用する]** (プッシュ サブスクリプションの場合)。  
  
-   プル サブスクリプションの場合、接続は [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのコンテキストでも作成できます。 このフィールドには、次のいずれかが表示されます。 **[ログイン '\<Login>' を使用する]** 、 **['\<ドメイン>\\<ログイン\>' の権限を借用する]** 、 **['\<コンピューター>\\<ログイン\>' の権限を借用する]** 。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、Windows アカウントのコンテキストを使用して、すべての接続を作成することをお勧めします。  
  
 **[パブリッシャーおよびディストリビューターへの接続]**  
 マージ レプリケーションの場合に表示されます。 パブリッシャーおよびディストリビューターに接続するコンテキストを作成します。 ローカル接続は常に、エージェントを実行する Windows アカウントのコンテキストを使用して作成されます。  
  
-   プッシュ サブスクリプションの場合、ローカル接続はパブリッシャーとディストリビューターへの接続であるため、このフィールドには常に次が表示されます。 **['\<ドメイン>\\<ログイン\>' の権限を借用する]** または **['\<コンピューター>\\<ログイン\>' の権限を借用する]** (プッシュ サブスクリプションの場合)。  
  
-   プル サブスクリプションの場合、接続は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのコンテキストでも作成できます。 このフィールドには、次のいずれかが表示されます。 **[ログイン '\<Login>' を使用する]** 、 **['\<ドメイン>\\<ログイン\>' の権限を借用する]** 、 **['\<コンピューター>\\<ログイン\>' の権限を借用する]** 。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、Windows アカウントのコンテキストを使用して、すべての接続を作成することをお勧めします。  
  
 **[サブスクライバーへの接続]**  
 サブスクライバーに接続するコンテキストを作成します。 ローカル接続は常に、エージェントを実行する Windows アカウントのコンテキストを使用して作成されます。  
  
-   プル サブスクリプションの場合、ローカル接続はサブスクライバーへの接続であるため、このフィールドには常に次が表示されます。 **['\<ドメイン>\\<ログイン\>' の権限を借用する]** または **['\<コンピューター>\\<ログイン\>' の権限を借用する]** (プッシュ サブスクリプションの場合)。  
  
-   プッシュ サブスクリプションの場合、接続は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのコンテキストでも作成できます。 このフィールドには、次のいずれかが表示されます。 **[ログイン '\<Login>' を使用する]** 、 **['\<ドメイン>\\<ログイン\>' の権限を借用する]** 、 **['\<コンピューター>\\<ログイン\>' の権限を借用する]** 。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、Windows アカウントのコンテキストを使用して、すべての接続を作成することをお勧めします。  
  
## <a name="see-also"></a>参照  
 [プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [プッシュ サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [ID およびアクセス制御 (レプリケーション)](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [レプリケーション エージェントのセキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [レプリケーションのセキュリティ設定の表示および変更](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
