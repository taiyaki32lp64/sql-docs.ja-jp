---
title: 'バックアップと復元: 相互運用性と共存 (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server], related features
- restoring [SQL Server], files
- restoring files [SQL Server], related features
- backups [SQL Server], files or filegroups
- file backups [SQL Server], related features
ms.assetid: 69f212b8-edcd-4c5d-8a8a-679ced33c128
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96fd1b081ec9d990014dc61db7938f745cffa041
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922437"
---
# <a name="backup-and-restore-interoperability-and-coexistence-sql-server"></a>バックアップと復元: 相互運用性と共存 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のいくつかの機能のバックアップと復元に関する考慮事項について説明します。 このような機能には、ファイル復元とデータベースの起動、オンライン復元と無効化されたインデックス、データベース ミラーリング、段階的な部分復元、およびフルテキスト インデックスが含まれます。  
  
 **このトピックの内容**  
  
-   [ファイル復元とデータベースの起動](#FileRestoreAndDbStartup)  
  
-   [オンライン復元と無効化されたインデックス](#OnlineRestoreAndDisabledIndexes)  
  
-   [データベース ミラーリングおよびバックアップと復元](#DbMandBnR)  
  
-   [段階的な部分復元とフルテキスト インデックス](#PiecemealAndFTIndexes)  
  
-   [ファイル バックアップと復元と圧縮](#FileBnRandCompression)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="FileRestoreAndDbStartup"></a> ファイル復元とデータベースの起動  
 ここで説明する内容は、複数のファイル グループを含む [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのみに適用されます。  
  
> [!NOTE]  
>  データベースが起動されると、そのデータベースの終了時にファイルがオンラインだったファイル グループのみが復旧され、オンラインになります。  
  
 データベースの起動中に問題が発生した場合、復旧は失敗し、データベースは SUSPECT に設定されます。 問題のファイルを特定できる場合、データベース管理者は、それらのファイルをオフラインにし、データベースの再起動を試行できます。 ファイルをオフラインにするには、次の [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) ステートメントを使用します。  
  
 ALTER DATABASE *database_name*ファイルの変更 (名前 **=' *`filename`* '** 、オフライン)  
  
 起動に成功した場合、オフライン ファイルが含まれるファイル グループはすべてオフライン状態で維持されます。  
  
##  <a name="OnlineRestoreAndDisabledIndexes"></a> オンライン復元と無効化されたインデックス  
 ここで説明する内容は、複数のファイル グループを含むデータベースと、単純復旧モデルの場合の 1 つ以上の読み取り専用ファイル グループに適用されます。  
  
 これらのケースにおいて、データベースがオンラインの場合、インデックスの作成、削除、有効化や無効化を行うことができるのは、インデックスのいずれかの部分を保持しているファイル グループがすべてオンラインのときだけです。  
  
 オフラインのファイル グループを復元する方法については、「[オンライン復元 &#40;SQL Server&#41;](online-restore-sql-server.md)」を参照してください。  
  
##  <a name="DbMandBnR"></a> データベース ミラーリングおよびバックアップと復元  
 ここで説明する内容は、複数のファイル グループを含む完全復旧モデルのデータベースだけに関連しています。  
  
> [!NOTE]  
>  データベース ミラーリング機能は、将来のバージョンの Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] を使用します。  
  
 データベース ミラーリングは、データベースの可用性を高めるためのソリューションです。 ミラーリングはデータベースごとに実装され、完全復旧モデルを使用するデータベースでのみ機能します。 詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  データベースのファイル グループのサブセットのコピーを配布するには、レプリケーションを使用します。ファイル グループ内のオブジェクトのうち、他のサーバーにコピーしたいものだけをレプリケートします。 レプリケーションの詳細については、「 [SQL Server のレプリケーション](../../relational-databases/replication/sql-server-replication.md)」を参照してください。  
  
### <a name="creating-the-mirror-database"></a>ミラー データベースの作成  
 WITH NORECOVERY を指定してプリンシパル データベースのバックアップをミラー サーバーに復元すると、ミラー データベースが作成されます。 この復元したデータベースの名前は、元のデータベースと同じ名前のままにする必要があります。 詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)のいくつかの機能のバックアップと復元に関する考慮事項について説明します。  
  
 段階的な部分復元シーケンスの使用がサポートされている場合は、これを使用してミラー データベースを作成できます。 ただし、ミラーリングを開始できるのは、すべてのファイル グループを復元し、通常はログ バックアップを復元して、ミラー データベースの状態をプリンシパル データベースの状態に十分近づけてからです。 詳細については、「[段階的な部分復元の実行 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)」を参照してください。  
  
### <a name="restrictions-on-backup-and-restore-during-mirroring"></a>ミラーリング中のバックアップおよび復元の制限  
 データベース ミラーリング セッションがアクティブの場合は、次の制限があります。  
  
-   ミラー データベースのバックアップおよび復元は実行できません。  
  
-   プリンシパル データベースのバックアップは可能ですが、BACKUP LOG WITH NORECOVERY オプションは使用できません。  
  
-   プリンシパル データベースの復元は実行できません。  
  
##  <a name="PiecemealAndFTIndexes"></a> 段階的な部分復元とフルテキスト インデックス  
 ここで説明する内容は、複数のファイル グループを含むデータベースのみ (単純復旧モデルのデータベースでは、読み取り専用ファイル グループのみ) に適用されます。  
  
 フルテキスト インデックスは、データベース ファイル グループに格納され、段階的な部分復元による影響を受ける可能性があります。 関連するテーブル データのいずれかと同じファイル グループにフルテキスト インデックスが格納されている場合、段階的な部分復元は想定どおりに機能します。  
  
> [!NOTE]  
>  フルテキスト インデックスが格納されているファイル グループのファイル グループ ID を表示するには、 [sys.fulltext_indexes](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql)の data_space_id 列を選択します。  
  
### <a name="full-text-indexes-and-tables-in-separate-filegroups"></a>ファイル グループが異なるフルテキスト インデックスとテーブル  
 フルテキスト インデックスが、関連するテーブル データのいずれとも異なるファイル グループに格納されている場合、先にどちらのファイル グループを復元しオンラインにするかによって段階的な部分復元の動作が異なります。  
  
-   関連するテーブル データを含むファイル グループより先に、フルテキスト インデックスを含むファイル グループが復元され、オンラインになる場合は、フルテキスト インデックスがオンラインになるとすぐ、フルテキスト検索が想定どおりに機能します。  
  
-   フルテキスト インデックスを含むファイル グループより先に、テーブル データを含むファイル グループが復元され、オンラインになる場合は、フルテキストの動作に影響があります。 インデックスがオンラインになっていないと、カタログの作成、カタログの再構築、またはカタログの再編成を起動する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが失敗するためです。 このようなステートメントには、CREATE FULLTEXT INDEX、ALTER FULLTEXT INDEX、DROP FULLTEXT INDEX、および ALTER FULLTEXT CATALOG があります。  
  
     この場合、次の要因が重要です。  
  
    -   フルテキスト インデックスに変更の追跡がある場合、インデックスのファイル グループがオンラインなっていないと、ユーザー DML が失敗します。 インデックスのファイル グループがオンラインになっていないと、削除操作も失敗します。  
  
    -   変更の追跡の状態にかかわらず、インデックスが使用できないので、フルテキスト クエリは失敗します。 フルテキスト クエリの実行時に、フルテキスト インデックスを含むファイル グループがオフラインだった場合、エラーが返されます。  
  
    -   状態関数 (FULLTEXTCATALOGPROPERTY など) は、フルテキスト インデックスにアクセスする必要がない場合にのみ成功します。 たとえば、オンラインのフルテキスト メタデータへのアクセスは成功しますが、 **uniquekeycount、itemcount** は失敗します。  
  
     フルテキスト インデックスのファイル グループが復元され、オンラインになった後は、インデックス データとテーブル データの整合性が保たれています。  
  
 ベース テーブルのファイル グループとフルテキスト インデックスのファイル グループの両方がオンラインになるとすぐに、一時停止中のフルテキスト作成がすべて再開されます。  
  
##  <a name="FileBnRandCompression"></a> ファイル バックアップと復元と圧縮  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、読み取り専用ファイル グループや読み取り専用データベースの NTFS ファイル システム データ圧縮がサポートされます。  
  
 圧縮された NTFS ファイルでは、読み取り専用ファイル グループのファイルの復元がサポートされます。 このようなファイル グループのバックアップや復元は、基本的には読み取り専用ファイル グループと同様に機能しますが、次の例外があります。  
  
-   圧縮されたボリュームに読み書き可能なファイル (読み書き可能なデータベースのプライマリ ファイルやログ ファイルなど) を復元すると、失敗してエラーが表示されます。  
  
-   圧縮されたボリュームに読み取り専用データベースを復元することは可能です。  
  
> [!NOTE]  
>  読み取りと書き込みが可能なデータベースのログ ファイルは、圧縮されたファイル システムには配置しないでください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [フルテキスト カタログとフルテキスト インデックスのバックアップおよび復元](../search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server データベースのバックアップと復元](back-up-and-restore-of-sql-server-databases.md)   
 [レプリケートされたデータベースのバックアップと復元](../replication/administration/back-up-and-restore-replicated-databases.md)   
 [アクティブなセカンダリ:セカンダリ レプリカでバックアップ&#40;AlwaysOn 可用性グループ&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
  
  
