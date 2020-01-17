---
title: MSSQLSERVER_41333 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab94977bcd3bf5a9b0b26ac7be76cb67d58e0755
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913988"
---
# <a name="mssqlserver41333"></a>MSSQLSERVER_41333
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|41333|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|CROSS_CONTAINER_ISOLATION_FAILURE|  
|メッセージ テキスト|次に示すトランザクションは、スナップショット分離を使用したうえでメモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャにアクセスする必要があります。RepeatableRead トランザクション、Serializable トランザクション、RepeatableRead または Serializable 分離でメモリ最適化されていないテーブルにアクセスするトランザクション。|  
  
## <a name="explanation"></a>説明  
 ディスク ベース トランザクションと XTP トランザクションの間の分離レベルが高いユーザーに対しては、制約があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 メモリ最適化テーブル (およびネイティブ コンパイル プロシージャ) とディスク ベース テーブルでは、高レベルの分離操作を実行しないでください。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
