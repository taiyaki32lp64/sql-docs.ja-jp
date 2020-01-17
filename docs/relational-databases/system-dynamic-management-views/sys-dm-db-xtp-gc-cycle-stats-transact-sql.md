---
title: sys.dm_db_xtp_gc_cycle_stats (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_gc_cycle_stats_TSQL
- dm_db_xtp_gc_cycle_stats
- sys.dm_db_xtp_gc_cycle_stats_TSQL
- sys.dm_db_xtp_gc_cycle_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_gc_cycle_stats dynamic management view
ms.assetid: bbc9704e-158e-4d32-b693-f00dce31cd2f
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 95e173cd20bd04c3b5a5a6cd7ad7299ef13971d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026852"
---
# <a name="sysdm_db_xtp_gc_cycle_stats-transact-sql"></a>sys.dm_db_xtp_gc_cycle_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  1 つ以上の行を削除したコミット済みトランザクションの現在の状態を出力します。 アイドル状態のガベージ コレクション スレッドは、毎分または最後のガベージ コレクション サイクル以降にコミット済み DML トランザクションの数が内部しきい値を超えたときを解除します。 ガベージ コレクション サイクルの一環として、コミット済みトランザクションは、generation と関連付けられている 1 つ以上のキューに移動されます。 古いバージョンを生成したトランザクションは、次のようにして、16 の generation にわたり 16 トランザクションごとの単位にグループ化されます。  
  
-   Generation 0:これは、最も古いアクティブなトランザクションより前にコミットされたすべてのトランザクションを格納します。 これらのトランザクションによって生成される行バージョンがすぐにガベージ コレクションで使用します。  
  
-   Generation 1 ~ 14:最も古いアクティブなトランザクションより後のタイムスタンプを持つトランザクションを格納します。 行バージョンに対してガベージ コレクションを実行することはできません。 各ジェネレーションには、最大 16 個のトランザクションを保持できます。 合計 224 (14 * 16) のトランザクションがこれらのジェネレーションで存在できます。  
  
-   Generation 15:タイムスタンプが最も古いアクティブなトランザクションより後の残りのトランザクションは generation 15 に移動します。 generation 0 と同様、generation 15 にもトランザクション数の制限はありません。  
  
 メモリが不足している場合、ガベージ コレクション スレッドは、最も古いアクティブなトランザクションのヒントを積極的に更新します。これにより、ガベージ コレクションが強制されます。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|cycle_id|**bigint**|ガベージ コレクション サイクルの一意の識別子。|  
|ticks_at_cycle_start|**bigint**|サイクルが開始した時点におけるティックします。|  
|ticks_at_cycle_end|**bigint**|サイクルが終了した時点におけるティックします。|  
|base_generation|**bigint**|データベースの現在のベース generation 値です。 これは、ガベージ コレクションのトランザクションを識別するために使用される最も古いアクティブなトランザクションのタイムスタンプを表します。 最も古いアクティブなトランザクション id は 16 の増分値で更新されます。 たとえば、トランザクション id として 124、125、126 がある.139、値は 124 になります。 また、たとえばトランザクション 140 を追加した場合、この値は 140 になります。|  
|xacts_copied_to_local|**bigint**|トランザクションのパイプラインからデータベースの generation 配列にコピーされたトランザクションの数|  
|xacts_in_gen_0 xacts_in_gen_15|**bigint**|generation ごとのトランザクションの数|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="usage-scenario"></a>使用シナリオ  
 27 generation が表示されている列のサブセットの出力例を次に示します。  
  
```  
cycle_id   ticks_at_cycle_start ticks_at_cycle_end   base_generation  xacts_in_gen_0    xacts_in_gen_1  
  
1          123160509            123160509            1                    0                    0  
2          123176822            123176822            1                    0                    1  
3          123236826            123236826            1                    0                    1  
4          123296829            123296829            1                    0                    1  
5          123356832            123356941            129                  0                    0  
6          123357473            123357473            129                  0                    0  
7          123417486            123417486            129                  0                    0  
8          123477489            123477489            129                  0                    0  
9          123537492            123537492            129                  0                    0  
10         123597500            123597500            129                  0                    0  
11         123657504            123657504            129                  0                    0  
12         123717507            123717507            129                  0                    0  
13         123777510            123777510            129                  0                    0  
14         123837513            123837513            129                  0                    0  
15         123897516            123897516            129                  0                    0  
16         123957516            123957516            129                  0                    0  
17         124017516            124017516            129                  0                    0  
18         124077517            124077517            129                  0                    0  
19         124137517            124137517            129                  0                    0  
20         124197518            124197518            129                  0                    0  
21         124257518            124257518            129                  0                    0  
22         124317523            124317523            129                  0                    0  
23         124377526            124377526            129                  0                    0  
24         124437529            124437529            129                  0                    0  
25         124497533            124497533            129                  0                    0  
26         124557536            124557536            129                  0                    0  
27         124617539            124617539            129                  0                    0  
  
```  
  
## <a name="see-also"></a>関連項目  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
