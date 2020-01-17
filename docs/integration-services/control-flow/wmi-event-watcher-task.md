---
title: WMI イベント監視タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmieventwatchertask.f1
- sql13.dts.designer.wmieventwatcher.general.f1
- sql13.dts.designer.wmieventwatcher.wmiquery.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Event Watcher task [Integration Services]
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d31b2d7515eaebc7d0c2e5fb5861d8b6b51ad6f7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293710"
---
# <a name="wmi-event-watcher-task"></a>WMI イベント監視タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  WMI イベント監視タスクは、Windows Management Instrumentation Query Language (WQL) イベント クエリを使用して対象のイベントを指定することにより、Windows Management Instrumentation (WMI) イベントを監視します。 WMI イベント監視タスクは、次の目的で使用できます。  
  
-   ファイルがフォルダーに追加されたという通知を待機し、ファイルの処理を開始します。  
  
-   サーバー上の利用可能なメモリが、指定した割合を下回った場合、ファイルを削除するパッケージを実行します。  
  
-   アプリケーションのインストールを監視し、そのアプリケーションを使用するパッケージを実行します。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、WMI 情報を読み取るタスクが含まれています。  
  
 このタスクの詳細については、次のトピックを参照してください。  
  
-   [WMI データ リーダー タスク](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
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
 次の表は、WMI イベント監視タスクのカスタム ログ エントリの一覧です。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|タスクが監視しているイベントが発生したことを示します。|  
|**WMIEventWatcherTimedout**|タスクがタイムアウトしたことを示します。|  
|**WMIEventWatcherWatchingForWMIEvents**|タスクが WQL クエリの実行を開始したことを示します。 このエントリには、クエリが含まれています。|  
  
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
  
 監視元がファイルの場合、WMI イベント監視タスクは、ファイル接続マネージャーを使用してファイルに接続します。 詳細については、「 [フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)」を参照してください。  
  
 WMI イベント監視タスクは、WMI 接続マネージャーを使用して、WMI 情報を読み取るサーバーに接続します。 詳細については、「 [WMI 接続マネージャー](../../integration-services/connection-manager/wmi-connection-manager.md)」を参照してください。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-wmi-event-watcher-task"></a>プログラムによる WMI イベント監視タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
## <a name="wmi-event-watcher-task-editor-general-page"></a>[WMI イベント監視タスク エディター] ([全般] ページ)
  **[WMI イベント監視タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、WMI イベント監視タスクに名前を付けて説明を記述することができます。  
  
 WQL (WMI Query Language) の詳細については、MSDN ライブラリにある Windows Management Instrumentation のトピック「 [WQL を使用したクエリ](/windows/win32/wmisdk/querying-with-wql)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 WMI イベント監視タスクに一意の名前を提供します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 WMI イベント監視タスクの説明を入力します。  
  
## <a name="wmi-event-watcher-task-editor-wmi-options-page"></a>[WMI イベント監視タスク エディター] ([WMI オプション] ページ)
  **[WMI イベント監視タスク エディター]** ダイアログ ボックスの **[WMI オプション]** ページを使用すると、WQL (Windows Management Instrumentation Query Language) クエリのソースや、WMI イベント監視タスクがどのように WMI (Microsoft Windows Instrumentation) イベントに応答するかを指定できます。  
  
 WQL (WMI Query Language) の詳細については、MSDN ライブラリにある Windows Management Instrumentation のトピック「 [WQL を使用したクエリ](/windows/win32/wmisdk/querying-with-wql)」を参照してください。  
  
### <a name="static-options"></a>静的オプション  
 **[WMIConnectionName]**  
 WMI 接続マネージャーを一覧から選択するか、[\<**新しい WMI 接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [WMI 接続マネージャー](../../integration-services/connection-manager/wmi-connection-manager.md)、[WMI 接続マネージャー エディター](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **[WQLQuerySourceType]**  
 タスクで実行する WQL クエリのソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|ソースを WQL クエリに設定します。 この値を選択すると、動的オプションの **[WQLQuerySource]** が表示されます。|  
|**[ファイル接続]**|WQL クエリを含むファイルを選択します。 この値を選択すると、動的オプションの **[WQLQuerySource]** が表示されます。|  
|**変数**|ソースを、WQL クエリを定義する変数に設定します。 この値を選択すると、動的オプションの **[WQLQuerySource]** が表示されます。|  
  
 **[ActionAtEvent]**  
 WMI イベントをログに記録すると共に [!INCLUDE[ssIS](../../includes/ssis-md.md)] アクションを実行するか、単にイベントをログに記録するだけにするかを指定します。  
  
 **[AfterEvent]**  
 WMI イベントを受け取った後にタスクを成功または失敗させるか、イベントの発生をタスクで引き続き監視するかを指定します。  
  
 **[ActionAtTimeout]**  
 WMI クエリのタイムアウトをログに記録すると共に [!INCLUDE[ssIS](../../includes/ssis-md.md)] イベントを発生させるか、単にタイムアウトをログに記録するだけにするかを指定します。  
  
 **[AfterTimeout]**  
 タイムアウトに対してタスクを成功または失敗させるか、別のタイムアウトの発生をタスクで引き続き監視するかを指定します。  
  
 **[NumberOfEvents]**  
 監視するイベントの数を指定します。  
  
 **Timeout**  
 イベントが発生するのを待機する秒数を指定します。 値 0 は、タイムアウトを設定しないことを意味します。  
  
### <a name="wqlquerysource-dynamic-options"></a>[WQLQuerySource] の動的オプション  
  
#### <a name="wqlquerysource--direct-input"></a>[WQLQuerySource] = [直接入力]  
 **[WQLQuerySource]**  
 クエリを指定します。または、参照ボタン ( [...] ) をクリックし、 **[WQL クエリ]** ダイアログ ボックスを使用してクエリを入力します。  
  
#### <a name="wqlquerysource--file-connection"></a>[WQLQuerySource] = [ファイル接続]  
 **[WQLQuerySource]**  
 ファイル接続マネージャーを一覧から選択するか、\< **[新しい接続...]** をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="wqlquerysource--variable"></a>[WQLQuerySource] = [変数]  
 **[WQLQuerySource]**  
 一覧で変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
