---
title: 事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication], about precomputed partitions
ms.assetid: 85654bf4-e25f-4f04-8e34-bbbd738d60fa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8f80afa10c1dbd067648db26c2bed0f423f371b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250549"
---
# <a name="optimize-parameterized-filter-performance-with-precomputed-partitions"></a>事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化
  事前計算済みパーティションは、フィルター選択されたマージ パブリケーションのパフォーマンス最適化に使用されます。 フィルター選択されたパブリケーションで論理レコードを使用する場合にも事前計算済みパーティションが必要になります。 論理レコードの詳細については、「[論理レコードによる関連行への変更をグループ化](group-changes-to-related-rows-with-logical-records.md)」を参照してください。  
  
 サブスクライバーがパブリッシャーに同期するとき、パブリッシャーはサブスクライバーのフィルターを評価して、サブスクライバーのパーティションまたはデータセットに属する行を識別する必要があります。 フィルター選択されたデータセットを受け取る各サブスクライバーに対して、パブリッシャーの変更内容のパーティション メンバーシップを決定する処理を *パーティション評価*と呼びます。 事前計算済みパーティションがない場合は、特定のサブスクライバーに対する最後のマージ エージェントの実行以降、パブリッシャーのフィルター選択された列に対して加えられた変更ごとにパーティション評価を実行する必要があります。さらに、パブリッシャーと同期するすべてのサブスクライバーについて、この処理を繰り返し行う必要があります。  
  
 ただし、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンで実行中のパブリッシャーとサブスクライバーが事前計算済みパーティションを使用している場合は、パブリッシャーのすべての変更に対するパーティション メンバーシップは既に計算済みであり、変更が行われる時点まで有効になります。 その結果、サブスクライバーはパブリッシャーとの同期時に、パーティションに関連する変更内容のダウンロードを即座に開始できます。パーティションの評価処理が実行されることはありません。 パブリケーションに変更点、サブスクライバー、およびアーティクルが多数存在する場合は、この機能によってパフォーマンスの大幅な向上が期待できます。  
  
 事前計算済みパーティションを使用するだけでなく、スナップショットを事前に生成するか、最初の同期時にサブスクライバーからスナップショットの生成および適用を要求できるようにしてください。 これらのオプションの両方またはどちらかを使用して、パラメーター化されたフィルターを使用するパブリケーションに対するスナップショットを提供します。 これらのオプションのどちらかを指定しないと、 **bcp** ユーティリティを使用するのではなく、一連の SELECT ステートメントおよび INSERT ステートメントを使用してサブスクリプションが初期化されます。この処理は、かなり低速で実行されます。 詳細については、「 [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md)」を参照してください。  
  
 **事前計算済みパーティションを使用するには**  
  
 上記のガイドラインに準拠するすべての新規および既存パブリケーションでは、事前計算済みパーティションが既定で有効になっています。 この設定は [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を使用して変更することもできますし、プログラムを使用して変更することもできます。 詳細については、「 [Optimize Parameterized Row Filters](../publish/optimize-parameterized-row-filters.md)」を参照してください。  
  
## <a name="requirements-for-using-precomputed-partitions"></a>事前計算済みパーティションを使用するための要件  
 以下の要件が満たされる場合、新規に作成されるマージ パブリケーションは既定で事前計算済みパーティションが有効になります。また、既存のパブリケーションは自動的にこの機能が使用できるようにアップグレードされます。 パブリケーションが要件を満たさない場合は、事前計算済みパーティションを使用できるようにパブリケーションを変更できます。 要件を満たすアーティクルと要件を満たさないアーティクルが混在している場合は、パブリケーションを 2 つ作成し、そのうちの 1 つで事前計算済みパーティションを有効にすることを検討してください。  
  
### <a name="requirements-for-filter-clauses"></a>フィルター句の必要要件  
  
-   HOST_NAME() や SUSER_SNAME() など、パラメーター化された行フィルターで使用する関数はパラメーター化されたフィルター句に直接記述してください。ビューまたは動的関数の内部で入れ子にすることはできません。 これらの関数の詳細については、「[HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql)、「[SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql)」、および「[パラメーター化された行フィルター](parameterized-filters-parameterized-row-filters.md)」を参照してください。  
  
-   パーティションの作成後、各サブスクライバーに返される値を変更することはできません。 たとえば、フィルターで HOST_NAME() を使用する場合 (および HOST_NAME() の値をオーバーライドしない場合)、サブスクライバーでコンピューター名を変更しないでください。  
  
-   結合フィルターに動的関数 (HOST_NAME() や SUSER_SNAME() など、同期するサブスクライバーによって異なる値に評価される関数) を含めることはできません。 動的関数はパラメーター化された行フィルターでのみ使用できます。  
  
-   非決定的関数はフィルター句の中では使用できません。 非決定的関数の詳細については、「 [Deterministic and Nondeterministic Functions](../../user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
-   結合フィルター句またはパラメーター化されたフィルター句で参照されるビューに動的関数を含めることはできません。  
  
-   循環結合フィルターのリレーションシップをパブリケーションに格納することはできません。  
  
### <a name="database-collation"></a>データベースの照合順序  
  
-   事前計算済みパーティションを使用する場合、比較を行う際にはテーブルや列ではなくデータベースの照合順序が常に使用されます。 以下のシナリオについて考えてみます。  
  
    -   大文字と小文字が区別される照合順序のデータベースに、大文字と小文字が区別されない照合順序のテーブルが格納されています。  
  
    -   テーブルに **ComputerName**列が含まれており、パラメーター化されたフィルター内でサブスクライバーのホスト名と比較されます。  
  
    -   この列が "MYCOMPUTER" という値の行と "mycomputer" という値の行が 1 つずつテーブルに含まれています。  
  
     サブスクライバーが "mycomputer" というホスト名で同期する場合、このサブスクライバーが受け取る行は 1 行のみです。データベースの照合順序により、大文字と小文字を区別して比較されるからです。 事前計算済みパーティションを使用しない場合、サブスクライバーは両方の行を受け取ります。テーブルの照合順序により、大文字と小文字は区別されないからです。  
  
## <a name="performance-of-precomputed-partitions"></a>事前計算済みパーティションのパフォーマンス  
 事前計算済みパーティションを使用する場合、サブスクライバーからパブリッシャーに変更内容をアップロードするときに若干のパフォーマンス コストがかかります。ただし、マージ処理に必要な時間の大部分は、パーティションの評価とパブリッシャーからサブスクライバーへの変更内容のダウンロードに費やされます。したがって、全体としてはパフォーマンスが大きく向上します。 パフォーマンスがどの程度向上するかは、同時に同期するサブスクライバーの数、およびあるパーティションから別のパーティションに行を移動する同期ごとの更新数によって異なります。  
  
## <a name="see-also"></a>参照  
 [パラメーター化された行フィルター](parameterized-filters-parameterized-row-filters.md)  
  
  
