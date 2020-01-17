---
title: 解釈された Transact-SQL を使用したメモリ最適化テーブルへのアクセス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c81ac6c0c8dcf7e24c80b426654164c668fcf3a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468609"
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>解釈された Transact-SQL を使用したメモリ最適化テーブルへのアクセス
  いくつかの例外を除き、[!INCLUDE[tsql](../../includes/tsql-md.md)] クエリまたは DML 操作 (SELECT、INSERT、UPDATE、または DELETE)、アドホック バッチ、および SQL モジュール (ストアド プロシージャ、テーブル値関数、トリガー、ビューなど) を使用して、メモリ最適化テーブルにアクセスできます。  
  
 インタープリターによって処理される [!INCLUDE[tsql](../../includes/tsql-md.md)] とは、ネイティブ コンパイル ストアド プロシージャとは異なる、 [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチまたはストアド プロシージャを意味します。 インタープリターによって処理される [!INCLUDE[tsql](../../includes/tsql-md.md)] による、メモリ最適化されたテーブルへのアクセスは、相互運用アクセスと呼ばれます。  
  
 メモリ最適化テーブルには、ネイティブ コンパイル ストアド プロシージャを使用してアクセスすることもできます。 ネイティブ コンパイル ストアド プロシージャは、パフォーマンスが重要な OLTP 操作に推奨されます。  
  
 解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] によるアクセスは、次のシナリオにお勧めします。  
  
-   アドホック クエリおよび管理タスク。  
  
-   通常は構造を使用するレポート クエリ (ウィンドウ関数など) は、ネイティブ コンパイル ストアド プロシージャでは使用できません。  
  
-   アプリケーション コードの変更を最小限に抑えて (またはコードを変更することなく)、アプリケーションのパフォーマンスが重要な部分をメモリ最適化テーブルに移行するには、次の手順を実行します。 テーブルを移行すると、パフォーマンス向上を確認できることがあります。 ストアド プロシージャをネイティブ コンパイル ストアド プロシージャに移行すると、いっそうのパフォーマンス向上が確認されることがあります。  
  
-   ネイティブ コンパイル ストアド プロシージャでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用できません。  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] 構造は、メモリ最適化テーブル内のデータにアクセスする、解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャでサポートされていません。  
  
|領域|サポートされていない|  
|----------|-----------------|  
|テーブルへのアクセス|TRUNCATE TABLE<br /><br /> MERGE (ターゲットとしてのメモリ最適化テーブル)<br /><br /> 動的カーソルおよびキーセット カーソル (これらは自動的に静的カーソルに降格されます)。<br /><br /> コンテキスト接続を使用した CLR モジュールからのアクセス。<br /><br /> インデックス付きビューから、メモリ最適化されたテーブルへの参照。|  
|複数のデータベース間|複数データベースにまたがるクエリ<br /><br /> 複数データベースにまたがるトランザクション<br /><br /> リンク サーバー|  
  
## <a name="table-hints"></a>テーブル ヒント  
 テーブル ヒントの詳細については、 [テーブル ヒント &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table). [!INCLUDE[hek_2](../../includes/hek-2-md.md)] をサポートするために SNAPSHOT 分離が追加されました。  
  
 次のテーブル ヒントは、解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してメモリ最適化テーブルにアクセスする場合はサポートされません。  
  
|||||  
|-|-|-|-|  
|HOLDLOCK|IGNORE_CONSTRAINTS|IGNORE_TRIGGERS|NOWAIT|  
|PAGLOCK|READCOMMITTED|READCOMMITTEDLOCK|READPAST|  
|READUNCOMMITTED|ROWLOCK|SPATIAL_WINDOW_MAX_CELLS = *integer*|TABLOCK|  
|TABLOCKXX|UPDLOCK|XLOCK||  
  
 解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用した明示的または暗黙的なトランザクションからメモリ最適化テーブルにアクセスする場合は、SNAPSHOT、REPEATABLEREAD、SERIALIZABLE などの分離レベルのテーブル ヒントを含める必要があります。あるいは、MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT を使用することもできます。 詳細については、次を参照してください。[メモリ最適化テーブルでのトランザクション分離レベルに関するガイドライン](memory-optimized-tables.md)と[ALTER DATABASE SET Options &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)します。  
  
> [!NOTE]  
>  自動コミット モードで実行されるクエリでアクセスするメモリ最適化テーブルの場合、分離レベルのテーブル ヒントは必要ありません。  
  
## <a name="see-also"></a>参照  
 [Transact-SQL によるインメモリ OLTP のサポート](transact-sql-support-for-in-memory-oltp.md)   
 [インメモリ OLTP への移行](migrating-to-in-memory-oltp.md)  
  
  
