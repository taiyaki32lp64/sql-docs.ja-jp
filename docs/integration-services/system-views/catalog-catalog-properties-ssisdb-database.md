---
title: catalog.catalog_properties (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 12/11/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9b5f7628f0284cb4662f0cf88bff1fd80cb2014e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295229"
---
# <a name="catalogcatalog_properties-ssisdb-database"></a>catalog.catalog_properties (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロパティを表示します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar (256)**|カタログ プロパティの名前。|  
|property_value|**nvarchar (256)**|カタログ プロパティの値。|  
  
## <a name="remarks"></a>Remarks  
 このビューは、各カタログ プロパティの行を表示します。
  
|プロパティ名|[説明]|  
|-------------------|-----------------|  
|**DEFAULT_EXECUTION_MODE**|パッケージのサーバー全体の既定の実行モード - `Server` (0) または `Scale Out` (1)。 |
|**ENCRYPTION_ALGORITHM**|機密データの暗号化に使用される暗号化アルゴリズムの種類。 サポートされている値は、`DES`、`TRIPLE_DES`、`TRIPLE_DES_3KEY`、`DESX`、`AES_128`、`AES_192`、および `AES_256` です。 注:プロパティを変更するには、カタログ データベースがシングル ユーザー モードである必要があります。|
|**IS_SCALEOUT_ENABLED**|値が `True` の場合、SSIS Scale Out 機能が有効になります。 Scale Out を有効にしていない場合、このプロパティがビューに表示されない可能性があります。|
|**MAX_PROJECT_VERSIONS**|1 つのプロジェクトで保持される新しいプロジェクト バージョンの数。 バージョンのクリーンアップを有効にすると、この数を超える以前のバージョンは削除されます。|  
|**OPERATION_CLEANUP_ENABLED**|値が `TRUE` の場合、**RETENTION_WINDOW** (日) より古い操作の詳細および操作のメッセージは、カタログから削除されます。 値が `FALSE` の場合は、すべての操作の詳細と操作のメッセージがカタログに格納されます。 注: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ジョブでは操作のクリーンアップを実行します。|  
|**RETENTION_WINDOW**|操作の詳細と操作のメッセージがカタログに格納される日数。 値が `-1` の場合、リテンション期間は無期限です。 注:クリーンアップが必要ない場合は、**OPERATION_CLEANUP_ENABLED** を **FALSE** に設定します。|
|**SCHEMA_BUILD**|SSISDB カタログ データベース スキーマのビルド番号。 この番号は、SSISDB カタログが作成またはアップグレードされるたびに変わります。|
|**SCHEMA_VERSION**|SSISDB カタログ データベース スキーマのメジャー バージョン番号。 この番号は、SSISDB カタログが作成またはメジャー バージョンがアップグレードされるたびに変わります。|
|**VALIDATION_TIMEOUT**|検証が、このプロパティで指定された秒数で完了しなかった場合、検証は停止します。|  
|**SERVER_CUSTOMIZED_LOGGING_LEVEL**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーの既定のカスタマイズされたログ記録レベル。 カスタマイズされたログ記録レベルを作成していない場合、このプロパティがビューに表示されない可能性があります。|
|**SERVER_LOGGING_LEVEL**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーの既定のログ記録レベル。|
|**SERVER_OPERATION_ENCRYPTION_LEVEL**|値が 1 (`PER_EXECUTION`) の場合、*実行*のたびに証明書と対称キーが作成されます。これらは機密性の高い実行パラメーターと実行ログを保護するために使用されます。 値が 2 (`PER_PROJECT`) の場合、*プロジェクト*ごとに証明書と対称キーが 1 回作成されます。 このプロパティの詳細については、SSIS ストアド プロシージャ [catalog.cleanup_server_log](../system-stored-procedures/catalog-cleanup-server-log.md#remarks) の「解説」を参照してください。|
|**VERSION_CLEANUP_ENABLED**|値が `TRUE` の場合は、プロジェクト バージョンの **MAX_PROJECT_VERSIONS** 番号のみがカタログに格納され、その他のプロジェクト バージョンは削除されます。 値が **FALSE** の場合は、すべてのプロジェクトのバージョンがカタログに格納されます。 注: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ジョブでは操作のクリーンアップを実行します。|
|||
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
  
