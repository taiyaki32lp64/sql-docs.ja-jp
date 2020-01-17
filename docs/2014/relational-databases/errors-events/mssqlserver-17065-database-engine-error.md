---
title: MSSQLSERVER_17065 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17065 (Database Engine error)
ms.assetid: 63c2ba5a-be34-461e-bee1-03c25b396cd2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 33dfe774838aa88dc0c68829ae0abe34f3f1dda9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869756"
---
# <a name="mssqlserver17065"></a>MSSQLSERVER_17065
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|17065|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLASSERT_BOTH|  
|メッセージ テキスト|SQL Server アサーション:ファイル: \<%s >、行 = %d 失敗したアサーション = ' % $s ': %s。 このエラーはタイミングに関係している可能性があります。 ステートメントの再実行後もエラーが解決しない場合は、DBCC CHECKDB を使用してデータベースの構造上の整合性を確認するか、またはサーバーを再起動してインメモリ データ構造体が壊れていないことを確認してください。|  
  
## <a name="explanation"></a>説明  
 このエラーは、一時的なタイミングに関係する問題や、メモリ内またはディスク上のデータの破損によって発生する可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 例外を発生させたステートメントを再実行します。 タイミングに関係しているイベントによって発生したエラーの場合、エラーは再び発生しません。 問題が引き続き発生する場合は、DBCC CHECKDB を実行してディスク上の破損を確認します。 サーバーを再起動し、インメモリ データ構造体が壊れていないことを確認します。  
  
## <a name="see-also"></a>参照  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
