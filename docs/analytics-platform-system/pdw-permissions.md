---
title: アクセス許可
description: この記事では、並列データウェアハウスのデータベース権限を管理するための要件とオプションについて説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d60c6f492b0735e70a2c3103e48ad08953039adc
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400870"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>並列データウェアハウスでのアクセス許可の管理
この記事では、SQL Server PDW のデータベース権限を管理するための要件とオプションについて説明します。  
  
## <a name="BackupRestoreBasics"></a>データベースエンジンアクセス許可の基本  
SQL Server PDW に対するデータベースエンジン権限は、ログインを通じてサーバーレベルで管理されます。データベースレベルでは、データベースユーザーとユーザー定義データベースロールによって管理されます。  
  
**ログイン**  
ログインは、SQL Server PDW にログオンするための個々のユーザーアカウントです。 SQL Server PDW では、Windows 認証と SQL Server 認証を使用したログインがサポートされます。  Windows 認証ログインは、SQL Server PDW によって信頼されている任意のドメインの Windows ユーザーまたは Windows グループにすることができます。 SQL Server 認証ログインは SQL Server PDW によって定義および認証されるため、パスワードを指定して作成する必要があります。  
  
**Sysadmin**固定サーバーロールのメンバー ( **sa**ログインなど) は、データベースユーザーにマップされていなくてもデータベースに接続できます。 これらは**dbo**ユーザーにマップされます。 また、データベースの所有者は**dbo**ユーザーとしてもマップされます。  
  
**[サーバー ロール]**  
サーバーレベルのアクセス許可の便利なグループを提供する、構成済みの役割のセットを備えた4つの特別なサーバーロールがあります。 **Sysadmin**、 **MediumRC**、 **LargeRC**、 **XLargeRCfixed**の各サーバーロールは、現在 SQL Server PDW で実装されている唯一のサーバーロールです。 **Sa**ログインは**sysadmin**固定サーバーロールの唯一のメンバーであり、 **sysadmin**ロールに追加のログインを追加することはできません。 ログインには、 **sysadmin**固定サーバーロールと同じように、 **CONTROL SERVER**権限を与えることができます。 他のサーバーロールにメンバーを追加するには、 [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)を使用します。 SQL Server PDW は、ユーザー定義のサーバーロールをサポートしていません。  
  
**データベースユーザー**  
ログインには、データベースにデータベースユーザーを作成し、そのデータベースユーザーをログインにマッピングすることによって、データベースへのアクセス権が付与されます。 通常、データベース ユーザー名はログイン名と同じですが、同じにする必要はありません。 各データベース ユーザーは、単一のログインにマッピングされます。 ログインはデータベース内の 1 つのユーザーにのみマッピングできますが、異なる複数のデータベースにデータベース ユーザーとしてマッピングできます。  
  
