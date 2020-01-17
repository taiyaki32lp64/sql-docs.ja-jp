---
title: catalog.create_execution (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8076434e550f27ac292eec1b7385fce93d60e3ec
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295557"
---
# <a name="catalogcreate_execution-ssisdb-database"></a>catalog.create_execution (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの実行のインスタンスを作成します。  
  
 このストアド プロシージャは既定のサーバーのログ レベルを使用します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.create_execution [@folder_name = folder_name  
     , [@project_name =] project_name  
     , [@package_name =] package_name  
  [  , [@reference_id =] reference_id ]  
  [  , [@use32bitruntime =] use32bitruntime ] 
  [  , [@runinscaleout =] runinscaleout ]
  [  , [@useanyworker =] useanyworker ] 
     , [@execution_id =] execution_id OUTPUT  
```  
  
## <a name="arguments"></a>引数  
 [@folder_name =] *folder_name*  
 実行するパッケージが格納されているフォルダーの名前。 *folder_name* は **nvarchar(128)** です。  
  
 [@project_name =] *project_name*  
 実行するパッケージが格納されているプロジェクトの名前。 *project_name* は **nvarchar(128)** です。  
  
 [@package_name =] *package_name*  
 実行するパッケージの名前。 *package_name* は **nvarchar (260)** です。  
  
 [@reference_id =] *reference_id*  
 環境参照の一意識別子。 このパラメーターはオプションです。 *reference_id* は **bigint** です。  
  
 [@use32bitruntime =] *use32bitruntime*  
 64 ビット オペレーティング システムで 32 ビットのランタイムを使用してパッケージを実行すべきかどうかを示します。 値 1 を使用すると、64 ビット オペレーティング システムで実行しているときに、32 ビット ランタイムでパッケージを実行します。 値 0 を使用すると、64 ビット オペレーティング システムで実行しているときに、64 ビット ランタイムでパッケージを実行します。 このパラメーターはオプションです。 *Use32bitruntime* は **bit** です。  
 
 [@runinscaleout =] *runinscaleout*  
 実行が Scale Out であるかどうかを示します。パッケージを Scale Out で実行するには、値 1 を使用します。Scale Out を使用せずにパッケージを実行するには、値 0 を使用します。このパラメーターはオプションです。 指定しない場合、その値は [SSISDB].[catalog].[catalog_properties] で DEFAULT_EXECUTION_MODE に設定されます。 *runinscaleout* は **bit** です。 
 
[@useanyworker =] *useanyworker*  
任意の Scale Out Worker の実行が許可されるかどうかを示します。

-   任意の Scale Out Worker を使用してパッケージを実行するには、値 1 を使用します。 `@useanyworker` を True に設定すると、(Worker 構成ファイルに指定されている) 最大タスク数に到達していない Worker でパッケージを実行できます。 Worker 構成ファイルについては、「[Integration Services (SSIS) Scale Out Worker](../scale-out/integration-services-ssis-scale-out-worker.md)」を参照してください。

-   すべての Scale Out Worker にパッケージの実行を許可しないことを示すには、値 0 を使用します。 `@useanyworker` を False に設定すると、Scale Out Manager を使用するか、ストアド プロシージャ `[catalog].[add_execution_worker]` を呼び出し、パッケージの実行が許可される Worker を指定する必要があります。 別のパッケージを既に実行している Worker を指定した場合、その Worker は現在のパッケージの実行を完了してから別の実行を要求します。

このパラメーターはオプションです。 指定しない場合、その値は 1 に設定されます。 *useanyworker* は **bit** です。 
  
 [@execution_id =] *execution_id*  
 実行のインスタンスの一意識別子を返します。 *execution_id* は **bigint** です。  

  
## <a name="remarks"></a>Remarks  
 実行は、パッケージの実行の 1 つのインスタンス中にパッケージによって使用されるパラメーター値を指定するために使用されます。  
  
 環境参照を指定した場合、*reference_id* パラメーター、ストアド プロシージャは、プロジェクトおよびパッケージ パラメーターをリテラル値や対応する環境変数から参照される値を設定します。 環境参照が指定されている場合は、パッケージの実行中、既定のパラメーター値が使用されます。 特定の実行のインスタンスに使用される値を正確に判断するには、このストアド プロシージャからの *execution_id* 出力パラメーター値を使用して、[execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) ビューをクエリします。  
  
 実行で指定できるのは、エントリ ポイントのパッケージとしてマークされたパッケージのみです。 エントリ ポイントではないパッケージを指定すると、実行が失敗します。  
  
## <a name="example"></a>例  
 次の例では catalog.create_execution を呼び出して、Scale Out ではない、Child1.dtsx パッケージの実行のインスタンスを作成します。integration Services Project1 にはパッケージが含まれています。 例では catalog.set_execution_parameter_value を呼び出して、Parameter1、Parameter2、LOGGING_LEVEL の各パラメーターの値を設定します。 例では catalog.start_execution を呼び出して、実行のインスタンスを起動します。  
  
```sql  
Declare @execution_id bigint  
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Child1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'TestDeply4', @project_name=N'Integration Services Project1', @use32bitruntime=False, @reference_id=Null  
Select @execution_id  
DECLARE @var0 sql_variant = N'Child1.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter1', @parameter_value=@var0  
DECLARE @var1 sql_variant = N'Child2.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter2', @parameter_value=@var1  
DECLARE @var2 smallint = 1  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var2  
EXEC [SSISDB].[catalog].[start_execution] @execution_id  
GO  
```  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   プロジェクトの READ および EXECUTE 実行権限と、該当する場合は、参照先の環境での READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  

 @runinscaleout が 1 の場合、ストアド プロシージャには、次のアクセス許可のいずれかが必要です。
 
-   **ssis_admin** データベース ロールのメンバーシップ

-   **ssis_cluster_executor** データベース ロールのメンバーシップ

-   **sysadmin** サーバー ロールのメンバーシップ
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   パッケージが存在しない。  
  
-   ユーザーに適切なアクセス許可がない。  
  
-   環境参照 *reference_id* が無効である。  
  
-   指定したパッケージが、エントリ ポイントのパッケージではない。  
  
-   参照先の環境変数のデータ型が、プロジェクトまたはパッケージ パラメーターのデータ型と異なる。  
  
-   プロジェクトまたはパッケージに、値が必要なパラメーターが含まれているが、値が割り当てられていない。  
  
-   参照先の環境変数が、環境参照 *reference_id* が指定する環境に見つかりません。  
  
## <a name="see-also"></a>参照  
 [catalog.start_execution &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [catalog.add_execution_worker &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  
