---
title: レプリケーション モニターのパブリッシャーの追加および削除 (SSMS)
description: SQL Server Management Studio (SSMS) でレプリケーション モニターのパブリッシャーを追加および削除する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, adding and removing Publishers
ms.assetid: fa36c4b4-bfa5-494e-92e3-07a02d7332c3
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: d46f710bfae73527f414017108954bf4e9129f8f
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75320771"
---
# <a name="add-and-remove-publishers-from-replication-monitor"></a>レプリケーション モニターのパブリッシャーの追加および削除
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  パブリッシャーになっているサーバーからレプリケーション モニターを起動すると、そのサーバーは自動的にモニターに追加されます。 その他のパブリッシャーを追加するには、 **[パブリッシャーの追加]** ダイアログ ボックスを使用します。 追加したパブリッシャーは、モニターの左ペインのグループの中に表示されます。 既定で **[マイ パブリッシャー]** グループが含まれていますが、新しいグループを作成して、1 つ以上のレプリケーション トポロジを管理できます。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
### <a name="to-add-a-sql-server-publisher"></a>SQL Server パブリッシャーを追加するには  
  
1.  左ペインで **[レプリケーション モニター]** ノードまたはパブリッシャー グループのノードを右クリックし、 **[パブリッシャーの追加]** をクリックします。  
  
2.  **[パブリッシャーの追加]** ダイアログ ボックスで、 **[追加]** をクリックし、 **[SQL Server パブリッシャーの追加]** をクリックします。  
  
3.  **[サーバーへの接続]** ダイアログ ボックスで、パブリッシャーの名前を入力し、認証の種類を選択します。 **[SQL Server 認証]** を選択した場合は、ログインとパスワードを入力します。 指定した資格情報はレプリケーション モニターによって保存され、今後このサーバーに接続するときに使用されます。 指定する Windows アカウントまたは SQL Server ログインは、固定サーバーロール **sysadmin** またはディストリビューション データベースの固定データベース ロール **replmonitor** のメンバーである必要があります。  
  
4.  **[接続]** をクリックします。 パブリッシャーがリモート ディストリビューターを使用している場合は、ディストリビューターに接続するための **[サーバーへの接続]** ダイアログ ボックスが表示されます。 指定した資格情報はレプリケーション モニターによって保存され、今後このサーバーに接続するときに使用されます。 指定する Windows アカウントまたは SQL Server ログインは、固定サーバーロール **sysadmin** またはディストリビューション データベースの固定データベース ロール **replmonitor** のメンバーである必要があります。  
  
5.  パブリッシャーとディストリビューターの名前が、 **[次のパブリッシャーの監視を開始します]** グリッドに表示されます。  
  
6.  パブリッシャーに対して更新や接続のオプションを指定するには、グリッドでパブリッシャーを選択し、必要に応じてオプションを変更します。 更新オプションの詳細については、「 [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)」を参照してください。  
  
7.  レプリケーション モニターでパブリッシャーを表示するグループを選択します。 新しいグループを作成するには、 **[新しいグループ]** をクリックし、グループ名を入力します。次に、 **[このパブリッシャーを次のグループに表示する]** ボックスの一覧でそのグループを選択します。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-an-oracle-publisher"></a>Oracle パブリッシャーを追加するには  
  
1.  左ペインで **[レプリケーション モニター]** ノードまたはパブリッシャー グループのノードを右クリックし、 **[パブリッシャーの追加]** をクリックします。  
  
2.  **[パブリッシャーの追加]** ダイアログ ボックスで、 **[追加]** をクリックし、 **[Oracle パブリッシャーの追加]** をクリックします。  
  
