---
title: MSSQLSERVER_17883 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17883 (Database Engine error)
ms.assetid: adaf1c04-e397-4a69-90b8-9353a37277ea
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f9f712ed8d37872c90eff773e81a657fb96c296
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915272"
---
# <a name="mssqlserver17883"></a>MSSQLSERVER_17883
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|17883|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SRV_SCHEDULER_NONYIELDING|  
|メッセージ テキスト|プロセス %ld:%ld:%ld (0x%lx) ワーカー 0x%p が、スケジューラ %ld で応答を停止している可能性があります。 Thread creation time: %I64d. スレッド CPU 概算使用時間: カーネル %I64d ミリ秒、ユーザー %I64d ミリ秒。 プロセスの使用率 %d%%。 システムのアイドル状態 %d%%。 間隔: %I64d ミリ秒。|  
  
## <a name="explanation"></a>説明  
 スケジューラで応答を停止しているスレッドに問題が発生している可能性があることを示します。  これは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内のバグが原因で発生するか、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行に必要なサイクルを十分に取得していない場合に発生する可能性があります。  スレッドが最終的に応答すると、このエラーは解決します。  
  
## <a name="user-action"></a>ユーザーの操作  
 システムの負荷が高すぎる場合は、負荷を軽減してください。それ以外の場合は、マイクロソフト カスタマー サポート サービスに連絡してください。  
  
  
