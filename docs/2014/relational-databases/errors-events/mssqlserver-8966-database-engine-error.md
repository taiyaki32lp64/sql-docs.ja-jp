---
title: MSSQLSERVER_8966 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dee5b45aac6518517434595b0f26ce18d219866b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913164"
---
# <a name="mssqlserver8966"></a>MSSQLSERVER_8966
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|8966|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC3_FAILED_TO_READ_AND_LATCH_PAGE|  
|メッセージ テキスト|ラッチ型 TYPE のページ P_ID を読み取ってラッチすることができません。 OPERATION が失敗しました。|  
  
## <a name="explanation"></a>説明  
 ページの読み取りに失敗したか、PFS ページまたは GAM ページでラッチを取得できませんでした。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに、ラッチ タイムアウトまたは他の添付メッセージが記録される場合があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 SQL エラー ログの添付メッセージを確認し、これらのエラーを解決します。  
  
  
