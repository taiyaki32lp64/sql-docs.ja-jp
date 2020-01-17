---
title: フルテキスト クエリのパフォーマンスの向上 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
ms.assetid: 0658dc74-25eb-4486-bbd6-e85c1f92c272
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e0b08e445cf22760f41da3e21e086c20fc927f8f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021158"
---
# <a name="improve-the-performance-of-full-text-queries"></a>フルテキスト クエリのパフォーマンスの向上
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  フルテキスト クエリのパフォーマンスを向上させるための推奨事項を次に示します。  
  
 フルテキスト クエリのパフォーマンスは、メモリ、ディスク速度、CPU 速度、コンピューター アーキテクチャなど、ハードウェア リソースの影響も受けます。  
  
-   [ALTER INDEX REORGANIZE](../../t-sql/statements/alter-index-transact-sql.md)を使用して、ベース テーブルのインデックスの断片化を解消します。  
  
-   [ALTER FULLTEXT CATALOG REORGANIZE](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)を使用して、フルテキスト カタログを再構成します。 このステートメントを実行するとそのカタログのフルテキスト インデックスがマスター マージされるため、この作業はパフォーマンス テストの前に行うようにしてください。  
  
-   フルテキスト キー列として、サイズの小さい列を選択します。 900 バイトの列がサポートされていますが、フルテキスト インデックスでは比較的小さいキー列を使用することをお勧めします。 **int** および **bigint** を使用すると、最適なパフォーマンスが得られます。  
  
-   整数型のフルテキスト キーを使用すると、 **docid** マッピング テーブルとの結合が回避されます。 したがって、整数型のフルテキスト キーにより、クエリのパフォーマンスが大幅に向上し、クロールのパフォーマンスも向上します。 フルテキスト キーがクラスター化インデックス キーでもある場合、パフォーマンスがさらに向上する可能性があります。  
  
-   複数の [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 述語を 1 つの CONTAINS 述語に統合します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、CONTAINS クエリに列の一覧を指定できます。  
  
-   フルテキスト キーまたは順位情報だけが必要な場合は、CONTAINS の代わりに [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) を使用し、FREETEXT の代わりに [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) を使用します。  
  
-   結果を制限してパフォーマンスを向上させるには、FREETEXTTABLE 関数および CONTAINSTABLE 関数の *top_n_by_rank* パラメーターを使用します。 *top_n_by_rank* を使用すると、最も関連性の高いヒットだけを呼び出すことができます。 ビジネス シナリオですべてのヒットを呼び出す必要がない場合 (つまり、 *総呼び出し*が不要な場合) にのみ、このパラメーターを使用してください。  
  
    > [!NOTE]  
    >  一般に、総呼び出しは法務シナリオで必要とされますが、e ビジネスなどのビジネス シナリオではパフォーマンスの方が重視されることがあります。  
  
-   フルテキスト クエリ プランをチェックして、適切な結合プランが選択されていることを確認します。 必要であれば結合ヒントやクエリ ヒントを使用します。 フルテキスト クエリでパラメーターが使用されている場合は、パラメーターの初回の値によってクエリ プランが決定されます。 OPTIMIZE FOR [クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md) を使用すると、クエリのコンパイルに使用される値を強制的に指定できます。 これにより、決定的なクエリ プランを実現してパフォーマンスを強化できます。  
  
-   非常に多くのフルテキスト インデックス フラグメントがフルテキスト インデックスに含まれている場合、クエリのパフォーマンスが大幅に低下する可能性があります。 フラグメントの数を減らすには、 [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの REORGANIZE オプションを使用してフルテキスト カタログを再構成します。 このステートメントは、実質的に、すべてのフラグメントを単一のより大きなフラグメントにマージし、フルテキスト インデックスから古いエントリをすべて削除します。  
  
-   フルテキスト検索では、CONTAINSTABLE で指定した論理演算子 (AND、OR) を、SQL 結合として実装することも、フルテキスト実行 STVF (ストリーミング テーブル値関数) 内部に実装することもできます。 通常、論理演算子を 1 種類だけ使用するクエリはフルテキスト実行によってのみ実装され、論理演算子が混在するクエリは SQL 結合も保持します。 フルテキスト実行 STVF 内部に論理演算子を実装すると、複数の特別なインデックス プロパティが使用され、SQL 結合よりはるかに高速になります。 この理由から、可能な限り 1 種類だけの論理演算子を使用してクエリを作成することをお勧めします。  
  
-   選択的リレーションの述語が含まれているアプリケーションにおいて、選択的リレーションの述語と非選択的なフルテキスト述語を使用するクエリでは、クエリ オプティマイザーを使用するように記述した場合に最適なパフォーマンスを得られる可能性があります。 この場合、効果的なクエリ プランを作成するために述語を利用するかプッシュダウンを適用するかが、クエリ オプティマイザーによって判断されます。 この方法は、リレーショナル データをフルテキスト データとしてインデックス作成するよりも単純であり、多くの場合、効率的でもあります。  
  
## <a name="related-resources"></a>関連リソース  
 [SQL Server 2008 フルテキスト検索: 内部と機能強化](https://go.microsoft.com/fwlink/?LinkId=129544)  
  
## <a name="see-also"></a>参照  
 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)   
 [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
  
