---
title: MSSQLSERVER_41332 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: be21e36f47e2bae00387e1f5aed087c94688f930
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver41332"></a>MSSQLSERVER_41332
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|41332|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQL_SNAPSHOT_NOT_SUPPORTED|  
|メッセージ テキスト|セッション TRANSACTION ISOLATION LEVEL が SNAPSHOT に設定されている場合、メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャはアクセスまたは作成できません。|  
  
## <a name="explanation"></a>説明  
トランザクションはスナップショット分離レベルで開始され、互換性のない機能を使用しようとしました。  
  
## <a name="user-action"></a>ユーザーの操作  
他の分離レベルでトランザクションを開始します。 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
