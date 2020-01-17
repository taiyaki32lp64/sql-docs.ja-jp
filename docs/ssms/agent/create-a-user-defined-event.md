---
title: ユーザー定義イベントの作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, user-defined events
- user-defined events [SQL Server]
- multiple language support [SQL Server], alerts
- languages [SQL Server], alerts
- severity levels [SQL Server]
- global considerations [SQL Server], alerts
- events [SQL Server], user-defined
- SQL Server Agent alerts, multiple-language environments
- alerts [SQL Server], user-defined events
- alerts [SQL Server], multiple-language environments
- custom events [SQL Server Agent]
- international considerations [SQL Server], alerts
ms.assetid: 03d71a35-97fa-4bba-aa9a-23ac9c9cf879
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1f5eb2eb09293cc08469cb9865edad30a4dcbc8a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267319"
---
# <a name="create-a-user-defined-event"></a>ユーザー定義イベントの作成
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって定義済みのイベント以外のイベントを監視するには、ユーザー定義イベントを作成します。 また、各ユーザー定義イベントに対して重大度レベルを割り当てることもできます。  
  
> [!NOTE]  
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用中に、各ユーザー定義イベント メッセージに対して **[Windows アプリケーション イベント ログに書き込む]** オプションを選択して、そのメッセージがログに書き込まれるように設定できます。 既定では、ユーザー定義メッセージが生成された場合でも、その重大度が 19 より低い場合は [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows アプリケーション ログに送られません。 したがって、重大度が 19 より低いユーザー定義メッセージは、SQL Server エージェントの警告をトリガーしません。  
  
ユーザー定義イベントには、それぞれ一意のメッセージ番号が付けられている必要があります。 ユーザー定義イベントのメッセージ番号は、50,000 より大きくする必要があります。 イベントに対するメッセージを複数の言語で定義することもできます。 ただし、他の言語のメッセージを追加するには、 **En-US** エラー メッセージが存在している必要があります。  
  
複数言語の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境を管理する場合は、サポートされている各言語でユーザー定義メッセージを作成することをお勧めします。 たとえば、英語サーバーとドイツ語サーバーの両方で使用する新しいイベント メッセージを作成する場合、イベント番号と重大度はどちらのサーバーに対しても同じものを使用しますが、各サーバーに異なる言語を割り当ててください。  
  
次のタスクでは、ユーザー定義イベントの作成方法とイベントに応答する警告についての情報が得られます。  
  
**メッセージ番号に基づいた警告を作成するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**重大度レベルに基づいた警告を作成するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**警告に対する応答を定義するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)  
  
**ユーザー定義のイベント エラー メッセージを作成するには**  
  
-   [Transact-SQL](https://msdn.microsoft.com/54746d30-f944-40e5-a707-f2d9be0fb9eb)  
  
**ユーザー定義のイベント エラー メッセージを変更するには**  
  
-   [Transact-SQL](https://msdn.microsoft.com/1b28f280-8ef9-48e9-bd99-ec14d79abaca)  
  
**ユーザー定義のイベント エラー メッセージを削除するには**  
  
-   [Transact-SQL](https://msdn.microsoft.com/17287a15-cdde-43d1-bb18-9f920bc15db8)  
  
**警告を無効にしたり、再び有効にするには**  
  
-   [SQL Server Management Studio](../../ssms/agent/disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  
## <a name="see-also"></a>参照  
[sp_update_alert (Transact-SQL)](https://msdn.microsoft.com/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  
