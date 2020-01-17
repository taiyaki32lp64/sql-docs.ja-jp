---
title: データベース | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- data warehouse [SQL Server]
- OLTP databases [SQL Server]
- databases [SQL Server], about databases
ms.assetid: 316eea58-81b8-4bf3-a1fc-801946740e94
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7de13f529dc0aab0c897ebe3dc1cb19220b13fd7
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154583"
---
# <a name="databases"></a>データベース
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベースは、特定の構造化データを格納するテーブルの集合です。 テーブルは一連の行 (レコードまたはタプル) と列 (属性) から構成されます。 テーブル内の各列は、特定の種類の情報 (日付、名前、金額、数字など) を格納するようにデザインされています。  
  
## <a name="basic-information-about-databases"></a>データベースに関する基本情報  
 コンピューターには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを 1 つまたは複数インストールできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各インスタンスは、1 つまたは複数のデータベースを格納できます。  データベース内には、スキーマと呼ばれるオブジェクト所有権グループが少なくとも 1 つ存在します。 それぞれのスキーマには、テーブル、ビュー、ストアド プロシージャなどのデータベース オブジェクトが存在します。 証明書や非対称キーなど、一部のオブジェクトは、データベースに含まれていますがスキーマには含まれていません。 テーブルの作成の詳細については、「 [テーブル](../tables/tables.md)」をご覧ください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベースは、ファイル システムのファイルに格納されます。 ファイルは、ファイル グループとしてグループ化することができます。 ファイルおよびファイル グループの詳細については、「 [データベース ファイルとファイル グループ](database-files-and-filegroups.md)」をご覧ください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにアクセスしたユーザーは、ログインとして識別されます。 データベースにアクセスしたユーザーは、データベース ユーザーとして識別されます。 データベース ユーザーは、ログインをベースに作成することができます。 包含データベースが有効になっている場合、ログインに基づかないデータベース ユーザーを作成できます。 ユーザーの詳細については、「[CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)」をご覧ください。  
  
 データベースへのアクセス権を持つユーザーには、そのデータベース内のオブジェクトへのアクセス権を与えることができます。 個々のユーザーに権限を付与することもできますが、データベース ロールを作成して、データベース ユーザーを追加したうえで、ロールへのアクセス権を付与することをお勧めします。 ユーザーではなくロールに対して権限を付与した方が、ユーザー数の増加や絶え間ない変更の中で、権限の一貫性を保ちやすく理解もしやすくなります。 ロールの権限の詳細については、「[CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql)」および「[プリンシパル &#40;データベース エンジン&#41;](../security/authentication-access/principals-database-engine.md)」をご覧ください。  
  
## <a name="working-with-databases"></a>データベースの操作  
 データベースを操作するユーザーの多くは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ツールを使用します。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ツールには、データベースおよびデータベース内のオブジェクトを作成するためのグラフィカル ユーザー インターフェイスが備わっています。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] には、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを記述することでデータベースを対話的に操作できるクエリ エディターも用意されています。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール ディスクからインストールすることも、MSDN からダウンロードすることもできます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|||  
|-|-|  
|[システム データベース](system-databases.md)|[データまたはログ ファイルのデータベースからの削除](delete-data-or-log-files-from-a-database.md)|  
|[包含データベース](contained-databases.md)|[データベースのデータ領域とログ領域情報の表示](display-data-and-log-space-information-for-a-database.md)|  
|[Azure でのデータファイルの SQL Server](sql-server-data-files-in-microsoft-azure.md)|[データベースのサイズを大きくする](increase-the-size-of-a-database.md)|  
|[データベース ファイルとファイル グループ](database-files-and-filegroups.md)|[データベースの名前変更](rename-a-database.md)|  
|[データベースの状態](database-states.md)|[データベースをシングル ユーザー モードに設定する](set-a-database-to-single-user-mode.md)|  
|[ファイルの状態](file-states.md)|[データベースの圧縮](shrink-a-database.md)|  
|[データベース サイズの見積もり](estimate-the-size-of-a-database.md)|[ファイルの圧縮](shrink-a-file.md)|  
|[他のサーバーへのデータベースのコピー](copy-databases-to-other-servers.md)|[データベースのプロパティの表示または変更](view-or-change-the-properties-of-a-database.md)|  
|[データベースのデタッチとアタッチ &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)|[SQL Server インスタンス上のデータベースの一覧表示](view-a-list-of-databases-on-an-instance-of-sql-server.md)|  
|[データベースに対するデータ ファイルまたはログ ファイルの追加](add-data-or-log-files-to-a-database.md)|[データベースの互換性レベルの表示または変更](view-or-change-the-compatibility-level-of-a-database.md)|  
|[データベースの構成設定の変更](change-the-configuration-settings-for-a-database.md)|[メンテナンス プラン ウィザードの使用](../maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|[ データベースの作成](create-a-database.md)|[ユーザー定義データ型の別名の作成](create-a-user-defined-data-type-alias.md)|  
|[データベースの削除](delete-a-database.md)|[Database Snapshots &#40;SQL Server&#41;](database-snapshots-sql-server.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
 [インデックス](../indexes/indexes.md)  
  
 [ビュー](../views/views.md)  
  
 [ストアド プロシージャ &#40;データベース エンジン&#41;](../stored-procedures/stored-procedures-database-engine.md)  
  
  
