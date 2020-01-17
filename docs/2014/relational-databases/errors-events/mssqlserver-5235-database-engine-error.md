---
title: MSSQLSERVER_5235 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5235 (Database Engine error)
ms.assetid: 1aa7e6a5-7ccb-43c8-a1fd-d50e92e0a798
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d6cbfac91613c2374e42da5b33e75ed5cade2bcf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913759"
---
# <a name="mssqlserver5235"></a>MSSQLSERVER_5235
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|5235|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC4_ERRORLOG_SUMMARY_PREMATURE_TERMINATION|  
|メッセージ テキスト|[EMERGENCY] エラー状態 ERROR_STATE により、USER_NAME から実行された DBCC DBCC_COMMAND_DETAILS が異常終了しました。 経過時間:HOURS 時間 MINUTES 分 SECONDS 秒。|  
  
## <a name="explanation"></a>説明  
 これは、コマンドの実行中に予期しない異常終了が発生した場合に DBCC によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに出力される概要メッセージです。 予期しない異常終了の種類は、メッセージで報告されるエラー状態で示されます。  
  
 次の表に、エラー状態の一覧と定義を示します。  
  
|エラー状態|定義|  
|-----------------|----------------|  
|状態 0|致命的なメタデータの破損により、ステートメントが終了しました。 このメッセージは、1 件以上のエラー 8930 を伴います。|  
|状態 1|内部チェック エラーにより、ステートメントが終了しました。 このメッセージは、1 件以上のエラー 8967 を伴います。|  
|状態 2|ストレージ エンジンのコア システム テーブルの基本システム テーブル チェックが失敗しました。 このメッセージは、1 件以上のエラー [7984](mssqlserver-7984-database-engine-error.md)、7985、[7986](mssqlserver-7986-database-engine-error.md)、[7987](mssqlserver-7987-database-engine-error.md)、または [7988](mssqlserver-7988-database-engine-error.md) を伴います。|  
|状態 3|トランザクション ログの再構築後にデータベースを起動できなかったため、DBCC 緊急モードでの修復が失敗しました。 このメッセージは、エラー 7909 を伴います。|  
|状態 4|コマンドの実行中に、アサーションの失敗またはアクセス違反が発生しました。|  
|状態 5|不明なエラーが発生し、DBCC コマンドが予期せず終了しました。|  
  
## <a name="user-action"></a>ユーザーの操作  
 次の表に、指定されたエラー状態に対応するユーザーのアクションを示します。  
  
|エラー状態|ユーザーのアクション|  
|-----------------|-----------------|  
|状態 0|バックアップからの復元を行います。|  
|状態 1|[!INCLUDE[msCoName](../../includes/msconame-md.md)] カスタマー サポート サービス (CSS) に問い合わせます。|  
|状態 2|バックアップからの復元を行います。|  
|状態 3|バックアップからの復元を行います。|  
|状態 4|CSS に問い合わせます。|  
|状態 5|コマンドを再実行します。 問題が解決しない場合は、CSS に問い合わせます。|  
  
## <a name="see-also"></a>参照  
 [DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)  
  
  
