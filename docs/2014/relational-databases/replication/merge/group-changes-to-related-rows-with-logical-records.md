---
title: 論理レコードによる関連行への変更のグループ化 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ad76799c-4486-4b98-9705-005433041321
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b05d3b02c4fcd0d90b0b96a1a32c792537818e1e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62999856"
---
# <a name="group-changes-to-related-rows-with-logical-records"></a>論理レコードによる関連行への変更のグループ化
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 マージ レプリケーションの既定の動作では、データの変更は行ごとに処理されます。 この動作は多くの場合に適切ですが、アプリケーションによっては、関連する行を 1 つの単位として処理することが必要です。 マージ レプリケーションの論理レコード機能を使用すると、異なるテーブルの関連する行の間にリレーションシップを定義し、それらの行を 1 つの単位として処理できます。  
  
> [!NOTE]  
>  論理レコード機能は、単独で使用することも、結合フィルターと組み合わせて使用することもできます。 結合フィルターの詳細については、「 [Join Filters](join-filters.md)」を参照してください。 論理レコードを使用するには、パブリケーションの互換性レベルが少なくとも 90 RTM である必要があります。  
  
 以下の 3 つの関連テーブルについて考えてみます。  
  
 ![列名のみを持つ 3 つのテーブルの論理レコード](../media/logical-records-01.gif "列名のみを持つ 3 つのテーブルの論理レコード")  
  
 **Customers** テーブルは、このリレーションシップの親テーブルであり、主キー列 **CustID**を持ちます。 **Orders** テーブルは、主キー列 **OrderID**を持ちます。また、 **Customers** テーブルの **CustID** 列を参照する **CustID** 列に、外部キー制約が設定されています。 同様に、 **OrderItems** テーブルは主キー列 **OrderItemID**を持ちます。また、 **Orders** テーブルの **OrderID** 列を参照する **OrderID** 列に、外部キー制約が設定されています。  
  
 この例の論理レコードは、単一の **CustID** 値に関連付けられている **Orders** テーブルのすべての行と、 **Orders** テーブル内の行に関連付けられている **OrderItems** テーブルのすべての行で構成されます。 次の図は、Customer2 の論理レコードに含まれる、3 つのテーブルのすべての行を示しています。  
  
 ![値を持つ論理レコードの 3 つのテーブル](../media/logical-records-02.gif "値を持つ論理レコードの 3 つのテーブル")  
  
 アーティクル間で論理レコード リレーションシップを定義するには、「 [マージテーブル記事間の論理レコード関係を定義する](../publish/define-a-logical-record-relationship-between-merge-table-articles.md)」を参照してください。  
  
## <a name="benefits-of-logical-records"></a>論理レコードの利点  
 論理レコード機能には、2 つの主な利点があります。  
  
-   データ変更が 1 つの単位として適用されます。  
  
-   競合の検出および解決が、複数のテーブルの複数の行で同時に実行されます。  
  
### <a name="the-application-of-changes-as-a-unit"></a>変更を 1 つの単位として適用  
 論理レコードを使用している場合、マージ処理が接続の切断などで中断されると、関連するレプリケートされた変更の部分的に完了したセットは、ロールバックされます。 たとえば、サブスクライバーが **OrderID** = 6 で新しい注文を追加し、 **OrderItems** テーブルに **OrderID** = 6 用の新しい 2 つの行を **OrderItemID** = 10 および **OrderItemID** = 11 で追加したとします。  
  
 ![値を持つ論理レコードの 3 つのテーブル](../media/logical-records-04.gif "値を持つ論理レコードの 3 つのテーブル")  
  
 **OrderID** = 6 の **Orders** 行の処理を完了後、 **OrderItems** 10 および 11 の処理が完了するまでの間にレプリケーション処理が中断されると、論理レコードを使用していない場合、 **OrderID** = 6 の **OrderTotal** 値は、 **OrderItems** 行の **OrderAmount** 値の合計とは一致しません。 論理レコードを使用している場合、 **OrderID** = 6 の **Orders** 行は、関連する **OrderItems** の変更がレプリケートされるまで、コミットされません。  
  
 別のシナリオで、論理レコードを使用していて、だれかがマージ処理による変更の適用中にテーブルに対してクエリを実行した場合、そのユーザーには、変更がすべて完了するまで、部分的にレプリケートされた変更は表示されません。 たとえば、レプリケーション処理で **OrderID** = 6 の Orders 行をアップロードしても、 **OrderItems** 行がレプリケートされる前にユーザーがテーブルに対してクエリを実行した場合、 **OrderTotal** 値は、 **OrderAmount** 値の合計とは一致しません。 論理レコードを使用している場合、 **Orders** 行は、 **OrderItems** 行の処理が完了し、トランザクションが 1 つの単位としてコミットされるまで表示されません。  
  
