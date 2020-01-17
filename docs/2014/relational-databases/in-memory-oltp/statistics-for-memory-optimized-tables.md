---
title: メモリ最適化テーブルの統計 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e47a8c6f5b0da31aea9168bbbc56bd9b28afb96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63155795"
---
# <a name="statistics-for-memory-optimized-tables"></a>メモリ最適化テーブルの統計
  クエリ オプティマイザーでは、クエリのパフォーマンスを向上させるクエリ プランを作成するために列に関する統計を使用します。 統計はデータベースのテーブルから収集され、データベース メタデータに格納されます。  
  
 統計は自動的に作成されますが、手動で作成することもできます。 たとえば、統計は、インデックスの作成時にインデックス キー列に対して自動的に作成されます。 統計の作成の詳細については、「 [Statistics](../statistics/statistics.md)」を参照してください。  
  
 テーブル データは通常、時間の経過に伴い、行が挿入、更新、または削除されて変化します。 これは、統計を定期的に更新する必要があることを意味します。 既定では、ディスク ベース テーブルの統計は、オプティマイザーが統計が古くなったと判断したときに自動的に更新されます。  
  
 メモリ最適化テーブルの統計は、既定では更新されません。 手動で更新する必要があります。 使用[UPDATE STATISTICS &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/update-statistics-transact-sql)の個々 の列、インデックス、またはテーブル。 使用[sp_updatestats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)と、すべてのユーザーとデータベースの内部テーブルの統計を更新します。  
  
 使用する場合[CREATE STATISTICS &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-statistics-transact-sql)または[UPDATE STATISTICS &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)を指定する必要があります`NORECOMPUTE`自動統計を無効にするにはメモリ最適化テーブルを更新します。 ディスク ベース テーブルでは、 [sp_updatestats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)テーブルが前回変更された場合のみの統計を更新[sp_updatestats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)します。 メモリ最適化テーブルでは、 [sp_updatestats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)常に更新された統計情報を生成します。 [sp_updatestats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)はメモリ最適化テーブルに適したオプションは、それ以外の場合に個別に統計を更新できるように、どのテーブルが大幅に変更する必要があります。  
  
 統計情報は、データのサンプリングまたはフル スキャンを実行するのいずれかで生成するか。 サンプリング統計は、データ分布を推定するためにテーブル データのサンプルのみを使用します。 フルスキャン統計は、データの分布を調べるためにテーブル全体をスキャンします。 通常、フルスキャン統計の方が正確ですが、計算にかかる時間が長くなります。 サンプリング統計はより速く収集できます。  
  
 ディスク ベース テーブルでは、既定ではサンプリング統計が使用されます。 メモリ最適化テーブルでは、フルスキャン統計のみをサポートしています。 使用する場合[CREATE STATISTICS &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-statistics-transact-sql)または[UPDATE STATISTICS &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)、指定する必要があります、`FULLSCAN`オプションは、メモリ最適化テーブル。  
  
 メモリ最適化テーブルの統計に関するその他の注意点を次に示します。  
  
-   メモリ最適化テーブルのインデックスはテーブルを使用して作成されます。 インデックス キー列の統計は、テーブルが空のときに作成されます。 したがって、これらの統計は、データがテーブルに読み込まれた後に更新する必要があります。  
  
-   ネイティブ コンパイル ストアド プロシージャの場合、プロシージャのコンパイル時にプロシージャ内のクエリの実行プランが最適化されます。 これは、統計が更新されたときではなく、プロシージャが作成されたときおよびサーバーが再起動されたときにのみ発生します。 したがって、テーブルには代表的なデータのセットが含まれている必要があり、統計はプロシージャが作成される前に最新の状態にする必要があります  (ネイティブ コンパイル ストアド プロシージャは、データベースがオフラインになってから再度オンラインに戻った場合、またはサーバーが再起動された場合に再コンパイルされます)。  
  
## <a name="guidelines-for-statistics-when-deploying-memory-optimized-tables"></a>メモリ最適化テーブルを配置するときの統計のガイドライン  
 クエリ オプティマイザーでクエリ プランを作成するときに最新の統計が使用されるように、次の 5 つの手順を使用してメモリ最適化テーブルを配置します。  
  
1.  テーブルとインデックスを作成します。 インデックスは、`CREATE TABLE` ステートメントでインラインで指定されます。  
  
2.  テーブルにデータを読み込みます。  
  
3.  テーブル上の統計を更新します。  
  
4.  テーブルにアクセスするストアド プロシージャを作成します。  
  
5.  ワークロードを実行します。これには、ネイティブ コンパイル ストアド プロシージャ、解釈された [!INCLUDE[tsql](../../../includes/tsql-md.md)] ストアド プロシージャ、およびアドホック バッチが混在する場合があります。  
  
 データを読み込んで統計を更新してからネイティブ コンパイル ストアド プロシージャを作成することにより、オプティマイザーで統計をメモリ最適化テーブル用に使用できます。 これによって、プロシージャをコンパイルすると効率的なクエリ プランが作成されます。  
  
## <a name="guidelines-for-maintaining-statistics-on-memory-optimized-tables"></a>メモリ最適化テーブルでの統計の管理のガイドライン  
 統計を最新に保つためには、メモリ最適化テーブルの統計を定期的に更新します。  
  
 データが頻繁に変更される場合は、統計を頻繁に更新する必要があります。 たとえば、バッチ更新の後にテーブルの統計を更新します。 統計を更新した後、更新された統計の利点を得られるように、ネイティブ コンパイル ストアド プロシージャを削除して再作成します。  
  
 .  
  
 ピーク ワークロード中に統計を更新しないでください。  
  
 統計を更新するには:  
  
-   使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]に[メンテナンス プランの作成](../maintenance-plans/create-a-maintenance-plan.md)で、[統計の更新タスク](../maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
-   または、後で説明する [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを使用して統計を更新します。  
  
 1 つのメモリ最適化テーブルの統計を更新する (*myschema*します。 *Mytable*)、次のスクリプトを実行します。  
  
```  
UPDATE STATISTICS myschema.Mytable WITH FULLSCAN, NORECOMPUTE  
```  
  
 現在のデータベース内のすべてのメモリ最適化テーブルの統計を更新するには、次のスクリプトを実行します。  
  
```sql  
DECLARE @sql NVARCHAR(MAX) = N''  
  
SELECT @sql += N'  
   UPDATE STATISTICS ' + quotename(schema_name(schema_id)) + N'.' + quotename(name) + N' WITH FULLSCAN, NORECOMPUTE'  
FROM sys.tables WHERE is_memory_optimized=1  
  
EXEC sp_executesql @sql  
```  
  
 データベース内のすべてのテーブルの統計を更新する実行[sp_updatestats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)します。  
  
 次のサンプルでは、メモリ最適化テーブルの最終更新日を報告します。 この情報は、統計を更新する必要があるかどうかを判断するのに役立ちます。  
  
```sql  
select t.object_id, t.name, sp.last_updated as 'stats_last_updated'  
from sys.tables t join sys.stats s on t.object_id=s.object_id cross apply sys.dm_db_stats_properties(t.object_id, s.stats_id) sp  
where t.is_memory_optimized=1  
```  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブル](memory-optimized-tables.md)  
  
  
