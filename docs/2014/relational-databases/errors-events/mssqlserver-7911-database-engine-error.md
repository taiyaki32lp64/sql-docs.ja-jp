---
title: MSSQLSERVER_7911 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7911 (Database Engine error)
ms.assetid: dd8390f3-0f77-4fb2-ba94-631a56e42bc6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dbb5a12fdcb3c326957d719882feec4fe948190c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761844"
---
# <a name="mssqlserver7911"></a>MSSQLSERVER_7911
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|7911|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC2_REPAIR_PAGE_DEALLOCATED|  
|メッセージ テキスト|修復:ページ P_ID はオブジェクト ID O_ID、インデックス ID I_ID、パーティション ID PN_ID、アロケーション ユニット ID A_ID (型 TYPE) から割り当て解除されました。|  
  
## <a name="explanation"></a>説明  
 単一ページ スロット配列の IAM (Index Allocation Map) ページから 1 ページが割り当て解除されたことを示す、REPAIR からの情報メッセージです。  
  
## <a name="user-action"></a>ユーザーの操作  
 なし  
  
  
