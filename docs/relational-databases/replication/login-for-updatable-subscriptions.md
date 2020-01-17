---
title: '[更新可能なサブスクリプション] のログイン | Microsoft Docs'
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3bdb3585647e64ad1a175900263628b607eb0041
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710363"
---
# <a name="login-for-updatable-subscriptions"></a>[更新可能なサブスクリプション] のログイン
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  即時更新するために、このウィザードの **[更新可能なサブスクリプション]** ページで **[レプリケート]** を選択した場合は、パブリッシャーへの接続に使用する、サブスクライバーでのアカウントを指定する必要があります。 
  
 接続はサブスクライバーで起動されるトリガーによって使用され、サブスクライバーに変更を反映します。 このアカウントは、 **[更新可能なサブスクリプション]** ページで **[変更をキューに登録し、可能な場合はコミット]** を選択している場合でも必要です。 サブスクリプションの新規作成ウィザードでは、必要に応じて即時更新に切り替えることができるキュー更新が既定で構成されます。  
  
> **重要!!** 接続用に指定するアカウントには、レプリケーションによってパブリケーション データベース内に作成されるビューのデータの挿入、更新、および削除だけを実行できる権限を与える必要があります。 それ以外の権限は与えないでください。 各サブスクライバーで構成したアカウントに、**syncobj_** _\<HexadecimalNumber>_ の形式で名前が指定されたパブリケーション データベース内のビューに対する権限を与えます。  
  
 接続の種類として、3 つのオプションがあります。  
  
-   定義済みのリンク サーバーまたはリモート サーバー。  
  
-   レプリケーションによって作成されるリンク サーバー。このウィザードで指定した資格情報を使用して接続を行います。  
  
-   レプリケーションによって作成されるリンク サーバー。サブスクライバーで変更を行うユーザーの資格情報を使用して接続を行います。  
  
 最初の 2 つのオプションは、このウィザードで指定できます。 最後のオプションは、[sp_link_publication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) を使用した場合にだけ指定できます。`@security_mode` パラメーターに値 **1** を指定します。  
  
## <a name="options"></a>オプション  
 **[SQL Server 認証を使用して接続するリンク サーバーを作成する]**  
 レプリケーションにより、 **[ログイン]** フィールドおよび **[パスワード]** フィールドに指定された資格情報に基づいてリンク サーバーが作成されます。  
  
 **[ログイン]**  
 このトピックに記載された権限だけを持つ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを入力します。  
  
 **[パスワード]**  
 **[ログイン]** に指定したログインに使用する複雑なパスワードを入力します。  
    
 **[定義済みのリンク サーバーまたはリモート サーバーを使用する]**  
 このオプションを使用するには、定義済みのリンク サーバーまたはリモート サーバーが必要です。 詳細については、「[リンク サーバー &#40;データベース エンジン&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)」および「[リモート サーバー](../../database-engine/configure-windows/remote-servers.md)」を参照してください。 リンク サーバーまたはリモート サーバーに使用するログインに対して複雑なパスワードが設定されていて、このトピックに記載された権限だけが設定されていることを確認してください。  
  
## <a name="see-also"></a>参照  
 [トランザクション パブリケーションの更新可能なサブスクリプションの作成](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [レプリケーションのセキュリティ設定の表示および変更](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [トランザクション レプリケーションの更新可能なサブスクリプション](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
