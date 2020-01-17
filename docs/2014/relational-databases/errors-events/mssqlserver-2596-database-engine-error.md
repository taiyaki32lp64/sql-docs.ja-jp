---
title: MSSQLSERVER_2596 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 21209de55bc010c2c85285f4cbed7305c6755f4c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914369"
---
# <a name="mssqlserver2596"></a>MSSQLSERVER_2596
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2596|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|メッセージ テキスト|修復ステートメントは処理されませんでした。 データベースを読み取り専用モードにすることはできません。|  
  
## <a name="explanation"></a>説明  
 このメッセージは、データベースが読み取り専用モードであることを示しています。 データベースが読み取り専用モードである場合は、修復が不可能です。  
  
## <a name="user-action"></a>ユーザーの操作  
 ALTER DATABASE を使用してデータベースを読み取り/書き込み可能に設定し、DBCC コマンドを再実行します。  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
