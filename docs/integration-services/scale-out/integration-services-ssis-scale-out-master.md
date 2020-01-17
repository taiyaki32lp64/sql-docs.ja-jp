---
title: SQL Server Integration Services (SSIS) Scale Out Master | Microsoft Docs
description: この記事では、SSIS Scale Out の Scale Out Master コンポーネントについて説明します
ms.custom: performance
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: e3e52a854224210ed4561dbce12877fbb4c0f6fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082120"
---
# <a name="integration-services-ssis-scale-out-master"></a>Integration Services (SSIS) Scale Out Master

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Scale Out Master では、SSISDB カタログと Scale Out Master サービスを利用して Scale Out システムが管理されます。 

SSISDB カタログでは、Scale Out Worker、パッケージ、実行に関するすべての情報が保存されます。 Scale Out Worker を有効にして、Scale Out でパッケージを実行するインターフェイスを提供します。詳細については、「[チュートリアル:Integration Services Scale Out をセットアップする](walkthrough-set-up-integration-services-scale-out.md)」と「[Integration Services でパッケージを実行する](run-packages-in-integration-services-ssis-scale-out.md)」を参照してください。

Scale Out Master サービスは、Scale Out Worker との通信を担当する Windows サービスです。 HTTPS 経由で Scale Out Worker のパッケージ実行の状態を返し、SSISDB のデータを操作します。 

## <a name="scale-out-views-and-stored-procedures-in-ssisdb"></a>Scale Out ビューと SSISDB のストアド プロシージャ

### <a name="views"></a>ビュー

- [[catalog].[master_properties]](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)
- [[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)

### <a name="stored-procedures"></a>ストアド プロシージャ

- Scale Out Worker を管理する場合:
    - [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)
    - [[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)

- Scale Out のパッケージを実行する場合:
    - [[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)
    - [[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)
    - [[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)

## <a name="configure-the-scale-out-master-service"></a>Scale Out Master サービスを構成する

`<drive>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config` ファイルを使用して、SSIS Scale Out サービスを構成します。 構成ファイルの更新後に、サービスを再起動する必要があります。


|構成  |[説明]  |[既定値]  |
|---------|---------|---------|
|PortNumber|Scale Out Worker との通信に利用されるネットワーク ポート番号。|8391|
|SSLCertThumbprint|Scale Out Worker との通信の保護に利用される SSL 証明書のサムプリント。|Scale Out Master のインストール時に指定される SSL 証明書のサムプリント|
|SqlServerName|SSISDB カタログが含まれている [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] の名前。 たとえば、ServerName\\InstanceName です。|Scale Out Master と共にインストールされる SQL Server の名前。|
|CleanupCompletedJobsIntervalInMs|完了した実行ジョブを消去する間隔 (ミリ秒単位)。|43200000|
|DealWithExpiredTasksIntervalInMs|期限切れ実行ジョブを処理する間隔 (ミリ秒単位)。|300000|
|MasterHeartbeatIntervalInMs|Scale Out Master ハートビートの間隔 (ミリ秒単位)。 このプロパティでは、Scale Out Master が SSISDB カタログでのそのオンライン ステータスを更新する間隔が指定されます。|30000|
|SqlConnectionTimeoutInSecs|SSISDB に接続するときの SQL 接続のタイムアウト (秒)。|15|
||||    

## <a name="view-the-scale-out-master-service-log"></a>Scale Out Master サービス ログを表示する

Scale Out Master サービス ログ ファイルは `<drive>:\Users\[account]\AppData\Local\SSIS\ScaleOut\Master` フォルダーにあります。 

*[account]* パラメーターは、Scale Out Master サービスを実行するアカウントです。 既定では、このアカウントは `SSISScaleOutMaster140` です。

## <a name="next-steps"></a>次の手順

[Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)
