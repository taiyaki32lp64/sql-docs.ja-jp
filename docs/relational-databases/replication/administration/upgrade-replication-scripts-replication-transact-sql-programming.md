---
title: レプリケーション スクリプトのアップグレード (レプリケーション SP)
description: レプリケーション ストアド プロシージャを使用して、レプリケーション トポロジをプログラムで構成するために使用するスクリプトをアップグレードする方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server replication], upgrading
- upgrading SQL Server, replicated databases
- upgrading replication applications
- replication [SQL Server], scripting
- replication [SQL Server], upgrading
- upgrading replicated databases
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 0d582af912f94fe0e0755340eb4d5ace892e72da
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75320046"
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>レプリケーション スクリプトのアップグレード (レプリケーション Transact-SQL プログラミング)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプト ファイルを使用して、レプリケーション トポロジをプログラムで構成できます。 詳細については、「[Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)」 (レプリケーション システム ストアド プロシージャの概念) を参照してください。  
  
> [!IMPORTANT]  
>  **sysadmin** ロールのメンバーが実行するスクリプトについては、アップグレードは必須ではありませんが、このトピックの説明に従って既存のスクリプトを変更することをお勧めします。 「 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)」の「エージェントに必要な権限」に記載されている各レプリケーション エージェントの最小権限を持つアカウントを指定します。  
  
 このようにセキュリティが強化されたことで、レプリケーション エージェント ジョブの実行に使用される [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows アカウントを明示的に指定できるため、権限をより詳細に設定できます。既存のスクリプトに含まれる次のストアド プロシージャは、このセキュリティ強化の影響を受けます。  
  
-   **sp_addpublication_snapshot**  
  
     [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行して、スナップショット エージェントをディストリビューターで実行するジョブを作成するときに、Windows 資格情報を `@job_login` および `@job_password` に指定することが必要になりました。  
  
-   **sp_addpushsubscription_agent**  
  
     [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) を実行して、ジョブを明示的に追加し、ディストリビューターでディストリビューション エージェント ジョブを実行する Windows 資格情報 (`@job_login` および `@job_password`) を指定することが必要になりました。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] よりも前のバージョンの [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]では、プッシュ サブスクリプションが作成されるときにこの操作が自動的に実行されました。  
  
-   **sp_addmergepushsubscription_agent**  
  
     [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) を実行して、ジョブを明示的に追加し、ディストリビューターでマージ エージェント ジョブを実行する Windows 資格情報 (`@job_login` および `@job_password`) を指定することが必要になりました。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] よりも前のバージョンの [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]では、プッシュ サブスクリプションが作成されるときにこの操作が自動的に実行されました。  
  
-   **sp_addpullsubscription_agent**  
  
     [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) を実行して、ディストリビューション エージェントをサブスクライバーで実行するジョブを作成するときに、Windows 資格情報を `@job_login` および `@job_password` に指定することが必要になりました。  
  
-   **sp_addmergepullsubscription_agent**  
  
     [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) を実行して、マージ エージェントをサブスクライバーで実行するジョブを作成するときに、Windows 資格情報を `@job_login` および `@job_password` に指定することが必要になりました。  
  
-   **sp_addlogreader_agent**  
  
     [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) を実行して、ジョブを手動で追加し、ログ リーダー エージェントをディストリビューターで実行するときに使用する Windows 資格情報を入力することが必要になりました。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] よりも前のバージョンの [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]では、トランザクション パブリケーションが作成されるときにこの操作が自動的に実行されました。  
  
-   **sp_addqreader_agent**  
  
     [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) を実行して、ジョブを手動で追加し、キュー リーダー エージェントをディストリビューターで実行するときに使用する Windows 資格情報を入力することが必要になりました。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] よりも前のバージョンの [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]では、キュー更新をサポートするトランザクション パブリケーションが作成されるときにこの操作が自動的に実行されました。  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] で導入されたセキュリティ モデルでは、レプリケーション エージェントは常に `@job_name` と `@job_password` に指定された資格情報を使用して Windows 認証を行い、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスに接続します。 レプリケーション エージェント ジョブを実行する際に使用する Windows アカウントの要件の詳細については、「 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納した場合は、ファイル自体が暗号化されていることを確認してください。  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションを構成するスクリプトをアップグレードするには  
  
1.  既存のスクリプトで、[sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) の前に、パブリッシャー側のパブリケーション データベースに [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) を実行します。 ログ リーダー エージェントの実行に使用される Windows 資格情報を、`@job_name` および `@job_password` で指定します。 パブリッシャーに接続するときにエージェントで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証が使用される場合は、`@publisher_security_mode` に **0** を指定し、`@publisher_login` と `@publisher_password` に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン情報を指定する必要もあります。 これにより、パブリケーション データベース用のログ リーダー エージェント ジョブが作成されます。  
  
    > [!NOTE]  
    >  この手順はトランザクション パブリケーションにのみ適用されます。スナップショット パブリケーションの場合は不要です。  
  
