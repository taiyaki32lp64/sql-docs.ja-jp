---
title: パブリケーション データベースでのスキーマの変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], schema changes
- snapshot replication [SQL Server], replicating schema changes
- merge replication [SQL Server replication], replicating schema changes
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
- publishing [SQL Server replication], schema changes
ms.assetid: 926c88d7-a844-402f-bcb9-db49e5013b69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 65436da64ca7c718de053dab520edad71dac6228
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68199453"
---
# <a name="make-schema-changes-on-publication-databases"></a>パブリケーション データベースでのスキーマの変更
  レプリケーションは、パブリッシュされたオブジェクトに対するさまざまなスキーマ変更をサポートしています。 パブリッシュされた適切なオブジェクトに対して、以下に示すスキーマ変更を [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パブリッシャーで実行した場合、既定ではすべての [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サブスクライバーにその変更が反映されます。  
  
-   ALTER TABLE  
  
-   ALTER TABLE SET LOCK ESCALATION (スキーマ変更レプリケーションが有効で、トポロジに [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] または [!INCLUDE[ssEWnoversion](../../../includes/ssewnoversion-md.md)] サブスクライバーが含まれている場合は使用しないでください) ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
     データ定義言語 (DDL) トリガーはレプリケートできないため、ALTER TRIGGER を使用できるのは、データ操作言語 (DML) トリガーに対してのみです。  
  
> [!IMPORTANT]  
>  テーブルに対するスキーマ変更は、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) を使用して行う必要があります。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]でスキーマ変更を行うと、 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] は、テーブルを削除して再作成しようとします。 パブリッシュされたオブジェクトは削除できないため、スキーマ変更は失敗します。  
  
 トランザクション レプリケーションおよびマージ レプリケーションの場合、スキーマ変更はディストリビューション エージェントまたはマージ エージェントが実行されたときに、その増分が反映されます。 スナップショット レプリケーションの場合、スキーマ変更は新しいスナップショットがサブスクライバーで適用されるときに反映されます。 スナップショット レプリケーションでは、同期が行われるたびにスキーマの新しいコピーがサブスクライバーに送信されます。 したがって、以前にパブリッシュされたオブジェクトに対するすべてのスキーマ変更 (上に列挙したもの以外も含む) は、同期のたびに自動的に反映されます。  
  
 パブリケーションでのアーティクルの追加と削除については、「[既存のパブリケーションでのアーティクルの追加および削除](add-articles-to-and-drop-articles-from-existing-publications.md)」を参照してください。  
  
 **スキーマの変更をレプリケートするには**  
  
 上に列挙したスキーマ変更は既定でレプリケートされます。 スキーマ変更のレプリケートを無効にする方法については、「 [Replicate Schema Changes](replicate-schema-changes.md)」を参照してください。  
  
## <a name="considerations-for-schema-changes"></a>スキーマ変更に関する注意点  
 スキーマ変更をレプリケートする際には、以下の点に注意してください。  
  
### <a name="general-considerations"></a>全般的な注意点  
  
-   スキーマ変更は、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]の制限の対象となります。 たとえば、ALTER TABLE で主キー列を変更することはできません。  
  
-   データ型マッピングは、初期スナップショットに対してのみ実行されます。 スキーマ変更で、以前のバージョンのデータ型へのマッピングは行われません。 たとえば、`ALTER TABLE ADD datetime2 column` というステートメントを [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] で使用している場合、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] サブスクライバーでは、データ型が `nvarchar` に変換されません。 場合によっては、スキーマ変更がパブリッシャーでブロックされます。  
  
-   スキーマ変更の反映を許可するようにパブリケーションが設定されている場合は、関連するスキーマ オプションがパブリケーションのアーティクルに対してどのように設定されているかに関係なく、スキーマ変更が反映されます。 たとえば、外部キー制約をレプリケートしないようにテーブル アーティクルに対して指定している場合に、外部キーをテーブルに追加する ALTER TABLE コマンドをパブリッシャーで実行すると、サブスクライバーで外部キーがテーブルに追加されます。 これを回避するには、ALTER TABLE コマンドを実行する前にスキーマ変更の反映を無効にします。  
  
-   スキーマ変更は、サブスクライバー (再パブリッシュ サブスクライバーを含む) では行わず、パブリッシャーでのみ行います。 マージ レプリケーションについては、サブスクライバーでスキーマを変更できないようになっています。 トランザクション レプリケーションでは変更できますが、変更するとレプリケーションが失敗する可能性があります。  
  
-   再パブリッシュ サブスクライバーに反映された変更は、既定でそのサブスクライバーに反映されます。  
  
-   パブリッシャーには存在するがサブスクライバーには存在しないオブジェクトや制約を参照しているスキーマ変更は、パブリッシャーでは成功しますが、サブスクライバーでは失敗します。  
  
-   外部キーを追加するときに参照されるサブスクライバーのすべてのオブジェクトは、パブリッシャーの対応するオブジェクトと名前と所有者が同じである必要があります。  
  
