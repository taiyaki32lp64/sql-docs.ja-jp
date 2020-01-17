---
title: クラスター化列ストア インデックスの使用 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 5af6b91c-724f-45ac-aff1-7555014914f4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1e65c3e277eb9a3e5e3703525b9c1ac06b423c96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773741"
---
# <a name="using-clustered-columnstore-indexes"></a>クラスター化列ストア インデックスの使用
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクラスター化 columnstore インデックスを使用するタスクです。  
  
 列ストア インデックスの概要については、次を参照してください。[列ストア インデックスの概念](../relational-databases/indexes/columnstore-indexes-described.md)します。  
  
 クラスター化列ストア インデックスについては、次を参照してください。[クラスター化列ストア インデックスを使用して](../relational-databases/indexes/indexes.md)します。  
  
## <a name="contents"></a>目次  
  
-   [クラスター化列ストア インデックスを作成します。](#create)  
  
-   [クラスター化列ストア インデックスを削除します。](#drop)  
  
-   [クラスター化列ストア インデックスにデータを読み込む](#load)  
  
-   [クラスター化列ストア インデックスのデータを変更します。](#change)  
  
-   [クラスター化列ストア インデックスを再構築します。](#rebuild)  
  
-   [クラスター化列ストア インデックスを再構成します。](#reorganize)  
  
##  <a name="create"></a> クラスター化列ストア インデックスを作成します。  
 クラスター化列ストア インデックスを作成するには、まずヒープまたはクラスター化インデックスとして行ストア テーブルを作成しを使用して、[クラスター化列ストア インデックスの作成&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql)クラスター化されたテーブルに変換するステートメント列ストア インデックスです。 クラスター化 columnstore インデックスにクラスター化インデックスと同じ名前を付ける場合は、DROP_EXISTING オプションを使用します。  
  
 この例では、テーブルをヒープとして作成してから、cci_Simple という名前のクラスター化 columnstore インデックスに変換します。 こうすることで、テーブル全体のストレージが行ストアから列ストアに変更されます。  
  
```  
CREATE TABLE T1(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_T1 ON T1;  
GO  
```  
  
 例については、例」セクションを参照してください。 [CREATE CLUSTERED COLUMNSTORE INDEX &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)します。  
  
##  <a name="drop"></a> クラスター化列ストア インデックスを削除します。  
 使用して、 [DROP INDEX &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/drop-index-transact-sql)クラスター化列ストア インデックスを削除するステートメント。 この操作は、インデックスを削除し、列ストア テーブルを行ストア ヒープに変換します。  
  
##  <a name="load"></a> クラスター化列ストア インデックスにデータを読み込む  
 標準的な読み込み方法を使用して既存のクラスター化列ストア インデックスにデータを追加できます。  たとえば、bcp 一括読み込みツール、Integration Services、および INSERT.SELECT を使用して、クラスター化列ストア インデックスにすべてのデータを読み込むことができます。  
  
 クラスター化 columnstore インデックスでは、columnstore の列セグメントの断片化を防ぐためにデルタストアを活用します。  
  
### <a name="loading-into-a-partitioned-table"></a>パーティション分割されたテーブルへの読み込み  
 パーティション分割されたデータの場合、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] はまずパーティションに各行を割り当て、次にパーティション内のデータの columnstore 処理を実行します。 各パーティションには、独自の行グループと少なくとも 1 つのデルタストアがあります。  
  
### <a name="deltastore-loading-scenarios"></a>デルタストアの読み込みのシナリオ  
 デルタストアの行は、行グループに許容されている最大行数になるまで蓄積されます。 デルタストアの行グループあたりの行数の最大数が含まれている[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]行グループ"CLOSED"としてマークされます。 バック グラウンド プロセスは、「組ムーバー」と呼ばれる、CLOSED 行グループを検索し、場所、行グループは列セグメントに圧縮され、列セグメントが、列ストアに格納されている列ストアに移動します。  
  
 各クラスター化 columnstore インデックスに対して複数のデルタストアが許容されます。  
  
-   デルタストアがロックされている場合、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は別のデルタストアのロックを獲得しようとします。 使用できるデルタストアがない場合、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は新しいデルタストアを作成します。  
  
-   パーティション テーブルでは、各パーティションに 1 つ以上のデルタストアが許容されます。  
  
 クラスター化 columnstore インデックスのみについて、次のシナリオは、読み込まれた行が columnstore に直接移動するときと、デルタストアに移動するときについて説明します。  
  
 この例では、行グループはそれぞれ 102,400 ～ 1,048,576 個の行を持つことができます。  
  
|一括読み込みを行う行|列ストアに追加される行|デルタストアに追加される行|  
|-----------------------|-----------------------------------|----------------------------------|  
|102,000|0|102,000|  
|145,000|145,000<br /><br /> 行グループのサイズ:145,000|0|  
|1,048,577|1,048,576<br /><br /> 行グループのサイズ:1,048,576|1|  
|2,252,152|2,252,152<br /><br /> 行グループのサイズ:1,048,576、1,048,576、155,000|0|  
  
 次の例は、1,048,577 個の行をパーティションに読み込んだ結果を示しています。 この結果では、列ストアに 1 つの圧縮された行グループ (圧縮された列セグメントとして)、およびデルタストアに 1 行があります。  
  
```  
SELECT * FROM sys.column_store_row_groups  
```  
  
 ![一括読み込みの行グループとデルタストア](../../2014/database-engine/media/sql-server-pdw-columnstore-batchload.gif "Rowgroup and deltastore for a batch load")  
  

  
##  <a name="change"></a> クラスター化列ストア インデックスのデータを変更します。  
 クラスター化 columnstore インデックスでは挿入、更新、および DML 削除操作がサポートされます。  
  
 使用[挿入&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/insert-transact-sql)行を挿入します。 行はデルタストアに追加されます。  
  
 [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) を使用して行を削除します。  
  
-   行が列ストアにある場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は行を論理的に削除されたとしてマークしますが、インデックスが再構築されるまで行の物理ストレージを再確保することはありません。  
  
-   行がデルタストアにある場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は論理的および物理的に行を削除します。  
  
 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) を使用して行を更新します。  
  
-   行が列ストアにある場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は行を論理的に削除されたとしてマークし、更新された行をデルタストアに挿入します。  
  
-   行がデルタストアにある場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、デルタストアの行を更新します。  
  
##  <a name="rebuild"></a> クラスター化列ストア インデックスを再構築します。  
 使用[CREATE CLUSTERED COLUMNSTORE INDEX &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql)または[ALTER INDEX &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/alter-index-transact-sql)既存のクラスター化列ストア インデックスの完全な再構築を実行します。 また、ALTER INDEX … REBUILD を使用して特定のパーティションを再構築できます。  
  
### <a name="rebuild-process"></a>再構築プロセス  
 クラスター化列ストア インデックスを再構築する際、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は以下のように動作します。  
  
-   再構築が行われている間、テーブルまたはパーティションを排他的にロックします。  再構築の間、データは "オフライン" になって使用できません。  
  
-   テーブルから論理的に削除された行を物理的に削除することで、列ストアをデフラグします。削除されたバイトは物理メディアで再利用されます。  
  
-   インデックスを再構築する前に、デルタストアの行ストア データを columnstore のデータとマージします。 再構築が終了すると、すべてのデータが columnstore 形式で格納され、デルタストアが空になります。  
  
-   すべてのデータを列ストアに再圧縮します。 再構築が行われている間、列ストア インデックスのコピーが 2 つ存在します。 再構築が完了したら、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] により、元の列ストア インデックスが削除されます。  
  
### <a name="recommendations-for-rebuilding-a-clustered-columnstore-index"></a>クラスター化 Columnstore インデックスの再構築の推奨設定  
 クラスター化 columnstore インデックスを再構築すると、断片化の解消およびすべての行を columnstore に移動する場合に便利です。 次の推奨事項が用意されています。  
  
-   テーブル全体ではなくパーティションを再構築します。  
  
    1.  インデックスが大きいとテーブル全体の再構築には時間がかかり、再構築中にインデックスの追加コピーを格納するために十分なディスク領域が必要です。 通常は、最近使用されたパーティションを再構築するだけで済みます。  
  
    2.  パーティション テーブルでは、columnstore インデックス全体を再構築する必要はありません。断片化は最近変更されたパーティションのみで起きる可能性が高いためです。 ファクト テーブルや大きなディメンション テーブルは通常、テーブルのチャンク上でバックアップおよび管理を行うためにパーティション分割されます。  
  
-   負荷の高い DML 操作後にパーティションを再構築します。  
  
     パーティションを再構築すると、パーティションの断片化を解消し、ディスク ストレージが減少します。 再構築すると、削除のマークが付けられた columnstore からすべての行が削除され、すべての行がデルタストアから columnstore に移動されます。  
  
-   データを読み込んだ後に、パーティションを再構築します。  
  
     これにより、すべてデータが columnstore に格納されます。 複数の負荷が同時に発生した場合は、各パーティションは複数のデルタストアを持つ可能性があります。 再構築すると、すべてのデルタストア行が columnstore に移動されます。  
  
##  <a name="reorganize"></a> クラスター化列ストア インデックスを再構成します。  
 クラスター化 columnstore インデックスを再構成すると、すべての CLOSED 行グループが columnstore に移動されます。 再構成を実行するには使用[ALTER INDEX &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)REORGANIZE オプションを使用します。  
  
 再構成は、CLOSED 行グループを columnstore に移動するためには必要はありません。 組ムーバー プロセスでは、最終的にすべての閉じた行グループが発見され移動されます。 ただし、組ムーバーはシングル スレッドであるため、ワークロードに対応できるだけ十分な速度で行グループを移動できない可能性があります。  
  
### <a name="recommendations-for-reorganizing"></a>再構成に関する推奨事項  
 クラスター化列ストア インデックスを再構成するとき:  
  
-   クエリのパフォーマンスの利点をできるだけ早く得るために、1 つ以上のデータが読み込まれた後にクラスター化列ストア インデックスを再編成します。 再構成ではデータを圧縮するために最初に追加の CPU リソースが必要とされ、システムの全体的なパフォーマンスが遅くなる場合があります。 しかし、データが圧縮されるとすぐにクエリ パフォーマンスが改善します。  
  
  
