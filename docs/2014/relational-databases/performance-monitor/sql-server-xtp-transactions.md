---
title: XTP トランザクション |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96d60ae8fc176fc1fc108d907f33f01877795955
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151126"
---
# <a name="xtp-transactions"></a>XTP Transactions
  XTP Transactions パフォーマンス オブジェクトには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内の XTP エンジン トランザクションに関連するカウンターが含まれています。  
  
 この表は、 **XTP トランザクション**カウンター。  
  
|カウンター|説明|  
|-------------|-----------------|  
|**Cascading aborts/sec**|コミット依存ロールバックが原因でロールバックされたトランザクション数に関する 1 秒あたりの平均です。|  
|**Commit dependencies taken/sec**|トランザクションにより処理されたコミット依存の数に関する 1 秒間の平均です。|  
|**Read-only transactions prepared/sec**|コミット処理の目的で準備された読み取り専用トランザクションの数に関する 1 秒あたりの値です。|  
|**Save point refreshes/sec**|セーブポイントが "更新" された回数に関する 1 秒あたりの平均です。 セーブポイントの更新が発生するのは、既存のセーブポイントを、トランザクションの有効期間内での現在の状態にリセットしたときです。|  
|**Save point rollbacks/sec**|トランザクションがセーブポイントまでロールバックされた回数に関する 1 秒あたりの平均です。|  
|**Save points created /sec**|セーブポイントが作成された回数に関する 1 秒あたりの平均です。|  
|**Transaction validation failure/sec**|トランザクションが検証処理に失敗した回数に関する 1 秒間の平均です。|  
|**Transactions aborted by user/sec**|トランザクションがユーザーによって中止された回数に関する 1 秒間の平均です。|  
|**Transactions aborted/sec**|トランザクションが (ユーザーとシステムの両方によって) 中止された回数に関する 1 秒間の平均です。|  
|**Transactions created/sec**|システム内でトランザクションが作成された回数に関する 1 秒間の平均です。<br /><br /> XTP トランザクションは、ディスク ベース トランザクションとは別にカウントされます (Databases:Transactions/sec に反映)。 たとえば、読み取り専用トランザクションは Transactions created/sec でカウントされますが、Databases:Transactions/sec ではカウントされません。|  
  
## <a name="see-also"></a>参照  
 [XTP &#40;、インメモリ OLTP&#41;パフォーマンス カウンター](../../integration-services/performance/performance-counters.md)  
  
  
