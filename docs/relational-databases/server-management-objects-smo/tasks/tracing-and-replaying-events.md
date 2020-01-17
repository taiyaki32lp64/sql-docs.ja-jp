---
title: イベントのトレースと再生 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d83b716d9919bf322097b8ded8409950982d961c
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148358"
---
# <a name="tracing-and-replaying-events"></a>イベントのトレースおよび再生
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO では、 <xref:Microsoft.SqlServer.Management.Trace> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]名前空間の**Trace**オブジェクトと**Replay**オブジェクトによって、またはのインスタンスの監視に使用される機能にプログラムからアクセスできます。[!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 各イベントに関するデータをキャプチャし、ファイルやテーブルに保存して、後で分析できます。 たとえば、実稼動環境を監視して、どのプロシージャの実行が遅く、パフォーマンスに影響を与えているかを確認できます。  
  
 **Trace**オブジェクトと**Replay**オブジェクトには、の[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスでトレースを作成するために使用できる一連のオブジェクトが用意されています。 これらのオブジェクトをユーザー独自のアプリケーションから使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] または [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] に対してトレースを手動で作成することもできます。 また、SMO**トレース**オブジェクトを使用して、、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]、または DTS ログを監視することによって作成された SQL トレースファイルとテーブルを読み取ることができます。  
  
 SMO**トレース**オブジェクトを使用すると、次の機能を実行できます。  
  
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
  
 **トレース**オブジェクトと**再生**オブジェクトからのトレースデータは、SMO アプリケーションで使用できます。また、 [SQL Server プロファイラー](../../../tools/sql-server-profiler/sql-server-profiler.md)を使用して手動で調べることもできます。 トレースデータは、トレース機能を提供する[SQL トレース](../../../relational-databases/sql-trace/sql-trace.md)ストアドプロシージャとも互換性があります。  
  
 SMO トレース オブジェクトは、Microsoft.SQLServer.ConnectionInfo.dll ファイルへの参照が必要となる <xref:Microsoft.SqlServer.Management.Trace> 名前空間に存在します。  
  
 **Trace**オブジェクトと**Replay**オブジェクトには、のインスタンスとの[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]接続を確立するための[serverconnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A>オブジェクトが必要です。 [Serverconnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)オブジェクトは、ConnectionInfo ファイルへの参照を必要とする、 [microsoft の sqlserver](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common)名前空間に存在しています。  
  
> [!NOTE]  
>  **トレース**オブジェクトと**再生**オブジェクトは、64ビットプラットフォームではサポートされていません。  
  
  
