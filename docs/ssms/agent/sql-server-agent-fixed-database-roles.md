---
title: SQL Server エージェントの固定データベース ロール | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, roles
- SQLAgentUserRole database role
- SQLAgentReaderRole database role
- multiple roles
- security [SQL Server Agent], fixed database roles
- fixed database roles [SQL Server]
- SQLAgentOperatorRole database role
ms.assetid: 719ce56b-d6b2-414a-88a8-f43b725ebc79
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9ae6f9aae067208eedd0ffe6218f703d55e3696f
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304927"
---
# <a name="sql-server-agent-fixed-database-roles"></a>SQL Server エージェントの固定データベース ロール
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、次の **msdb** データベースの固定データベース ロールが用意されています。これらのロールを使用することで、管理者は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントへのアクセスをより細かく制御できます。 特権レベルの低いロールから順に、次に示します。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
上記のどのロールのメンバーでもないユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]に接続しても、オブジェクト エクスプローラーには **[SQL Server エージェント]** ノードは表示されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用するユーザーは、上記のいずれかの固定データベース ロールのメンバーであるか、または固定サーバー ロール **sysadmin** のメンバーである必要があります。  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>SQL Server エージェントの固定データベース ロールの権限  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのデータベース ロールの各権限の相互関係は、同心構造になっています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント オブジェクト (警告、オペレーター、ジョブ、スケジュール、プロキシなど) に対して、高いレベルの特権を持つロールは、低いレベルの特権を持つロールの権限を継承します。 たとえば、最も特権レベルの低い **SQLAgentUserRole** のメンバーが proxy_A へのアクセスを許可された場合、 **SQLAgentReaderRole** および **SQLAgentOperatorRole** の両方のメンバーは、proxy_A へのアクセスが明示的に許可されていなくても、このプロキシへのアクセス権が自動的に与えられていることになります。 これは、セキュリティに影響することがあります。セキュリティ上の影響については、次のセクションの各ロールの説明に記載します。  
  
### <a name="sqlagentuserrole-permissions"></a>SQLAgentUserRole の権限  
**SQLAgentUserRole** には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの固定データベース ロールのうち、最も低い特権レベルが設定されています。 オペレーター、ローカル ジョブ、ジョブ スケジュールのみに対する権限があります。 **SQLAgentUserRole** のメンバーは、所有しているローカル ジョブおよびジョブ スケジュールのみに対する権限を持っています。 このメンバーが、マルチサーバー ジョブ (マスター サーバーとターゲット サーバーのジョブ) を使用することはできません。また、ジョブの所有権を変更して、所有していないジョブへのアクセス権を得ることもできません。 **SQLAgentUserRole** のメンバーは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の **[ジョブ ステップのプロパティ]** ダイアログ ボックスでのみ、使用できるプロキシのリストを表示できます。 **SQLAgentUserRole** のメンバーに対しては、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクト エクスプローラーには **[ジョブ]** ノードだけが表示されます。  
  
> [!IMPORTANT]  
> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** **Agentdatabaseroles** のメンバーに対してプロキシへのアクセスを許可する前に、セキュリティ上の影響について検討してください。 **SQLAgentReaderRole** および **SQLAgentOperatorRole** は、自動的に **SQLAgentUserRole**のメンバーになります。 つまり、 **SQLAgentReaderRole** および **SQLAgentOperatorRole** のメンバーは、 **SQLAgentUserRole** に許可されたすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシにアクセスし、これらのプロキシを使用できることになります。  
  
次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント オブジェクトに対する **SQLAgentUserRole** の権限の概要を示します。  
  
|操作|オペレーター|ローカル ジョブ<br /><br />(所有しているジョブのみ)|ジョブ スケジュール<br /><br />(所有しているスケジュールのみ)|プロキシ|  
|----------|-------------|-----------------------------------|-------------------------------------------|-----------|  
|作成/変更/削除|いいえ|はい<br /><br />ジョブの所有権は変更できません。|はい|いいえ|  
|リストの表示 (列挙)|はい<br /><br />**sp_notify_operator** および Management Studio の **[ジョブのプロパティ]** ダイアログ ボックスで使用できるオペレーターのリストを取得できます。|はい|はい|はい<br /><br />プロキシのリストは、Management Studio の **[ジョブ ステップのプロパティ]** ダイアログ ボックスにのみ表示できます。|  
|有効化/無効化|いいえ|はい|はい|適用なし|  
|プロパティの表示|いいえ|はい|はい|いいえ|  
|実行/停止/開始|適用なし|はい|適用なし|適用なし|  
|ジョブ履歴の表示|適用なし|はい|適用なし|適用なし|  
|ジョブ履歴の削除|適用なし|いいえ<br /><br />所有しているジョブのジョブ履歴を削除するには、 **SQLAgentUserRole** のメンバーは、 **sp_purge_jobhistory** に対する EXECUTE 権限が明示的に許可されている必要があります。 他のジョブのジョブ履歴は削除できません。|適用なし|適用なし|  
|アタッチ/デタッチ|適用なし|適用なし|はい|適用なし|  
  