-   インデックスの明示的な追加、削除、および変更はサポートされていません。 制約 (主キー制約など) に対して暗黙的に作成されたインデックスはサポートされます。  
  
-   レプリケーションによって管理されている ID 列の変更や削除はサポートされていません。 ID 列の自動管理の詳細については、「[ID 列のレプリケート](replicate-identity-columns.md)」を参照してください。  
  
-   非決定的関数を含むスキーマ変更はサポートされていません。これは、パブリッシャーとサブスクライバーのデータが異なる結果になる可能性があるためです (この状態を "未集約" と言います)。 たとえば、 `ALTER TABLE SalesOrderDetail ADD OrderDate DATETIME DEFAULT GETDATE()`というコマンドをパブリッシャーで実行した場合、このコマンドがサブスクライバーにレプリケートされて実行されると異なる値になります。 非決定的関数の詳細については、「 [Deterministic and Nondeterministic Functions](../../user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
-   制約には明示的に名前を付けることをお勧めします。 明示的に制約に名前を付けない場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が制約の名前を生成するので、これらの名前がパブリッシャーと各サブスクライバーで異なります。 このことが原因で、スキーマ変更のレプリケーション中に問題が発生することがあります。 たとえば、パブリッシャー側で列を削除することにより依存制約が削除されると、レプリケーションは、サブスクライバー側でこの制約を削除しようとします。 制約の名前が異なるので、サブスクライバーでの削除は失敗します。 制約の名前付けの問題によって同期に失敗する場合、サブスクライバー側で制約を手動で削除して、マージ エージェントを再実行してください。  
  
-   テーブルをレプリケーション用にパブリッシュする場合、パブリケーション スナップショットが既に生成されている場合は、そのテーブルの列を XML のデータ型に変更することはできません。列を変更するには、まずレプリケーションを削除する必要があります。  
  
-   パブリッシュされたテーブルで DDL を実行する場合、Read uncommitted はサポートされる分離レベルでありません。  
  
-   `SET CONTEXT_INFO` を使用して、パブリッシュされたオブジェクトに対してスキーマの変更が実行されるトランザクションのコンテキストを変更しないでください。  
  
#### <a name="adding-columns"></a>列の追加  
  
-   テーブルに新しい列を追加し、その列を既存のパブリケーションに含めるには、ALTER TABLE \<Table> ADD \<Column> を実行します。 この列は、既定ですべてのサブスクライバーにレプリケートされます。 この列では、NULL 値を許容するか既定の制約を含める必要があります。 列の追加の詳細については、このトピックの「マージ レプリケーション」を参照してください。  
  
-   テーブルに新しい列を追加し、その列を既存のパブリケーションに含めない場合は、スキーマ変更のレプリケーションを無効にしてから、ALTER TABLE \<Table> ADD \<Column> を実行します。  
  
-   既存のパブリケーションに既存の列を含めるには、[sp_articlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)、[sp_mergearticlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスを使用します。  
  
     詳しくは、「 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)」をご覧ください。 この場合は、サブスクリプションの再初期化が必要になります。  
  
-   パブリッシュされたテーブルに ID 列を追加することはサポートされていません。これは、列がサブスクライバーにレプリケートされると集約されなくなる可能性があるからです。 パブリッシャーの ID 列の値は、影響を受けるテーブルの行が物理的に格納されている順序に依存します。 サブスクライバーで行が同じように格納されているとは限らないため、同じ行で ID 列の値が異なる可能性があります。  
  
#### <a name="dropping-columns"></a>列の削除  
  
-   既存のパブリケーションから列を削除し、その列をパブリッシャーのテーブルから削除するには、ALTER TABLE \<Table> DROP \<Column> を実行します。 この列は、既定ですべてのサブスクライバーのテーブルから削除されます。  
  
-   既存のパブリケーションから列を削除し、その列をパブリッシャーのテーブルからは削除しない場合は、[sp_articlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)、[sp_mergearticlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスを使用します。  
  
     詳しくは、「 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)」をご覧ください。 この場合は、新しいスナップショットの生成が必要になります。  
  
-   削除する列は、データベースのどのパブリケーションのどのアーティクルのフィルター句でも使用できません。  
  
-   パブリッシュされたアーティクルから列を削除するときには、データベースに影響する可能性のある列の制約、インデックスまたはプロパティについて考慮する必要があります。 以下に例を示します。  
  
    -   主キーで使用されている列をトランザクション パブリケーションのアーティクルから削除することはできません。それらの列は、レプリケーションによって使用されます。  
  
    -   マージ パブリケーションのアーティクルから rowguid 列を削除したり、更新サブスクリプションをサポートしているトランザクション パブリケーションのアーティクルから mstran_repl_version 列を削除することはできません。それらの列は、レプリケーションによって使用されます。  
  
    -   インデックスの変更は、サブスクライバーに反映されません。パブリッシャー側で列を削除することにより依存インデックスが削除されても、インデックスの削除はレプリケートされません。 パブリッシャー側で列を削除する前に、サブスクライバー側でインデックスを削除する必要があります。この操作を行っておくと、列をパブリッシャーからサブスクライバーにレプリケートするときに列の削除に成功します。 サブスクライバー側のインデックスが原因で同期に失敗する場合、手動でインデックスを削除して、マージ エージェントを再実行してください。  
  
    -   制約は、削除が可能になるように明示的に名前を付ける必要があります。 詳細については、このトピックの「全般的な注意点」を参照してください。  
  
### <a name="transactional-replication"></a>トランザクション レプリケーション  
  
-   スキーマ変更は、以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を実行しているサブスクライバーにも反映されますが、DDL ステートメントに含まれているすべての構文が、サブスクライバーで実行されているバージョンでサポートされている必要があります。  
  
     サブスクライバーがデータを再パブリッシュする場合にサポートされるスキーマ変更は、列の追加と削除のみです。 これらの変更は、ALTER TABLE DDL 構文ではなく、[sp_repladdcolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql) と [sp_repldropcolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql) を使用して、パブリッシャーで行う必要があります。  
  
-   スキーマ変更は、SQL Server 以外のサブスクライバーにはレプリケートされません。  
  
-   スキーマ変更は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のパブリッシャーからは反映されません。  
  
-   テーブルとしてレプリケートされたインデックス付きビューを変更することはできません。 インデックス付きビューとしてレプリケートされたインデックス付きビューは変更できますが、変更すると、インデックス付きビューではなく通常のビューになります。  
  
-   パブリケーションが即時更新サブスクリプションやキュー更新サブスクリプションをサポートしている場合は、スキーマ変更を行う前にシステムを停止する (パブリッシュされたテーブルのすべての操作をパブリッシャーとサブスクライバーで停止して、保留中のデータ変更をすべてのノードに反映する) 必要があります。 スキーマ変更がすべてのノードに反映されたら、パブリッシュされたテーブルの操作を再開できます。  
  
-   パブリケーションがピア ツー ピア トポロジにある場合は、スキーマ変更を行う前にシステムを停止する必要があります。 詳細については、「[レプリケーション トポロジの停止 &#40;レプリケーション Transact-SQL プログラミング&#41;](../administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)」を参照してください。  
  
-   テーブルに timestamp 列を追加して、timestamp を binary(8) にマップすると、すべてのアクティブなサブスクリプションでアーティクルが再初期化されます。  
  
### <a name="merge-replication"></a>マージ レプリケーション  
  
-   マージ レプリケーションでスキーマ変更がどのように処理されるかは、パブリケーションの互換性レベルと、スナップショットがネイティブ モード (既定) とキャラクター モードのどちらに設定されているかによって決まります。  
  
    -   スキーマ変更をレプリケートするには、パブリケーションの互換性レベルが少なくとも 90RTM である必要があります。 サブスクライバーが以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行している場合や、互換性レベルが 90RTM 未満の場合でも、[sp_repladdcolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql) や [sp_repldropcolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql) を使用して列の追加や削除を行うことができます。 ただし、これらのプロシージャは非推奨です。  
  
    -   [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]で導入されたデータ型の列を既存のアーティクルに追加すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は次のように動作します。  
  
        ||100RTM、ネイティブ モードのスナップショット|100RTM、キャラクター モードのスナップショット|その他すべての互換性レベル|  
        |-|-----------------------------|--------------------------------|------------------------------------|  
        |`hierarchyid`|変更を許可する|変更をブロックする|変更をブロックする|  
        |`geography` および `geometry`|変更を許可する|変更を許可する<sup>1</sup>|変更をブロックする|  
        |`filestream`|変更を許可する|変更をブロックする|変更をブロックする|  
        |`date`、`time`、`datetime2`、および `datetimeoffset`|変更を許可する|変更を許可する<sup>1</sup>|変更をブロックする|  
  
         <sup>1</sup> SQL Server Compact サブスクライバー、サブスクライバーでは、これらのデータ型に変換します。  
  
-   スキーマ変更の適用時にエラー (サブスクライバーで利用できないテーブルを参照する外部キーを追加した結果のエラーなど) が発生すると、同期が失敗し、サブスクリプションを再初期化しなければならなくなります。  
  
-   結合フィルターやパラメーター化されたフィルターに含まれている列に対してスキーマ変更を行う場合は、すべてのサブスクリプションを再初期化し、スナップショットを再生成する必要があります。  
  
-   マージ レプリケーションには、トラブルシューティングの際にスキーマ変更をスキップするストアド プロシージャが用意されています。 詳細については、「[sp_markpendingschemachange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql)」および「[sp_enumeratependingschemachanges &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [ALTER VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-view-transact-sql)   
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-procedure-transact-sql)   
 [ALTER FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-function-transact-sql)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [データとデータベース オブジェクトのパブリッシュ](publish-data-and-database-objects.md)   
 [カスタム トランザクション プロシージャの再生成によるスキーマ変更の反映](../transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)  
  
  
