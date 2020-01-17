---
title: SQL Server Audit (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- audit
helpviewer_keywords:
- SQL Server Audit
- audits [SQL Server], SQL Server Audit
ms.assetid: 0c1fca2e-f22b-4fe8-806f-c87806664f00
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8286c918c224b92e1f391931569030a7218252f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68198421"
---
# <a name="sql-server-audit-database-engine"></a>SQL Server Audit (データベース エンジン)
  [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] のインスタンスや個々のデータベースの *監査* を行うためには、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]で発生するイベントの追跡およびログ記録が必要です。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査では、サーバー レベルのイベントのためのサーバー監査仕様とデータベース レベルのイベントのためのデータベース監査仕様を含めることができる、サーバー監査を作成できます。 監査イベントは、イベント ログまたは監査ファイルへ書き込むことができます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]では、個々のインストール環境についての政府や標準による要件に応じて、複数のレベルの監査を使用できます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査には、サーバーおよびデータベースのさまざまなオブジェクトの監査を有効化、保存、および表示するためのツールとプロセスが用意されています。  
  
 サーバー監査アクション グループをインスタンスごとに、データベース監査アクション グループまたはデータベース監査アクションをデータベースごとに、それぞれ記録できます。 監査可能なアクションが検出されるたびに監査イベントが発生します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のすべてのエディションでサーバー レベルの監査がサポートされます。 データベース レベルの監査は、Enterprise、Developer、および Evaluation Edition に限定されています。 詳しくは「 [Features Supported by the Editions of SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」をご覧ください。  
  
## <a name="sql-server-audit-components"></a>SQL Server 監査のコンポーネント  
 *監査* では、複数の要素が、サーバー アクションやデータベース アクションの特定のグループのための 1 つのパッケージに組み合わされています。 レポート定義がグラフィックやデータ要素と組み合わされてレポートが生成されるように、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査の複数のコンポーネントが組み合わされて、監査と呼ばれる出力が生成されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査では、 *拡張イベント* を使用して監査を作成できます。 拡張イベントの詳細については、「 [拡張イベント](../../extended-events/extended-events.md)」を参照してください。  
  
### <a name="sql-server-audit"></a>SQL Server Audit  
 *SQL Server 監査* オブジェクトは、監視するサーバー レベルまたはデータベース レベルのアクションおよびアクションのグループの 1 つのインスタンスを収集します。 監査は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス レベルで行われます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスごとに複数の監査を使用できます。  
  
 監査を定義する場合、結果を出力する場所を指定します。 これが監査の出力先です。 監査は *無効* な状態で作成されるため、アクションの監査は自動的には行われません。 監査を有効にすると、監査の出力先が監査からデータを受け取るようになります。  
  
### <a name="server-audit-specification"></a>サーバー監査の仕様  
 *サーバー監査の仕様* オブジェクトは監査に属しています。 サーバー監査の仕様は監査ごとに 1 つ作成できます。これは、サーバー監査の仕様も監査も [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのスコープで作成されるためです。  
  
 サーバー監査の仕様は、拡張イベント機能によって発生するさまざまなサーバー レベルのアクション グループを収集します。 サーバー監査の仕様には、 *監査アクション グループ* を含めることができます。 監査アクション グループとは、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]で発生するアトミック イベントであるアクションの定義済みのグループです。 これらのアクションは監査に送信されて、ターゲットに記録されます。  
  
 データベース レベルの監査アクション グループと監査アクションの詳細については、「 [SQL Server 監査のアクション グループとアクション](sql-server-audit-action-groups-and-actions.md)」を参照してください。  
  
### <a name="database-audit-specification"></a>データベース監査の仕様  
 *Database Audit Specification* オブジェクトも、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査に属しています。 各監査では [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースごとに 1 つのデータベース監査の仕様を作成できます。  
  
 データベース監査の仕様は、拡張イベント機能によって発生するデータベース レベルの監査アクションを収集します。 データベース監査の仕様には、監査アクション グループまたは監査イベントを追加できます。 *監査イベント* とは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エンジンで監査できるアトミックなアクションです。 *監査アクション グループ* とは、アクションの定義済みのグループです。 これらはいずれも、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースのスコープにあります。 これらのアクションは監査に送信されて、ターゲットに記録されます。 ユーザーのデータベース監査の仕様に、システム ビューなどのサーバー スコープ オブジェクトは含めないでください。  
  
 データベース レベルの監査アクション グループと監査アクションの詳細については、「 [SQL Server 監査のアクション グループとアクション](sql-server-audit-action-groups-and-actions.md)」を参照してください。  
  
### <a name="target"></a>移行先  
 監査の結果はターゲットに送信されます。ターゲットには、ファイル、Windows セキュリティ イベント ログ、または Windows アプリケーション イベント ログを使用できます。 定期的にログをレビューおよびアーカイブして、ターゲットに追加のレコードを書き込むための十分なスペースを確保しておく必要があります。  
  
> [!IMPORTANT]  
>  Windows アプリケーション イベント ログの読み取りおよび書き込みは、認証されているユーザーならば、だれでも行うことができます。 アプリケーション イベント ログでは、Windows セキュリティ イベント ログほど高いアクセス許可は要求されません。したがって、Windows セキュリティ イベント ログに比べてセキュリティが低くなります。  
  
 Windows セキュリティ ログへの書き込みを行うには、"セキュリティ監査の生成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **" ポリシーに** サービス アカウントを追加する必要があります。 既定では、ローカル システム、ローカル サービス、およびネットワーク サービスがこのポリシーに追加されています。 この設定は、セキュリティ ポリシー スナップイン (secpol.msc) を使用して構成できます。 さらに、 **オブジェクト アクセスの監査** セキュリティ ポリシーを、 **成功** と **失敗**の両方について有効にする必要があります。 この設定は、セキュリティ ポリシー スナップイン (secpol.msc) を使用して構成できます。 [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] Windows Server 2008 では、設定することもできるより細かい**生成されたアプリケーション**監査ポリシー プログラムを使用してコマンドラインからのポリシー (`AuditPol.exe)`します。 Windows セキュリティ ログへの書き込みを有効にする手順の詳細については、「 [セキュリティ ログへの SQL サーバー監査イベントの書き込み](write-sql-server-audit-events-to-the-security-log.md)」を参照してください。 Auditpol.exe プログラムの詳細については、 [グループ ポリシーを使用して詳細なセキュリティの監査を構成する方法](https://support.microsoft.com/kb/921469/)に関するサポート技術情報の記事 921469 を参照してください。 Windows イベント ログは、すべての Windows オペレーティング システムで使用できます。 Windows イベント ログの詳細については、「 [イベント ビューアーの概要](https://go.microsoft.com/fwlink/?LinkId=101455)」を参照してください。 監査でより厳密なアクセス許可が必要な場合は、バイナリ ファイル ターゲットを使用します。  
  
 改ざんを防止するために監査情報をファイルに保存している場合、次の方法でそのファイルの場所へのアクセスを制限できます。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントには、読み取り権限と書き込み権限の両方が必要です。  
  
-   通常、監査管理者には、読み取り権限と書き込み権限が必要です。 これは、監査管理者が監査ファイルを管理 (他の共有への監査ファイルのコピー、監査ファイルのバックアップなど) するための Windows アカウントであることを前提としています。  
  
-   監査ファイルの読み取りが許可されている監査リーダーには、読み取り権限が必要です。  
  
 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] がファイルへの書き込みを行っているときでも、他の Windows ユーザーは、権限を持っていれば、監査ファイルを読み取ることができます。 排他ロックを取得すると読み取り操作が行われないようになりますが、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] では排他ロックを取得しません。  
  
 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] は監査ファイルにアクセスできるため、CONTROL SERVER 権限を持っている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインは、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] を利用して監査ファイルにアクセスできます。 監査ファイルの読み取りを行っているユーザーを記録するには、master.sys.fn_get_audit_file に監査を定義します。 これにより、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を介して監査ファイルにアクセスした、CONTROL SERVER 権限を持つログインが記録されます。  
  
 監査管理者が別の場所に監査ファイルをコピーする場合 (アーカイブ用など)、新しい場所に対する ACL は、次の権限に限定する必要があります。  
  
