---
title: 変更データ キャプチャの有効化と無効化
ms.custom: seo-dt-2019
ms.date: 01/02/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- change data capture [SQL Server], enabling databases
- change data capture [SQL Server], disabling databases
- change data capture [SQL Server], disabling tables
ms.assetid: b741894f-d267-4b10-adfe-cbc14aa6caeb
author: rothja
ms.author: jroth
ms.openlocfilehash: 82ff8e58891d07ccbecfef119c05c0cef1bbb06e
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095269"
---
# <a name="enable-and-disable-change-data-capture-sql-server"></a>変更データ キャプチャの有効化と無効化 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、データベースおよびテーブルに対して変更データ キャプチャを有効または無効にする方法について説明します。  
  
## <a name="enable-change-data-capture-for-a-database"></a>データベースでの変更データ キャプチャの有効化  
 個々のテーブルに対してキャプチャ インスタンスを作成する前に、 **sysadmin** 固定サーバー ロールのメンバーがデータベースで変更データ キャプチャを有効にする必要があります。 これは、データベース コンテキストでストアド プロシージャ [sys.sp_cdc_enable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md) を実行することにより行われます。 データベースが既に有効であるかどうかを確認するには、**sys.databases** カタログ ビューの **is_cdc_enabled** 列に対してクエリを実行します。  
  
 データベースで変更データ キャプチャを有効にすると、 **cdc** スキーマ、 **cdc** ユーザー、メタデータ テーブル、その他のシステム オブジェクトがデータベースに作成されます。 **cdc** スキーマには、変更データ キャプチャ メタデータ テーブルが含まれています。ソース テーブルで変更データ キャプチャを有効にした後には、変更データのリポジトリとして機能する個々の変更テーブルも含まれます。 **cdc** スキーマには、変更データのクエリの実行に使用する関連のシステム関数も含まれています。  
  
 変更データ キャプチャでは、 **cdc** スキーマと **cdc** ユーザーを専用で使用することが必要です。 *cdc* という名前のスキーマやデータベース ユーザーが現在データベースに存在する場合は、そのスキーマやユーザーを削除するか、名前を変更しないと、そのデータベースで変更データ キャプチャを有効にすることはできません。  
  
 データベースの有効化の例については、データベースでの変更データ キャプチャの有効化のテンプレートを参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でこのテンプレートを見つけるには、 **[表示]** メニューの **[テンプレート エクスプローラー]** をクリックし、 **[SQL Server テンプレート]** を選択します。 **Change Data Capture** はサブフォルダーです。 このトピックで参照したすべてのテンプレートは、このフォルダー内にあります。 **ツール バーには** [テンプレート エクスプローラー] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] アイコンもあります。  
  
```sql  
-- ====  
-- Enable Database for CDC template   
-- ====  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_db  
GO  
```  
  
## <a name="disable-change-data-capture-for-a-database"></a>データベースでの変更データ キャプチャの無効化  
 **sysadmin** 固定サーバー ロールのメンバーは、データベース コンテキストでストアド プロシージャ [sys.sp_cdc_disable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) を実行し、データベースの変更データ キャプチャを無効にすることができます。 データベースを無効にする前に個々のテーブルを無効にする必要はありません。 データベースを無効にすると、 **cdc** ユーザー、スキーマ、変更データ キャプチャ ジョブなど、関連するすべての変更データ キャプチャ メタデータが削除されます。 ただし、変更データ キャプチャによって作成されたゲーティング ロールは自動的には削除されないので、明示的に削除する必要があります。 データベースが有効になっているかどうかを確認するには、sys.databases カタログ ビューの **is_cdc_enabled** 列に対してクエリを実行します。  
  
 変更データ キャプチャが有効になっているデータベースを削除すると、変更データ キャプチャ ジョブも自動的に削除されます。  
  
 データベースの無効化の例については、データベースでの変更データ キャプチャの無効化のテンプレートを参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でこのテンプレートを見つけるには、 **[表示]** 、 **[テンプレート エクスプローラー]** 、 **[SQL Server テンプレート]** の順にクリックします。 **Change Data Capture** は、このトピックで参照されるすべてのテンプレートを含んだサブフォルダーです。 **ツール バーには** [テンプレート エクスプローラー] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] アイコンもあります。  
  
```sql  
-- =======  
-- Disable Database for Change Data Capture template   
-- =======  
USE MyDB  
GO  
EXEC sys.sp_cdc_disable_db  
GO  
```  
  
## <a name="enable-change-data-capture-for-a-table"></a>テーブルでの変更データ キャプチャの有効化  
 データベースで変更データ キャプチャを有効にすると、 **db_owner** 固定データベース ロールのメンバーはストアド プロシージャ **sys.sp_cdc_enable_table**を使用して個々のソース テーブルに対してキャプチャ インスタンスを作成できるようになります。 ソース テーブルで変更データ キャプチャが既に有効にされているかどうかを確認するには、 **sys.tables** カタログ ビューの is_tracked_by_cdc 列を調べます。  
  
 キャプチャ インスタンスの作成時に、次のオプションを指定できます。  
  
 **キャプチャするソース テーブルの列**。  
  
 既定では、ソース テーブルのすべての列がキャプチャ対象列として識別されます。 プライバシーやパフォーマンス上の理由で、列のサブセットのみを追跡する場合は、 *\@captured_column_list* パラメーターを使用して列のサブセットを指定します。  
  
 **変更テーブルを含むファイル グループ。**  
  
 既定では、変更テーブルはデータベースの既定のファイル グループにあります。 データベース所有者が個々の変更テーブルの場所を制御するには、 *\@filegroup_name* パラメーターを使用して、キャプチャ インスタンスに関連付けられている変更テーブルに対して特定のファイル グループを指定します。 指定するファイル グループはあらかじめ存在している必要があります。 通常、変更テーブルはソース テーブルとは別のファイル グループに配置することをお勧めします。 *\@filegroup_name* パラメーターの使用例については、**ファイル グループ オプションを指定するテーブルの有効化**のテンプレートをご覧ください。  
  
