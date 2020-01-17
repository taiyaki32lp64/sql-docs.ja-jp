---
title: トレース ファイルとテーブル サイズの制限 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- maximum file size for traces
- traces [SQL Server], file size
- size [SQL Server], tables
- file rollover option [SQL Server]
- size [SQL Server], files
ms.assetid: 88c31b02-f44c-4a14-be8b-437f2097de12
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b12834eac33fd016279b6f2f3a79cee413c3d23d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072884"
---
# <a name="limit-trace-file-and-table-sizes"></a>トレース ファイルとテーブル サイズの制限
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL トレースの結果のサイズは、トレースに含まれているイベント クラスと [!INCLUDE[ssDE](../../includes/ssde-md.md)] の使用方法によって異なります。 頻繁に発生するイベント クラスをトレースする場合、最大ファイル サイズまたは最大行数を設定することにより、トレースで収集されるデータの量を最小限に抑えることができます。 最大ファイル サイズまたは最大行数を指定することにより、トレース ファイルまたはテーブルが指定された上限を超えて大きくならないようにすることができます。  
  
> [!NOTE]  
>  既存のファイルにトレース データを保存する場合、そのファイルにデータを追加するか、またはそのファイルを上書きできます。 ファイルにデータを追加する場合、トレース ファイルが既に指定した最大ファイル サイズに達しているか、または最大ファイル サイズを超えているときは、最大ファイル サイズを増やすか、または新しいファイルを指定するよう通知されます。 トレース テーブルについても同じです。  
  
## <a name="maximum-file-size"></a>最大ファイル サイズ  
 最大ファイル サイズが指定されたトレースでは、その最大ファイル サイズに達すると、ファイルへのトレース情報の保存が停止されます。 このオプションを使用すると、イベントをより小さく管理しやすいファイルにグループ化できるようになります。 また、ファイル サイズを制限すると、自動トレースをより安全に実行できるようになります。これは、最大ファイル サイズに達するとトレースが停止するためです。 最大ファイル サイズは、Transact-SQL ストアド プロシージャまたは [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して作成されたトレースに対して設定できます。  
  
 最大ファイル サイズ オプションの上限は 1 GB です。 既定の最大ファイル サイズは 5 MB です。  
  
### <a name="enabling-file-rollover"></a>ファイルのロールオーバーの有効化  
 ファイルのロールオーバー オプションを使用すると、最大ファイル サイズに達したときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって現在のファイルが閉じられ、新しいファイルが作成されます。 新しいファイルの名前は以前のファイルと同じになりますが、その順番を示すために名前に整数が追加されます。 たとえば、元のトレース ファイルの名前が filename_1.trc である場合、次のトレース ファイルの名前は filename_2.trc になります。 新しいロールオーバー ファイルに割り当てられた名前が既存のファイルで既に使用されている場合、その既存のファイルは、読み取り専用でない限り上書きされます。 トレース データをファイルに保存する場合、ファイルのロールオーバー オプションが既定で有効になります。  
  
> [!NOTE]  
>  ファイルのロールオーバー オプションを有効にすると、トレースは他の方法によって停止されるまで続行されます。 ファイル サイズの制限に達した後でトレースを停止するには、ファイルのロールオーバー オプションを無効にします。  
  
 **トレース ファイルの最大ファイル サイズを設定するには**  
  
 [トレース ファイルの最大ファイル サイズの設定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
## <a name="maximum-number-of-rows"></a>最大行数  
 最大行数が指定されたトレースでは、その最大行数に達すると、テーブルへのトレース情報の保存が停止されます。 1 つのイベントによって 1 つの行が構成されるため、このパラメーターでは、収集されるイベント数の制限が設定されます。 最大行数を設定すると、自動トレースを実行しやすくなります。 たとえば、トレース データをテーブルに保存するトレースを開始する必要があるが、ファイルが大きくなりすぎたらトレースを停止する場合、その操作を自動トレースで行うことができます。  
  
 最大行数を指定し、その最大行数に達した場合、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] が実行されている限りトレースは続行されますが、トレース情報はそれ以上記録されません。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] トレースが停止されるまで、トレース結果の表示が続行されます。  
  
 **トレースの最大行数を設定するには**  
  
 [トレース テーブルの最大テーブル サイズの設定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
## <a name="see-also"></a>参照  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)  
  
  