-   監査管理者 - 読み取り/書き込み  
  
-   監査リーダー - 読み取り  
  
 監査管理者または監査リーダーしかアクセスしない、別の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンス ( [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)]のインスタンスなど) から監査レポートを作成することをお勧めします。 レポート作成用に別の [!INCLUDE[ssDE](../../../includes/ssde-md.md)] のインスタンスを使用することで、許可されていないユーザーによる監査レコードへのアクセスを防ぐことができます。  
  
 Windows BitLocker ドライブ暗号化または Windows 暗号化ファイル システムを使用して監査ファイルが格納されているフォルダーを暗号化することにより、許可されていないアクセスに対する保護を強化することができます。  
  
 ターゲットに書き込まれる監査レコードの詳細については、「 [SQL Server Audit Records](sql-server-audit-records.md)」を参照してください。  
  
## <a name="overview-of-using-sql-server-audit"></a>SQL Server 監査の使用の概要  
 監査は、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用して定義することができます。 監査を作成して有効にすると、ターゲットがエントリを受け取るようになります。  
  
 Windows イベント ログを閲覧するには、Windows の **イベント ビューアー** ユーティリティを使用します。 ファイル ターゲットの場合は、 **の** [ログ ファイルの表示] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] か、 [fn_get_audit_file](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql) 関数を使用して、対象のファイルを閲覧できます。  
  
 監査の作成および使用の一般的な手順は次のとおりです。  
  