3.  **[サーバーへの接続]** ダイアログ ボックスで、Oracle パブリッシャーに関連付けられている [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターの名前を入力し、認証の種類を選択します。 **[SQL Server 認証]** を選択した場合は、ログインとパスワードを入力します。 指定した資格情報はレプリケーション モニターによって保存され、今後このサーバーに接続するときに使用されます。 指定する Windows アカウントまたは SQL Server ログインは、固定サーバーロール **sysadmin** またはディストリビューション データベースの固定データベース ロール **replmonitor** のメンバーである必要があります。  
  
4.  **[接続]** をクリックします。  
  
5.  パブリッシャーとディストリビューターの名前が、 **[次のパブリッシャーの監視を開始します]** グリッドに表示されます。  
  
6.  パブリッシャーに対して更新や接続のオプションを指定するには、グリッドでパブリッシャーを選択し、必要に応じてオプションを変更します。 更新オプションの詳細については、「 [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)」を参照してください。  
  
7.  レプリケーション モニターでパブリッシャーを表示するグループを選択します。 新しいグループを作成するには、 **[新しいグループ]** をクリックし、グループ名を入力します。次に、 **[このパブリッシャーを次のグループに表示する]** ボックスの一覧でそのグループを選択します。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-one-or-more-publishers-that-use-the-same-distributor"></a>同じディストリビューターを使用する 1 つ以上のパブリッシャーを追加するには  
  
1.  左ペインで **[レプリケーション モニター]** ノードまたはパブリッシャー グループのノードを右クリックし、 **[パブリッシャーの追加]** をクリックします。  
  
2.  **[パブリッシャーの追加]** ダイアログ ボックスで、 **[追加]** をクリックし、 **[ディストリビューターを指定し、そのパブリッシャーを追加する]** をクリックします。  
  
3.  **[サーバーへの接続]** ダイアログ ボックスで、ディストリビューターの名前を入力し、認証の種類を選択します。 **[SQL Server 認証]** を選択した場合は、ログインとパスワードを入力します。 指定した資格情報はレプリケーション モニターによって保存され、今後このサーバーに接続するときに使用されます。 指定する Windows アカウントまたは SQL Server ログインは、固定サーバーロール **sysadmin** またはディストリビューション データベースの固定データベース ロール **replmonitor** のメンバーである必要があります。  
  
4.  **[接続]** をクリックします。  
  
5.  ディストリビューターと各パブリッシャーの名前が、 **[次のパブリッシャーの監視を開始します]** グリッドに表示されます。 既にレプリケーション モニターに追加されているパブリッシャーはグリッドに表示されません。  
  
6.  パブリッシャーに対して更新や接続のオプションを指定するには、グリッドでパブリッシャーを選択し、必要に応じてオプションを変更します。 更新オプションの詳細については、「 [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)」を参照してください。  
  
7.  レプリケーション モニターでパブリッシャーを表示するグループを選択します。 新しいグループを作成するには、 **[新しいグループ]** をクリックし、グループ名を入力します。次に、 **[このパブリッシャーを次のグループに表示する]** ボックスの一覧でそのグループを選択します。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-modify-settings-for-the-publisher-and-publisher-groups"></a>パブリッシャーおよびパブリッシャー グループの設定を変更するには  
  
1.  左ペインでパブリッシャーを右クリックし、 **[パブリッシャーの設定]** をクリックします。  
  
2.  **[パブリッシャーの設定]** ダイアログ ボックスで設定を変更します。  
  
    -   レプリケーション モニターがサーバーに接続するときに使用する資格情報を変更するには、 **[パブリッシャー接続]** または **[ディストリビューター接続]** をクリックし、 **[サーバーへの接続]** ダイアログ ボックスに資格情報を入力します。  
  
    -   パブリッシャーを別のグループに移動するには、 **[次のパブリッシャーの監視を開始します]** グリッドでパブリッシャーを選択し、 **[このパブリッシャーを次のグループに表示する]** ボックスの一覧で新しいグループを選択します。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-publisher-from-replication-monitor"></a>レプリケーション モニターからパブリッシャーを削除するには  
  
1.  左ペインでパブリッシャーを右クリックします。  
  
2.  **[削除]** をクリックします。  
  
### <a name="to-add-a-publisher-group-to-replication-monitor"></a>レプリケーション モニターにパブリッシャー グループを追加するには  
  
1.  パブリッシャー グループは、パブリッシャーを追加するとき、またはパブリッシャーの設定を変更するときにしか作成できません。 詳細については、パブリッシャーを追加する手順を参照してください。  
  
### <a name="to-remove-a-publisher-group-from-replication-monitor"></a>レプリケーション モニターからパブリッシャー グループを削除するには  
  
1.  すべてのパブリッシャーを別のグループに移動するか、レプリケーション モニターから削除します。 詳細については、このトピックの上記の手順を参照してください。  
  
2.  パブリッシャー グループを右クリックし、 **[削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [[ディストリビューションの構成]](../../../relational-databases/replication/configure-distribution.md)   
 [レプリケーションの監視](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