```sql  
-- =========  
-- Enable a Table Specifying Filegroup Option Template  
-- =========  
USE MyDB  
GO  
  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = N'MyRole',  
@filegroup_name = N'MyDB_CT',  
@supports_net_changes = 1  
GO  
```  
  
 **変更テーブルへのアクセスを制御するためのロール。**  
  
 名前付きのロールの目的は、変更データへのアクセスを制御することです。 指定されるロールは、既存の固定サーバー ロールの場合もデータベース ロールの場合もあります。 指定のロールが存在しない場合は、その名前のデータベース ロールが自動的に作成されます。 **sysadmin** ロールのメンバーと **db_owner** ロールのメンバーには、変更テーブルのデータへのフル アクセス権が与えられます。 他のすべてのユーザーには、ソース テーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。 さらに、ロールが指定されている場合、 **sysadmin** ロールと **db_owner** ロールのいずれのメンバーでもないユーザーも、指定のロールのメンバーである必要があります。  
  
 ゲーティング ロールを使用しない場合は、 *\@role_name* パラメーターを明示的に NULL に設定する必要があります。 ゲーティング ロールなしでテーブルを有効にする例については、 **ゲーティング ロールなしでのテーブルの有効化** のテンプレートをご覧ください。  
  
```sql  
-- =========  
-- Enable a Table Without Using a Gating Role template   
-- =========  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = NULL,  
@supports_net_changes = 1  
GO  
  
```  
  
 **差分変更を照会するための関数。**  
  
 キャプチャ インスタンスには、定義した期間内に発生したすべての変更テーブル エントリを返すためのテーブル値関数が常に含まれています。 この関数の名前は、"cdc.fn_cdc_get_all_changes_" の後ろにキャプチャ インスタンス名を付加したものです。 詳細については、「[cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)」を参照してください。  
  
 *\@supports_net_changes* パラメーターを 1 に設定すると、キャプチャ インスタンスに対して差分変更追跡の関数も生成されます。 この関数では、呼び出しで指定した期間内に変更された各行についてそれぞれ 1 つの変更のみが返されます。 詳細については、「[cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)」を参照してください。  
  
 差分変更のクエリをサポートするには、行を一意に識別するための主キーまたは一意のインデックスがソース テーブルに必要です。 一意のインデックスを使用する場合は、 *\@index_name* パラメーターを使用してインデックスの名前を指定する必要があります。 主キーまたは一意のインデックスで定義した列は、キャプチャするソース列の一覧に含まれている必要があります。  
  
 両方のクエリ関数を使用したキャプチャ インスタンスの作成例については、 **テーブルでのすべての変更クエリと差分変更クエリの有効化** のテンプレートを参照してください。  
  
```sql  
-- =============  
-- Enable a Table for All and Net Changes Queries template   
-- =============  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = N'MyRole',  
@supports_net_changes = 1  
GO  
```  
  
> [!NOTE]
>  既存の主キーのあるテーブルで変更データ キャプチャが有効化され、代替となる一意のインデックスの識別に *\@index_name* パラメーターが使用されていない場合、変更データ キャプチャ機能では主キーが使用されます。 その後は、テーブルの変更データ キャプチャを無効にしてからでなければ、主キーに変更を加えることはできません。 これは、変更データ キャプチャの構成時に差分変更のクエリのサポートが要求されたかどうかには関係ありません。 変更データ キャプチャが有効化された時点でテーブルに主キーがない場合、その後追加された主キーは変更データ キャプチャでは無視されます。 変更データ キャプチャでは、テーブルで変更データ キャプチャが有効化された後で作成された主キーは使用しないので、キーおよびキー列は制限なく削除できます。  
  
## <a name="disable-change-data-capture-for-a-table"></a>テーブルでの変更データ キャプチャの無効化  
 **db_owner** 固定データベース ロールのメンバーは、ストアド プロシージャ **sys.sp_cdc_disable_table**を使用して個々のソース テーブルのキャプチャ インスタンスを削除できます。 ソース テーブルで変更データ キャプチャが現在有効になっているかどうかを確認するには、 **sys.tables** カタログ ビューの **is_tracked_by_cdc** 列を調べます。 無効化の後、データベースに対して有効なテーブルがない場合は、変更データ キャプチャ ジョブも削除されます。  
  
 変更データ キャプチャが有効になっているテーブルを削除すると、そのテーブルに関連する変更データ キャプチャ メタデータも自動的に削除されます。  
  
 テーブルの無効化の例については、テーブルでのキャプチャ インスタンスの無効化のテンプレートを参照してください。  
  
```sql  
-- =====  
-- Disable a Capture Instance for a Table template   
-- =====  
USE MyDB  
GO  
EXEC sys.sp_cdc_disable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@capture_instance = N'dbo_MyTable'  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [変更データの処理 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [変更データ キャプチャの管理と監視 &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
