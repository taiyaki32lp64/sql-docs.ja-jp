---
title: MSSQLSERVER_18264 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 18264 (Database Engine error)
ms.assetid: 3050fc56-2be5-43cf-916b-50a3ac5f89aa
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 06ae22f5e2e7344a5934493bb893a07bdb20383a
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver18264"></a>MSSQLSERVER_18264
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|Microsoft SQL Server|  
|イベント ID|18264|  
|イベント ソース|MSSQLENGINE|  
|コンポーネント|SQLEngine|  
|シンボル名|STRMIO_DBDUMP|  
|メッセージ テキスト|データベースがバックアップされました。 データベース: %s、作成日 (時間): %s(%s)、ダンプされたページ: %d、最初の LSN: %s、最後の LSN: %s、ダンプ デバイスの数: %d、デバイス情報: (%s)。 このメッセージは情報提供だけを目的としています。 ユーザーによる操作は不要です。|  
  
## <a name="explanation"></a>説明  
既定では、バックアップが成功するたびに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログおよびシステム イベント ログにこの情報メッセージが追加されます。 トランザクション ログを頻繁にバックアップすると、これらのメッセージがすぐに蓄積され、他のメッセージを探すのが困難になるほど大きなエラー ログが生成されることがあります。  
  
## <a name="user-action"></a>ユーザーの操作  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のトレース フラグ **3226** を使用すると、これらのログ エントリを除外できます。 頻度の高いログ バックアップを実行している場合やスクリプトがこれらのエントリに依存していない場合は、このトレース フラグを有効にすると便利です。  
  
トレース フラグの使用方法の詳細については、SQL Server オンライン ブックを参照してください。  
  
## <a name="see-also"></a>参照  
[トレース フラグ &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
