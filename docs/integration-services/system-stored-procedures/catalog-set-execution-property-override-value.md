---
title: catalog.set_execution_property_override_value | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a8e85c35552a8bcbf4190bd3ce36b4a65be96789
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295303"
---
# <a name="catalogset_execution_property_override_value"></a>catalog.set_execution_property_override_value 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの実行のインスタンスにプロパティの値を設定します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.set_execution_property_override_value [ @execution_id = execution_id  
    , [ @property_path = ] property_path  
    , [ @property_value = ] property_value  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>引数  
 [ @execution_id = ] *execution_id*  
 実行のインスタンスの一意の識別子。 *execution_id* は **bigint** です。  
  
 [ @property_path = ] *property_path*  
 パッケージ内のプロパティのパス。 *property_path* は **nvarchar(4000)** です。  
  
 [ @property_value = ] *property_value*  
 プロパティに割り当てるオーバーライド値。 *property_value* は **nvarchar(max)** です。  
  
 [ @sensitive = ] *sensitive*  
 値が 1 のとき、プロパティはセンシティブで、格納されるときに暗号化されます。 値が 0 のとき、プロパティはセンシティブではなく、値はプレーンテキストで格納されます。 *sensitive* 引数は **bit** です。  
  
## <a name="remarks"></a>Remarks  
 このプロシージャは、 **[パッケージの実行]** ダイアログの **[詳細設定]** タブの **[プロパティのオーバーライド]** セクションと同じ機能を実行します。 プロパティのパスは、パッケージ タスクの **[パッケージのパス]** プロパティから取得されます。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   ユーザーに適切な権限がない  
  
-   実行識別子が有効ではない  
  
-   プロパティ パスが無効  
  
-   プロパティ値のデータ型が、プロパティのデータ型と一致しない  
  
## <a name="see-also"></a>参照  
 [catalog.set_execution_parameter_value &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
  
