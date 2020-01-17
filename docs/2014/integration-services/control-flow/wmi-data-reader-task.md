---
title: WMI データ リーダー タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmidatareadertask.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 12340ae2ba13bf6219cf9940a56eeaa8b995f3e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829495"
---
# <a name="wmi-data-reader-task"></a>WMI データ リーダー タスク
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
  
 実行元または実行先がファイルの場合、WMI データ リーダー タスクは、ファイル接続マネージャーを使用してファイルに接続します。 詳細については、「 [フラット ファイル接続マネージャー](../connection-manager/file-connection-manager.md)」をご覧ください。  
  
 WMI データ リーダー タスクは、WMI 接続マネージャーを使用して、WMI 情報を読み取るサーバーに接続します。 詳細については、「 [WMI 接続マネージャー](../connection-manager/wmi-connection-manager.md)」をご覧ください。  
  
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
 次の表は、WMI データ リーダー タスクのカスタム ログ エントリの一覧です。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」をご覧ください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|タスクが WMI データの読み取りを開始したことを示します。|  
|`WMIDataReaderOperation`|タスクで実行された WQL クエリを報告します。|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>WMI データ リーダー タスクの構成  
 プロパティはプログラムによって設定するか、または [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[WMI データ リーダー タスク エディター] &#40;[WMI オプション] ページ&#41;](../wmi-data-reader-task-editor-wmi-options-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