1.  監査を作成し、ターゲットを定義します。  
  
2.  監査にマップするサーバー監査の仕様またはデータベース監査の仕様を作成します。 その監査の仕様を有効にします。  
  
3.  監査を有効にします。  
  
4.  Windows **イベント ビューアー**、 **[ログ ファイルの表示]** 、または fn_get_audit_file 関数を使用して、監査イベントを閲覧します。  
  
 詳細については、「 [サーバー監査およびサーバー監査の仕様を作成する](create-a-server-audit-and-server-audit-specification.md) 」および「 [サーバー監査およびデータベース監査の仕様を作成する](create-a-server-audit-and-database-audit-specification.md)」を参照してください。  
  
## <a name="considerations"></a>考慮事項  
 監査の開始時にエラーが発生すると、サーバーが起動しなくなります。 その場合にサーバーを起動するには、コマンド ラインで **-f** オプションを使用します。  
  
 監査に対して ON_FAILURE=SHUTDOWN が指定されているために監査エラーによってサーバーがシャットダウンしたり起動しなくなったりすると、MSG_AUDIT_FORCED_SHUTDOWN イベントがログに書き込まれます。 シャットダウンはこの設定が初めて検出されたときに生じるため、このイベントが書き込まれるのは 1 回だけです。 このイベントは、シャットダウンを引き起こした監査のエラー メッセージの後に書き込まれます。 管理者は、 **-m** フラグを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をシングル ユーザー モードで起動することで、監査に伴うシャットダウンを回避することができます。 シングル ユーザー モードで起動すると、ON_FAILURE=SHUTDOWN が指定されているすべての監査がダウングレードされて、そのセッションでは ON_FAILURE=CONTINUE として実行されます。 **-m** フラグを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を起動すると、エラー ログに MSG_AUDIT_SHUTDOWN_BYPASSED メッセージが書き込まれます。  
  
 スタートアップ オプションの詳細については、「 [データベース エンジン サービスのスタートアップ オプション](../../../database-engine/configure-windows/database-engine-service-startup-options.md)」を参照してください。  
  
### <a name="attaching-a-database-with-an-audit-defined"></a>定義済みの監査を含むデータベースのインポート  
 監査の仕様が含まれていて、サーバーに存在しない GUID が指定されているデータベースをアタッチすると、 *孤立した* 監査の仕様が発生します。 この場合は、一致する GUID を持つ監査がサーバー インスタンスに存在しないため、監査イベントは記録されません。 この状況を修正するには、ALTER DATABASE AUDIT SPECIFICATION コマンドを使用して、孤立した監査の仕様を既存のサーバー監査に関連付けます。 または、CREATE SERVER AUDIT コマンドを使用して、指定されている GUID を持つ新しい Server 監査を作成します。  
  
 監査の仕様が定義されているデータベースを、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査をサポートしていない別のエディションの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] など) にアタッチすることもできますが、監査イベントは記録されません。  
  
### <a name="database-mirroring-and-sql-server-audit"></a>データベース ミラーリングと SQL Server 監査  
 データベース監査の仕様が定義されていて、データベース ミラーリングを使用するデータベースには、そのデータベース監査の仕様が含まれます。 ミラー化された SQL インスタンスでも正しく機能するようにするには、以下の項目を構成する必要があります。  
  
-   データベース監査の仕様が監査レコードを書き込めるようにするには、同じ GUID を持つ監査をミラー サーバーに作成する必要があります。 これは、CREATE AUDIT WITH GUID コマンドを使用して構成できます`=` *\<ソース Server Audit の GUID*>。  
  
