---
title: catalog.rename_environment (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: c73d7452-31c5-4f4e-afcc-e9eca760c826
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 532513a6d8c62cb1f1f36e6dc2c8b83a7c96089b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295396"
---
# <a name="catalogrename_environment-ssisdb-database"></a>catalog.rename_environment (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの環境の名前を変更します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.rename_environment [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @new_environment_name= ] new_environment_name  
```  
  
## <a name="arguments"></a>引数  
 [ @folder_name = ] *folder_name*  
 環境を含むフォルダーの名前です。 *folder_name* は **nvarchar(128)** です。  
  
 [ @environment_name = ] *environment_name*  
 環境の元の名前。 *Environment_name* は **nvarchar(128)** です。  
  
 [ @new_environment_name = ] *new_environment_name*  
 環境の新しい名前。 *new_environment_name* は **nvarchar(128)** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   環境の MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   元の環境名が無効  
  
-   新しい名前が既存の環境で既に使用されている  
  
## <a name="remarks"></a>Remarks  
 環境の名前を変更しても、プロジェクトの環境参照は自動的に更新されません。 したがって、環境参照を更新する必要があります。 このストアド プロシージャ は、環境名を変更することで環境参照が壊れた場合でも成功します。 環境参照は、このストアド プロシージャが完了した後で更新する必要があります。  
  
> [!NOTE]  
>  環境参照が有効でない場合、これらの参照を使用する対応するパッケージの検証および実行が失敗します。  
  
  
