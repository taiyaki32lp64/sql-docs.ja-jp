---
title: SQL Server XTP IO ガバナー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 975dca6fe0151b5bd1fc1d72b9d14e47a57413d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915210"
---
# <a name="sql-server-xtp-io-governor"></a>SQL Server XTP IO ガバナー
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server XTP IO ガバナーのパフォーマンス オブジェクトには、インメモリ OLTP IO レート ガバナーに関連するカウンターが含まれています。

次の表で、 **SQL Server XTP IO ガバナー** カウンターについて説明します。

|カウンター|[説明]|  
|-------------|-----------------|  
|**1 秒あたりの不十分なクレジット待機数**|レート オブジェクトのクレジット不足に起因する待機数 (1 秒あたり)。|
|**1 秒あたりに発行された Io 数**|フラッシュ スレッドにより発行された Io 数 (1 秒あたり)。|
|**1 秒あたりのログ ブロック数**|コントローラーによって処理されたログ ブロック数 (1 秒あたり)。|
|**実行されなかったクレジット スロット数**|レート オブジェクトからのクレジットを待ったために実行されなかったクレジット スロット数。|
|**1 秒あたりの古いレート オブジェクト待機数**|古いレート オブジェクトに起因する待機数 (1 秒あたり)。|
|**公開されたレート オブジェクトの合計**|公開されたレート オブジェクトの合計数。|
 

## <a name="see-also"></a>参照  
[SQL Server XTP &#40;インメモリ OLTP&#41; パフォーマンス カウンター](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