### <a name="the-application-of-conflict-handling-to-more-than-one-table"></a>複数のテーブルへの競合処理の適用  
 2 つのサブスクライバーが上記のデータセットを保持しているケースを考えてみます。  
  
-   最初のサブスクライバーのユーザーは、 **OrderItemID** 5 の **OrderAmount** を 100 から 150 に変更し、 **OrderID** 3 の **OrderTotal** を 200 から 250 に変更します。  
  
-   2 番目のサブスクライバーのユーザーは、 **OrderItemID** 6 の **OrderAmount** を 25 から 125 に変更し、 **OrderID** 3 の **OrderTotal** を 200 から 300 に変更します。  
  
 これらの変更が論理レコードを使用せずにレプリケートされると、異なる **OrderTotal** の値が競合し、それらのうちのいずれかのみがレプリケートされます。 しかし、 **OrderItems** テーブルの競合してない変更は、競合することなくレプリケートされます。結果として、最終的な **OrderTotal** 値は、 **OrderItems** 行との一貫性を持たない状態になります。 このシナリオで論理レコードを使用した場合、 **Orders** テーブルの失われた変更に関連する **OrderItems** の変更もロールバックされ、最終的な **OrderTotal** 値は **OrderItems** 行の正確な集計になります。  
  
 論理レコードが使用される場合の競合の検出と解決に関する選択肢については、「[Detecting and Resolving Conflicts in Logical Records](advanced-merge-replication-conflict-resolving-in-logical-record.md)」 (論理レコードの競合の検出および解決) を参照してください。  
  
## <a name="considerations-for-using-logical-records"></a>論理レコードの使用に関する注意点  
 論理レコードを使用するときは、以下の点に注意してください。  
  
### <a name="general-considerations"></a>全般的な注意点  
  
-   論理レコード内のテーブルは可能な限り少なくすることをお勧めします。テーブル数は 5 つ以下にすることをお勧めします。  
  
-   論理レコードでは、次のデータ型の列は参照できません。  
  
    -   `varchar(max)` および `nvarchar(max)`  
  
    -   `varbinary(max)`  
  
    -   `text` および `ntext`  
  
    -   `image`  
  
    -   `XML`  
  
    -   `UDT`  
  
-   パブリッシュされたテーブルの外部キーのリレーションシップを CASCADE オプションで定義することはできません。 詳細については、「[CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)」および「[ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)」を参照してください。  
  
-   論理リレーション句で使用されている列は更新できません。  
  
-   ビジネス ロジック ハンドラーまたはカスタム競合回避モジュールによるカスタム競合解決は、論理レコードに含まれているアーティクルについてはサポートされていません。  
  
-   パラメーター化されたフィルターを含むパブリケーションで論理レコードが使用されている場合、各サブスクライバーをそのパーティションのスナップショットで初期化する必要があります。 サブスクライバーを別の方法で初期化した場合、マージ エージェントは失敗します。 詳細については、「 [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md)」を参照してください。  
  
-   論理レコードに関連する競合は、競合表示モジュールに表示されません。 これらの競合に関する情報を表示するには、レプリケーション ストアド プロシージャを使用します。 詳細については、「[マージ パブリケーションの競合情報の表示 (レプリケーション Transact-SQL プログラミング)](../view-conflict-information-for-merge-publications.md)」を参照してください。  
  
