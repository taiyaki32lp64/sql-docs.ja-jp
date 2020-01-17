---
title: MSSQLSERVER_17884 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e31c7a78b74a307bc4c57216ef6c87e989493519
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915134"
---
# <a name="mssqlserver17884"></a>MSSQLSERVER_17884
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|17884|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SRV_SCHEDULER_DEADLOCK|  
|メッセージ テキスト|ノード %d のプロセスに割り当てられた新しいクエリが、この %d 秒間ワーカー スレッドで選択されませんでした。 クエリのブロックまたは長時間実行をこの条件に含めることができますが、クライアントの応答時間が低下する可能性があります。 "max worker threads" 構成オプションを使用して使用可能なスレッド数を増やすか、現在実行中のクエリを最適化してください。  SQL プロセス使用率: %d%%。 システムのアイドル状態: %d%%。|  
  
## <a name="explanation"></a>説明  
 各スケジューラで処理の進行が示されません。デッドロックが原因である可能性があり、その場合、スレッドは進行せず、新しい作業は選択されず処理されません。 プロセス使用率が低い場合は、コンピューター上の他のプロセスによってサーバー プロセスの CPU 不足が発生している可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 ブロックが発生して処理が進行していない理由を特定し、それに応じて状況に対処します。 プロセス使用率が低い場合は、他のプロセスによって発生しているシステムへの負荷を確認します。  
  
  
