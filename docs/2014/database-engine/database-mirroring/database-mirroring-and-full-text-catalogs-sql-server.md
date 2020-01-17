---
title: データベース ミラーリングとフルテキスト カタログ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- full-text catalogs [SQL Server], database mirroring
- catalogs [SQL Server], database mirroring
ms.assetid: e34072ae-fe8a-462d-bb03-02fa0987f793
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e90e2386fcd6c6d2f71e1cea31f253f8baac9195
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807297"
---
# <a name="database-mirroring-and-full-text-catalogs-sql-server"></a>データベース ミラーリングとフルテキスト カタログ (SQL Server)
  フルテキスト カタログが格納されたデータベースをミラー化するには、通常どおりにバックアップを使用してプリンシパル データベースの完全バックアップを作成した後、そのバックアップを復元してデータベースをミラー サーバーにコピーします。 詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)」を参照してください。  
  
## <a name="full-text-catalog-and-indexes-before-failover"></a>フェールオーバー前のフルテキスト カタログとフルテキスト インデックス  
 新しく作成されたミラー データベースのフルテキスト カタログは、データベースがバックアップされた時点と同じものです。 データベース ミラーリングの開始後、DDL ステートメント (CREATE FULLTEXT CATALOG、ALTER FULLTEXT CATALOG、および DROP FULLTEXT CATALOG) によって加えられたカタログレベルの変更は、ミラー データベース上で再生するためにログ記録されミラー サーバーに送信されます。 ただし、インデックスレベルの変更は、プリンシパル サーバーにログ記録されないため、ミラー データベース上では再現されません。 このため、プリンシパル データベース上でフルテキスト カタログの内容が変更されると、ミラー データベース上のフルテキスト カタログの内容と同期されていない状態になります。  
  
## <a name="full-text-indexes-after-failover"></a>フェールオーバー後のフルテキスト インデックス  
 フェールオーバー後、次のような状況では、新しいプリンシパル サーバー上でフルテキスト インデックスのフル クロールを実行することが必要になる場合や役立つ場合があります。  
  
-   フルテキスト インデックスでの変更の追跡が無効になっている場合は、次のステートメントを使用し、そのインデックスでフル クロールを開始する必要があります。  
  
     ALTER FULLTEXT INDEX ON *table_name* START FULL POPULATION  
  
-   変更の追跡を自動的に実行するようにフルテキスト インデックスが構成されている場合、そのフルテキスト インデックスは自動的に同期されます。 ただし、同期によってフルテキスト操作のパフォーマンスは若干低下します。 パフォーマンスが極端に低下する場合は、変更の追跡を無効にしてから、自動的に実行されるように再設定することにより、フル クロールを開始できます。  
  
    -   変更の追跡を無効にするには、次のステートメントを実行します。  
  
         ALTER FULLTEXT INDEX ON *table_name* SET CHANGE_TRACKING OFF  
  
    -   変更の追跡が自動的に実行されるように設定するには、次のステートメントを実行します。  
  
         ALTER FULLTEXT INDEX ON *table_name* SET CHANGE_TRACKING AUTO  
  
    > [!NOTE]  
    >  変更の自動追跡が有効かどうかを確認するには、 [OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql) 関数を使用して、テーブルの **TableFullTextBackgroundUpdateIndexOn** プロパティをクエリできます。  
  
 詳細については、「 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  フェールオーバー後にクロールを開始することは、復元後にクロールを開始することと同じです。  
  
## <a name="after-forcing-service"></a>サービスの強制後  
 サービスをミラー サーバーに強制 (データ損失が伴う場合もあります) した後、フル クロールを開始します。 フル クロールの開始方法は、フルテキスト インデックスの変更が追跡されるかどうかによって異なります。 詳細については、このトピックの「フェールオーバー後のフルテキスト インデックス」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-index-transact-sql)   
 [データベース ミラーリング &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [フルテキスト カタログとフルテキスト インデックスのバックアップおよび復元](../../relational-databases/indexes/indexes.md)  
  
  
