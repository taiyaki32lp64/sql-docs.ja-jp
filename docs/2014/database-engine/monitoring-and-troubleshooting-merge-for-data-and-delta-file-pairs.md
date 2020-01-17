---
title: データファイルとデルタファイルのペアのマージの監視とトラブルシューティング |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a8b0bacc-4d2c-42e4-84bf-1a97e0bd385b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c7a13345da45d7e6c31a53bc51371306da444a96
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228177"
---
# <a name="monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs"></a>データ ファイルとデルタ ファイルのペアのマージに関する監視とトラブルシューティング
  インメモリ OLTP は、マージ ポリシーを使用して、データ ファイルとデルタ ファイルの隣接するペアを自動的にマージします。 マージ操作を無効にすることはできません。  
  
 データ ファイルとデルタ ファイルのペアは、次のように監視できます。  
  
-   ストレージの全体的なサイズとインメモリ ストレージのサイズを比較します。 ストレージが過度に大きい場合、マージが発生していない可能性があります。 詳細については、  
  
-   [Transact-sql&#41;&#40;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql)使用し dm_db_xtp_checkpoint_files て、データファイルとデルタファイル内の使用されている領域を確認し、必要に応じてマージがトリガーされないかどうかを確認します。  
  
## <a name="performing-a-manual-merge"></a>手動マージの実行  
 [Sp_xtp_merge_checkpoint_files &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)を使用して、手動マージを実行できます。  
  
 次のクエリを使用して、データ ファイルとデルタ ファイルに関する情報を取得します。  
  
```sql  
select checkpoint_file_id, file_type_desc, internal_storage_slot, file_size_in_bytes, file_size_used_in_bytes,   
inserted_row_count, deleted_row_count, lower_bound_tsn, upper_bound_tsn   
from sys.dm_db_xtp_checkpoint_files  
where state = 1  
order by file_type_desc, upper_bound_tsn  
```  
  
 マージされていない3つのデータファイルが見つかったとします。 最初のデータ ファイルの `lower_bound_tsn` 値と最後のデータ ファイルの `upper_bound_tsn` を使用して、次のコマンドを実行できます。  
  
```sql  
exec sys.sp_xtp_merge_checkpoint_files 'H_DB',  12345, 67890  
```  
  
 15,836 の行が含まれるデータ ファイルと 5,279 の削除行が含まれるデルタ ファイルのペアが 3 組あったとします。 マージ後、新しいデータ ファイルの行数は 31,872、削除行は 0 になります。 新しいデータ ファイルのサイズが、最初に割り当てられたサイズである 128 MB を大きく上回る場合があります。 これは、手動マージによってマージ ポリシーがオーバーライドされ、要求されたファイルのマージが強制されるためです。  
  
 [メモリ最適化テーブルを持つデータベースのチェックポイントファイルのブログ状態の移行で](https://blogs.technet.com/b/dataplatforminsider/archive/2014/01/23/state-transition-of-checkpoint-files-in-databases-with-memory-optimized-tables.aspx)は、データファイルとデルタファイルのペアの開始からガベージコレクションへの状態遷移について説明します。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化オブジェクトのストレージの作成と管理](../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
