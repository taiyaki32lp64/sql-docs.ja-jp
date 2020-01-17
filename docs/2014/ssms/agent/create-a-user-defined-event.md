---
title: ユーザー定義イベントの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5625e65b1da45e05002b540774f441f2deabd3f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63260946"
---
# <a name="create-a-user-defined-event"></a>ユーザー定義イベントの作成
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって定義済みのイベント以外のイベントを監視するには、ユーザー定義イベントを作成します。 また、各ユーザー定義イベントに対して重大度レベルを割り当てることもできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用中に、各ユーザー定義イベント メッセージに対して **[Windows アプリケーション イベント ログに書き込む]** オプションを選択して、そのメッセージがログに書き込まれるように設定できます。 既定では、ユーザー定義メッセージが生成された場合でも、その重大度が 19 より低い場合は [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーション ログに送られません。 したがって、重大度が 19 より低いユーザー定義メッセージは、SQL Server エージェントの警告をトリガーしません。  
  
 ユーザー定義イベントには、それぞれ一意のメッセージ番号が付けられている必要があります。 ユーザー定義イベントのメッセージ番号は、50,000 より大きくする必要があります。 イベントに対するメッセージを複数の言語で定義することもできます。 ただし、他の言語のメッセージを追加するには、 **En-US** エラー メッセージが存在している必要があります。  
  
 複数言語の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境を管理する場合は、サポートされている各言語でユーザー定義メッセージを作成することをお勧めします。 たとえば、英語サーバーとドイツ語サーバーの両方で使用する新しいイベント メッセージを作成する場合、イベント番号と重大度はどちらのサーバーに対しても同じものを使用しますが、各サーバーに異なる言語を割り当ててください。  
  
 次のタスクでは、ユーザー定義イベントの作成方法とイベントに応答する警告についての情報が得られます。  
  
 **メッセージ番号に基づいた警告を作成するには**  
  
-   [SQL Server Management Studio](create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **重大度レベルに基づいた警告を作成するには**  
  
-   [SQL Server Management Studio](create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **警告に対する応答を定義するには**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)  
  
 **ユーザー定義のイベント エラー メッセージを作成するには**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql)  
  
 **ユーザー定義のイベント エラー メッセージを変更するには**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-altermessage-transact-sql)  
  
 **ユーザー定義のイベント エラー メッセージを削除するには**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-dropmessage-transact-sql)  
  
 **警告を無効にしたり、再び有効にするには**  
  
-   [SQL Server Management Studio](disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
## <a name="see-also"></a>参照  
 [sp_update_alert &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
  
