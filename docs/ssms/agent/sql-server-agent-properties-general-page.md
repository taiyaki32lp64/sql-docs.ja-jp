---
title: '[SQL Server エージェントのプロパティ] ([全般] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f2e0439e214eb047749ddc3822737dffb4223a49
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265270"
---
# <a name="sql-server-agent-properties-general-page"></a>[SQL Server エージェントのプロパティ]\([全般] ページ)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このページを使用すると、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスの全般プロパティを表示したり、変更したりできます。  
  
## <a name="options"></a>オプション  
**[サービスの状態]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスの現在の状態を表示します。  
  
**[予期しない停止時に SQL Server を自動的に再起動する]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が予期せず停止した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動します。  
  
**[予期しない停止時に SQL Server エージェントを自動的に再起動する]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが予期せず停止した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを再起動します。  
  
**Filename**  
エラー ログのファイル名を指定します。  
  
**[...]**  
エラー ログ ファイルを参照します。  
  
**[実行トレース メッセージを含める]**  
エラー ログに実行トレース メッセージを含めます。 トレース メッセージにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの処理に関する詳細情報が得られます。 そのため、このオプションを選択した場合は、ログ ファイルに必要なディスク領域が大きくなります。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントに関係すると思われる問題をトラブルシューティングするときにのみ選択してください。  
  
**[OEM ファイルに書き込む]**  
エラー ログ ファイルを非 Unicode ファイルとして書き込みます。 これにより、ログ ファイルによって消費されるディスク領域が減少します。 ただし、このオプションを有効にすると Unicode データを含むメッセージが読み取りにくくなる場合があります。  
  
**[Net Send 受信者]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによってログ ファイルに書き込まれるメッセージの、Net Send 通知を受信するオペレーターの名前を入力します。  
  
## <a name="see-also"></a>参照  
[オペレーター](../../ssms/agent/operators.md)  
[SQL Server エージェント エラー ログ](../../ssms/agent/sql-server-agent-error-log.md)  
  