### <a name="publication-settings"></a>パブリケーションの設定  
  
-   パブリケーションの互換性レベルは 90 RTM 以上である必要があります。 詳細については、「[Replication Backward Compatibility](../replication-backward-compatibility.md)」 (レプリケーションの下位互換性) の「Publication Compatibility Level」(パブリケーションの互換性レベル) を参照してください。  
  
-   パブリケーションではネイティブ スナップショット モードを使用する必要があります。 論理レコードをサポートしない [!INCLUDE[ssEW](../../../includes/ssew-md.md)]にレプリケートしている場合を除き、これが既定になります。  
  
-   パブリケーションでは Web 同期は許可されません。 Web 同期の詳細については、「 [Web Synchronization for Merge Replication](../web-synchronization-for-merge-replication.md)」を参照してください。  
  
-   フィルター選択されたパブリケーションで論理レコードを使用するには  
  
    -   事前計算済みパーティションも使用する必要があります。 事前計算済みパーティションの要件は、論理レコードにも適用されます。 詳細については、「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](parameterized-filters-optimize-for-precomputed-partitions.md)」を参照してください。  
  
    -   重複しないパラメーター化されたフィルターは使用できません。 詳細については、「 [Parameterized Row Filters](parameterized-filters-parameterized-row-filters.md)」の「[パーティションのオプション] の設定」を参照してください。  
  
-   パブリケーションで結合フィルターを使用する場合、論理レコード リレーションシップに含まれるすべての結合フィルターに対し、 **join unique key** プロパティを **true** に設定する必要があります。 詳しくは、「 [Join Filters](join-filters.md)」をご覧ください。  
  
### <a name="relationships-between-tables"></a>テーブル間のリレーションシップ  
  
-   論理レコードを介して関連付けられたテーブルは、主キーと外部キーのリレーションシップを持っている必要があります。  
  
-   NOT FOR REPLICATION オプションは外部キー制約には設定できません。  
  
-   子テーブルは親テーブルを 1 つだけ持つことができます。  
  
     たとえば、データベース追跡の Class と Students が、次のような設計になっているとします。  
  
     ![複数の親テーブルを持つ子テーブル](../media/logical-records-03.gif "複数の親テーブルを持つ子テーブル")  
  
     論理レコードを使用して、このリレーションシップの 3 つのテーブルを表すことはできません。これは、 **ClassMembers** の行が単一の主キー行と関連付けられていないからです。 テーブル **Classes** および **ClassMembers** で論理レコードを形成することは可能であり、テーブル **ClassMembers** および **Students**で論理レコードを形成することも可能です。しかし、3 つのテーブルすべてで論理レコードを形成することはできません。  
  
-   パブリケーションに循環結合フィルター リレーションシップを含めることはできません。  
  
     **Customers**テーブル、 **Orders**テーブル、および **OrderItems**テーブルの例でいうと、 **Orders** テーブルに **OrderItems** テーブルを参照する外部キー制約もある場合、論理レコードは使用できません。  
  
## <a name="performance-implications-of-logical-records"></a>論理レコードのパフォーマンスへの影響  
 論理レコード機能を使用すると、パフォーマンスに影響を与えます。 論理レコードを使用しない場合、レプリケーション エージェントは特定のアーティクルに対するすべての変更を同時に処理できます。また、変更は行ごとに適用されるため、変更を適用するために必要なロックおよびトランザクション ログの要件は、最小限になります。  
  
 論理レコードを使用する場合、マージ エージェントは各論理レコード全体に対する変更をまとめて処理する必要があります。 これにより、マージ エージェントが行をレプリケートするためにかかる時間に影響を与えます。 さらに、エージェントは各論理レコードに対して個別にトランザクションを開くため、ロックの要件が増大します。  
  
## <a name="see-also"></a>関連項目  
 [マージ レプリケーションのアーティクル オプション](article-options-for-merge-replication.md)  
  
  
