---
title: 変更データ キャプチャ テーブル (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a4372d0b-50ca-4e58-80f6-2ed3cb52a84a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7d6d87ee8b2aa05c3156acb2db9c6604380db887
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082683"
---
# <a name="change-data-capture-tables-transact-sql"></a>変更データ キャプチャのテーブル (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  変更データ キャプチャでは、変更のデータ操作言語 (DML) と、テーブルに対するデータ定義言語 (DDL) 変更をデータ ウェアハウスに増分読み込むことができるように、テーブルで追跡を有効します。 このセクションのトピックでは、変更データ キャプチャ操作で使用される情報を格納するシステム テーブルについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [cdc.<capture_instance>_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
 関連付けられているソース テーブルにおけるキャプチャ対象列に加えられた変更ごとに 1 つの行を返します。  
  
 [cdc.captured_columns](../../relational-databases/system-tables/cdc-captured-columns-transact-sql.md)  
 キャプチャ インスタンスで追跡されている各列に対して 1 つの行を返します。  
  
 [cdc.change_tables](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
 データベース内の変更テーブルごとに 1 行を返します。  
  
 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)  
 変更データ キャプチャが有効になっているテーブルに対して行われたデータ定義言語 (DDL) の変更について、各変更に対応する 1 行を返します。  
  
 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)  
 変更テーブルの行を持つトランザクションごとに 1 つの行を返します。 このテーブルは、トランザクションのコミット ログ シーケンス番号 (LSN) コミットの値と時刻の間でマップを使用します。  
  
 [cdc.index_columns](../../relational-databases/system-tables/cdc-index-columns-transact-sql.md)  
 変更テーブルに関連付けられた各インデックス列について、対応する 1 行を返します。  
  
 [dbo.cdc_jobs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
 変更データ キャプチャのエージェント ジョブの構成パラメーターを返します。  
  
## <a name="see-also"></a>関連項目  
 [変更データ キャプチャ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [変更データ キャプチャ関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)  
  
  
