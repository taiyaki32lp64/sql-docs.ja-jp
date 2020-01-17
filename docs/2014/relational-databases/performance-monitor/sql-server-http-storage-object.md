---
title: SQL Server:HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f104f7a6395442484be15f1e72c849edbf11e74f
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152679"
---
# <a name="sql-server-http_storage_object"></a>SQL Server:HTTP_STORAGE_OBJECT
  **SQLServer: HTTP_STORAGE_OBJECT**パフォーマンスオブジェクトは、Azure Storage アカウントを監視するパフォーマンスカウンターで構成されています。 [Azure 機能で SQL Server データファイル](../databases/sql-server-data-files-in-microsoft-azure.md)を使用すると、Azure Storage blob にデータベースファイルを格納できます。 このパフォーマンスオブジェクトは、各 Azure Storage アカウントを別のドライブとして扱います。  
  
|カウンター名|説明|  
|------------------|-----------------|  
|**Read Bytes/sec**|読み取り操作中に HTTP ストレージから転送されている 1 秒あたりのデータ量。|  
|**Write Bytes/sec**|書き込み操作中に HTTP ストレージから転送されている 1 秒あたりのデータ量。|  
|**Total Bytes/sec**|読み取りまたは書き込み操作中に HTTP ストレージから転送されている 1 秒あたりのデータ量。|  
|**Reads/sec**|HTTP ストレージでの 1 秒あたりの読み取り数。|  
|**Writes/sec**|HTTP ストレージでの 1 秒あたりの書き込み数。|  
|**Transfers/sec**|HTTP ストレージでの 1 秒あたりの読み取りおよび書き込み操作数。|  
|**平均Bytes/Read**|読み取りごとに HTTP ストレージから転送された平均バイト数。|  
|**平均Bytes/Write**|書き込みごとに HTTP ストレージから転送された平均バイト数。|  
|**平均Bytes/Transfer**|読み取りまたは書き込み操作中に HTTP ストレージから転送された平均バイト数。|  
|**Avg. microsec/Read**|HTTP ストレージからの読み取りごとに要する平均マイクロ秒数。|  
|**Avg. microsec/Write**|HTTP ストレージへの書き込みごとに要する平均マイクロ秒数。|  
|**Avg. microsec/Transfer**|HTTP ストレージへの転送ごとに要する平均マイクロ秒数。|  
|**Outstanding HTTP Storage I/O**|HTTP ストレージに対する未処理 I/O の合計数。|  
|**HTTP Storage I/O Retry/sec**|HTTP ストレージに送信された 1 秒あたりの再試行要求数。|  
  
## <a name="see-also"></a>関連項目  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)  
  
  
