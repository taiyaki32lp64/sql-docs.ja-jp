---
title: システム データベース | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- system databases [SQL Server]
- displaying system database data
- modifying system data
- viewing system database data
ms.assetid: 30468a7c-4225-4d35-aa4a-ffa7da4f1282
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 916fd6d996a1a5270173d290c61f262ddf3f797b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871129"
---
# <a name="system-databases"></a>システム データベース
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、次のシステム データベースが用意されています。  
  
|システム データベース|説明|  
|---------------------|-----------------|  
|[master データベース](master-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスのシステムレベルの情報をすべて記録します。|  
|[msdb データベース](msdb-database.md)|警告やジョブのスケジュールを設定するために SQL Server エージェントにより使用されます。|  
|[model データベース](model-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで作成されたすべてのデータベースのテンプレートとして使用されます。 データベース サイズ、照合順序、復旧モデル、およびその他のデータベース オプションなどの **model** データベースに変更を加えると、その変更内容は、それ以降に作成されるすべてのデータベースに適用されます。|  
|[Resource データベース](resource-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に装備されているシステム オブジェクトを格納する読み取り専用のデータベースです。 システム オブジェクトは、物理的には **Resource** データベースに保存されていますが、すべてのデータベースの **sys** スキーマに論理的に表示されます。|  
|[tempdb データベース](tempdb-database.md)|一時オブジェクトや生成途中の結果セットを保存するためのワークスペースです。|  
  
## <a name="modifying-system-data"></a>システム データの変更  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ユーザーは、システム テーブル、システム ストアド プロシージャ、カタログ ビューなどのシステム オブジェクトに含まれている情報を直接更新できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、代わりに完全な管理ツール セットが用意されています。ユーザーは、これらのツールを使用して、システムを完全に管理し、データベース内のすべてのユーザーとオブジェクトを管理できます。 その一部を次に示します。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]などの管理ユーティリティ。  
  
-   SQL-SMO API。 このツールを使用すると、プログラマはアプリケーションに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を管理するための完全な機能を含めることができます。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトとストアド プロシージャ。 これらのツールでは、システム ストアド プロシージャと [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL ステートメントを使用できます。  
  
 上記のツールを使用すると、アプリケーションをシステム オブジェクトの変更による影響から保護できます。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に追加された新機能をサポートするために、そのバージョンのシステム テーブルを変更する必要があることがあります。 多くの場合、システム テーブルを直接参照する SELECT ステートメントを実行しているアプリケーションでは、旧形式のシステム テーブルに依存しています。 そのような場合、システム テーブルに対して SELECT ステートメントを実行するアプリケーションが作成し直されるまで、サイトを新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアップグレードできない可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、システム ストアド プロシージャ、DDL、および SQL-SMO の公開された各インターフェイスを考慮し、これらの旧バージョンとの互換性を維持できるように機能します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム テーブルで定義されたトリガーでは、システムの動作が変更されることがあるので、このようなトリガーはサポートしていません。  
  
> [!NOTE]  
>  システム データベースを UNC 共有ディレクトリに置くことはできません。  
  
## <a name="viewing-system-database-data"></a>システム データベース データの表示  
 システム テーブルに対する直接的なクエリを実行するような [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、アプリケーションが必要とする情報を取得する方法が他にない場合を除いて、作成しないでください。 代わりに、アプリケーションで、次のツールを使用してカタログ情報やシステム情報を取得することをお勧めします。  
  
-   システム カタログ ビュー。  
  
-   SQL-SMO。  
  
-   WMI (Windows Management Instrumentation) インターフェイス。  
  
-   カタログ関数、メソッド、属性、または、ADO、OLE DB、ODBC などのアプリケーションで使用されるデータ API のプロパティ。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] システム ストアド プロシージャと組み込み関数。  
  
## <a name="related-tasks"></a>Related Tasks  
 [システム データベースのバックアップと復元 &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [オブジェクト エクスプローラーのシステム オブジェクトの非表示](../../ssms/object/object-explorer.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [カタログ ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)  
  
 [データベース](databases.md)  
  
  
