---
title: catalog.configure_catalog (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4e8da4de862bf67a552da61a5d921e7c6c4c51fa
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281347"
---
# <a name="catalogconfigure_catalog-ssisdb-database"></a>catalog.configure_catalog (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  カタログ プロパティを特定の値に設定することによって [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログを構成します。  
  
## <a name="syntax"></a>構文  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>引数  
 [ @property_name = ] *property_name*  
 カタログ プロパティの名前。 *property_name* は **nvarchar (255)** です。 使用可能なプロパティの詳細については、「[catalog.catalog_properties &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)」を参照してください。  
  
 [ @property_value = ] *property_value*  
 カタログ プロパティの値。 *property_value* は **nvarchar (255)** です。 プロパティ値の詳細については、「[catalog.catalog_properties &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>Remarks  
 このストアド プロシージャは、各 *property_name* に対して *property_value* が有効であるかどうかを決定します。  
  
 このストアド プロシージャは、実行が保留中、キュー状態、実行中、一時停止中など、アクティブな実行がない場合にのみ実行できます  
  
 カタログが構成されている間、すべての他のカタログ ストアド プロシージャは、「サーバーは現在構成中です」というエラー メッセージが表示されて失敗します。
  
 カタログが構成されている場合は、エントリが操作ログに書き込まれます。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   プロパティが存在しない  
  
-   プロパティ値が無効  
  
  
