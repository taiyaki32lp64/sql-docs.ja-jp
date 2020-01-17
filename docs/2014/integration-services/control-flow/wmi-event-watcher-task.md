---
title: WMI イベント監視タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmieventwatchertask.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Event Watcher task [Integration Services]
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4add98b6c085d52238a528c313008bc688ae6e54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829505"
---
# <a name="wmi-event-watcher-task"></a>WMI イベント監視タスク
  WMI イベント監視タスクは、Windows Management Instrumentation Query Language (WQL) イベント クエリを使用して対象のイベントを指定することにより、Windows Management Instrumentation (WMI) イベントを監視します。 WMI イベント監視タスクは、次の目的で使用できます。  
  
-   ファイルがフォルダーに追加されたという通知を待機し、ファイルの処理を開始します。  
  
-   サーバー上の利用可能なメモリが、指定した割合を下回った場合、ファイルを削除するパッケージを実行します。  
  
-   アプリケーションのインストールを監視し、そのアプリケーションを使用するパッケージを実行します。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、WMI 情報を読み取るタスクが含まれています。  
  
 このタスクの詳細については、次のトピックを参照してください。  
  
-   [WMI データ リーダー タスク](wmi-data-reader-task.md)  
  
## <a name="wql-queries"></a>WQL クエリ  
 WQL は SQL 言語仕様の 1 つで、WMI イベント通知やその他 WMI 固有の機能をサポートする拡張機能が付いています。 WQL の詳細については、 [MSDN ライブラリ](https://go.microsoft.com/fwlink/?linkid=62553)にある Windows Management Instrumentation のマニュアルを参照してください。  
  
> [!NOTE]  
>  WMI クラスは、Windows のバージョンによって異なります。  
  
 次のクエリは、CPU 使用率が 40% を超えた場合の通知を監視します。  
  
```  
SELECT * from __InstanceModificationEvent WITHIN 2 WHERE TargetInstance ISA 'Win32_Processor' and TargetInstance.LoadPercentage > 40  
```  
  
 次のクエリは、ファイルがフォルダーに追加された場合の通知を監視します。  
  
```  
SELECT * FROM __InstanceCreationEvent WITHIN 10 WHERE TargetInstance ISA "CIM_DirectoryContainsFile" and TargetInstance.GroupComponent= "Win32_Directory.Name=\"c:\\\\WMIFileWatcher\""   
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-event-watcher-task"></a>WMI イベント監視タスクで使用できるカスタム ログ メッセージ  
 次の表は、WMI イベント監視タスクのカスタム ログ エントリの一覧です。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」をご覧ください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|タスクが監視しているイベントが発生したことを示します。|  
|`WMIEventWatcherTimedout`|タスクがタイムアウトしたことを示します。|  
|`WMIEventWatcherWatchingForWMIEvents`|タスクが WQL クエリの実行を開始したことを示します。 このエントリには、クエリが含まれています。|  
  
## <a name="configuration-of-the-wmi-event-watcher-task"></a>WMI イベント監視タスクの構成  
 WMI データ リーダー タスクは、次の方法で構成できます。  
  
-   使用する WMI 接続マネージャーを指定します。  
  
-   WQL クエリの実行元を指定します。 実行元には、タスクの外部の変数またはファイルを設定できます。また、クエリはタスクのプロパティ内に格納できます。  
  
-   WMI イベントが発生したときにタスクが実行するアクションを指定します。 イベント通知およびイベント後の状態のログが記録できます。または、WMI イベント、通知、およびイベント後の状態に関連する情報を提供する、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のカスタム イベントを発生させることができます。  
  
-   イベントに対するタスクの応答方法を定義します。 タスクは、イベントに応じて、成功または失敗するように構成できます。または、単にイベントを再度監視するように構成することもできます。  
  
-   WMI クエリがタイムアウトしたときに、タスクが実行するアクションを指定します。タイムアウトとタイムアウト後の状態のログを記録できます。または、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のカスタム イベントを発生させ、WMI イベントのタイムアウトを示し、タイムアウトとタイムアウトの状態のログを記録できます。  
  
-   タイムアウトに対するタスクの応答方法を定義します。タスクは成功または失敗するように構成できます。または、単にイベントを再度監視するように構成することもできます。  
  
-   タスクがイベントを監視する回数を指定します。  
  
-   タイムアウトを指定します。  
  
 監視元がファイルの場合、WMI イベント監視タスクは、ファイル接続マネージャーを使用してファイルに接続します。 詳細については、「 [フラット ファイル接続マネージャー](../connection-manager/file-connection-manager.md)」を参照してください。  
  
 WMI イベント監視タスクは、WMI 接続マネージャーを使用して、WMI 情報を読み取るサーバーに接続します。 詳細については、「 [WMI 接続マネージャー](../connection-manager/wmi-connection-manager.md)」を参照してください。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[WMI イベント監視タスク エディター] &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [[WMI イベント監視タスク エディター] &#40;[WMI オプション] ページ&#41;](../wmi-event-watcher-task-editor-wmi-options-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-wmi-event-watcher-task"></a>プログラムによる WMI イベント監視タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
  
