---
title: ページ復元 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restorepage.general.f1
helpviewer_keywords:
- restoring pages [SQL Server]
- pages [SQL Server], restoring
- databases [SQL Server], damaged
- page restores [SQL Server]
- pages [SQL Server], damaged
- restoring [SQL Server], pages
ms.assetid: 07e40950-384e-4d84-9ac5-84da6dd27a91
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f45fe94756ffa30a458aabbb078f6b01c9821918
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921037"
---
# <a name="restore-pages-sql-server"></a>ページ復元 (SQL Server)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してページを復元する方法について説明します。 ページ復元の目的は、データベース全体を復元することなく 1 つ以上の損傷したページを復元することです。 通常、復元候補のページは、そのページにアクセスする際に発生したエラーによって、"問題あり" に設定されています。 問題ありに設定されているページは、 [msdb](/sql/relational-databases/system-tables/suspect-pages-transact-sql) データベースの **suspect_pages** テーブルで特定できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [どのような場合にページ復元が役立つか](#WhenUseful)  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **ページを復元する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="WhenUseful"></a> どのような場合にページ復元が役立つか  
 ページ復元の目的は、損傷した個々のページを修復することです。 少数のページに関する復元と復旧は、ファイルの復元を行うより高速に実行でき、復元処理中にオフラインになるデータ量が少なくなる場合があります。 ただし、1 つのファイル内の多数のページを復元しなければならない場合は、ファイル全体を復元する方が効率的です。 たとえば、デバイス上の多くのページが損傷している場合は、デバイスの故障が差し迫っていることを示している可能性があるので、できれば別の場所にファイルを復元し、デバイスを修復することを検討します。  
  
 また、すべてのページ エラーが復元を必要とするわけではありません。 セカンダリ インデックスなど、キャッシュされたデータで発生する問題は、データを再計算することで解決される可能性があります。 たとえば、データベース管理者がセカンダリ インデックスを削除して再構築した場合、破損したデータは修正されていますが、 [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) テーブルにはそのことが記録されません。  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   ページの復元は、完全復旧モデルまたは一括ログ復旧モデルを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに適用されます。 ページ復元は、読み取り/書き込みファイル グループでのみサポートされます。  
  
-   復元できるのはデータベース ページのみです。 ページ復元を使用して、次のものを復元することはできません。  
  
    -   [トランザクション ログ]  
  
    -   アロケーション ページ:グローバル アロケーション マップ (GAM) ページ、共有グローバル アロケーション マップ (SGAM) ページ、およびページ空き容量 (PFS) ページ。  
  
    -   すべてのデータ ファイルのページ 0 (ファイルのブート ページ)  
  
    -   ページ 1:9 (データベースのブート ページ)  
  
    -   フルテキスト カタログ  
  
-   データベースで一括ログ復旧モデルを使用している場合、ページ復元には次の追加条件があります。  
  
    -   オフライン データはログに記録されないため、ファイル グループまたはページのデータがオフラインであるときにバックアップを行うと、一括ログ データで問題が発生します。 オフライン ページが原因で、ログのバックアップが失敗する可能性があります。 この場合、最新のバックアップへの復元を実行する場合よりもデータ損失の可能性が低い、DBCC REPAIR の使用を検討します。  
  
    -   一括ログ データベースのログ バックアップで不正なページが検出された場合は、WITH CONTINUE_AFTER_ERROR が指定されていないと失敗します。  
  
    -   ページ復元は、一般的に一括ログ復旧では使用できません。  
  
         ページ復元の実行で推奨されるのは、データベースを完全復旧モデルに設定し、ログ バックアップを試行する方法です。 ログ バックアップが成功した場合は、ページ復元を開始できます。 ログ バックアップが失敗した場合は、前回のログ バックアップ以降の作業をあきらめるか、REPAIR_ALLOW_DATA_LOSS オプションを指定して DBCC を実行してみる必要があります。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   ページ復元のシナリオ:  
  
     オフライン ページ復元  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションでは、データベースがオフラインのときにページ復元を実行できます。 オフライン ページ復元では、損傷したページの復元中はデータベースがオフラインです。 データベースは、復元シーケンスの最後にオンラインになります。  
  
     オンライン ページ復元  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition では、データベースがオフラインであるときにはオフライン復元が使用される一方、オンラインでのページ復元もサポートされます。 ほとんどの場合、ページを復元しているファイル グループを含むデータベースをオンラインにしたまま、損傷したページを復元できます。 プライマリ ファイル グループがオンラインの場合、そのセカンダリ ファイル グループがオフラインでも、通常は、オンラインによるページ復元が実行されます。 ただし、場合によっては、損傷したページをオフラインで復元することも必要です。 たとえば、特定の重要なページが損傷したことが原因で、データベースを起動できない可能性がある場合などです。  
  
    > [!WARNING]  
    >  破損したページにデータベースの重要なメタデータが格納されている場合、オンラインでのページ復元を試行する際、メタデータに対する必要な更新処理に失敗する可能性があります。 この場合は、オフラインでのページ復元を実行できます。ただし、その場合はまず、RESTORE WITH NORECOVERY でトランザクション ログをバックアップして、 [ログ末尾のバックアップ](tail-log-backups-sql-server.md) を作成しておく必要があります。  
  
