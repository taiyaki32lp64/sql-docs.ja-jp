---
title: MSSQLSERVER_1222 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01325e8d83a5a7d7b65398f4e0cb981b1fca7540
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915899"
---
# <a name="mssqlserver1222"></a>MSSQLSERVER_1222
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1222|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LK_TIMEOUT|  
|メッセージ テキスト|ロック要求がタイムアウトしました。|  
  
## <a name="explanation"></a>説明  
 必要なリソースが、このクエリが待機できる時間より長く別のトランザクションによって拘束されています。  
  
## <a name="user-action"></a>ユーザーの操作  
 問題を軽減するには、次の操作を行います。  
  
1.  可能であれば、必要なリソースのロックを保持しているトランザクションを探します。 **sys.dm_os_waiting_tasks** および **sys.dm_tran_locks** 動的管理ビューを使用してください。  
  
2.  トランザクションがロックをまだ保持している場合は、必要に応じてこのトランザクションを中止します。  
  
3.  クエリを再実行します。  
  
 このエラーが頻繁に発生する場合は、ロック要求のタイムアウト時間を変更するか、原因となっているトランザクションを修正してロックの拘束時間を短くします。  
  
  
