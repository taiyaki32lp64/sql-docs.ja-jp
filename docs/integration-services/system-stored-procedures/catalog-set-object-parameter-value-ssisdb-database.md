---
title: catalog.set_object_parameter_value (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 36d73a0248be0bd8f9a0873e5ae8445ee68af2e4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295280"
---
# <a name="catalogset_object_parameter_value-ssisdb-database"></a>catalog.set_object_parameter_value (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのパラメーターの値を設定します。 他の値が割り当てられていない場合は、値を環境変数に関連付けるか、または既定で使用されるリテラル値を割り当てます。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.set_object_parameter_value [@object_type =] object_type   
    , [@folder_name =] folder_name   
    , [@project_name =] project_name   
    , [@parameter_name =] parameter_name   
    , [@parameter_value =] parameter_value   
 [  , [@object_name =] object_name ]  
 [  , [@value_type =] value_type ]  
```  
  
## <a name="arguments"></a>引数  
 [@object_type =] *object_type*  
 パラメーターの型。 値 `20` を使用するとプロジェクトのパラメーターを示し、値 `30` を使用するとパッケージのパラメーターを示します。 *object_type* は **smallInt** です。  
  
 [@folder_name =] *folder_name*  
 パラメーターを含むフォルダーの名前。 *folder_name* は **nvarchar(128)** です。  
  
 [@project_name =] *project_name*  
 パラメーターを含むプロジェクトの名前。 *project_name* は **nvarchar(128)** です。  
  
 [@parameter_name =] *parameter_name*  
 パラメーターの名前。 *parameter_name* は **nvarchar(128)** です。  
  
 [@parameter_value =] *parameter_value*  
 パラメーターの値。 *parameter_value* は **sql_variant** です。  
  
 [@object_name =] *object_name*  
 パッケージの名前です。 パラメーターがパッケージ パラメーターである場合に必要な引数です。 *object_name* は **nvarchar (260)** です。  
  
 [@value_type =] *value_type*  
 パラメーター値の型。 文字 `V` を使用すると、*parameter_value* がリテラル値であり、実行前に他の値が割り当てられることのない既定値として使用されることを示します。 文字 `R` を使用すると、*parameter_value* が参照先の値であり、環境変数の名前に設定されたことを示します。 この引数は省略可能です。文字 `V` が既定で使用されます。 *value_type* は **char (1)** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   プロジェクトの READ および MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 ストアド プロシージャがエラーを発生させる可能性がある条件を以下に示します。  
  
-   パラメーターの型が無効  
  
-   プロジェクト名が無効  
  
-   パッケージ パラメーターで、パッケージ名が無効  
  
-   値の型が無効  
  
-   ユーザーに適切な権限がない  
  
## <a name="remarks"></a>Remarks  
  
-   *value_type* が指定されていない場合は、*parameter_value* のリテラル値が既定で使用されます。 リテラル値を使用すると、[object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) ビューの *value_set* が `1` に設定されます。 NULL パラメーター値は許可されません。  
  
-   *value_type* に参照先の値を示す文字 `R` が指定されている場合、*parameter_value* は環境変数の名前を参照します。  
  
-   値 `20` は、プロジェクト パラメーターを示すため *object_type* で使用される場合があります。 この場合、*object_name* の値は不要で、*object_name* に指定された値は無視されます。 この値は、ユーザーがプロジェクトのパラメーターを設定するときに使用されます。  
  
-   値 `30` は、プロジェクト パラメーターを示すため *object_type* で使用される場合があります。 この場合は、対応するパッケージを示すため、*object_name* の値が使用されます。 *object_name* が指定されていない場合、このストアド プロシージャはエラーを返し、終了します。  
  
  