-   バイナリ ファイル ターゲットの場合は、監査記録が書き込まれる場所に対する適切なアクセス許可がミラー サーバーのサービス アカウントに必要です。  
  
-   Windows イベント ログ ターゲットの場合は、ミラー サーバーが配置されているコンピューターのセキュリティ ポリシーで、セキュリティ イベント ログまたはアプリケーション イベント ログへのサービス アカウントのアクセスが許可されている必要があります。  
  
### <a name="auditing-administrators"></a>監査管理者  
 メンバー、`sysadmin`固定サーバー ロールとして識別される、 **dbo**各データベース内のユーザー。 管理者のアクションを監査するには、 **dbo** ユーザーのアクションを監査します。  
  
## <a name="creating-and-managing-audits-with-transact-sql"></a>Transact-SQL を使用した監査の作成と管理  
 DDL ステートメント、動的管理ビューと関数、およびカタログ ビューを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査のすべての機能を実装できます。  
  
### <a name="data-definition-language-statements"></a>データ定義言語ステートメント  
 以下の DDL ステートメントを使用して、監査の仕様を作成、変更、および削除することができます。  
  
|||  
|-|-|  
|[ALTER AUTHORIZATION](/sql/t-sql/statements/alter-authorization-transact-sql)|[CREATE SERVER AUDIT](/sql/t-sql/statements/create-server-audit-transact-sql)|  
|[ALTER DATABASE AUDIT SPECIFICATION](/sql/t-sql/statements/alter-database-audit-specification-transact-sql)|[CREATE SERVER AUDIT SPECIFICATION](/sql/t-sql/statements/create-server-audit-specification-transact-sql)|  
|[ALTER SERVER AUDIT](/sql/t-sql/statements/alter-server-audit-specification-transact-sql)|[DROP DATABASE AUDIT SPECIFICATION](/sql/t-sql/statements/drop-database-encryption-key-transact-sql)|  
|[ALTER SERVER AUDIT SPECIFICATION](/sql/t-sql/statements/alter-server-audit-transact-sql)|[DROP SERVER AUDIT](/sql/t-sql/statements/drop-server-audit-transact-sql)|  
|[CREATE DATABASE AUDIT SPECIFICATION](/sql/t-sql/statements/create-database-audit-specification-transact-sql)|[DROP SERVER AUDIT SPECIFICATION](/sql/t-sql/statements/drop-server-audit-specification-transact-sql)|  
  
### <a name="dynamic-views-and-functions"></a>動的ビューと関数  
 次の表に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査に使用できる動的ビューと関数の一覧を示します。  
  
|動的ビューと関数|説明|  
|---------------------------------|-----------------|  
|[sys.dm_audit_actions](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql)|監査ログで報告される可能性のあるすべての監査アクション、および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit の一部として構成できるすべての監査アクション グループに対して 1 つの行を返します。|  
|[sys.dm_server_audit_status](/sql/relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql)|監査の現在の状態に関する情報を提供します。|  
|[sys.dm_audit_class_type_map](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql)|監査ログ内の class_type フィールドを、sys.dm_audit_actions 内の class_desc フィールドにマップするテーブルを返します。|  
|[fn_get_audit_file](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)|サーバー監査で作成された監査ファイルからの情報を返します。|  
  
### <a name="catalog-views"></a>カタログ ビュー  
 次の表に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査に使用できるカタログ ビューの一覧を示します。  
  