### <a name="sqlagentreaderrole-permissions"></a>SQLAgentReaderRole の権限  
**SQLAgentReaderRole** には、すべての **SQLAgentUserRole** の権限、および使用できるマルチサーバー ジョブのリスト、ジョブのプロパティ、およびジョブの履歴を表示する権限が含まれています。 このロールのメンバーは、所有しているジョブとジョブ スケジュールだけでなく、使用できるすべてのジョブとジョブ スケジュール、およびそのプロパティのリストを表示することもできます。 **SQLAgentReaderRole** のメンバーは、ジョブの所有権を変更して、所有していないジョブへのアクセス権を得ることはできません。 **SQLAgentReaderRole** のメンバーに対しては、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクト エクスプローラーには **[ジョブ]** ノードだけが表示されます。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agentdatabaseroles** のメンバーに対してプロキシへのアクセスを許可する前に、セキュリティ上の影響について検討してください **。** **SQLAgentReaderRole** のメンバーは、自動的に **SQLAgentUserRole**のメンバーになります。 つまり、 **SQLAgentReaderRole** のメンバーは、 **SQLAgentUserRole** に対して許可されたすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシにアクセスし、これらのプロキシを使用できることになります。  
  
次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント オブジェクトに対する **SQLAgentReaderRole** の権限の概要を示します。  
  
|操作|オペレーター|ローカル ジョブ|マルチサーバー ジョブ|ジョブ スケジュール|プロキシ|  
|----------|-------------|--------------|--------------------|-----------------|-----------|  
|作成/変更/削除|いいえ|可 (所有しているジョブのみ)<br /><br />ジョブの所有権は変更できません。|いいえ|可 (所有しているスケジュールのみ)|いいえ|  
|リストの表示 (列挙)|はい<br /><br />**sp_notify_operator** および Management Studio の **[ジョブのプロパティ]** ダイアログ ボックスで使用できるオペレーターのリストを取得できます。|はい|はい|はい|はい<br /><br />プロキシのリストは、Management Studio の **[ジョブ ステップのプロパティ]** ダイアログ ボックスにのみ表示できます。|  
|有効化/無効化|いいえ|可 (所有しているジョブのみ)|いいえ|可 (所有しているスケジュールのみ)|適用なし|  
|プロパティの表示|いいえ|はい|はい|はい|いいえ|  
|プロパティの編集|いいえ|可 (所有しているジョブのみ)|いいえ|可 (所有しているスケジュールのみ)|いいえ|  
|実行/停止/開始|適用なし|可 (所有しているジョブのみ)|いいえ|適用なし|適用なし|  
|ジョブ履歴の表示|適用なし|はい|はい|適用なし|適用なし|  
|ジョブ履歴の削除|適用なし|いいえ<br /><br />所有しているジョブのジョブ履歴を削除するには、 **SQLAgentReaderRole** のメンバーは、 **sp_purge_jobhistory** に対する EXECUTE 権限が明示的に許可されている必要があります。 他のジョブのジョブ履歴は削除できません。|いいえ|適用なし|適用なし|  
|アタッチ/デタッチ|適用なし|適用なし|適用なし|可 (所有しているスケジュールのみ)|適用なし|  
  
### <a name="sqlagentoperatorrole-permissions"></a>SQLAgentOperatorRole の権限  
**SQLAgentOperatorRole** には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの固定データベース ロールのうち、最も高いレベルの特権が設定されています。 これには、 **SQLAgentUserRole** および **SQLAgentReaderRole**のすべての権限が含まれています。 このロールのメンバーは、オペレーターおよびプロキシのプロパティを表示することも、サーバー上で使用できるプロキシおよび警告を列挙することもできます。  
  
**SQLAgentOperatorRole** のメンバーは、ローカル ジョブおよびスケジュールに関する追加の権限を持っています。 すべてのローカル ジョブを実行、停止、または開始したり、サーバー上のローカル ジョブのジョブ履歴を削除できます。 また、サーバー上のすべてのローカル ジョブおよびスケジュールを、有効または無効にすることもできます。 ローカル ジョブまたはスケジュールを有効または無効にするには、このロールのメンバーはストアド プロシージャ **sp_update_job** および **sp_update_schedule**を使用する必要があります。 **SQLAgentOperatorRole** のメンバーは、ジョブまたはスケジュールの名前か ID を指定するパラメーター、および **\@enabled** パラメーターのみを指定できます。 他のパラメーターを指定すると、ストアド プロシージャの実行は失敗します。 **SQLAgentOperatorRole** のメンバーは、ジョブの所有権を変更して、所有していないジョブへのアクセス権を得ることはできません。  
  
