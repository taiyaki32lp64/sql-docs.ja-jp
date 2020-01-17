---
title: default trace enabled サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], traces
- traces [SQL Server], logs
- default trace enabled option
ms.assetid: 1322d668-44f4-469e-8fd6-e0d02a81c8f2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 33a04235580d70567b1de09180b10526255811bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011945"
---
# <a name="default-trace-enabled-server-configuration-option"></a>default trace enabled サーバー構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **default trace enabled** オプションは、既定のトレース ログ ファイルを有効または無効にする場合に使用します。 既定のトレース機能では、主に構成オプションに関連する操作および変更の詳しい永続的なログが提供されます。  
  
> [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
  
## <a name="purpose"></a>用途  
 既定のトレース機能は、問題が初めて発生したときに、その問題を診断するために必要なログ データを提供することによって、データベース管理者によるトラブルシューティングを支援します。  
  
## <a name="viewing"></a>表示  
 既定のトレース ログは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] で開いて確認するか、 [!INCLUDE[tsql](../../includes/tsql-md.md)] システム関数を使用して `fn_trace_gettable` でクエリできます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、通常のトレース出力ファイルを開く場合と同様に、既定のトレース ログ ファイルを開くことができます。 既定のトレース ログは、ロールオーバー トレース ファイルを使用して、既定により `\MSSQL\LOG` ディレクトリに保存されます。 既定のトレース ログ ファイルのベース ファイル名は `log.trc`です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の標準インストールの場合、既定のトレースが有効になっているため、TraceID 1 になります。 インストール後や他のトレースの作成後に有効にした場合、TraceID の数値が大きくなることがあります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler を使用してこのトレース ファイルを表示する方法については、「[トレース ファイルを開く&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)」をご覧ください。  
  
### <a name="example"></a>例:  
 次のステートメントは、既定の場所にある既定のトレース ログを開きます。  
  
```  
SELECT *   
FROM fn_trace_gettable  
('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\LOG\log.trc', default);  
GO  
  
```  
  
## <a name="configuring"></a>構成  
 **default trace enabled** オプションを 1 に設定すると、 **既定のトレース**が有効になります。 このオプションの既定値は 1 (ON) です。 0 に設定すると、トレースがオフになります。  
  
 **default trace enabled** オプションは拡張オプションです。 **sp_configure** システム ストアド プロシージャを使用して **default trace enabled** オプションの設定を変更するには、 **show advanced options** を 1 に設定する必要があります。 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>参照  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