|カタログ ビュー|説明|  
|-------------------|-----------------|  
|[sys.database_ audit_specifications](/sql/relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql)|サーバー インスタンス上の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査に含まれるデータベース監査仕様に関する情報を含みます。|  
|[sys.database_audit_specification_details](/sql/relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql)|すべてのデータベースについてサーバー インスタンス上の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査に含まれる、データベース監査仕様に関する情報を含みます。|  
|[sys.server_audits](/sql/relational-databases/system-catalog-views/sys-server-audits-transact-sql)|サーバー インスタンス内の各 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査について行を 1 つずつ含みます。|  
|[sys.server_audit_specifications](/sql/relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql)|サーバー インスタンス上の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査に含まれるサーバー監査仕様に関する情報を含みます。|  
|[sys.server_audit_specifications_details](/sql/relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql)|サーバー インスタンス上の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査に含まれるサーバー監査仕様の詳細 (アクション) に関する情報を含みます。|  
|[sys.server_file_audits](/sql/relational-databases/system-catalog-views/sys-server-file-audits-transact-sql)|サーバー インスタンス上の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査に含まれるファイル監査の種類に関する拡張情報を含みます。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査の各機能とコマンドには、個別の権限要件があります。  
  
 サーバー監査またはサーバー監査の仕様を作成、変更、削除する場合、サーバー プリンシパルには、ALTER ANY SERVER AUDIT または CONTROL SERVER の権限が必要です。 データベース監査の仕様を作成、変更、削除する場合、データベース プリンシパルには、ALTER ANY DATABASE AUDIT 権限、またはデータベースに対する ALTER 権限か CONTROL 権限が必要です。 さらに、プリンシパルには、データベースに接続する権限、または ALTER ANY SERVER AUDIT 権限か CONTROL SERVER 権限が必要です。  
  
 特に指定がない限り、カタログ ビューを表示する場合、プリンシパルに次のいずれかのロールまたは権限が必要です。  
  
-   固定サーバー ロール sysadmin のメンバーシップ。  
  
-   CONTROL SERVER 権限。  
  
-   VIEW SERVER STATE 権限。  
  
-   ALTER ANY AUDIT 権限。  
  
-   VIEW AUDIT STATE 権限 (sys.server_audits カタログ ビューにアクセスするプリンシパルのみに付与)。  
  
 動的管理ビューを使用するには、プリンシパルに VIEW SERVER STATE または ALTER ANY AUDIT 権限が必要です。  
  
 アクセス権および権限を付与する方法の詳細については、「[GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)」を参照してください。  
  
> [!CAUTION]  
>  sysadmin ロールのプリンシパルによって監査コンポーネントが勝手に書き換えられることも、db_owner ロールのプリンシパルによってデータベース内の監査の仕様が勝手に書き換えられることもないとはいえません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査では、監査の仕様を作成または変更するログオンが、ALTER ANY DATABASE AUDIT 以上の権限を持っているかどうかが検証されます。 ただし、データベースにアタッチするときには検証は行われません。 すべてのデータベース監査の仕様は、sysadmin ロールまたは db_owner ロールのプリンシパルと同等の信頼性しかないと見なす必要があります。  
  
## <a name="related-tasks"></a>Related Tasks  
 [サーバー監査およびサーバー監査の仕様を作成する](create-a-server-audit-and-server-audit-specification.md)  
  
 [サーバー監査およびデータベース監査の仕様を作成する](create-a-server-audit-and-database-audit-specification.md)  
  
 [SQL Server 監査ログを表示する](view-a-sql-server-audit-log.md)  
  
 [セキュリティ ログへの SQL Server 監査イベントの書き込み](write-sql-server-audit-events-to-the-security-log.md)  
  
## <a name="topics-closely-related-to-auditing"></a>監査と密接に関連したトピック  
 [[サーバーのプロパティ] &#40;[セキュリティ] ページ&#41;](../../../database-engine/configure-windows/server-properties-security-page.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログインの監査をオンにする方法について説明します。 監査レコードは Windows アプリケーション ログに格納されます。  
  
 [c2 audit mode サーバー構成オプション](../../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の C2 セキュリティ準拠の監査モードについて説明します。  
  
 [Security Audit イベント カテゴリ &#40;SQL Server Profiler&#41;](../../../relational-databases/event-classes/security-audit-event-category-sql-server-profiler.md)  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]で使用できる監査イベントについて説明します。 詳細については、「 [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md)」を参照してください。  
  
 [SQL トレース](../../sql-trace/sql-trace.md)  
 SQL トレースを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Profiler からではなく、ユーザー独自のアプリケーションからトレースを手動で作成する方法について説明します。  
  
 [DDL トリガー](../../triggers/ddl-triggers.md)  
 データ定義言語 (DDL) トリガーを使用してデータベースの変更を追跡する方法について説明します。  
  
 [Microsoft TechNet:SQL Server TechCenter:SQL Server 2005 - セキュリティと保護](https://go.microsoft.com/fwlink/?LinkId=101152)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セキュリティに関する最新の情報を提供します。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server 監査のアクション グループとアクション](sql-server-audit-action-groups-and-actions.md)   
 [SQL Server 監査レコード](sql-server-audit-records.md)  
  
  
