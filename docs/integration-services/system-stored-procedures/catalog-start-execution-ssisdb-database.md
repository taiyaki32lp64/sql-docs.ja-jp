---
title: catalog.start_execution (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 341d48d35404cd8d18c3f1474693305b7fadb3cf
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296720"
---
# <a name="catalogstart_execution-ssisdb-database"></a>catalog.start_execution (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの実行のインスタンスを起動します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.start_execution [@execution_id =] execution_id [, [@retry_count =] retry_count]  
```  
  
## <a name="arguments"></a>引数  
 [@execution_id =] *execution_id*  
 実行のインスタンスの一意の識別子。 *execution_id* は **bigint** です。
 
 [@retry_count =] *retry_count*  
 実行に失敗した場合の再試行回数。 実行が Scale Out である場合にのみ有効になります。このパラメーターはオプションです。 指定しない場合、その値は 0 に設定されます。 *retry_count* は **int** です。
  
## <a name="remarks"></a>Remarks  
 実行は、パッケージの実行の 1 つのインスタンス中にパッケージによって使用されるパラメーター値を指定するために使用されます。 実行のインスタンスが作成された後、インスタンスが起動する前に、対応するプロジェクトが再配置される場合があります。 この場合、実行のインスタンスは古いプロジェクトを参照します。 この無効な参照により、ストアド プロシージャが失敗します。  
  
> [!NOTE]  
>  実行を起動できるのは 1 回のみです。 実行のインスタンスを起動するには、それが作成された状態である必要があります ([catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) ビューの **status** 列の値が `1`)。  
  
## <a name="example"></a>例  
 次の例では catalog.create_execution を呼び出して、Child1.dtsx パッケージの実行のインスタンスを作成します。 integration Services Project1 にはパッケージが含まれています。 例では catalog.set_execution_parameter_value を呼び出して、Parameter1、Parameter2、LOGGING_LEVEL の各パラメーターの値を設定します。 例では catalog.start_execution を呼び出して、実行のインスタンスを起動します。  
  
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
  
-   実行のインスタンスの READ および MODIFY 権限、プロジェクトの READ および EXECUTE 権限、参照先の環境の READ 権限 (該当する場合)。  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   ユーザーに適切な権限がない  
  
-   実行識別子が有効ではない  
  
-   実行は既に開始されている、または既に完了している (実行は 1 回しか起動できない)  
  
-   プロジェクトに関連する環境参照が有効ではない  
  
-   必要なパラメーターが設定されていない  
  
-   実行のインスタンスに関連付けられているプロジェクトのバージョンが古い (実行できるのはプロジェクトの最新バージョンのみ)  
  
  
