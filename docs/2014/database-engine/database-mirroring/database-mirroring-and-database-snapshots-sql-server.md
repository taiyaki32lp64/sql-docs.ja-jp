---
title: データベース ミラーリングとデータベース スナップショット (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- snapshots [SQL Server database snapshots], database mirroring
- database snapshots [SQL Server], database mirroring
ms.assetid: 0bf1be90-7ce4-484c-aaa7-f8a782f57c5f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3c643ad9a84c6afe5b6ff08fd6716753ef42f79e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807269"
---
# <a name="database-mirroring-and-database-snapshots-sql-server"></a>データベース ミラーリングとデータベース スナップショット (SQL Server)
  可用性を維持するために運用しているミラー データベースを利用して、レポート作成の負荷を軽減できます。 ミラー データベースをレポート作成に利用するには、ミラー データベースでデータベース スナップショットを作成し、クライアント接続要求を最新のスナップショットに出力します。 データベース スナップショットは、その作成時に存在していたソース データベースの静的な読み取り専用スナップショットであり、トランザクションに一貫性があります。 ミラー データベースにデータベース スナップショットを作成するには、データベースは同期済みのミラーリング状態になっている必要があります。  
  
 ミラー データベース自体とは異なり、データベース スナップショットはクライアントにアクセスできます。 ミラー サーバーがプリンシパル サーバーと通信している間は、レポート作成用クライアントに対してスナップショットに接続するように指示できます。 データベース スナップショットは静的なので、新しいデータは使用できないことに注意してください。 ユーザーが比較的新しいデータを使用できるようにするには、定期的に新しいデータベース スナップショットを作成し、アプリケーションが着信クライアント接続を最新のスナップショットに出力することが必要です。  
  
 新しいデータベース スナップショットはほとんど空ですが、時間が経過し、初めて更新されるデータベース ページが増えるにつれて拡張されます。 データベース上の各スナップショットはこのように段階的に拡張されるため、各データベース スナップショットは、通常のデータベースと同じ量のリソースを消費します。 ミラー サーバーおよびプリンシパル サーバーの構成によって異なりますが、1 つのミラー データベースに過度に多くのデータベース スナップショットを配置すると、プリンシパル データベース上のパフォーマンスが低下する可能性があります。 そのため、ミラー データベースには少数の比較的新しいスナップショットのみを保持することをお勧めします。 通常、置き換えるスナップショットを作成した後に、着信クエリを新しいスナップショットに再出力し、現在のクエリが完了した後に以前のスナップショットを削除する必要があります。  
  
> [!NOTE]  
>  データベース スナップショットの詳細については、「 [Database Snapshots &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)」を参照してください。  
  
 役割の交代が発生した場合、データベースとそのスナップショットは、一時的にユーザーの接続を切断して、再起動されます。 その後、データベース スナップショットは、そのデータベース スナップショットが作成されたサーバー インスタンス上に残り、それが新しいプリンシパル データベースになります。 ユーザーは、フェールオーバーの発生後、このスナップショットを引き続き使用できます。 ただし、これによって、新しいプリンシパル サーバーにさらに負荷がかかります。 パフォーマンスを重視する環境の場合は、新しいミラー データベースが使用できるようになったらその新しいミラー データベース上にスナップショットを作成し、クライアントを新しいスナップショットに再出力し、以前のミラー データベースからすべてのデータベース スナップショットを削除することをお勧めします。  
  
> [!NOTE]  
>  頻繁にスケールアウトされる、レポート ソリューション専用サーバーの場合は、レプリケーションを検討してください。 詳細については、「 [SQL Server Replication](../install-windows/install-sql-server-replication.md)」を参照してください。  
  
## <a name="example"></a>例  
 この例では、ミラー データベースでスナップショットを作成します。  
  
 データベース ミラーリング セッションのデータベースが [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]であるとします。 この例では、 `AdventureWorks` ドライブにある `F` データベースのミラー コピーでデータベース スナップショットを 3 つ作成します。 これらのスナップショットには、おおよその作成時間を識別するために `AdventureWorks_0600`、 `AdventureWorks_1200`、および `AdventureWorks_1800` という名前が付けられています。  
  
1.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]のミラーで最初のデータベース スナップショットを作成します。  
  
    ```  
    CREATE DATABASE AdventureWorks_0600  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_0600.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
2.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]のミラーで 2 番目のデータベース スナップショットを作成します。 まだ `AdventureWorks_0600` を使用している場合は、このスナップショットを引き続き使用できます。  
  
    ```  
    CREATE DATABASE AdventureWorks_1200  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1200.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     この時点で、新しいクライアント接続をプログラムによって最新のスナップショットに出力できます。  
  
3.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]のミラーで 3 番目のスナップショットを作成します。 まだ `AdventureWorks_0600` または `AdventureWorks_1200` を使用している場合は、このスナップショットを引き続き使用できます。  
  
    ```  
    CREATE DATABASE AdventureWorks_1800  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1800.SNP')  
        AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     この時点で、新しいクライアント接続をプログラムによって最新のスナップショットに出力できます。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベース スナップショットの作成 &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [データベース スナップショットの表示 &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [データベース スナップショットの削除 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  

  
## <a name="see-also"></a>関連項目  
 [Database Snapshots &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [データベース ミラーリング セッションへのクライアントの接続 &#40;SQL Server&#41;](connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  
