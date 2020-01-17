---
title: MSSQLSERVER_1204 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1204 (Database Engine error)
ms.assetid: de6ece78-79de-484d-9224-ca0f7645815f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee0544c14bbf3e05fcb59e16a9bb3e0d8e61e33b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916103"
---
# <a name="mssqlserver1204"></a>MSSQLSERVER_1204
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1204|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LK_OUTOF|  
|メッセージ テキスト|この時点では、SQL Server データベース エンジンのインスタンスは LOCK リソースを取得できません。 アクティブなユーザーが少ないときにステートメントを再実行してください。 データベース管理者に依頼して、このインスタンスのロックとメモリの構成を確認するか、実行時間の長いトランザクションを確認してください。|  
  
## <a name="explanation"></a>説明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が、ロック リソースを獲得できません。 このエラーは次のいずれかが原因で生じている可能性があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が、オペレーティング システムからのメモリをこれ以上割り当てることができない。他のプロセスによってメモリが使用されているか、**max server memory** オプションが構成された状態でサーバーが動作していることが原因です。  
  
-   ロック マネージャーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用できるメモリのうち最大 60% までしか使用できない。  
  
## <a name="user-action"></a>ユーザーの操作  
 SQL Server が十分なメモリを割り当てられないようであれば、次の操作を行ってみます。  
  
-   SQL Server 以外のアプリケーションがリソースを消費している場合は、そのアプリケーションを停止するか、別のサーバーで実行することを検討します。 これにより、他のプロセスからメモリが解放され、SQL Server で使用できるようになります。  
  
-   max server memory を構成した場合は、設定値を大きくします。  
  
 使用可能なメモリの最大量がロック マネージャーによって使用されたと考えられる場合は、ロックの大半を取得しているトランザクションを見つけて中止します。 次のスクリプトは、ロックの大半を取得しているトランザクションを見つけるために使用できます。  
  
```  
SELECT request_session_id, COUNT (*) num_locks  
FROM sys.dm_tran_locks  
GROUP BY request_session_id   
ORDER BY count (*) DESC  
```  
  
 最も値が大きいセッション ID を見つけ、KILL コマンドでそのセッションを中止します。  
  
  