**SQLAgentOperatorRole**のメンバーに対しては、 **オブジェクト エクスプローラーには**[ジョブ] **ノード、** [警告] **ノード、** [オペレーター] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ノード、および **[プロキシ]** ノードのみが表示されます。 このロールのメンバーに表示されないのは、 **[エラー ログ]** ノードだけです。  
  
> [!IMPORTANT]  
> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** の **Agentdatabaseroles** のメンバーに対してプロキシへのアクセスを許可する前に、セキュリティ上の影響について検討してください。 **SQLAgentOperatorRole** のメンバーは、自動的に **SQLAgentUserRole** および **SQLAgentReaderRole**のメンバーになります。 つまり、 **SQLAgentOperatorRole** のメンバーは、 **SQLAgentUserRole** または **SQLAgentReaderRole** に対して許可されたすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシにアクセスし、これらのプロキシを使用できることになります。  
  
次の表に、 **エージェント オブジェクトに対する** SQLAgentOperatorRole [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の権限の概要を示します。  
  
|操作|オブジェクト エクスプローラーには|オペレーター|ローカル ジョブ|マルチサーバー ジョブ|ジョブ スケジュール|プロキシ|  
|----------|----------|-------------|--------------|--------------------|-----------------|-----------|  
|作成/変更/削除|いいえ|いいえ|可 (所有しているジョブのみ)<br /><br />ジョブの所有権は変更できません。|いいえ|可 (所有しているスケジュールのみ)|いいえ|  
|リストの表示 (列挙)|はい|はい<br /><br />**sp_notify_operator** および Management Studio の **[ジョブのプロパティ]** ダイアログ ボックスで使用できるオペレーターのリストを取得できます。|はい|はい|はい|はい|  
|有効化/無効化|いいえ|いいえ|はい<br /><br />**SQLAgentOperatorRole** のメンバーは、ストアド プロシージャ **sp_update_job** を使用し、 **\@enabled** パラメーターおよび **\@job_id** (または **\@job_name**) パラメーターの値を指定することにより、所有していないローカル ジョブを有効または無効にできます。 このロールのメンバーが、このストアド プロシージャに対して他のパラメーターを指定した場合、プロシージャの実行は失敗します。|いいえ|はい<br /><br />**SQLAgentOperatorRole** のメンバーは、ストアド プロシージャ **sp_update_schedule** を使用し、 **\@enabled** パラメーターおよび **\@schedule_id** (または **\@name**) パラメーターの値を指定することにより、所有していないスケジュールを有効または無効にできます。 このロールのメンバーが、このストアド プロシージャに対して他のパラメーターを指定した場合、プロシージャの実行は失敗します。|適用なし|  
|プロパティの表示|はい|はい|はい|はい|はい|はい|  
|プロパティの編集|いいえ|いいえ|可 (所有しているジョブのみ)|いいえ|可 (所有しているスケジュールのみ)|いいえ|  
|実行/停止/開始|適用なし|適用なし|はい|いいえ|適用なし|適用なし|  
|ジョブ履歴の表示|適用なし|適用なし|はい|はい|適用なし|適用なし|  
|ジョブ履歴の削除|適用なし|適用なし|はい|いいえ|適用なし|適用なし|  
|アタッチ/デタッチ|適用なし|適用なし|適用なし|適用なし|可 (所有しているスケジュールのみ)|適用なし|  
  
## <a name="assigning-users-multiple-roles"></a>ユーザーへの複数のロールの割り当て  
固定サーバー ロール **sysadmin** のメンバーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのすべての機能にアクセスできます。 **sysadmin** ロールのメンバーではないが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの複数の固定データベース ロールのメンバーであるユーザーの場合、これらのロールの同心構造権限モデルについて覚えておくことが重要です。 特権レベルの高いロールには常に、そのロールよりも特権レベルが低いロールの権限がすべて含まれているため、複数のロールのメンバーであるユーザーは、そのユーザーがメンバーとして属しているロールの中で、最も特権レベルの高いロールに関連付けられた権限を自動的に持っていることになります。  
  
## <a name="see-also"></a>参照  
[SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)  
[sp_update_job (Transact-SQL)](https://msdn.microsoft.com/cbdfea38-9e42-47f3-8fc8-5978b82e2623)  
[sp_update_schedule (Transact-SQL)](https://msdn.microsoft.com/97b3119b-e43e-447a-bbfb-0b5499e2fefe)  
[sp_notify_operator (Transact-SQL)](https://msdn.microsoft.com/c440f5c9-9884-4196-b07c-55d87afb17c3)  
[sp_purge_jobhistory (Transact-SQL)](https://msdn.microsoft.com/237f9bad-636d-4262-9bfb-66c034a43e88)  
  