-   ページ復元では、ページ レベルのエラー報告 (ページ チェックサムを含む) および追跡の機能を活用することができます。 チェックサムや破損した書き込みによって壊れていることが検出されたページ ( *損傷したページ*) は、ページ復元操作によって復元できます。 復元されるのは、明示的に指定したページのみです。 指定した各ページが、指定のデータ バックアップから取得されたページのコピーで置き換えられます。  
  
     それ以降、ログ バックアップを復元した場合、復元対象のページが少なくとも 1 つ存在するデータベース ファイルにのみ適用されます。 また、最新の完全復元または差分復元にチェーンが途切れていないログ バックアップを適用し、ページを含むファイル グループに現在のログ ファイルの状態を反映する必要があります。 ファイル復元と同様に、ロールフォワード セットは 1 つのログ再実行パスで進められます。 正常にページ復元を完了するには、データベースとの一貫性が保たれた状態になるようにページを復旧する必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 復元するデータベースが存在しない場合、ユーザーは RESTORE を実行できる CREATE DATABASE 権限を使用する必要があります。 データベースが存在する場合、既定では、RESTORE 権限は **sysadmin** 固定サーバー ロールおよび **dbcreator** 固定サーバー ロールのメンバーと、データベースの所有者 (**dbo**) に与えられています (FROM DATABASE_SNAPSHOT オプションを使用する場合、データベースは常に存在します)。  
  
 RESTORE 権限は、サーバーでメンバーシップ情報を常に確認できるロールに与えられます。 固定データベース ロールのメンバーシップは、データベースがアクセス可能で破損していない場合にのみ確認することができますが、RESTORE の実行時にはデータベースがアクセス可能で損傷していないことが必ずしも保証されないため、 **db_owner** 固定データベース ロールのメンバーには RESTORE 権限は与えられません。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、新たに [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でのページ復元がサポートされます。  
  
#### <a name="to-restore-pages"></a>ページを復元するには  
  
1.  適切な [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、オブジェクト エクスプローラーでサーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開します。 復元するデータベースに応じて、ユーザー データベースを選択するか、 **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックし、 **[タスク]** 、 **[復元]** の順にポイントし、 **[ページ]** をクリックします。 **[ページの復元]** ダイアログ ボックスが開きます。  
  
     **[復元]**  
     このセクションでは、 **[データベースの復元]\([全般] ページ)** の [[復元先]](../../integration-services/general-page-of-integration-services-designers-options.md)と同じ機能を実行します。  
  
     **[データベース]**  
     復元するデータベースを指定します。 新しいデータベースを入力するか、ドロップダウン リストから既存のデータベースを選択します。 このリストには、システム データベース **master** および **tempdb**を除いた、サーバー上のすべてのデータベースが表示されます。  
  
    > [!WARNING]  
    >  パスワードで保護されたバックアップを復元するには、 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) ステートメントを使用する必要があります。  
  
     **[ログ末尾のバックアップ]**  
     **[バックアップ デバイス]** に、データベースのログ末尾バックアップを保存するファイル名を入力または選択します。  
  
     **バックアップ セット**  
     このセクションには、復元に関連するバックアップ セットが表示されます。  
  
    |[ヘッダー]|値|  
    |------------|------------|  
    |**名前**|バックアップ セットの名前です。|  
    |**コンポーネント**|バックアップ コンポーネント: **[データベース]** 、 **[ファイル]** 、または **[\<空白>]** (トランザクション ログ用)。|  
    |**型**|実行するバックアップの種類: **[完全]** 、 **[差分]** 、 **[トランザクション ログ]** 。|  
    |**[サーバー]**|バックアップ操作を実行した [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスの名前。|  
    |**[データベース]**|バックアップ操作に呼び出されるデータベース名です。|  
    |**[Position]**|ボリューム内でのバックアップ セットの位置。|  
    |**最初の LSN**|バックアップ セット内の最初のトランザクションのログ シーケンス番号 (LSN)。 ファイル バックアップの場合は空白。|  
    |**最後の LSN**|バックアップ セット内の最後のトランザクションのログ シーケンス番号 (LSN)。 ファイル バックアップの場合は空白。|  
    |**チェックポイントの LSN**|バックアップが作成された時点で最新のチェックポイントのログ シーケンス番号 (LSN)。|  
    |**全 LSN**|最新のデータベースの完全バックアップのログ シーケンス番号 (LSN)。|  
    |**[開始日]**|バックアップ操作が開始した日時で、クライアントの地域設定で表示されます。|  
    |**完了日**|バックアップ操作が完了したときの日付と時刻。クライアントの地域設定で表示されます。|  
    |**Size**|バックアップ セットのサイズ (バイト単位) です。|  
    |**[ユーザー名]**|バックアップ操作を実行したユーザーの名前。|  
    |**[有効期限]**|バックアップ セットの期限が切れる日付と時刻。|  
  
     **[確認]** をクリックして、ページ復元操作の実行に必要なバックアップ ファイルの整合性を確認します。  
  
4.  破損したページを識別するには、 **[データベース]** ボックスで適切なデータベースを選択した状態で、 **[データベース ページの確認]** をクリックします。 この操作の実行には時間がかかります。  
  
    > [!WARNING]  
    >  破損していない特定のページを復元するには、 **[追加]** をクリックし、復元するページの **[ファイル ID]** と **[ページ ID]** を入力します。  
  
5.  ページ グリッドを使用して、復元対象のページを特定します。 最初、このグリッドには、 [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) システム テーブルから取得されたデータが表示されます。 このグリッドにページを追加したりグリッドからページを削除したりするには、 **[追加]** または **[削除]** をクリックします。 詳細については、「 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](manage-the-suspect-pages-table-sql-server.md)を使用してページを復元する方法について説明します。  
  
6.  **[バックアップ セット]** グリッドに、既定の復元プランのバックアップ セットが一覧表示されます。 必要に応じて **[確認]** をクリックし、バックアップが読み取り可能かどうか、また、バックアップ セットに不備がないかどうかを、実際には復元せずに確認します。 詳細については、「[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)」をご覧ください。  
  
     **[ページ]**  
  
7.  ページ グリッドに一覧表示されたページを復元するには、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 RESTORE DATABASE ステートメントでページを指定するには、ページを含むファイルのファイル ID とページのページ ID が必要です。 必須の構文は次のとおりです。  
  
 `RESTORE DATABASE <database_name>`  
  
 `PAGE = '<file: page> [ ,... n ] ' [ ,... n ]`  
  
 `FROM <backup_device> [ ,... n ]`  
  
 `WITH NORECOVERY`  
  
 PAGE オプションのパラメーターの詳細については、「[RESTORE の引数 &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)」を参照してください。 RESTORE DATABASE の構文の詳細については、「[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)」を参照してください。  
  
#### <a name="to-restore-pages"></a>ページを復元するには  
  
1.  復元する損傷したページのページ ID を取得します。 チェックサムまたは破損した書き込みのエラーによってページ ID が返され、ページを指定するために必要な情報が提供されます。 損傷したページのページ ID を検索するには、次のいずれかのソースを使用します。  
  
    |ページ ID のソース|トピック|  
    |-----------------------|-----------|  
    |**msdb..suspect_pages**|[suspect_pages テーブルの管理 &#40;SQL Server&#41;](manage-the-suspect-pages-table-sql-server.md)|  
    |エラー ログ|[SQL Server エラー ログの表示 &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)|  
    |イベント トレース|[イベントの監視と応答](../../ssms/agent/monitor-and-respond-to-events.md)|  
    |DBCC|[DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)|  
    |WMI プロバイダー|[WMI Provider for Server Events の概念](../wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)|  
  
2.  損傷したページが含まれている、データベースの完全バックアップ、ファイル バックアップ、またはファイル グループ バックアップを使用して、ページ復元を開始します。 RESTORE DATABASE ステートメントで PAGE 句を使用して、復元する全ページのページ ID の一覧を指定します。  
  
3.  最新の差分バックアップを適用します。  
  
4.  後続のログ バックアップを適用します。  
  
5.  復元されたページの最終 LSN を含むデータベースの新しいログ バックアップ (最後に復元されたページがオフラインになった時点までのログ バックアップ) を作成します。 この最終 LSN が、再実行ターゲット LSN になります。最終 LSN は、復元シーケンス内の最初の復元の一環として設定されます。 損傷したページを含むファイルのオンラインのロールフォワードは、再実行ターゲット LSN で停止することができます。 ファイルの現在の再実行ターゲット LSN は、**sys.master_files** の **redo_target_lsn** 列で確認できます。 詳細については、「[sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)」を参照してください。  
  
6.  新しいログ バックアップを復元します。 この新しいログ バックアップを適用すると、ページ復元が完了し、ページが使用可能な状態になります。  
  
    > [!NOTE]  
    >  この復元シーケンスは、ファイル復元シーケンスと似ています。 実際、ページ復元とファイル復元は、どちらも同じ復元シーケンスで実行することができます。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、 `B` を指定して、ファイル `NORECOVERY`の 4 つの損傷したページを復元します。 次に、 `NORECOVERY`を使用して 2 つのログ バックアップを適用してから、 `RECOVERY`を使用してログ末尾のバックアップを復元します。 次の例では、オンライン復元を実行します。 この例では、ファイル `B` のファイル ID が `1`で、損傷したページのページ ID は `57`、 `202`、 `916`、および `1016`です。  
  
```sql  
RESTORE DATABASE <database> PAGE='1:57, 1:202, 1:916, 1:1016'  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;   
BACKUP LOG <database> TO <new_log_backup>;   
RESTORE LOG <database> FROM <new_log_backup> WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](manage-the-suspect-pages-table-sql-server.md)   
 [SQL Server データベースのバックアップと復元](back-up-and-restore-of-sql-server-databases.md)  
  
  
