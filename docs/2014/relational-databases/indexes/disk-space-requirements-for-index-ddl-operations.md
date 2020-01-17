---
title: インデックス DDL 操作に必要なディスク領域 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- temporary disk space [SQL Server]
ms.assetid: 35930826-c870-44c1-a966-a6a4638f62ef
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7dbb3fafd32ead6587d9c64eb6ccf2294ed4918b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63161807"
---
# <a name="disk-space-requirements-for-index-ddl-operations"></a>インデックス DDL 操作に必要なディスク領域
  ディスク領域は、インデックスを作成、再構築、または削除するときの重要な検討事項です。 ディスク領域が不足すると、パフォーマンスが低下したり、インデックス操作が失敗したりする場合があります。 このトピックでは、インデックス DDL (データ定義言語) 操作に必要なディスク領域を判断するのに役立つ一般的な情報を提供します。  
  
## <a name="index-operations-that-require-no-additional-disk-space"></a>追加のディスク領域を必要としないインデックス操作  
 次のインデックス操作では、追加のディスク領域は必要ありません。  
  
-   ALTER INDEX REORGANIZE (ただし、ログ領域は必要です)  
  
-   DROP INDEX (非クラスター化インデックスを削除している場合)  
  
-   DROP INDEX (MOVE TO 句を指定せずにオフラインでクラスター化インデックスを削除していて、非クラスター化インデックスが存在しない場合)  
  
-   CREATE TABLE (PRIMARY KEY 制約または UNIQUE 制約)  
  
## <a name="index-operations-that-require-additional-disk-space"></a>追加のディスク領域が必要なインデックス操作  
 他のすべてのインデックス DDL 操作では、操作中に使用する一時ディスク領域と、新しいインデックス構造を格納する永続的なディスク領域が追加で必要になります。  
  
 新しいインデックス構造を作成する場合、古い (作成元の) 構造と新しい (作成先の) 構造の両方を格納するディスク領域が、それぞれ適切なファイルおよびファイル グループで必要になります。 古い構造の割り当ては、インデックス作成トランザクションがコミットされるまで解除されません。  
  
 次のインデックス DDL 操作では、新しいインデックス構造が作成され、追加のディスク領域が必要になります。  
  
-   CREATE INDEX  
  
-   CREATE INDEX WITH DROP_EXISTING  
  
-   ALTER INDEX REBUILD  
  
-   ALTER TABLE ADD CONSTRAINT (PRIMARY KEY または UNIQUE)  
  
-   ALTER TABLE DROP CONSTRAINT (PRIMARY KEY または UNIQUE) (制約がクラスター化インデックスに基づいている場合)  
  
-   DROP INDEX MOVE TO (クラスター化インデックスのみ該当)  
  
## <a name="temporary-disk-space-for-sorting"></a>並べ替え用の一時ディスク領域  
 作成元の構造と作成先の構造を格納するために必要なディスク領域以外に、並べ替えに使用する一時ディスク領域も必要になります。ただし、クエリ オプティマイザーにより、並べ替えを必要としない実行プランが検出された場合は除きます。  
  
 並べ替えが必要な場合、一度に 1 つの新しいインデックスに対して並べ替えが実行されます。 たとえば、1 つのステートメント内でクラスター化インデックスと関連する非クラスター化インデックスを再構築すると、インデックスは順番に並べ替えられます。 したがって、並べ替えに必要な追加の一時ディスク領域のサイズは、並べ替えるインデックスの中で最も大きなインデックスのサイズと同じサイズになります。 通常は、クラスター化インデックスのサイズが最も大きくなります。  
  
 SORT_IN_TEMPDB オプションを ON に設定した場合は、最も大きいインデックスのサイズが **tempdb**のサイズを超えないようにする必要があります。 このオプションを使用すると、インデックスの作成に使用する一時ディスク領域は増えますが、 **tempdb** がユーザー データベースとは異なるディスク セットにある場合、インデックスの作成に必要な時間を短縮できることがあります。  
  
 SORT_IN_TEMPDB を OFF (既定) に設定した場合、パーティション インデックスを含む各インデックスは、作成先のディスク領域で並べ替えられます。この場合、必要になるのは新しいインデックス構造のディスク領域のみです。  
  
 ディスク領域の計算例については、「 [インデックスのディスク領域の例](index-disk-space-example.md)」をご覧ください。  
  
## <a name="temporary-disk-space-for-online-index-operations"></a>オンライン インデックス操作用の一時ディスク領域  
 インデックス操作をオンラインで実行する場合、追加の一時ディスク領域が必要になります。  
  
 クラスター化インデックスをオンラインで作成、再構築、または削除すると、古いブックマークを新しいブックマークにマップする非クラスター化インデックスが一時的に作成されます。 SORT_IN_TEMPDB オプションを ON に設定した場合、この一時インデックスは **tempdb**に作成されます。 SORT_IN_TEMPDB を OFF に設定した場合は、新しいインデックスと同じファイル グループまたはパーティション構成が使用されます。 一時マッピング インデックスには、テーブルの行ごとに 1 つのレコードが格納されます。レコードの内容は、古いブックマーク列と新しいブックマーク列を組み合わせたもので、uniqueifier とレコード識別子が含まれます。両方のブックマークで使用されている列のコピーは 1 つしか含まれません。 オンラインでのインデックス操作の詳細については、「 [オンラインでのインデックス操作の実行](perform-index-operations-online.md)」を参照してください。  
  
> [!NOTE]  
>  SORT_IN_TEMPDB オプションは、DROP INDEX ステートメントには設定できません。 一時マッピング インデックスは、常に新しいインデックスと同じファイル グループまたはパーティション構成に作成されます。  
  
 オンライン インデックス操作では、行のバージョン管理を使用して、他のトランザクションによる変更がインデックス操作に影響を与えないようにしています。 そのため、読み取った行の共有ロックを要求する必要がなくなります。 オンライン インデックス操作と同時にユーザーの更新操作と削除操作を実行するには、 **tempdb**にバージョン レコード用の領域が必要になります。 詳細については、「 [オンラインでのインデックス操作の実行](perform-index-operations-online.md) 」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [インデックスのディスク領域の例](index-disk-space-example.md)  
  
 [インデックス操作用のトランザクション ログのディスク領域](transaction-log-disk-space-for-index-operations.md)  
  
 [テーブル サイズの見積もり](../databases/estimate-the-size-of-a-table.md)  
  
 [クラスター化インデックスのサイズの見積もり](../databases/estimate-the-size-of-a-clustered-index.md)  
  
 [非クラスター化インデックスのサイズの算出](../databases/estimate-the-size-of-a-nonclustered-index.md)  
  
 [ヒープ サイズの見積もり](../databases/estimate-the-size-of-a-heap.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
 [インデックスの FILL FACTOR の指定](specify-fill-factor-for-an-index.md)  
  
 [インデックスの再編成と再構築](indexes.md)  
  
  
