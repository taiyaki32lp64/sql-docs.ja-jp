---
title: WMI データ リーダー タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmidatareadertask.f1
- sql13.dts.designer.wmidatareadertask.general.f1
- sql13.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e0c1b30985bf93ff1b04af85e45bf64e53c75853
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293717"
---
# <a name="wmi-data-reader-task"></a>WMI データ リーダー タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  WMI データ リーダー タスクは、WQL (Windows Management Instrumentation Query Language) を使用してクエリを実行し、コンピューター システムに関する WMI から情報を返します。 WMI データ リーダー タスクは、次の目的で使用できます。  
  
-   ローカルまたはリモート コンピューター上の Windows イベント ログのクエリを実行し、その情報をファイルまたは変数に書き込みます。  
  
-   ハードウェア コンポーネントの存在、状態、またはプロパティに関する情報を取得し、この情報を使用して制御フロー内の他のタスクを実行するかどうかを決定します。  
  
-   アプリケーションの一覧を取得し、インストールされている各アプリケーションのバージョンを判別します。  
  
 WMI データ リーダー タスクは、次の方法で構成できます。  
  
-   使用する WMI 接続マネージャーを指定します。  
  
-   WQL クエリの実行元を指定します。 このクエリは、タスクのプロパティ内に格納できます。または、タスク外の変数またはファイル内にも格納できます。  
  
-   WQL クエリ結果の形式を定義します。 このタスクでは、テーブル、プロパティの名前と値のペア、またはプロパティ値の形式がサポートされています。  
  
-   クエリの実行先を指定します。 この実行先には、変数またはファイルを設定できます。  
  
-   クエリの実行先で、上書き、保持、または追加のいずれを行うかを示します。  
  
 実行元または実行先がファイルの場合、WMI データ リーダー タスクは、ファイル接続マネージャーを使用してファイルに接続します。 詳細については、「 [フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)」をご覧ください。  
  
 WMI データ リーダー タスクは、WMI 接続マネージャーを使用して、WMI 情報を読み取るサーバーに接続します。 詳細については、「 [WMI 接続マネージャー](../../integration-services/connection-manager/wmi-connection-manager.md)」をご覧ください。  
  
