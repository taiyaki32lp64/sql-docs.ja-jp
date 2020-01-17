---
title: catalog.set_execution_parameter_value (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 055d86c9-befd-4e63-acb1-6dfe833549d2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f75065f38d47964ab3bbc07f22bb809061fb22d4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295309"
---
# <a name="catalogset_execution_parameter_value-ssisdb-database"></a>catalog.set_execution_parameter_value (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの実行のインスタンスにパラメーターの値を設定します。  
  
 実行インスタンス開始後は、パラメーターの値は変更できません。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.set_execution_parameter_value [ @execution_id = execution_id  
    , [ @object_type = ] object_type  
    , [ @parameter_name = ] parameter_name  
    , [ @parameter_value = ] parameter_value  
```  
  
## <a name="arguments"></a>引数  
 [ @execution_id = ] *execution_id*  
 実行のインスタンスの一意の識別子。 *execution_id* は **bigint** です。  
  
 [ @object_type = ] *object_type*  
 パラメーターの型。  
  
 次のパラメーターでは、*object_type* を 50 に指定します。  
  
-   LOGGING_LEVEL  
  
-   CUSTOMIZED_LOGGING_LEVEL  
  
-   DUMP_ON_ERROR  
  
-   DUMP_ON_EVENT  
  
-   DUMP_EVENT_CODE  
  
-   CALLER_INFO  
  
-   SYNCHRONIZED  
  
 値 `20` を使用するとプロジェクトのパラメーターを示し、値 `30` を使用するとパッケージのパラメーターを示します。  
  
 *object_type* は **smallint** です。  
  
 [ @parameter_name = ] *parameter_name*  
 パラメーターの名前。 *parameter_name* は **nvarchar(128)** です。  
  
 [ @parameter_value = ] *parameter_value*  
 パラメーターの値。 *parameter_value* は **sql_variant** です。  
  
## <a name="remarks"></a>Remarks  
 特定の実行に使用されたパラメーター値を調べるには、catalog.execution_parameter_values ビューに対してクエリを実行します。  
  
 パッケージの実行中にログに記録される情報のスコープを指定するには、*parameter_name* を LOGGING_LEVEL に設定して、*parameter_value* を次のいずれかの値に設定します。  
  
 *object_type* パラメーターを 50 に設定します。  
  
|[値]|Description|  
|-----------|-----------------|  
|0|なし<br /><br /> ログ記録をオフにします。 パッケージの実行状態のみがログに記録されます。|  
|1|Basic<br /><br /> カスタム イベントと診断イベントを除く、すべてのイベントをログに記録します。 これが既定値です。|  
|2|パフォーマンス<br /><br /> パフォーマンス統計、および OnError イベントと OnWarning のイベントのみをログに記録します。|  
|3|"詳細"<br /><br /> カスタム イベントと診断イベントを含む、すべてのイベントをログに記録されます。 <br />カスタム イベントには、Integration Services タスクによってログに記録されるイベントを含みます。 詳細については、「[ログ記録用のカスタム メッセージ](../../integration-services/performance/integration-services-ssis-logging.md#custom_messages)」を参照してください。|  
|4|ランタイムの系列<br /><br /> データ フロー内の系列を追跡するために必要なデータを収集します。|  
|100|カスタムのログ記録レベル<br /><br /> CUSTOMIZED_LOGGING_LEVEL パラメーターの設定を指定します。 指定できる値の詳細については、「[catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md)」を参照してください。<br /><br /> カスタマイズされたログ記録レベルの詳細については、「[SSIS サーバーでのパッケージ実行のログ記録を有効にする](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)」を参照してください。|  
  
 パッケージの実行中にエラーが発生した場合に、Integration Services サーバーによりダンプ ファイルが生成されるように指定するには、未実行の実行インスタンスに次のパラメーター値を設定します。  
  
|パラメーター|[値]|  
|---------------|-----------|  
|*execution_id*|実行のインスタンスの一意識別子|  
|*object_type*|50|  
|*parameter_name*|'DUMP_ON_ERROR|  
|*parameter_value*|1|  
  
 パッケージの実行中にイベントが発生した場合に、Integration Services サーバーによりダンプ ファイルを生成されるように指定するには、未実行の実行インスタンスに次のパラメーター値を設定します。  
  
|パラメーター|[値]|  
|---------------|-----------|  
|*execution_id*|実行のインスタンスの一意識別子|  
|*object_type*|50|  
|*parameter_name*|'DUMP_ON_EVENT|  
|*parameter_value*|1|  
  
 パッケージの実行中に、Integration Services サーバーによるダンプ ファイルの生成が行われる原因となるイベントを指定するには、未実行の実行インスタンスに次のパラメーター値を設定します。 複数のイベント コードは、セミコロンで区切ります。  
  
|パラメーター|[値]|  
|---------------|-----------|  
|*execution_id*|実行のインスタンスの一意識別子|  
|*object_type*|50|  
|*parameter_name*|DUMP_EVENT_CODE|  
|*parameter_value*|1 つまたは複数のイベント コード|  
  
## <a name="example"></a>例  
 次の例では、パッケージの実行中にエラーが発生した場合に、Integration Services サーバーによりダンプ ファイルが生成されるように指定しています。  
  
```sql
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_ERROR',1  
```  
  
## <a name="example"></a>例  
 次の例では、パッケージの実行中にイベントが発生した場合に、Integration Services サーバーによりダンプ ファイルが生成されるように指定し、サーバーによるファイルの生成が行われる原因となるイベントを指定しています。  
  
```sql
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_EVENT',1  
  
declare @event_code nvarchar(50)  
set @event_code = '0xC020801C'  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_EVENT_CODE', @event_code  
```  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの READ および MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   ユーザーに適切な権限がない  
  
-   実行識別子が有効ではない  
  
-   パラメーター名が無効  
  
-   パラメーター値のデータ型が、パラメーターのデータ型と一致しない  
  
## <a name="see-also"></a>参照  
 [catalog.execution_parameter_values &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)   
 [パッケージ実行用のダンプ ファイルを生成する](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
