---
title: master データベース | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], about
- master database [SQL Server]
ms.assetid: 660e909f-61eb-406b-bbce-8864dd629ba0
author: stevestein
ms.author: sstein
ms.openlocfilehash: e8c1447bfb5a4776430d24959267c7ec29aa48e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133601"
---
# <a name="master-database"></a>master データベース

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **master** データベースには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システムのシステム レベルの情報がすべて記録されます。 記録される情報には、ログオン アカウント、エンドポイント、リンク サーバー、システム構成設定など、インスタンス全体のメタデータが含まれます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、システム オブジェクトが **master** データベースではなく、 [Resource データベース](../../relational-databases/databases/resource-database.md)に格納されるようになりました。 また、 **master** は、他のすべてのデータベースの存在、それらのデータベース ファイルの場所、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の初期化情報を記録するデータベースでもあります。 したがって、 **master** データベースが使用できないと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を開始できません。  

> [!IMPORTANT]
> Azure SQL Database 単一データベースおよびエラスティック プールでは、master データベースと tempdb データベースのみが適用されます。 詳しくは、「[Azure SQL Database サーバーとは](https://docs.microsoft.com/azure/sql-database/sql-database-servers#what-is-an-azure-sql-database-server)」をご覧ください。 Azure SQL Database のコンテキストでの tempdb の詳細については、「[SQL Database の Tempdb データベース](tempdb-database.md#tempdb-database-in-sql-database)」を参照してください。 Azure SQL Database Managed Instance の場合、すべてのシステム データベースが適用されます。 Azure SQL Database の Managed Instance について詳しくは、「[マネージド インスタンスとは?](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)」をご覧ください。
  
## <a name="physical-properties-of-master"></a>master データベースの物理プロパティ

次の表は、SQL Server と Azure SQL Database Managed Instance に向けた **master** のデータ ファイルとログ ファイルの初期構成値の一覧です。 これらのファイルのサイズは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のエディションによって多少異なる場合があります。  
  
|ファイル|論理名|物理名|ファイル拡張|  
|----------|------------------|-------------------|-----------------|  
|プライマリ データ|master|master.mdf|ディスクがいっぱいになるまで 10% ずつ自動拡張|  
|Log|mastlog|mastlog.ldf|最大 2 TB まで 10% ずつ自動拡張|  
  
**master** のデータ ファイルとログ ファイルの移動方法の詳細については、「 [システム データベースの移動](../../relational-databases/databases/move-system-databases.md)」を参照してください。  

> [!IMPORTANT]
> Azure SQL Database サーバーの場合、ユーザーが **master** データベースのサイズを制御することはできません。
  
### <a name="database-options"></a>データベース オプション

SQL Server と Azure SQL Database Managed Instance に向けた **master** データベースの各データベース オプションの既定値と、そのオプションを変更できるかどうかを次の表に示します。 これらのオプションの現在の設定を表示するには、 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) カタログ ビューを使用します。  
  
> [!IMPORTANT]
> Azure SQL Database 単一データベースおよびエラスティック プールの場合、ユーザーがこれらのデータベースのオプションを制御することはできません。

