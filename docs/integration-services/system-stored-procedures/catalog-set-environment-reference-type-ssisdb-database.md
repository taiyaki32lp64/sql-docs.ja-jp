---
title: catalog.set_environment_reference_type (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b79e3a06-22c0-40e5-8933-1b3414db3329
author: chugugrace
ms.author: chugu
ms.openlocfilehash: de1e0cddcee34685e5921b7cc31837a301f44166
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295337"
---
# <a name="catalogset_environment_reference_type-ssisdb-database"></a>catalog.set_environment_reference_type (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトの既存の環境参照に関連付けられている参照の種類と環境名を設定します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.set_environment_reference_location [ @reference_id = reference_id  
    , [ @reference_type = ] reference_type  
 [  , [ @environment_folder_name = ] environment_folder_name ]  
```  
  
## <a name="arguments"></a>引数  
 [ @reference_id = ] *reference_id*  
 更新される環境参照の一意識別子。 *reference_id* は **bigint** です。  
  
 [ @reference_type = ] *reference_type*  
 環境をプロジェクトと同じフォルダーに配置できるか (相対参照)、または別のフォルダーに配置できるか (絶対参照) を示します。 相対参照を指定するには、値 `R` を使用します。 絶対参照を指定するには、値 `A` を使用します。 *reference_type* は **char(1)** です。  
  
 [ @environment_folder_name = ] *environment_folder_name*  
 環境が配置されているフォルダー。 この値は絶対参照にする必要があります。 *environment_folder_name* は **nvarchar(128)** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   プロジェクトに対する READ および MODIFY 権限、および環境に対する READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   フォルダー名、環境名、または参照 ID が有効ではない  
  
-   ユーザーに適切な権限がない  
  
-   *reference_location* パラメーターの `A` 文字を使用して絶対参照が指定されているが、フォルダー名は *environment_folder_name* パラメーターで指定されなかった。  
  
## <a name="remarks"></a>Remarks  
 プロジェクトでは、相対または絶対環境参照を使用できます。 相対参照は、名前によって環境を参照し、プロジェクトと同じフォルダーに格納されている必要があります。 絶対参照の場合、名前とフォルダーによって環境を参照します。プロジェクトとは異なるフォルダーに格納されている環境を参照する場合があります。 プロジェクトでは複数の環境を参照できます。  
  
> [!IMPORTANT]  
>  相対参照が指定されている場合、*environment_folder_name* パラメーター値は使用されず、環境フォルダー名が自動的に **NULL** に設定されます。 絶対参照が指定されている場合、フォルダー名は *environment_folder_name* パラメーターで指定する必要があります。  
  
  