**固定データベース ロール**  
固定データベースロールは、データベースレベルの権限の便利なグループを提供する、事前に構成されたロールのセットです。 [Sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)プロシージャを使用して、データベースユーザーとユーザー定義データベースロールを固定データベースロールに追加できます。 固定データベースロールの詳細については、「[固定データベースロール](#fixed-database-roles)」を参照してください。  
  
**ユーザー定義データベース ロール**  
**CREATE ROLE**権限を持つユーザーは、一般的な権限を持つユーザーのグループを表すために、新しいユーザー定義データベースロールを作成できます。 通常、権限の管理と監視を簡略化するために、権限はロール全体に対して付与または拒否されます。  
  
権限は、 **GRANT**ステートメントを使用して、セキュリティプリンシパル (ログイン、ユーザー、およびロール) に付与されます。 権限は、 **DENY**コマンドを使用して明示的に拒否されます。 以前に許可または拒否された権限は、 **REVOKE**ステートメントを使用して削除されます。 権限は累積的であるため、ユーザーはユーザー、ログイン、すべてのグループ メンバーシップに付与された権限をすべて受け取ります。ただし、権限の拒否はすべての付与をオーバーライドします。 <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
次の例は、権限を構成する一般的な方法および推奨される方法を示します。  
  
1.  Windows 認証を使用する場合は、SQL Server PDW に接続する Windows ユーザーまたは Windows グループごとにログインを作成します。 SQL Server 認証を使用する場合は、SQL Server PDW に接続するユーザーごとにログインを作成します。  
  
2.  必要なすべてのデータベースのログインごとにデータベースユーザーを作成します。  
  
3.  1つ以上のユーザー定義データベースロールを作成します。それぞれが同様の関数を表します。 たとえば、財務アナリストやセールス アナリストなどです。  
  
4.  1つ以上のユーザー定義データベースロールにデータベースユーザーを追加します。  
  
5.  ユーザー定義データベース ロールに権限を付与します。  
  
ログインはサーバーレベルのオブジェクトであり、 [server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)を表示することによって一覧表示できます。 サーバープリンシパルに対して許可できるのは、サーバーレベルの権限のみです。  
  
ユーザーおよびデータベースロールはデータベースレベルのオブジェクトであり、 [database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)を表示することによって一覧表示できます。 データベースプリンシパルに対して許可できるのは、データベースレベルの権限のみです。  
  
## <a name="BackupTypes"></a>既定の権限  
次に、既定のアクセス許可について説明します。  
  
-   Using **CREATE login**ステートメントによってログインが作成されると、ログインは**connect SQL**権限を受け取り、そのログインが SQL Server PDW に接続できるようになります。  
  
-   **CREATE user**ステートメントを使用してデータベースユーザーを作成すると、ユーザーは**connect ON database::** _<database_name>_ 権限を受け取り、ログインがユーザーとしてそのデータベースに接続できるようになります。  
  
-   暗黙のアクセス許可は明示的なアクセス許可から継承されるため、PUBLIC ロールを含むすべてのプリンシパルには、明示的または暗黙的なアクセス許可が既定でありません。 したがって、明示的なアクセス許可が存在しない場合は、暗黙のアクセス許可もありません。  
  
-   ログインがオブジェクトまたはデータベースの所有者になると、そのログインには常にオブジェクトまたはデータベースに対するすべての権限が与えられます。 所有権のアクセス許可は、明示的なアクセス許可として表示されません。 **GRANT**、 **REVOKE**、および**DENY**ステートメントは、所有権には影響しません。 所有権は、 [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)ステートメントを使用して変更できます。  
  
-   Sa ログインは、アプライアンス上のすべてのアクセス許可を持っています。 所有者のアクセス許可と同様に、sa アクセス許可を変更することはできず、明示的なアクセス許可として表示されません。 **GRANT**、 **REVOKE**、および**DENY**ステートメントは、sa 権限には影響しません。  
  
-   パブリックサーバーロールは、既定ではアクセス許可を受け取りません。また、他のサーバーロールからアクセス許可を継承することもありません。 PUBLIC サーバーロールには、 **GRANT**、 **REVOKE**、および**DENY**ステートメントを使用して明示的な権限を与えることができます。  
  
-   トランザクションにはアクセス許可は必要ありません。 すべてのプリンシパルは、 **BEGIN TRANSACTION**、 **COMMIT**、および**ROLLBACK** TRANSACTION コマンドを実行できます。 ただし、プリンシパルは、トランザクション内で各ステートメントを実行するための適切な権限を持っている必要があります。  
  
-   
  **USE** ステートメントでは、権限は必要ありません。 すべてのプリンシパルは、任意のデータベースで**use**ステートメントを実行できます。ただし、データベースにアクセスするには、データベースにユーザープリンシパルが必要であるか、ゲストユーザーが有効になっている必要があります。  
  
### <a name="the-public-role"></a>パブリックロール  
すべての新しいアプライアンスログインは、自動的に PUBLIC ロールに属します。 パブリックサーバーロールには、次の特性があります。  
  
-   既定では、パブリックサーバーロールにアクセス許可はありません。  
  
-   すべてのプリンシパルが PUBLIC サーバーロールのメンバーであり、PUBLIC サーバーロールが別のサーバーロールのメンバーではありません。  
  
-   PUBLIC サーバーロールは、暗黙的な権限を継承できません。 PUBLIC ロールに与えられた権限は、明示的に付与する必要があります。  
  
## <a name="BackupProc"></a>アクセス許可の決定  
ログインが特定のアクションを実行する権限を持っているかどうかは、ユーザーがメンバーであるログイン、ユーザー、およびロールに対して許可または拒否された権限によって異なります。 サーバーレベルの権限 ( **CREATE LOGIN**や**VIEW server STATE**など) は、サーバーレベルのプリンシパル (ログイン) で使用できます。 データベースレベルの権限 (テーブルからの**選択**やプロシージャの**実行**など) は、データベースレベルのプリンシパル (ユーザーおよびデータベースロール) で使用できます。  
  
### <a name="implicit-and-explicit-permissions"></a>暗黙的および明示的なアクセス許可  

  *明示的なアクセス許可*は、**GRANT** または **DENY** ステートメントによってプリンシパルに付与される **GRANT** または **DENY** アクセス許可です。 データベースレベルの権限は、 [database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)ビューに表示されます。 サーバーレベルの権限は、 [server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)ビューに表示されます。  
  
*暗黙の権限*は、プリンシパル (ログインまたはサーバーロール) によって継承された**GRANT**権限または**DENY**権限です。 アクセス許可は、次の方法で継承できます。  
  
-   プリンシパルが明示的に**GRANT**または**DENY**権限を持っていない場合でも、プリンシパルがロールのメンバーである場合、プリンシパルはロールから権限を継承できます。  
  
-   プリンシパルがいずれかのオブジェクトの親スコープ (テーブルのスキーマやデータベース全体の権限など) に対する権限を持っている場合、プリンシパルは下位のオブジェクト (テーブルなど) に対する権限を継承できます。  
  
-   プリンシパルは、下位のアクセス許可を含むアクセス許可を持つことで、アクセス許可を継承できます。 たとえば、 **alter ANY user**権限には、 **CREATE user**と**alter ON user::** _<name>_ permissions の両方が含まれます。  
  
### <a name="determining-permissions-when-performing-actions"></a>アクションの実行時のアクセス許可の決定  
プリンシパルに割り当てるアクセス許可を決定するプロセスは複雑です。 複数のロールのメンバーになることができるので、ロール階層内の複数のレベルを通じて権限を渡すことができるので、暗黙的な権限を決定するときに複雑さが発生します。  
  
次の一覧では、アクセス許可を決定するための一般的な規則について説明します。  
  
-   所有権は、アクセス許可を意味します。  
  
    オブジェクト所有者は、オブジェクトに対するすべての権限を持っています。 同様に、データベース所有者は、データベースに対するすべての権限と、データベース内のオブジェクトに対するすべての権限を持っています。 これらのアクセス許可は変更できません。  
  
-   権限は、サーバーロールのメンバーシップの階層内の複数のレベルにわたって継承できます。  
  
    たとえば、次のような状況があるとします。  
  
    -   ログイン David は、データベースロール PerfAnalysts のメンバーです。  
  
    -   PerfAnalysts は、データベースロールの実稼働のメンバーです。  
  
    -   David および PerfAnalysts は、Customer テーブルに対する**SELECT 権限を**持っていません。 権限が取り消されたか、明示的に許可されませんでした。  
  
    -   運用環境には、Customer テーブルに対する**SELECT**権限があります。  
  
    この場合、PerfAnalysts は、Customer テーブルに対する**grant**権限を実稼働から継承し、David は、customer テーブルに対する**Grant**権限を実稼働から継承します。  
  
-   権限の競合がある場合は、 **DENY**オーバーライドによって**付与**されます。  
  
    たとえば、login David が Customer テーブルに対する権限を持っておらず、customer テーブルに対して**DENY**権限を持つ2つのデータベースロール dbgroup1 のメンバーであり、かつ customer テーブルに対する**GRANT**権限を持つ dbgroup2 を持つとします。 この場合、David は、Customer テーブルの**DENY**権限を継承します。 これは、ロールが明示的または暗黙的にアクセス許可を取得したかどうかです。  
  
### <a name="auditing-permissions"></a>監査のアクセス許可  
ユーザーのアクセス許可を調べるには、次のチェックボックスをオンにします。  
  
-   システム管理者であるログインを確認するには、次のクエリを実行します。  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   次のクエリを実行して、明示的なアクセス許可が付与されているログインを特定します。  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   ユーザーデータベースで次のクエリを実行し、データベースロールのメンバーであるデータベースユーザーを特定します。  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   ユーザーデータベースで次のクエリを実行し、特定のアクセス許可が付与または拒否されているデータベースユーザーとロールを確認します。 Major_id で説明されている項目を識別するには、sys. オブジェクトや sys スキーマなどの追加のビューに対してクエリを実行する必要があります。  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>データベースアクセス許可のベストプラクティス  
  
-   実用的な最も細かいレベルでアクセス許可を付与します。 テーブルまたはビューレベルの権限で権限を許可すると、管理不能になる可能性があります。 ただし、データベースレベルで権限を許可すると、制限が緩くなる可能性があります。 データベースが、作業の境界を定義するスキーマを使用して設計されている場合、スキーマに対する権限の許可が、テーブルレベルとデータベースレベルの間で適切なセキュリティ侵害を行う可能性があります。  
  
-   ユーザーまたはログインではなく、ロールに権限を付与します。 ユーザーの代わりにロールを使用して権限を管理することにより、ユーザーまたはログインの権限をロールに移動することによって簡単にアクセス許可を付与または取り消すことができます。 関数がある人から別のユーザーに渡されると、ロールのメンバーシップが変更されても、ロールレベルでは、権限はそのまま維持されます。  
  
-   ジョブの機能に基づいてロールに権限を付与し、アクションを実行する会社グループに基づいてジョブ関数のロールを組み合わせる上位レベルのグループロールに対して権限を付与します。  
  
-   すべてのエンドユーザーには、一意のログインが必要です。 ユーザーがログインを共有できないようにします。 各ユーザーにログインを提供すると、監査証跡が確保され、アクセス許可の管理が容易になります。  
  
## <a name="fixed-database-roles"></a>固定データベース ロール
SQL Server には、サーバーに対する権限の管理に役立つ、事前に構成された (固定) データベースレベルのロールが用意されています。 事前に構成されたロールは、割り当てられたアクセス許可を変更できないということで修正されています。 ユーザー定義のデータベースロールを作成することもできます。 ユーザー定義のデータベースロールに割り当てられている権限を変更できます。  
  
ロールは、他のプリンシパルをグループ化するセキュリティプリンシパルです。 データベースロールは、アクセス許可のスコープでデータベース全体に適用されます。 データベースユーザーとその他のデータベースロールは、データベースロールのメンバーとして追加できます。 固定データベースロールを相互に追加することはできません。 (*ロール* は、Windows オペレーティング システムの *グループ* に似ています)。  
  
固定データベースロールは9つあります。  
  
-   **db_owner**  
  
-   **db_securityadmin**  
  
-   **db_accessadmin**  
  
-   **db_backupoperator**  
  
-   **db_ddladmin**  
  
-   **db_datawriter**  
  
-   **db_datareader**  
  
-   **db_denydatawriter**  
  
-   **db_denydatareader**  
  
### <a name="permissions-of-the-fixed-database-roles"></a>固定データベースロールの権限  
固定サーバーロールと固定データベースロールのシステムは、1980年に発行されたレガシシステムです。 固定ロールは引き続きサポートされており、ユーザー数が少ない環境や、セキュリティニーズがシンプルな環境で役に立ちます。 SQL Server 2005 以降では、権限を付与するより詳細なシステムが作成されました。 この新しいシステムはより粒度が高く、アクセス許可の付与と拒否のためのオプションが多数用意されています。 より詳細なシステムが複雑になるほど、学習が困難になりますが、ほとんどのエンタープライズシステムでは、固定ロールを使用する代わりにアクセス許可を付与する必要があります。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->次の表は、各固定データベースロールに関連付けられている権限を示しています。 この SQL Server グラフィックのすべてのアクセス許可は、APS では使用できません (または必要ありません)。  
  
![APS セキュリティの固定データベース ロール](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>関連コンテンツ  
  
-   ユーザー定義ロールを作成するには、「[ロールの作成](../t-sql/statements/create-role-transact-sql.md)」を参照してください。  
  
  
## <a name="fixed-server-roles"></a>固定サーバー ロール
固定サーバーロールは、SQL Server によって自動的に作成されます。 SQL Server PDW には SQL Server 固定サーバーロールの限定的な実装があります。 **Sysadmin**と**public**にのみ、メンバーとしてユーザーログインがあります。 **Setupadmin**ロールと**dbcreator**ロールは、SQL Server PDW によって内部的に使用されます。 他のメンバーを追加したり、ロールから削除したりすることはできません。  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin 固定サーバーロール  

  **sysadmin** 固定サーバー ロールのメンバーは、サーバーに対するすべての操作を実行できます。 **Sa**ログインは、 **sysadmin**固定サーバーロールの唯一のメンバーです。 追加のログインを**sysadmin**固定サーバーロールに追加することはできません。 
  **CONTROL SERVER** アクセス許可を付与すると、**sysadmin** 固定サーバー ロールのメンバーシップが概算されます。 次の例では、 **CONTROL SERVER**権限を fay という名前のログインに許可します。  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> **CONTROL SERVER**権限は、SQL Server PDW をほぼ完全に制御します。 可能な限り、より詳細な権限をログインに提供します。 たとえば、 **VIEW SERVER STATE**、 **ALTER any LOGIN**、 **view Any DATABASE**、または**CREATE any database**権限を付与することを検討してください。  
  
### <a name="public-server-role"></a>パブリックサーバーロール  
SQL Server PDW に接続できるすべてのログインは、 **public**サーバーロールのメンバーです。 すべてのログインは、任意のオブジェクトに対して**public**に付与された権限を継承します。 オブジェクトをすべてのユーザーが使用できるようにする場合にのみ、オブジェクトに対する**パブリック**アクセス許可を割り当てます。 **Public**ロールのメンバーシップは変更できません。  
  
> [!NOTE]  
> **public**は、他のロールとは異なる方法で実装されます。 すべてのサーバープリンシパルは public のメンバーであるため、 **public**ロールのメンバーシップは、 **server_role_members** DMV には記載されていません。  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>固定サーバーロールと権限の許可  
固定サーバーロールと固定データベースロールのシステムは、1980年に発行されたレガシシステムです。 固定ロールは引き続きサポートされており、ユーザー数が少ない環境や、セキュリティニーズがシンプルな環境で役に立ちます。 SQL Server 2005 以降では、権限を付与するより詳細なシステムが作成されました。 この新しいシステムはより粒度が高く、アクセス許可の付与と拒否のためのオプションが多数用意されています。 より詳細なシステムが複雑になるほど、学習が困難になりますが、ほとんどのエンタープライズシステムでは、固定ロールを使用する代わりにアクセス許可を付与する必要があります。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>関連トピック  
  
- [アクセス許可の付与](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