|データベース オプション|既定値|変更可否|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|いいえ|  
|ANSI_NULL_DEFAULT|OFF|はい|  
|ANSI_NULLS|OFF|はい|  
|ANSI_PADDING|OFF|はい|  
|ANSI_WARNINGS|OFF|はい|  
|ARITHABORT|OFF|はい|  
|AUTO_CLOSE|OFF|いいえ|  
|AUTO_CREATE_STATISTICS|ON|はい|  
|AUTO_SHRINK|OFF|いいえ|  
|AUTO_UPDATE_STATISTICS|ON|はい|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|はい|  
|CHANGE_TRACKING|OFF|いいえ|  
|CONCAT_NULL_YIELDS_NULL|OFF|はい|  
|CURSOR_CLOSE_ON_COMMIT|OFF|はい|  
|CURSOR_DEFAULT|GLOBAL|はい|  
|データベース可用性オプション|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|いいえ<br /><br /> いいえ<br /><br /> いいえ|  
|DATE_CORRELATION_OPTIMIZATION|OFF|はい|  
|DB_CHAINING|ON|いいえ|  
|ENCRYPTION|OFF|いいえ|  
|MIXED_PAGE_ALLOCATION|ON|いいえ|  
|NUMERIC_ROUNDABORT|OFF|はい|  
|PAGE_VERIFY|CHECKSUM|はい|  
|PARAMETERIZATION|SIMPLE|はい|  
|QUOTED_IDENTIFIER|OFF|はい|  
|READ_COMMITTED_SNAPSHOT|OFF|いいえ|  
|RECOVERY|SIMPLE|はい|  
|RECURSIVE_TRIGGERS|OFF|はい|  
|Service Broker のオプション|DISABLE_BROKER|いいえ|  
|TRUSTWORTHY|OFF|はい|  
  
これらのデータベース オプションの説明は、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。  
  
## <a name="restrictions"></a>制限  
**master** データベースでは、次の操作は実行できません。  
  
- ファイルまたはファイル グループの追加。  
- 照合順序の変更。 既定の照合順序はサーバーの照合順序です。  
- データベース所有者の変更。 **master** は **sa**が所有します。  
- フルテキスト カタログまたはフルテキスト インデックスの作成。  
- データベース内のシステム テーブルのトリガーの作成。  
- データベースの削除。  
- データベースからの **guest** ユーザーの削除。  
- 変更データ キャプチャの有効化。  
- データベース ミラーリングへの参加。  
- プライマリ ファイル グループ、プライマリ データ ファイル、またはログ ファイルの削除。  
- データベース名またはプライマリ ファイル グループ名の変更。  
- データベースの OFFLINE への設定。  
- データベースまたはプライマリ ファイル グループの READ_ONLY への設定。  
  
## <a name="recommendations"></a>推奨事項  
**master** データベースで作業を行っているときは、次の推奨設定を考慮してください。  
  
- **master** データベースの現在のバックアップを、常に使用可能にする。  
- 次の操作後には、できるだけ早く **master** データベースのバックアップを作成する。  
  
  - データベースの作成、変更、または削除  
  - サーバーまたはデータベースの構成値の変更  
  - ログオン アカウントの変更または追加  
  
- **master**にはユーザー オブジェクトを作成しない。 ユーザー オブジェクトを作成すると、 **master** をより頻繁にバックアップする必要があります。  
- **master** データベースでは TRUSTWORTHY オプションを ON に設定しないでください。  
  
## <a name="what-to-do-if-master-becomes-unusable"></a>master が使用できない状態になった場合の対処方法  
 **master** が使用できない状態になった場合、このデータベースを次のいずれかの方法で使用できる状態に戻すことができます。  
  
- 現在のデータベース バックアップから **master** を復元します。  
  
  サーバー インスタンスを起動できる場合は、データベースの完全バックアップから **master** を復元できます。 詳細については、「[master データベースの復元 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)」を参照してください。  
  
- **master** を完全に再構築します。  
  
  **master** に深刻な破損があり、それが原因で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を起動できない場合、 **master**を再構築する必要があります。 詳細については、「 [システム データベースの再構築](../../relational-databases/databases/rebuild-system-databases.md)」を参照してください。  
  
  > [!IMPORTANT]  
  >  **master** を再構築すると、すべてのシステム データベースが再構築されます。  
  
## <a name="related-content"></a>関連コンテンツ  
- [システム データベースの再構築](../../relational-databases/databases/rebuild-system-databases.md)  
- [システム データベース](../../relational-databases/databases/system-databases.md)  
- [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
- [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
- [データベース ファイルの移動](../../relational-databases/databases/move-database-files.md)  
