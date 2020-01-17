---
title: catalog.create_environment (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 66367092-9f6e-40e6-90bd-81efb078ab70
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 77fea02dc933b63fff97b359673ab702e63f50ea
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295561"
---
# <a name="catalogcreate_environment-ssisdb-database"></a>catalog.create_environment (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログで環境を作成します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.create_environment [@folder_name =] folder_name  
     , [@environment_name =] environment_name  
  [  , [@environment_description =] environment_description ]  
```  
  
## <a name="arguments"></a>引数  
 [@folder_name =] *folder_name*  
 環境を含むフォルダーの名前。 *folder_name* は **nvarchar(128)** です。  
  
 [@environment_name =] *environment_name*  
 環境の名前。 *Environment_name* は **nvarchar(128)** です。  
  
 [@environment_description=] *environment_description*  
 省略可能な環境の説明。 *environment_description* は **nvarchar(1024)** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   フォルダーの READ および MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   データベース ロール (database role)  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   フォルダー名が見つからない  
  
-   指定したフォルダーには、同じ名前を持つ環境が既に存在する  
  
## <a name="remarks"></a>Remarks  
 環境名は、フォルダー内で一意になる必要があります。  
  
  
