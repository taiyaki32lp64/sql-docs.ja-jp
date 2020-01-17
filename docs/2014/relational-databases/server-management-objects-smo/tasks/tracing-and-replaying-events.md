---
title: トレースおよび再生のイベント |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d478fa9203988d043212e4187792d816a69c0402
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62724792"
---
# <a name="tracing-and-replaying-events"></a>イベントのトレースおよび再生
  SMO で、[!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの監視に使用する [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 機能にプログラムでアクセスするには、<xref:Microsoft.SqlServer.Management.Trace> 名前空間の `Trace` オブジェクトおよび `Replay` オブジェクトを使用します。 各イベントに関するデータをキャプチャし、ファイルやテーブルに保存して、後で分析できます。 たとえば、実稼動環境を監視して、どのプロシージャの実行が遅く、パフォーマンスに影響を与えているかを確認できます。  
  
 `Trace` オブジェクトおよび `Replay` オブジェクトを使用すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに対するトレースを作成できます。 これらのオブジェクトをユーザー独自のアプリケーションから使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] または [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] に対してトレースを手動で作成することもできます。 また、SMO `Trace` オブジェクトを使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]、または DTS ログを監視することによって作成された SQL トレースのファイルおよびテーブルを読み取ることもできます。  
  
 SMO `Trace` オブジェクトによって、次の操作が可能になります。  
  
-   トレースの作成。  
  
-   トレース上でのフィルターの設定。  
  
-   トレースするイベントの設定。  
  
-   トレースの停止または開始。  
  
-   トレース ファイルおよびトレース テーブルの読み取り。  
  
-   トレースでのイベントに関する情報の取得。  
  
-   トレースでのフィルターに関する情報の取得。  
  
-   プログラムを使用したトレース データの操作。  
  
-   トレース テーブルおよびトレース ファイルの書き込み。  
  
-   トレース ファイルまたはトレース テーブルの再生。  
  
 トレース データ、`Trace`と`Replay`オブジェクトは、SMO アプリケーションで使用できるかを使用して手動で調べることができます[SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md)します。 トレース データと互換性のあるでも、 [SQL トレース](../../sql-trace/sql-trace.md)トレース機能を提供するストアド プロシージャ。  
  
 SMO トレース オブジェクトは、Microsoft.SQLServer.ConnectionInfo.dll ファイルへの参照が必要となる <xref:Microsoft.SqlServer.Management.Trace> 名前空間に存在します。  
  
 `Trace`と`Replay`オブジェクトを必要とする<xref:Microsoft.SqlServer.Management.Common.ServerConnection><xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A>オブジェクトのインスタンスとの接続を確立するために[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]します。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトは、<xref:Microsoft.SqlServer.Management.Common> 名前空間にあります。Microsoft.SQLServer.ConnectionInfo.dll ファイルへの参照が必要です。  
  
> [!NOTE]  
>   `Trace` オブジェクトおよび `Replay` オブジェクトは、64 ビット プラットフォームではサポートされていません。  
  
  
