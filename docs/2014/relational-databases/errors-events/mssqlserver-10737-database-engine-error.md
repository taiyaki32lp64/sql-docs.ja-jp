---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7d89c05ebd0b181b63f66fa0e0e0db99d54b952
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916146"
---
# <a name="mssqlserver10737"></a>MSSQLSERVER_10737
    
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
  
  
