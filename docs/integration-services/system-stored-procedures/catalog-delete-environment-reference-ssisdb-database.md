---
title: catalog.delete_environment_reference (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 1f68f157-c4e9-412c-92b3-53a2faaba29b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c345f8e1c797e864813b1b1fa0feb0a9cd028821
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47661480"
---
# <a name="catalogdeleteenvironmentreference-ssisdb-database"></a>catalog.delete_environment_reference (SSISDB データベース)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  環境参照を [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトから削除します。  
  
## <a name="syntax"></a>構文  
  
```sql  
delete_environment_reference [ @reference_id = ] reference_id  
```  
  
## <a name="arguments"></a>引数  
 [ @reference_id = ] *reference_id*  
 環境参照の一意識別子。 *reference_id* は **bigint** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   プロジェクトの MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   環境参照識別子が有効ではない  
  
-   ユーザーに適切な権限がない  
  
  
