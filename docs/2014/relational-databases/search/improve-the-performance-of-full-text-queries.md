---
title: フルテキスト クエリのパフォーマンスの向上 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: 0658dc74-25eb-4486-bbd6-e85c1f92c272
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96a37b1b59043079f52ca922f1ab3e7dfc9cc0ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011264"
---
# <a name="improve-the-performance-of-full-text-queries"></a>フルテキスト クエリのパフォーマンスの向上
  フルテキスト クエリのパフォーマンスを向上させるための推奨事項を次に示します。  
  
 フルテキスト クエリのパフォーマンスは、メモリ、ディスク速度、CPU 速度、コンピューター アーキテクチャなど、ハードウェア リソースの影響も受けます。  
  
-   [ALTER INDEX REORGANIZE](/sql/t-sql/statements/alter-index-transact-sql)を使用して、ベース テーブルのインデックスの断片化を解消します。  
  
-   [ALTER FULLTEXT CATALOG REORGANIZE](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)を使用して、フルテキスト カタログを再構成します。 このステートメントを実行するとそのカタログのフルテキスト インデックスがマスター マージされるため、この作業はパフォーマンス テストの前に行うようにしてください。  
  
-   フルテキスト キー列として、サイズの小さい列を選択します。 900 バイトの列がサポートされていますが、フルテキスト インデックスでは比較的小さいキー列を使用することをお勧めします。 `int` および `bigint` を使用すると、最適なパフォーマンスが得られます。  
  
-   整数型のフルテキスト キーを使用すると、 **docid** マッピング テーブルとの結合が回避されます。 したがって、整数型のフルテキスト キーにより、クエリのパフォーマンスが大幅に向上し、クロールのパフォーマンスも向上します。 フルテキスト キーがクラスター化インデックス キーでもある場合、パフォーマンスがさらに向上する可能性があります。  
  
-   複数の [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 述語を 1 つの CONTAINS 述語に統合します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、CONTAINS クエリに列の一覧を指定できます。  
  
-   フルテキスト キーまたは順位情報だけが必要な場合は、CONTAINS の代わりに [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) を使用し、FREETEXT の代わりに [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) を使用します。  
  
-   結果を制限してパフォーマンスを向上させるには、FREETEXTTABLE 関数および CONTAINSTABLE 関数の *top_n_by_rank* パラメーターを使用します。 *top_n_by_rank* を使用すると、最も関連性の高いヒットだけを呼び出すことができます。 ビジネス シナリオですべてのヒットを呼び出す必要がない場合 (つまり、 *総呼び出し*が不要な場合) にのみ、このパラメーターを使用してください。  
  
    > [!NOTE]  
    >  一般に、総呼び出しは法務シナリオで必要とされますが、e ビジネスなどのビジネス シナリオではパフォーマンスの方が重視されることがあります。  
  
-   フルテキスト クエリ プランをチェックして、適切な結合プランが選択されていることを確認します。 必要であれば結合ヒントやクエリ ヒントを使用します。 フルテキスト クエリでパラメーターが使用されている場合は、パラメーターの初回の値によってクエリ プランが決定されます。 OPTIMIZE FOR [クエリ ヒント](/sql/t-sql/queries/hints-transact-sql-query) を使用すると、クエリのコンパイルに使用される値を強制的に指定できます。 これにより、決定的なクエリ プランを実現してパフォーマンスを強化できます。  
  
-   非常に多くのフルテキスト インデックス フラグメントがフルテキスト インデックスに含まれている場合、クエリのパフォーマンスが大幅に低下する可能性があります。 フラグメントの数を減らすには、 [ALTER FULLTEXT CATALOG](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの REORGANIZE オプションを使用してフルテキスト カタログを再構成します。 このステートメントは、実質的に、すべてのフラグメントを単一のより大きなフラグメントにマージし、フルテキスト インデックスから古いエントリをすべて削除します。  
  
-   フルテキスト検索では、CONTAINSTABLE で指定した論理演算子 (AND、OR) を、SQL 結合として実装することも、フルテキスト実行 STVF (ストリーミング テーブル値関数) 内部に実装することもできます。 通常、論理演算子を 1 種類だけ使用するクエリはフルテキスト実行によってのみ実装され、論理演算子が混在するクエリは SQL 結合も保持します。 フルテキスト実行 STVF 内部に論理演算子を実装すると、複数の特別なインデックス プロパティが使用され、SQL 結合よりはるかに高速になります。 この理由から、可能な限り 1 種類だけの論理演算子を使用してクエリを作成することをお勧めします。  
  
-   選択的リレーションの述語が含まれているアプリケーションにおいて、選択的リレーションの述語と非選択的なフルテキスト述語を使用するクエリでは、クエリ オプティマイザーを使用するように記述した場合に最適なパフォーマンスを得られる可能性があります。 この場合、効果的なクエリ プランを作成するために述語を利用するかプッシュダウンを適用するかが、クエリ オプティマイザーによって判断されます。 この方法は、リレーショナル データをフルテキスト データとしてインデックス作成するよりも単純であり、多くの場合、効率的でもあります。  
  
## <a name="related-resources"></a>関連リソース  
 [SQL Server 2008 フルテキスト検索: 内部と機能強化](https://go.microsoft.com/fwlink/?LinkId=129544)  
  
## <a name="see-also"></a>関連項目  
 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql)   
 [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql)  
  
  
