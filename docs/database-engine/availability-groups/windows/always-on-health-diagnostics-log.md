---
title: リソース DLL による可用性グループの正常性診断ログ
description: SQL Server リソース DLL によって Always On 可用性グループの正常性が監視されるしくみについて説明します。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: c1862d8a-5f82-4647-a280-3e588b82a6dc
author: rothja
ms.author: jroth
ms.openlocfilehash: aa9d269333e5c39f12b82d739575652efdd6c2c4
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822070"
---
# <a name="sql-server-resource-dll-health-diagnostic-logs-for-availability-groups"></a>SQL Server リソース DLL による可用性グループの正常性診断ログ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  プライマリ可用性レプリカの正常性を監視するために、Windows Server フェールオーバー クラスタリング (WSFC) クラスターで実行される SQL Server リソース DLL は、[sp_server_diagnostics](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) という名前の SQL Server インスタンスのストアド プロシージャを使用します。  
  
 SQL Server リソース DLL は、SQL Server インスタンスとの専用の開かれた接続を維持し、SQL Server インスタンスは、それを介して、詳細な正常性診断を SQL Server リソース DLL に定期的に送信します。 クラスター内の可能性グループリソースで構成されたフェールオーバー ポリシー (FailoverConditionLevel プロパティ) と正常性診断の組み合わせが、クラスターによって使用され、可用性グループの再起動またはフェールオーバーが決定されます。 このストアド プロシージャは、SQL Server 2012 以降のインスタンスの WSFC クラスターに対する "ハートビート" であり、SQL Server 2008 R2 以前よりも細かく信頼性が高く、クエリ `SELECT @@SERVERNAME` でインスタンスへの定期的な接続が実施されます。 可用性グループの FailureConditonLevel プロパティを設定することで、フェールオーバーをトリガーする条件を制御できます。  
  
 **SQL Server フェールオーバー クラスター診断ログを使用する**
 
 SQL Server リソース DLL が sp_server_diagnostics から受け取るすべての正常性診断情報は、SQL Server インスタンスの既定のログ ディレクトリ (%PROGRAMFILES%\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Log) に自動的に保存されます。 これらのログは、SQLDIAG ログと呼ばれ、XEL (拡張イベント) ファイル形式で保存されます。 SQL Server ログ ディレクトリでこれらのファイルは、\<HOSTNAME>_\<INSTANCENAME>_SQLDIAG_X_XXXXXXXXX.xel 形式で保存されます。 SQLDIAG ログを調べることで、可用性グループ リソースの障害またはフェールオーバー イベントの根本原因を特定することができます。  
  
 SQLDIAG ログを表示するには、SQL Server Management Studio に .xel ファイルをドラッグします。  
  
  
