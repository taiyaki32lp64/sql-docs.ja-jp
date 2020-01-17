---
title: アラートのプロパティ-新しい警告 (全般 ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.general.f1
ms.assetid: f5c11610-62e3-44df-9800-a5dc35be4a09
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca5b07a0cd6e6282e4d61075d86ca6af6a2abd70
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63062150"
---
# <a name="alert-properties-new-alert-general-page"></a>アラートのプロパティ-新しいアラート ([全般] ページ)
  このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告の全般プロパティを表示および変更できます。  
  
## <a name="options"></a>および  
 **名前**  
 警告の名前を変更します。  
  
 **[有効化]**  
 警告を有効にします。 警告が有効でない場合、警告に指定されたアクションは発生しません。  
  
 **型**  
 警告の種類を選択します。  
  
-   **SQL Server イベント警告** は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows イベント ログ内のメッセージに応答します。  
  
-   **SQL Server パフォーマンス条件警告** は、パフォーマンス カウンター内の特定の条件に応答します。  
  
-   **WMI イベント警告** は、WMI (Windows Management Instrumentation) イベントに応答します。  
  
## <a name="sql-server-event-alert-options"></a>SQL Server イベント警告のオプション  
 **データベース名**  
 イベントの対象のデータベースを指定します。イベントが発生するデータベースに関係なくメッセージに応答するには、 **[すべてのデータベース]** を選択します。  
  
 **エラー番号**  
 このイベントがエラーに応答することを指定し、エラー番号を指定します。  
  
 **Severity**  
 このイベントが特定の重大度レベルのすべてのメッセージに応答することを指定し、重大度レベルを指定します。  
  
 **[メッセージに次の内容が含まれている場合に警告する]**  
 特定の文字列でイベントをフィルター処理します。 このオプションを選択した場合、警告は特定の文字列が含まれるイベントに対してだけ応答します。  
  
 **[メッセージ テキスト]**  
 イベントをフィルター処理するために使用する文字列を指定します。  
  
## <a name="sql-server-performance-condition-alerts"></a>SQL Server パフォーマンス条件警告  
 **Object**  
 監視対象のパフォーマンス オブジェクトを指定します。  
  
 **カウンター**  
 監視対象のパフォーマンス オブジェクト内のカウンターを指定します。  
  
 **インスタンス**  
 監視対象のカウンターのインスタンスを指定します。  
  
 **[警告カウンター]**  
 警告が応答するカウンターの動作を指定します。 たとえば、 **[Free space in tempdb (KB)]** カウンターの値が特定の値を下回る条件や、 **[SQL Compilations/sec]** が特定の値を上回る条件に応答するように警告を設定できます。  
  
 **[値]**  
 カウンターの値を指定します。  
  
## <a name="wmi-event-alert-options"></a>WMI イベント警告のオプション  
 **名前空間**  
 WQL (WMI Query Language) ステートメントに使用する名前空間を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されているコンピューター上の名前空間だけがサポートされます。  
  
 **クエリ**  
 警告が応答するイベントを識別する WQL ステートメントを指定します。  
  
## <a name="see-also"></a>関連項目  
 [Alerts](alerts.md)   
 [WMI provider for Server Events の WQL の使用](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)   
 [エラー番号を使用して通知を作成します。](create-an-alert-using-an-error-number.md)   
 [Create an Alert Using Severity Level](create-an-alert-using-severity-level.md)  
  
  