## <a name="wql-query"></a>WQL クエリ  
 WQL は SQL 言語仕様の 1 つで、WMI イベント通知やその他 WMI 固有の機能をサポートする拡張機能が付いています。 WQL の詳細については、 [MSDN ライブラリ](https://go.microsoft.com/fwlink/?linkid=7022)にある Windows Management Instrumentation のマニュアルを参照してください。  
  
> [!NOTE]  
>  WMI クラスは、Windows のバージョンによって異なります。  
  
 次の WQL クエリは、アプリケーション ログ イベント内のエントリを返します。  
  
```  
SELECT * FROM Win32_NTLogEvent WHERE LogFile = 'Application' AND (SourceName='SQLISService' OR SourceName='SQLISPackage') AND TimeGenerated > '20050117'  
```  
  
 次の WQL クエリは、論理ディスク情報を返します。  
  
```  
SELECT FreeSpace, DeviceId, Size, SystemName, Description FROM Win32_LlogicalDisk  
```  
  
 次の WQL クエリは、オペレーティング システムに対する QFE (Quick Fix Engineering) 更新の一覧を返します。  
  
```  
Select * FROM Win32_QuickFixEngineering  
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-data-reader-task"></a>WMI データ リーダー タスクで使用できるカスタム ログ メッセージ  
 次の表は、WMI データ リーダー タスクのカスタム ログ エントリの一覧です。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|タスクが WMI データの読み取りを開始したことを示します。|  
|**WMIDataReaderOperation**|タスクで実行された WQL クエリを報告します。|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>WMI データ リーダー タスクの構成  
 プロパティはプログラムによって設定するか、または [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="wmi-data-reader-task-editor-general-page"></a>[WMI データ リーダー タスク エディター] ([全般] ページ)
  **[WMI データ リーダー タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、WMI データ リーダー タスクの名前と説明を入力できます。  
  
  WQL (WMI Query Language) の詳細については、MSDN ライブラリにある Windows Management Instrumentation のトピック「 [WQL を使用したクエリ](/windows/win32/wmisdk/querying-with-wql)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 WMI データ リーダー タスクの一意な名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 WMI データ リーダー タスクの説明を入力します。  
  
## <a name="wmi-data-reader-task-editor-wmi-options-page"></a>[WMI データ リーダー タスク エディター] ([WMI オプション] ページ)
  **[WMI データ リーダー タスク エディター]** ダイアログ ボックスの **[WMI オプション]** ページを使用すると、WQL (Windows Management Instrumentation Query Language) クエリのソースおよびクエリ結果の出力先を指定できます。  
  
 WQL (WMI Query Language) の詳細については、MSDN ライブラリにある Windows Management Instrumentation のトピック「 [WQL を使用したクエリ](/windows/win32/wmisdk/querying-with-wql)」を参照してください。  
  
### <a name="static-options"></a>静的オプション  
 **[WMIConnectionName]**  
 WMI 接続マネージャーを一覧から選択するか、[\<**新しい WMI 接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [WMI 接続マネージャー](../../integration-services/connection-manager/wmi-connection-manager.md)、[WMI 接続マネージャー エディター](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **[WQLQuerySourceType]**  
 タスクで実行する WQL クエリのソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|ソースを WQL クエリに設定します。 この値を選択すると、動的オプションの **[WQLQuerySourceType]** が表示されます。|  
|**[ファイル接続]**|WQL クエリを含むファイルを選択します。 この値を選択すると、動的オプションの **[WQLQuerySourceType]** が表示されます。|  
|**変数**|WQL クエリを定義する変数に、ソースを設定します。 この値を選択すると、動的オプションの **[WQLQuerySourceType]** が表示されます。|  
  
 **[OutputType]**  
 データ テーブル、プロパティ値、またはプロパティ名と値のいずれを出力に含めるかを指定します。  
  
 **[OverwriteDestination]**  
 出力先のファイルまたは変数内の元のデータを変更しないか、上書きするか、データを追加するかを指定します。  
  
 **[DestinationType]**  
 タスクで実行する WQL クエリの出力先の種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[ファイル接続]**|WQL クエリの結果を保存するファイルを選択します。 この値を選択すると、動的オプションの **[DestinationType]** が表示されます。|  
|**変数**|WQL クエリの結果を保存する変数を設定します。 この値を選択すると、動的オプションの **[DestinationType]** が表示されます。|  
  
### <a name="wqlquerysourcetype-dynamic-options"></a>[WQLQuerySourceType] 動的オプション  
  
#### <a name="wqlquerysourcetype--direct-input"></a>[WQLQuerySourceType] = [直接入力]  
 **[WQLQuerySource]**  
 クエリを指定します。または、参照 ( [...] ) をクリックし、 **[WQL クエリ]** ダイアログ ボックスを使用してクエリを入力します。  
  
#### <a name="wqlquerysourcetype--file-connection"></a>[WQLQuerySourceType] = [ファイル接続]  
 **[WQLQuerySource]**  
 ファイル接続マネージャーを一覧から選択するか、\< **[新しい接続...]** をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="wqlquerysourcetype--variable"></a>[WQLQuerySourceType] = [変数]  
 **[WQLQuerySource]**  
 一覧で変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="destinationtype-dynamic-options"></a>[DestinationType] 動的オプション  
  
#### <a name="destinationtype--file-connection"></a>[DestinationType] = [ファイル接続]  
 **変換先**  
 ファイル接続マネージャーを一覧から選択するか、\< **[新しい接続...]** をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="destinationtype--variable"></a>[DestinationType] = [変数]  
 **変換先**  
 一覧で変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
