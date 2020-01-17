---
title: ID 列のレプリケート | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- identities [SQL Server replication]
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: eb2f23a8-7ec2-48af-9361-0e3cb87ebaf7
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: a0e861a1619921081a81fa52f72ba6fc88e98668
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908347"
---
# <a name="replicate-identity-columns"></a>ID 列のレプリケート
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  IDENTITY プロパティを列に割り当てると、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、その ID 列を含むテーブルに挿入された新しい行に対して連続する番号が自動的に生成されます。 詳細については、「[IDENTITY &#40;プロパティ&#41; &#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql-identity-property.md)」を参照してください。 ID 列は主キーの一部に含まれる場合があるため、ID 列の値が重複しないようにすることが重要です。 複数のノードで更新されるレプリケーション トポロジで ID 列を使用するには、レプリケーション トポロジ内の各ノードで異なる範囲の ID 値を使用して、重複が生じないようにする必要があります。  
  
 たとえば、パブリッシャーに 1 ～ 100 の範囲を、サブスクライバー A に 101 ～ 200 の範囲を、サブスクライバー B に 201 ～ 300 の範囲を、それぞれ割り当てることができます。 パブリッシャーに行が挿入され、ID 値がたとえば 65 の場合、この値が各サブスクライバーにレプリケートされます。 レプリケーションによって各サブスクライバーにデータが挿入されると、サブスクライバー テーブル内の ID 列の値は増えずに、リテラル値 65 が挿入されます。 ID 列の値が増えるのは、ユーザーによる挿入のみで、レプリケーション エージェントの挿入では増えません。  
  
 レプリケーションではすべての種類のパブリケーションおよびサブスクリプションの ID 列が処理され、列は手動で管理することも、レプリケーションで自動で管理することもできます。  
  
> [!NOTE]  
>  パブリッシュされたテーブルに ID 列を追加することはサポートされていません。これは、列がサブスクライバーにレプリケートされると集約されなくなる可能性があるからです。 パブリッシャーの ID 列の値は、影響を受けるテーブルの行が物理的に格納されている順序に依存します。 サブスクライバーで行が同じように格納されているとは限らないため、同じ行で ID 列の値が異なる可能性があります。  
  
## <a name="specifying-an-identity-range-management-option"></a>ID 範囲の管理オプションの指定  
 レプリケーションには、次の 3 つの ID 範囲の管理オプションがあります。  
  
-   自動。 サブスクリプションでの更新を使用するマージ レプリケーションおよびトランザクション レプリケーションで使用されます。 パブリッシャーおよびサブスクライバーのサイズの範囲を指定し、レプリケーションによって新しい範囲の割り当てを自動的に管理します。 レプリケーションによって、サブスクライバーの ID 列に NOT FOR REPLICATION オプションが設定されるため、サブスクライバーではユーザーの挿入のみによって値が増えます。  
  
    > [!NOTE]  
    >  サブスクライバーは、パブリッシャーと同期して新しい範囲を受け取る必要があります。 サブスクライバーには ID の範囲が自動的に割り当てられるため、サブスクライバーが新しい範囲を繰り返し要求すると、サブスクライバーは ID 範囲をすべて使用してしまう可能性があります。  
  
-   手動。 サブスクライバーでの更新を使用しないスナップショット レプリケーションおよびトランザクション レプリケーション、ピア ツー ピア トランザクション レプリケーション、またはアプリケーションがプログラムを介して ID 範囲を管理する必要がある場合に使用されます。 手動による管理を指定した場合は、範囲をパブリッシャーおよび各サブスクライバーに割り当て、初期の範囲が使用された場合は新しい範囲を割り当てる必要があります。 レプリケーションによって、サブスクライバーの ID 列に NOT FOR REPLICATION オプションが設定されます。  
  
-   [なし] : このオプションは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の以前のバージョンとの互換性が必要な場合のみ使用することをお勧めします。また、このオプションは、トランザクション パブリケーションのストアド プロシージャ インターフェイスからのみ使用できます。  
  
 ID 範囲の管理のオプションを指定するには、「[ID 列の管理](../../../relational-databases/replication/publish/manage-identity-columns.md)」を参照してください。  
  
## <a name="assigning-identity-ranges"></a>ID 範囲の割り当て  
 マージ レプリケーションとトランザクション レプリケーションでは、範囲の割り当てにさまざまな方法を使用します。これらの方法についてこのセクションで説明します。  
  
 ID 列をレプリケートする場合は 2 種類の範囲を考慮する必要があります。1 つはパブリッシャーおよびサブスクライバーに割り当てる範囲で、もう 1 つは列のデータ型の範囲です。 以下の表に、ID 列で通常使用されるデータ型で利用可能な範囲を示します。 この範囲は、トポロジ内のすべてのノードで使用されます。 たとえば、1 から開始され、増分が 1 に設定された **smallint** を使用すると、挿入の最大数は、パブリッシャーとすべてのサブスクライバーで 32,767 になります。 実際の挿入数は、使用する値にギャップがあるかどうか、およびしきい値が使用されているかどうかによって変わります。 しきい値の詳細については、「マージ レプリケーション」「キュー更新サブスクリプションを使用するトランザクション レプリケーション」のセクションを参照してください。  
  
 挿入が **db_owner** 固定データベース ロールのメンバーによって実行されている場合は、パブリッシャーがその挿入後に ID 範囲をすべて使用すると、新しい範囲が自動的に割り当てられます。 挿入がそのロール以外のユーザー、ログ リーダー エージェント、マージ エージェントによって実行されている場合は、**db_owner** ロールのメンバーであるユーザーが [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql.md) を実行する必要があります。 トランザクション パブリケーションの場合は、ログ リーダー エージェントを実行して新しい範囲を自動で割り当てる必要があります (既定ではエージェントは継続して実行されます)。  
  
> [!WARNING]  
>  大規模な一括挿入処理中、レプリケーション トリガーが起動されるのは、挿入の行ごとではなく 1 度だけです。 その結果、大規模な挿入処理中に ID 範囲が使い果たされると、 **INSERT INTO** ステートメントなど、挿入ステートメントが失敗する場合があります。  
  
|データ型|範囲|  
|---------------|-----------|  
|**tinyint**|自動管理ではサポートされません。|  
|**smallint**|-2^15 (-32,768) ～ 2^15-1 (32,767)|  
|**int**|-2^31 (-2,147,483,648) ～ 2^31-1 (2,147,483,647)|  
|**bigint**|-2^63 (-9,223,372,036,854,775,808) ～ 2^63-1 (9,223,372,036,854,775,807)|  
|**decimal** および **numeric**|-10^38+1 ～ 10^38-1|  
  
> [!NOTE]  
>  複数のテーブルで使用できる自動的に増分する番号、またはテーブルを参照せずにアプリケーションから呼び出すことができる自動的に増分する番号を作成するには、「[シーケンス番号](../../../relational-databases/sequence-numbers/sequence-numbers.md)」を参照してください。  
  
### <a name="merge-replication"></a>マージ レプリケーション  
 ID 範囲はパブリッシャーで管理されて、マージ エージェントによってサブスクライバーに反映されます (再パブリッシュ階層では、範囲はルートのパブリッシャーとリパブリッシャーで管理されます)。 ID 値はパブリッシャーのプールから割り当てられます。 パブリケーションの新規作成ウィザードまたは [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を使用して ID 列を含むアーティクルをパブリケーションに追加する場合は、次の値を指定します。  
  
-   `@identity_range` パラメーター。パブリッシャーと、クライアント サブスクリプションを使用するサブスクライバーの両方に最初に割り当てる ID 範囲のサイズを制御します。  
  
    > [!NOTE]  
    >  以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行しているサブスクライバーの場合、このパラメーターは (`@pub_identity_range` パラメーターではなく)、再パブリッシュ サブスクライバーの ID 範囲のサイズも制御します。  
  
-   `@pub_identity_range` パラメーター。サーバー サブスクリプションを使用するサブスクライバーに割り当てる再パブリッシュ用の ID 範囲のサイズを指定します (データを再パブリッシュする場合は必須)。 サーバー サブスクリプションを使用するすべてのサブスクライバーは、実際にはデータを再パブリッシュしない場合でも、再パブリッシュ用の範囲を受け取ります。  
  
-   `@threshold` パラメーター。[!INCLUDE[ssEW](../../../includes/ssew-md.md)] または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の以前のバージョンに対するサブスクリプションに、ID の新しい範囲が必要かどうかを判断するために使用されます。  
  
 たとえば、`@identity_range` に 10,000 を、`@pub_identity_range` に 500,000 を指定できます。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンを実行しているパブリッシャーとすべてのサブスクライバー (サーバー サブスクリプションを使用するサブスクライバーを含む) には、プライマリ範囲として 10,000 が割り当てられます。 サーバー サブスクリプションを使用するサブスクライバーには、500,000 のプライマリ範囲も割り当てられます。これは、再パブリッシュ サブスクライバーと同期するサブスクライバーで使用できます (再パブリッシュ サブスクライバーのパブリケーション内のアーティクルに対しては、`@identity_range`、`@pub_identity_range`、`@threshold` を指定する必要もあります)。  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンを実行している各サブスクライバーは、セカンダリ ID 範囲も受け取ります。 セカンダリ範囲のサイズはプライマリ範囲のサイズと同じです。プライマリ範囲がすべて使用されると、セカンダリ範囲が使用されて、マージ エージェントによって新しい範囲がサブスクライバーに割り当てられます。 新しい範囲はセカンダリ範囲となり、サブスクライバーで ID 値が使用される限りこのプロセスは継続されます。  
  
  
### <a name="transactional-replication-with-queued-updating-subscriptions"></a>キュー更新サブスクリプションを使用するトランザクション レプリケーション  
 ID 範囲はディストリビューターで管理されて、ディストリビューション エージェントによってサブスクライバーに反映されます。 ID 値はディストリビューターのプールから割り当てられます。 プールのサイズは、データ型のサイズと、ID 列に対して使用される増分に基づいています。 パブリケーションの新規作成ウィザードまたは [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) を使用して ID 列を含むアーティクルをパブリケーションに追加する場合は、次の値を指定します。  
  
-   `@identity_range` パラメーター。すべてのサブスクライバーに最初に割り当てる ID 範囲のサイズを指定します。  
  
-   `@pub_identity_range` パラメーター。パブリッシャーに割り当てる ID 範囲のサイズを指定します。  
  
-   `@threshold` パラメーター。サブスクリプションに ID の新しい範囲が必要になるタイミングを決定するために使用します。  
  
 たとえば、`@pub_identity_range` には 10,000、`@identity_range` には 1,000 (サブスクライバーの更新数が少ないと仮定)、`@threshold` には 80% を指定できます。 サブスクライバーの挿入数が 800 (1,000 の 80%) を超えると、サブスクライバーに新しい範囲が割り当てられます。 パブリッシャーの挿入数が 8,000 を超えると、パブリッシャーに新しい範囲が割り当てられます。 新しい範囲が割り当てられると、テーブル内の ID 範囲値にはギャップが生じます。 高いしきい値を指定すると、ギャップは小さくなりますが、システムのフォールト トレランスは低くなります。ディストリビューション エージェントが何らかの理由で実行できない場合、サブスクライバーで ID の消費がさらに進みやすくなります。  
  
## <a name="assigning-ranges-for-manual-identity-range-management"></a>手動で ID 範囲を管理する場合の範囲の割り当て  
 手動による ID 範囲の管理を指定した場合は、パブリッシャーと各サブスクライバーがそれぞれ異なる ID 範囲を使用することが必要です。 たとえば、 `IDENTITY(1,1)`と定義されている ID 列を含むパブリッシャーのテーブルがあるとします。ID 列は 1 から開始し、行が挿入されるたびに 1 ずつ増えていきます。 パブリッシャーのテーブルの行数が 5,000 で、アプリケーションを実行中にテーブルがある程度大きくなると考えられる場合、パブリッシャーでは範囲 1 ～ 10,000 を使用できます。 2 つのサブスクライバーの場合、サブスクライバー A では 10,001 ～ 20,000 を使用し、サブスクライバー B では 20,001 ～ 30,000 を使用できます。  
  
 サブスクライバーが、スナップショットまたは別の方法で初期化された後に、DBCC CHECKIDENT を実行してサブスクライバーに ID 範囲の開始位置を割り当てます。 たとえば、サブスクライバー A では、 `DBCC CHECKIDENT('<TableName>','reseed',10001)`を実行します。 サブスクライバー B では、 `CHECKIDENT('<TableName>','reseed',20001)`を実行します。  
  
 新しい範囲をパブリッシャーまたはサブスクライバーに割り当てるには、DBCC CHECKIDENT を実行し、新しい値を指定してテーブルを再作成します。 新しい範囲を割り当てる必要がある時点を指定するには、いくつかの方法があります。 たとえば、ノードがその範囲をすべて使用しそうになったことを検出するメカニズムをアプリケーションに用意し、DBCC CHECKIDENT を使用して新しい範囲を割り当てることができます。 また、CHECK 制約を追加して、使用される範囲 ID 値が不足しそうになると行を追加できなくなるようにすることもできます。  
  
## <a name="handling-identity-ranges-after-a-database-restore"></a>データベース復元後の ID 範囲の処理  
 自動 ID 範囲の管理を使用している場合、サブスクライバーがバックアップから復元されたときに、新しい ID 値の範囲が自動的に要求されます。 パブリッシャーをバックアップから復元する場合は、パブリッシャーに適切な範囲を割り当てる必要があります。 マージ レプリケーション用に、[sp_restoremergeidentityrange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-restoremergeidentityrange-transact-sql.md) を使用して新しい範囲を割り当てます。 トランザクション レプリケーションの場合は、使用されている最も高い値を特定してから、新しい範囲の開始位置を設定します。 パブリケーション データベースが復元された後に次の手順を実行します。  
  
1.  すべてのサブスクライバーのすべての操作を停止します。  
  
2.  ID 列を含むパブリッシュされたテーブルごとに、以下を実行します。  

    1.  各サブスクライバーのサブスクリプション データベースで `IDENT_CURRENT('<TableName>')`を実行します。  
  
    2.  すべてのサブスクライバーで検出された最も高い値を記録します。  
  
    3.  パブリッシャーのパブリケーション データベースで、 `DBCC CHECKIDENT(<TableName>','reseed',<HighestValueFound+1>`) を実行します。  
  
    4.  パブリッシャーのパブリケーション データベースで、 `sp_adjustpublisheridentityrange <PublicationName>, <TableName>`を実行します。  
  
    > [!NOTE]  
    >  ID 列の値が増分ではなく減分に設定されている場合は、検出された最も低い値を記録してから、その値から新しい範囲を設定します。  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../../t-sql/functions/ident-current-transact-sql.md)   
 [IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql.md)  
  
  
