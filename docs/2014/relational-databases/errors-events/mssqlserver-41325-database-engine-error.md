---
title: MSSQLSERVER_41325 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41325 (Database Engine error)
ms.assetid: 97c6a8bb-139a-44f3-9ed5-f46d047e8ed3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c78044f8790f3a1ab97d036467813efa3d30e6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913998"
---
# <a name="mssqlserver41325"></a>MSSQLSERVER_41325
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|41325|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|HK_TX_COMMIT_SR_VALIDATION|  
|メッセージ テキスト|現在のトランザクションは、SERIALIZABLE の検証の失敗が原因でコミットされませんでした。|  
  
## <a name="explanation"></a>説明  
 検証エラーが発生したため、トランザクションに失敗しました。  
  
## <a name="user-action"></a>ユーザーの操作  
 エラーが発生したトランザクションを再試行してください。 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
