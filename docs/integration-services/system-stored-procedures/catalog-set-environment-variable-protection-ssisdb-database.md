---
title: catalog.set_environment_variable_protection (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 005b6b2f-a5d9-4ea4-8d4e-beed6ab33c0d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc67461545e7a1585e5f45eb35c52a5630248391
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295319"
---
# <a name="catalogset_environment_variable_protection-ssisdb-database"></a>catalog.set_environment_variable_protection (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの環境変数のセンシティビティ ビットを設定します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.set_environment_variable_protection [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable_name  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>引数  
 [ @folder_name = ] *folder_name*  
 環境を含むフォルダーの名前です。 *folder_name* は **nvarchar(128)** です。  
  
 [ @environment_name = ] *environment_name*  
 環境の名前。 *Environment_name* は **nvarchar(128)** です。  
  
 [ @variable_name = ] *variable_name*  
 環境変数の名前。 *variable_name* は **nvarchar(128)** です。  
  
 [ @sensitive = ] *sensitive*  
 変数がセンシティブ値を含むかどうかを示します。 値 `1` を使用すると、環境変数の値がセンシティブであることを示し、値 `0` を使用するとセンシティブではないことを示します。 センシティブ値が格納される場合、その値は暗号化されます。 センシティブでない値は、プレーンテキストで格納されます。 *sensitive* パラメーターは **bit** です。  
  
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
  
-   フォルダー名が無効  
  
-   環境名が無効  
  
-   環境変数名が無効  
  
-   ユーザーに適切な権限がない  
  
  
