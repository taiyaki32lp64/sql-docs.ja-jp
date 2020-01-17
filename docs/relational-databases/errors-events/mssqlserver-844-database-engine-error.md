---
title: MSSQLSERVER_844 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 844 (Database Engine error)
ms.assetid: 2060c886-1226-4066-bc0c-de90a1cfb82b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 253e718adb82bbfaa0c74fe9d232db7387e7de3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101548"
---
# <a name="mssqlserver844"></a>MSSQLSERVER_844
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|844|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|BUFLATCH_TIMEOUT_CONTINUE|  
|メッセージ テキスト|バッファー ラッチを待機中にタイムアウトが発生しました。型 %d、BP %p、ページ %d:%d、状態 %#x、データベース ID: %d、アロケーション ユニット ID: %I64d%ls、タスク 0x%p : %d、待機時間 %d、フラグ 0x%I64x、所有しているタスク 0x%p。  待機を続行します。|  
  
## <a name="explanation"></a>説明  
プロセスが、ラッチの獲得を待機しています。 この問題は、I/O 操作の完了までに時間がかかりすぎている場合に生じることがあります。 このタイプのエラーは、他のタスクによってシステム プロセスがブロックされた結果に生じることが普通です。 場合によっては、ハードウェア障害によってこのエラーが生じることもあります。  
  
## <a name="user-action"></a>ユーザーの操作  
このエラーを回避するには、次の操作を試してみます。  
  
-   ワークロードを減らします。  
  
-   エラー ログまたはイベント ログで、関連する I/O エラーがないか調べます。 通常、I/O エラーはディスクに障害があることを示しています。  
  
-   応答していないタスクや他の重大なエラーがないか、エラー ログで調べます。  
  
-   アサートなどの重大なエラーが頻繁に発生する場合は、その問題を解決します。  
  
エラーが継続して発生する場合は、マイクロソフト カスタマー サービスおよびサポートに問い合わせてください。  
  