2.  (省略可能) [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) の前に、ディストリビューター側のディストリビューション データベースに [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) を実行します。 キュー リーダー エージェントの実行に使用される Windows 資格情報を、`@job_name` および `@job_password` で指定します。 これにより、ディストリビューター用のキュー リーダー エージェント ジョブが作成されます。  
  
    > [!NOTE]  
    >  この手順は、キュー更新サブスクライバーをサポートするトランザクション パブリケーションでのみ必要です。  
  
3.  (省略可) [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) の実行を更新して、新しいレプリケーション機能を実装するパラメーターに既定以外の値を設定します。  
  
4.  パブリッシャー側のパブリケーション データベースに対して、[sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) の後に、[sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 `@publication` を指定し、スナップショット エージェントの実行に使用する Windows 資格情報を `@job_name` と `@job_password` で指定します。 パブリッシャーに接続するときにエージェントで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証が使用される場合は、`@publisher_security_mode` に **0** を指定し、`@publisher_login` と `@publisher_password` に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン情報を指定する必要もあります。 これにより、パブリケーション用のスナップショット エージェント ジョブが作成されます。  
  
5.  (省略可) [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) の実行を更新して、新しいレプリケーション機能を実装するパラメーターに既定以外の値を設定します。  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションにサブスクリプションを追加するスクリプトをアップグレードするには  
  
1.  サブスクリプションを作成するストアド プロシージャを実行した後、ディストリビューション エージェント ジョブを作成するストアド プロシージャを実行して、サブスクリプションを同期するようにしてください。 使用するストアド プロシージャは、サブスクリプションの種類に応じて変わります。  
  
    -   プル サブスクリプションの場合、[sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) の実行を更新して、サブスクライバーでディストリビューション エージェントを実行するときの Windows 資格情報を `@job_name` と `@job_password` に指定します。 この操作は、 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)の実行後に行われます。 詳細については、「 [プル サブスクリプションの作成](../../../relational-databases/replication/create-a-pull-subscription.md)」をご覧ください。  
  
    -   プッシュ サブスクリプションの場合、パブリッシャーで、[sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) を実行します。 `@subscriber`、`@subscriber_db`、`@publication` を指定し、ディストリビューション エージェントをディストリビューターで実行するときの Windows 資格情報を `@job_name` および `@job_password` で指定して、このエージェント ジョブのスケジュールを指定します。 詳細については、「 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)」を参照してください。 この操作は、 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行後に行われます。 詳細については、「 [プッシュ サブスクリプションの作成](../../../relational-databases/replication/create-a-push-subscription.md)」をご覧ください。  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>マージ パブリケーションを構成するスクリプトをアップグレードするには  
  
1.  (省略可) 既存のスクリプトで、[sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) の実行を更新して、新しいレプリケーション機能を実装するパラメーターに既定以外の値を設定します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) の後に、[sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 `@publication` を指定し、スナップショット エージェントの実行に使用する Windows 資格情報を `@job_name` と `@job_password` で指定します。 パブリッシャーに接続するときにエージェントで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証が使用される場合は、`@publisher_security_mode` に **0** を指定し、`@publisher_login` と `@publisher_password` に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン情報を指定する必要もあります。 これにより、パブリケーション用のスナップショット エージェント ジョブが作成されます。  
  
3.  (省略可) [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) の実行を更新して、新しいレプリケーション機能を実装するパラメーターに既定以外の値を設定します。  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>マージ パブリケーションにサブスクリプションを追加するスクリプトをアップグレードするには  
  
1.  サブスクリプションを作成するストアド プロシージャを実行した後、マージ エージェント ジョブを作成するストアド プロシージャを実行して、サブスクリプションを同期するようにしてください。 使用するストアド プロシージャは、サブスクリプションの種類に応じて変わります。  
  
    -   プル サブスクリプションの場合、[sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) の実行を更新して、サブスクライバーでマージ エージェントを実行するときの Windows 資格情報を `@job_name` と `@job_password` に指定します。 この操作は、 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)の実行後に行われます。 詳細については、「 [プル サブスクリプションの作成](../../../relational-databases/replication/create-a-pull-subscription.md)」をご覧ください。  
  
    -   プッシュ サブスクリプションの場合、パブリッシャーで、[sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) を実行します。 `@subscriber`、`@subscriber_db`、`@publication` を指定し、マージ エージェントをディストリビューターで実行するときの Windows 資格情報を `@job_name` および `@job_password` で指定して、このエージェント ジョブのスケジュールを指定します。 詳細については、「 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)」を参照してください。 この操作は、 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)の実行後に行われます。 詳細については、「 [プッシュ サブスクリプションの作成](../../../relational-databases/replication/create-a-push-subscription.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次に、Product テーブルに関するトランザクション パブリケーションを作成する [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] スクリプトの例を示します。 このパブリケーションでは、フェールオーバーとしてキュー更新を使用する即時更新がサポートされます。 読みやすくするために、既定のパラメーターは削除されています。  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_1.sql)]  
  
