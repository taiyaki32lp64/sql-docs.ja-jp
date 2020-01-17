---
title: MSpeer_topologyresponse (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_topologyresponse
- MSpeer_topologyresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_topologyresponse
ms.assetid: 1bc5c0c6-c432-405c-89fd-e953d173a247
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4d64e4aa90aadb45e7f3c2aa09d23e06e5bda187
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026646"
---
# <a name="mspeer_topologyresponse-transact-sql"></a>MSpeer_topologyresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  トポロジ状態要求に対する各ノードの応答を保存するために、ピア ツー ピア レプリケーションで使用されます。 このテーブルは、パブリケーション データベース内に保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|request_id|**int**|内のトポロジ状態要求エントリを識別、 [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md)テーブル。|  
|peer|**sysname**|応答を生成するサーバー インスタンスの名前です。|  
|peer_version|**int**|パブリッシャーのバージョン番号を識別します。|  
|peer_db|**sysname**|応答を生成したピアでサブスクリプション データベースです。|  
|originator_id|**int**|競合検出のためにトポロジの各ノードを識別します。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」を参照してください。|  
|peer_conflict_retention|**int**|期間を日、そのメタデータは競合テーブルに格納されます。|  
|received_date|**datetime**|トポロジ要求を受信した時刻です。|  
|connection_info|**xml**|要求に応答したノードに関する情報。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
