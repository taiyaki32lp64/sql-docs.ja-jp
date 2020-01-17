---
title: データベース ファイルとファイル グループ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3d75dee637a5579ca3f189e14333fbf9356623d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917279"
---
# <a name="database-files-and-filegroups"></a>データベース ファイルとファイル グループ
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各データベースには、データ ファイルとログ ファイルという少なくとも 2 つのオペレーティング システム ファイルがあります。 データ ファイルには、テーブル、インデックス、ストアド プロシージャ、およびビューなどのデータおよびオブジェクトが含まれます。 ログ ファイルには、データベース内のすべてのトランザクションを復旧するために必要な情報が含まれます。 データ ファイルは、割り当てと管理の目的でファイル グループにまとめることができます。  
  
## <a name="database-files"></a>データベース ファイル  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースには、次の表で示すように 3 種類のファイルがあります。  
  
|ファイル|説明|  
|----------|-----------------|  
|1 次式|プライマリ データ ファイルにはデータベースの起動情報が含まれており、データベース内の他のファイルを指し示します。 ユーザー データおよびオブジェクトは、このファイルまたはセカンダリ データ ファイルに格納できます。 各データベースには 1 つのプライマリ データ ファイルがあります。 プライマリ データ ファイルに推奨されるファイル名拡張子は .mdf です。|  
|セカンダリ|セカンダリ データ ファイルは省略可能です。また、ユーザー定義であり、ユーザー データが格納されます。 セカンダリ ファイルを使用すると、各ファイルを異なるディスク ドライブに配置することにより、複数のディスクにデータを分散できます。 また、データベースが 1 つの Windows ファイルの最大サイズを超えた場合には、セカンダリ データ ファイルを使用してデータベースを拡張できます。<br /><br /> セカンダリ データ ファイルに推奨されるファイル名拡張子は .ndf です。|  
|トランザクション ログ|トランザクション ログ ファイルには、データベースの復旧に使用されるログ情報が格納されます。 1 つのデータベースにトランザクション ログ ファイルが少なくとも 1 つ必要です。 トランザクション ログに推奨されるファイル名拡張子は .ldf です。|  
  
 たとえば、データとオブジェクトをすべて格納するプライマリ ファイルを 1 つとトランザクション ログ情報を格納するログ ファイルを 1 つ含む **Sales** という単純なデータベースを作成することができます。 または、プライマリ ファイルを 1 つとセカンダリ ファイルを 5 つ含む **Orders** というより複雑なデータベースを作成できます。 データベース内のデータとオブジェクトは 6 つすべてのファイルに分散され、4 つのログ ファイルにトランザクション ログ情報が含まれます。  
  
 既定では、データとトランザクション ログは同一のドライブおよびパス上に配置されます。 これは、単一のディスク システムを処理するために行われますが、 実稼働環境では最適ではない場合があります。 そのため、データとログ ファイルは別のディスクに配置することをお勧めします。  
  
## <a name="filegroups"></a>ファイル グループ  
 各データベースには、1 つのプライマリ ファイル グループがあります。 プライマリ ファイル グループには、プライマリ データ ファイル、および他のファイル グループに配置されていないセカンダリ ファイルが含まれます。 ユーザー定義のファイル グループを作成して、データベースの管理、データの割り当て、および配置をしやすくするために、データ ファイルをグループ化できます。  
  
 たとえば、3 つのディスク ドライブ上に 1 つずつ、合計 3 つのファイル (Data1.ndf、Data2.ndf、Data3.ndf) を作成し、これらのファイルをファイル グループ **fgroup1**にまとめます。 次に、ファイル グループ **fgroup1**上にテーブルを作成します。 このテーブル内にあるデータに対するクエリが 3 つのディスクにわたって分散されるため、パフォーマンスが向上します。 RAID (Redundant Array of Independent Disks) ストライプ セットにファイルを 1 つ作成しても、同じくらいパフォーマンスを向上させることができます。 ただし、ファイルとファイル グループを使用すれば、新しいファイルを新しいディスクに容易に追加できます。  
  
 すべてのデータ ファイルは、次の表に一覧表示されているファイル グループに格納されます。  
  
|[ファイル グループ]|説明|  
|---------------|-----------------|  
|1 次式|プライマリ ファイルが含まれているファイル グループ。 すべてのシステム テーブルがプライマリ ファイル グループに割り当てられます。|  
|ユーザー定義|ユーザーがデータベースを最初に作成したとき、または後で変更したときに、ユーザーが特別に作成したファイル グループ。|  
  
### <a name="default-filegroup"></a>既定のファイル グループ  
 所属させるファイル グループを指定せずにデータベース内にオブジェクトを作成すると、そのオブジェクトは既定のファイル グループに割り当てられます。 どのような場合でも、必ず 1 つのファイル グループが既定のファイル グループとして指定されます。 既定のファイル グループ内のファイルは、他のファイル グループに割り当てられない新しいオブジェクトを十分に格納できる大きさである必要があります。  
  
 PRIMARY ファイル グループは、ALTER DATABASE ステートメントを使用して変更しない限り、既定のファイル グループです。 システム オブジェクトとシステム テーブルは、変更後の既定のファイル グループではなく、引き続き PRIMARY ファイル グループに格納されます。  
  
## <a name="related-content"></a>関連コンテンツ  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
 [ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