## <a name="example"></a>例  
 次に、トランザクション パブリケーションを作成する古いスクリプトをアップグレードする例を示します。これは [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンで正常に実行されます。 このパブリケーションでは、フェールオーバーとしてキュー更新を使用する即時更新がサポートされます。 新しいパラメーターの既定値は、明示的に宣言されています。  
  
> [!NOTE]  
>  Windows 資格情報は、 **sqlcmd** スクリプト変数を使用して実行時に指定されます。  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_2.sql)]  
  
## <a name="example"></a>例  
 次に、Customers テーブルに関するマージ パブリケーションを作成する [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] スクリプトの例を示します。 読みやすくするために、既定のパラメーターは削除されています。  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_3.sql)]  
  
## <a name="example"></a>例  
 次に、マージ パブリケーションを作成する古いスクリプトの例を示します。アップグレードすることにより、 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンで正常に実行されます。 新しいパラメーターの既定値は、明示的に宣言されています。  
  
> [!NOTE]  
>  Windows 資格情報は、 **sqlcmd** スクリプト変数を使用して実行時に指定されます。  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_4.sql)]  
  
## <a name="example"></a>例  
 次に、トランザクション パブリケーションへのプッシュ サブスクリプションを作成する [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] スクリプトの例を示します。 読みやすくするために、既定のパラメーターは削除されています。  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_5.sql)]  
  
## <a name="example"></a>例  
 次に、トランザクション パブリケーションへのプッシュ サブスクリプションを作成する古いスクリプトの例を示します。アップグレードすることにより、 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンで正常に実行されます。 新しいパラメーターの既定値は、明示的に宣言されています。  
  
> [!NOTE]  
>  Windows 資格情報は、 **sqlcmd** スクリプト変数を使用して実行時に指定されます。  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_6.sql)]  
  
## <a name="example"></a>例  
 次に、マージ パブリケーションへのプッシュ サブスクリプションを作成する [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] スクリプトの例を示します。 読みやすくするために、既定のパラメーターは削除されています。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>例  
 次に、マージ パブリケーションへのプッシュ サブスクリプションを作成する古いスクリプトの例を示します。アップグレードすることにより、 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンで正常に実行されます。 新しいパラメーターの既定値は、明示的に宣言されています。  
  
> [!NOTE]  
>  Windows 資格情報は、 **sqlcmd** スクリプト変数を使用して実行時に指定されます。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_8.sql)]  
  
## <a name="example"></a>例  
 次に、トランザクション パブリケーションへのプル サブスクリプションを作成する [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] スクリプトの例を示します。 読みやすくするために、既定のパラメーターは削除されています。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>例  
 次に、トランザクション パブリケーションへのプル サブスクリプションを作成する古いスクリプトの例を示します。アップグレードすることにより、 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンで正常に実行されます。 新しいパラメーターの既定値は、明示的に宣言されています。  
  
> [!NOTE]  
>  Windows 資格情報は、 **sqlcmd** スクリプト変数を使用して実行時に指定されます。  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_9.sql)]  
  
## <a name="example"></a>例  
 次に、マージ パブリケーションへのプル サブスクリプションを作成する [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] スクリプトの例を示します。 読みやすくするために、既定のパラメーターは削除されています。  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_10.sql)]  
  
## <a name="example"></a>例  
 次に、マージ パブリケーションへのプル サブスクリプションを作成する古いスクリプトの例を示します。アップグレードすることにより、 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンで正常に実行されます。 新しいパラメーターの既定値は、明示的に宣言されています。  
  
> [!NOTE]  
>  Windows 資格情報は、 **sqlcmd** スクリプト変数を使用して実行時に指定されます。  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_11.sql)]  
  
## <a name="see-also"></a>参照  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [ssSDSFull](../../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)   
 [レプリケーションのセキュリティ設定の表示および変更](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../../../relational-databases/replication/mssql-eng021797.md)   
 [MSSQL_ENG021798](../../../relational-databases/replication/mssql-eng021798.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [レプリケートされたデータベースのアップグレード](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
