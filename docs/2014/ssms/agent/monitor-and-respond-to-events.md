---
title: イベントの監視と応答 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- notifications [SQL Server], alert
- events [SQL Server], alerts
- alerts [SQL Server]
- notifications [SQL Server]
- events [SQL Server], automatically responding to
- administrator notifications [SQL Server Agent]
- automatic event responses
- SQL Server Agent alerts
- monitoring [SQL Server], events
- responding to events automatically
ms.assetid: f7fbe155-5b68-4777-bc71-a47637471f32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bb16e6e7fc21d3b399d63d2e833eb846d62278ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62720126"
---
# <a name="monitor-and-respond-to-events"></a>イベントの監視と応答
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用して、 *からのメッセージ、特定のパフォーマンス条件、WMI (Windows Management Instrumentation) イベントなどの*イベント [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を監視したり、イベントに自動的に応答したりできます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [警告](alerts.md)  
 警告の命名、および警告が応答するイベントやパフォーマンス条件の選択について説明します。  
  
 [ユーザー定義イベントの作成](create-a-user-defined-event.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によってあらかじめ定義されているイベント以外のイベントを作成する方法について説明します。  
  
 [オペレーター](operators.md)  
 ジョブが失敗または成功したときに通知を送信するために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで使用できる、管理者の別名の作成について説明します。  
  
## <a name="about-monitoring-and-responding-to-events"></a>イベントの監視と応答について  
 イベントへの自動応答を *警告*と呼びます。 1 つ以上のイベントの警告を定義して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがイベントの発生に応答する方法を指定できます。 警告は、管理者に通知するか、ジョブを実行するか、またはその両方を行ってイベントに応答できます。 警告は、別のコンピューターの Microsoft Windows アプリケーション ログにイベントを転送することもできます。 たとえば、重大度レベル 19 のイベントが発生した場合に、オペレーターに直ちに通知されるように指定できます。 データベース管理者は警告を定義することにより、より効果的に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を監視および管理できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、警告が定義されているイベントにのみ応答します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでによってイベントを監視するために使用される方法は、イベントの種類によって異なります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告がパフォーマンス カウンターに定義されていると、そのパフォーマンス カウンターは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって直接監視されます。 WMI イベントでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントにより WMI イベントのイベント クエリが登録されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からのメッセージに応答するために Windows アプリケーション ログが監視されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、このログに示されるメッセージだけに応答できます。 既定では、SQL Server によって、次のメッセージが Windows アプリケーション ログに記録されます。  
  
-   重大度レベルが 19 以上の sysmessages エラー。  
  
     重大度レベルが 19 より低い特定の sysmessages エラーもログに記録する場合は、sp_altermessage ストアド プロシージャを使用して、"常にログ記録されています" などのエラーを指定します。  
  
-   WITH LOG 構文を使用して実行されるすべての RAISERROR ステートメント。  
  
     RAISERROR WITH LOG は、SQL Server のインスタンスから Windows アプリケーション ログに書き込むのに推奨できる手段です。  
  
-   xp_logevent を使用してログ記録されたアプリケーション イベント。  
  
    > [!NOTE]  
    >  アプリケーション イベントのログ記録により、ログ領域が使用され、その結果 Windows アプリケーション ログの最大サイズを超える可能性があります。 SQL Server のイベント情報を失わないように、Windows アプリケーション ログの最大サイズが十分大きいかどうかを確認してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってメッセージがログ記録されると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者が定義した警告とメッセージが比較されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスは、イベントのソースが何であっても、イベントの警告で指定されたタスクを実行することによりそのイベントに応答します。  
  
## <a name="see-also"></a>関連項目  
 [sp_altermessage &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-altermessage-transact-sql)  
  
  
