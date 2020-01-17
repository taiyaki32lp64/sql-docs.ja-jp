---
title: catalog.move_environment (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b3fb5242-3c4c-4a87-b3e5-beb22fbab053
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bc0bc77fda49e715879dceec60d616143952c265
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296835"
---
# <a name="catalogmove_environment-ssisdb-database"></a>catalog.move_environment (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  特定のフォルダーの環境を [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログ内の別のフォルダーに移動します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.move_environment [ @source_folder = ] source_folder  
    , [ @environment_name = ] environment_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>引数  
 [ @source_folder = ] *source_folder*  
 環境が移動前に配置されていたソース フォルダーの名前。 *source_folder* は **nvarchar(128)** です。  
  
 [ @environment_name = ] *environment_name*  
 移動される環境の名前。 *Environment_name* は **nvarchar(128)** です。  
  
 [ @destination_folder = ] *destination_folder*  
 環境が移動後に配置される移動先フォルダーの名前。 *destination_folder* は **nvarchar(128)** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   環境の READ および MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   環境が移動元フォルダーに存在しない  
  
-   移動先のフォルダーに同じ名前の環境が既にある  
  
-   ユーザーに適切な権限がない  
  
## <a name="remarks"></a>Remarks  
 プロジェクトの環境参照は、移動中、環境に従って更新されません。 したがって、環境参照を更新する必要があります。 このストアド プロシージャ は、環境を移動することで環境参照が壊れた場合でも成功します。 環境参照は、このストアド プロシージャが完了した後で更新する必要があります。  
  
> [!NOTE]  
>  プロジェクトでは、相対または絶対環境参照を使用できます。 相対参照の場合、名前によって環境を参照します。この環境はプロジェクトと同じフォルダーに格納されている必要があります。 絶対参照の場合、名前とフォルダーによって環境を参照します。これらの参照は、プロジェクトとは異なるフォルダーに格納されている環境を参照する場合があります。  
  
  
