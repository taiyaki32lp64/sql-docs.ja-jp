---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 58a6ff1dda1e0694e17d891502c7dca9ebb31c8a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060580"
---
# <a name="mssqlserver10737"></a>MSSQLSERVER_10737
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|MSSQLSERVER|  
|イベント ID|10737|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|REBUILD_PARTITION_ALL_NOT_SPECIFIED|  
|メッセージ テキスト|ALTER TABLE REBUILD ステートメントまたは ALTER INDEX REBUILD ステートメントの DATA_COMPRESSION 句でパーティションを指定する場合は、PARTITION=ALL を指定する必要があります。 PARTITION=ALL 句を使用すると、DATA_COMPRESSION 句でサブセットのみを指定した場合でも、テーブルまたはインデックスのすべてのパーティションが必ず再構築されます。|  
  
## <a name="user-action"></a>ユーザーの操作  
ALTER TABLE ステートメントまたは ALTER INDEX ステートメントに PARTITION=ALL 句を追加します。 また、特定のパーティションを再構築するには、REBUILD PARTITION = \<partition-number-expr> WITH (DATA_COMPRESSION={ON | OFF}) を使用します。  
  
