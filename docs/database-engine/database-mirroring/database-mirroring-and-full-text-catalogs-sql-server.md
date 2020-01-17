---
title: データベース ミラーリングとフルテキスト カタログ
description: フルテキスト カタログを含むデータベースでデータベース ミラーを構成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: high-availability
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
ms.openlocfilehash: 816c5f5dea693a03054f2e35315ed3d121c7abaf
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822288"
---
# <a name="database-mirroring-and-full-text-catalogs-sql-server"></a>データベース ミラーリングとフルテキスト カタログ (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  フルテキスト カタログが格納されたデータベースをミラー化するには、通常どおりにバックアップを使用してプリンシパル データベースの完全バックアップを作成した後、そのバックアップを復元してデータベースをミラー サーバーにコピーします。 詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)を使用します。  
  
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
    >  変更の自動追跡が有効かどうかを確認するには、 [OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md) 関数を使用して、テーブルの **TableFullTextBackgroundUpdateIndexOn** プロパティをクエリできます。  
  
 詳細については、「 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
>  フェールオーバー後にクロールを開始することは、復元後にクロールを開始することと同じです。  
  
## <a name="after-forcing-service"></a>サービスの強制後  
 サービスをミラー サーバーに強制 (データ損失が伴う場合もあります) した後、フル クロールを開始します。 フル クロールの開始方法は、フルテキスト インデックスの変更が追跡されるかどうかによって異なります。 詳細については、このトピックの「フェールオーバー後のフルテキスト インデックス」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [フルテキスト カタログとフルテキスト インデックスのバックアップおよび復元](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
  
