---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 30b37236b321fc90372914f2af48a652d41fbe03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913600"
---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|5245|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|メッセージ テキスト|Object ID O_ID (object 'NAME'):DBCC は、ロック要求のタイムアウト期間を超過したため、このオブジェクトのロックを取得できませんでした。 このオブジェクトはスキップされたので、処理されません。|  
  
## <a name="explanation"></a>説明  
 DBCC が、指定されたオブジェクト用にテーブルのロック獲得を待機している間に、ロック要求のタイムアウトが発生しました。  
  
## <a name="user-action"></a>ユーザーの操作  
 DBCC コマンドを再実行します。  
  
  
