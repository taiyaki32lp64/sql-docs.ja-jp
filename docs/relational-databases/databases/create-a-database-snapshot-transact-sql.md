---
title: データベース スナップショットの作成 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], creating
ms.assetid: 187fbba3-c555-4030-9bdf-0f01994c5230
author: stevestein
ms.author: sstein
ms.openlocfilehash: 652ef86f26f92068465668cadeccf8e193db1f90
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708288"
---
# <a name="create-a-database-snapshot-transact-sql"></a>データベース スナップショットの作成 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース スナップショットを作成する唯一の方法は、 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用することです。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、データベース スナップショットの作成はサポートされません。  
  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
 任意の復旧モデルを使用できるソース データベースは、次の前提条件を満たす必要があります。  
  
-   サーバー インスタンスで、データベース スナップショットをサポートする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エディションが実行されている必要があります。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]でのデータベース スナップショットのサポートについては、「 [SQL Server 2016 の各エディションでサポートされる機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
-   ソース データベースは、データベース ミラーリング セッション内のミラー データベースである場合を除き、オンラインである必要があります。  
  
-   ミラー データベースにデータベース スナップショットを作成するには、データベースは同期済みの [ミラーリング状態](../../database-engine/database-mirroring/mirroring-states-sql-server.md)になっている必要があります。  
  
-   ソース データベースは、スケーラブルな共有データベースとして構成できません。  

- ソース データベースに MEMORY_OPTIMIZED_DATA ファイルグループを含めることはできません。 詳細については、「 [インメモリ OLTP に対してサポートされていない SQL Server の機能](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)」を参照してください 。

> [!IMPORTANT]
> その他の重要な考慮事項については、「 [Database Snapshots &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)を使用することです。  
  
##  <a name="Recommendations"></a> 推奨事項  
 このセクションでは、次のベスト プラクティスについて説明します。  
  
-   [ベスト プラクティス:データベース スナップショットの名前付け](#Naming)  
  
-   [ベスト プラクティス:データベース スナップショット数の制限](#Limiting_Number)  
  
-   [ベスト プラクティス:データベース スナップショットへのクライアント接続](#Client_Connections)  
  
####  <a name="Naming"></a> ベスト プラクティス:データベース スナップショットの名前付け  
 スナップショットを作成する前に、名前付けの方法を検討することが重要です。 各データベース スナップショットでは、一意のデータベース名が必要になります。 管理を容易にするために、次のようなデータベースを識別する情報を、スナップショット名に含めることができます。  
  
-   ソース データベースの名前。  
  
-   新しい名前がスナップショット用であるという指示  
  
-   任意のデータベース上のシーケンシャル スナップショットを区別するための、スナップショットの作成日や作成時刻、シーケンス番号、日時などの他のいくつかの情報  
  
 たとえば、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの一連のスナップショットについて考えてみます。 24 時間形式のクロックに基づいて、午前 6 時から午後 6 時までの間に、 6 時間間隔で毎日 3 つのスナップショットが作成されます。 毎日の各スナップショットは、24 時間保持された後削除され、同じ名前の新しいスナップショットに置き換えられます。 各スナップショット名は、次のように時刻を示しますが、日付は示しません。  
  
```  
AdventureWorks_snapshot_0600  
AdventureWorks_snapshot_1200  
AdventureWorks_snapshot_1800  
```  
  
 しかし、毎日のスナップショットの作成時刻が日によって異なる場合、あまり明確でない名前付け規則が適している場合もあります。たとえば次のような名前にします。  
  
```  
AdventureWorks_snapshot_morning  
AdventureWorks_snapshot_noon  
AdventureWorks_snapshot_evening  
```  
  
#### <a name="Limiting_Number"></a> ベスト プラクティス:データベース スナップショット数の制限  
 一連のスナップショットを長期にわたって作成することで、ソース データベースのシーケンシャルなスナップショットがキャプチャされます。 各スナップショットは、明示的に削除されるまで保持されます。 元のページが更新されるにつれて、各スナップショットが継続的に拡張されるので、新しいスナップショットの作成後に古いスナップショットを削除するとディスク領域を節約できます。  
  

**メモ** データベース スナップショットに戻すには、そのデータベースから他のすべてのスナップショットを削除する必要があります。  
  
####  <a name="Client_Connections"></a> ベスト プラクティス:データベース スナップショットへのクライアント接続  
 データベース スナップショットを使用するには、クライアントはそのスナップショットを見つける場所を認識している必要があります。 ユーザーは、あるデータベース スナップショットが作成または削除されている間でも、他のデータベース スナップショットから読み取ることができます。 ただし、既存のスナップショットを新しいスナップショットに置き換えるときに、クライアントを新しいスナップショットにリダイレクトする必要があります。 ユーザーは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、データベース スナップショットに手動で接続できます。 ただし、実稼働環境をサポートするには、ユーザーが意識しないうちにレポート作成クライアントをデータベースの最新のデータベース スナップショットにリダイレクトするような、プログラム ソリューションを作成する必要があります。  
  

  
####  <a name="Permissions"></a> Permissions  
 データベースを作成できるすべてのユーザーが、データベース スナップショットを作成できます。ただし、ミラー データベースのスナップショットを作成するには、 **sysadmin** 固定サーバー ロールのメンバーであることが必要です。  
  
##  <a name="TsqlProcedure"></a> データベース スナップショットの作成方法 (Transact-SQL の使用)  
 **データベース スナップショットを作成するには**  
  
>  この手順の例については、このセクションの後半の「 [例 (Transact-SQL)](#TsqlExample)」を参照してください。  
  
1.  ソース データベースの現在のサイズに基づいて、データベース スナップショットを格納するのに十分なディスク領域があることを確認します。 データベース スナップショットの最大サイズは、スナップショット作成時におけるソース データベースのサイズです。 詳細については、「[データベース スナップショットのスパース ファイルのサイズを表示する方法 &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)」を参照してください。  
  
2.  AS SNAPSHOT OF 句を使用して、CREATE DATABASE ステートメントをファイルに対して実行します。 スナップショットを作成するには、ソース データベースの各データベース ファイルの論理名を指定する必要があります。 構文は次のとおりです。  

     CREATE DATABASE *database_snapshot_name*  
  
     ON  
  
     (  
  
     NAME =*logical_file_name*,  
  
     FILENAME ='*os_file_name*'  
  
     ) [ ,...*n* ]  
  
     AS SNAPSHOT OF *source_database_name*  
  
     [;]  
  
     *source_**database_name* はソース データベース、*logical_file_name* はファイルを参照するときに SQL Server で使用される論理名、*os_file_name* はファイルを作成する際にオペレーティング システムが使用するパスとファイル名、*database_snapshot_name* はデータベースを戻す対象になるスナップショットの名前です。 この構文の詳細については、「 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)を使用することです。  
  
    > [!NOTE]  
    >  データベース スナップショットを作成する場合、ログ ファイル、オフラインのファイル、復元中のファイル、および機能していないファイルを CREATE DATABASE ステートメントで使用することはできません。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
  
> [!NOTE]  
>  この例で使用している拡張子 `.ss` は任意です。  
  
 ここでは、次の例について説明します。  
  
-   A. [AdventureWorks データベースのスナップショットを作成する](#Creating_on_AW)  
  
-   B. [Sales データベースのスナップショットを作成する](#Creating_on_Sales)
  
####  <a name="Creating_on_AW"></a> A. AdventureWorks データベースのスナップショットを作成する  
 この例では、 `AdventureWorks` データベースのデータベース スナップショットを作成します。 スナップショット名 `AdventureWorks_dbss_1800`と、そのスパース ファイルの名前 `AdventureWorks_data_1800.ss`は、作成時間が午後 6 時 (1,800 時間) であることを示しています。  
  
```  
CREATE DATABASE AdventureWorks_dbss1800 ON  
( NAME = AdventureWorks, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks_data_1800.ss' )  
AS SNAPSHOT OF AdventureWorks;  
GO  
```  
  
####  <a name="Creating_on_Sales"></a> B. Sales データベースのスナップショットを作成する  
 この例では、 `sales_snapshot1200`データベースのデータベース スナップショット `Sales` を作成します。 このデータベースは [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md). の例「ファイル グループのあるデータベースを作成する」で作成したものです。  
  
```  
--Creating sales_snapshot1200 as snapshot of the  
--Sales database:  
CREATE DATABASE sales_snapshot1200 ON  
( NAME = SPri1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\data\SPri1dat_1200.ss'),  
( NAME = SPri2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\data\SPri2dt_1200.ss'),  
( NAME = SGrp1Fi1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\data\SG1Fi1dt_1200.ss'),  
( NAME = SGrp1Fi2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\data\SG1Fi2dt_1200.ss'),  
( NAME = SGrp2Fi1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\data\SG2Fi1dt_1200.ss'),  
( NAME = SGrp2Fi2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\data\SG2Fi2dt_1200.ss')  
AS SNAPSHOT OF Sales;  
GO  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベース スナップショットの表示 &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [データベースをデータベース スナップショットに戻す](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
-   [データベース スナップショットの削除 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Database Snapshots &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  

