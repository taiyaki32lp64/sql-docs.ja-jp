---
title: DQS ログ ファイルの管理
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- logging
- log files
- dqs log files
ms.assetid: 4fccfd24-aede-4882-be69-ec1e82682e16
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 6edcf577b7783662a02efc3531ac02c2535ef078
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245419"
---
# <a name="manage-dqs-log-files"></a>DQS ログ ファイルの管理

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) のログ ファイルは、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]、および [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]の問題を診断およびトラブルシューティングする際に役に立ちます。 
  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]、および [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)]ごとに異なるログ ファイルが生成されます。  
  
 
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] を使用して、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] の機能とモジュールのログの重大度設定を構成できます。 また、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] コンピューターで DQS_MAIN データベースと XML ファイルの DQS ログ構成設定を手動で変更して、DQS ログ ファイルのその他の (詳細) 設定の一部を構成することもできます。  
  
##  <a name="DQSServer"></a>Data Quality Server のログファイル  
 
  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] のログ ファイルである DQServerLog.DQS_MAIN.log には、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]で実行されるアクティビティのログが含まれます。 SQL Server の既定のインスタンスをインストールした場合、DQServerLog.DQS_MAIN.log ファイルは C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log に格納されます。 
  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] のログ ファイルには、それぞれパイプ (|) で区切られた次の種類の情報が含まれています。  
  
-   日付と時刻  
  
-   スレッド名  
  
-   スレッド ID  
  
-   ログの重大度 (FATAL、ERROR、WARN、INFO、および DEBUG)  
  
    > [!NOTE]  
    >  DEBUG ログ重大度は、[詳細] と同じです。  
  
-   UID (内部 DQS インフラストラクチャ ID)  
  
-   名前空間  
  
-   クラスとメソッド  
  
-   メッセージ  
  
 これらに加えて、ログ ファイルには、アプリケーションのバージョン、コンピューター名、ユーザー名、およびオペレーティング システムに関する情報も表示されます。  
  
 
  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] ログ ファイルのサンプル エントリは、次のようになります。  
  
```  
23-08-2013 01:45:29|[]|4|INFO|PUID|InfInfoModuleStarting|Microsoft.Ssdqs.Core.Startup.ServerInit|Starting DQS ServerInit: version [12.0.0.0], machine name [DQS-TEST], user name [NT Service\MSSQLSERVER], operating system [Microsoft Windows NT 6.1.7600.0]...  
```  
  
 DQServerLog.DQS_MAIN.log ファイルはローリング ファイルです。既存のログ ファイルが、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] ログ構成設定で指定されたローリング ファイルのサイズを超えると、新しいログ ファイルが作成されます。 詳細については、「 [Configure Advanced Settings for DQS Log Files](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)」を参照してください。  
  
##  <a name="DQSClient"></a>ログファイルの Data Quality Client  
 
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のログ ファイルである DQClientLog.log には、クライアント側のログが含まれます。 
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のログ ファイルは %APPDATA%\SSDQS\Log に格納されます。 
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] ログ ファイルには、サーバー ログ ファイルと同様の情報が含まれますが、内容はクライアント側に関するものになります。  
  
 
  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] ログ ファイルと同様に、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] ログ ファイルもローリング ファイルです。既存のログ ファイルが、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] ログ構成設定で指定されたローリング ファイルのサイズを超えると、新しいログ ファイルが作成されます。 詳細については、「 [Configure Advanced Settings for DQS Log Files](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)」を参照してください。  
  
##  <a name="DQSCleansing"></a>DQS クレンジングコンポーネントのログファイル  
 
  [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] のログ ファイルである DQSSSISLog.log には、 [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]を使用して実行されたアクティビティのログが含まれます。 
  [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] コンポーネントのログ ファイルは %APPDATA%\SSDQS\Log に格納されます。 
  [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] ログ ファイルには、サーバー ログ ファイルと同様の情報が含まれますが、内容は [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)]に関するものになります。  
  
##  <a name="RT"></a>関連タスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]を使用して DQS ログ ファイルのログの重大度設定を構成する方法を説明します。|[DQS ログ ファイルの重大度レベルの構成](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|DQS ログ ファイルの詳細設定を手動で構成する方法を説明します。|[DQS ログ ファイルの詳細設定の構成](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
  
## <a name="see-also"></a>参照  
 [DQS 管理](../data-quality-services/dqs-administration.md)  
  
  
