---
title: catalog.create_environment_variable (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 91ed017b-6567-4bf2-b9f1-e2b5c70a5343
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8f7474200fa8156ab0663540611803276375ad6b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281189"
---
# <a name="catalogcreate_environment_variable-ssisdb-database"></a>catalog.create_environment_variable (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログで環境変数を作成します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.create_environment_variable [@folder_name =] folder_name  
    , [@environment_name =] environment_name  
    , [@variable_name =] variable_name  
    , [@data_type =] data_type  
    , [@sensitive =] sensitive  
    , [@value =] value  
    , [@description =] description  
```  
  
## <a name="arguments"></a>引数  
 [@folder_name =] *folder_name*  
 環境を含むフォルダーの名前です。 *folder_name* は **nvarchar(128)** です。  
  
 [@environment_name =] *environment_name*  
 環境の名前。 *Environment_name* は **nvarchar(128)** です。  
  
 [@variable_name =] *variable_name*  
 環境変数の名前。 *variable_name* は **nvarchar(128)** です。  
  
 [@data_type =] *data_type*  
 変数のデータ型。 サポートされている環境変数のデータ型は、**Boolean**、**Byte**、**DateTime**、**Double**、**Int16**、**Int32**、**Int64**、**Single**、**String**、**UInt32**、および **UInt64** です。 サポートされていない環境変数のデータ型は **Char**、**DBNull**、**Object**、および **Sbyte** です。 *data_type* パラメーターのデータ型は **nvarchar(128)** です。  
  
 [@sensitive =] *sensitive*  
 変数がセンシティブ値を含むかどうかを示します。 値 `1` を使用すると、環境変数の値がセンシティブであることを示し、値 `0` を使用するとセンシティブではないことを示します。 センシティブ値が格納される場合、その値は暗号化されます。 センシティブでない値は、プレーンテキストで格納されます。*Sensitive* は **bit** です。  
  
 [@value =] *value*  
 環境変数の値。 *value* は **sql_variant** です。  
  
 [@description =] *description*  
 環境変数の説明。 *value* は **nvarchar (1024)** です。  
  
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
  
-   フォルダー名、環境名、または環境変数名が無効  
  
-   変数名が環境に既に存在する  
  
-   ユーザーに適切な権限がない  
  
## <a name="remarks"></a>Remarks  
 パッケージの実行で使用するため、値をプロジェクト パラメーターまたはパッケージ パラメーターに効率的に割り当てるには、環境変数を使用できます。 環境変数は、パラメーター値を編成できるようにします。 変数名は、環境内で一意である必要があります。  
  
 ストアド プロシージャは変数のデータ型を検証して、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログでサポートされることを確認します。  
  
> [!TIP]  
>  サポートされていない **Sbyte** データ型の代わりに、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の **Int16** データ型を使用することを検討してください。  
  
 *value* パラメーターでこのストアド プロシージャに渡された値は、次の表に従って [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型に変換されます。  
  
|Integration Services データ型|SQL Server データ型|  
|------------------------------------|--------------------------|  
|**Boolean**|**bit**|  
|**Byte**|**binary**、**varbinary**|  
|**DateTime**|**datetime**、**datetime2**、**datetimeoffset**、**smalldatetime**|  
|**Double**|真数型: **decimal**、**numeric**。概数値: **float**、**real**|  
|**Int16**|**smallint**|  
|**Int32**|**int**|  
|**Int64**|**bigint**|  
|**Single**|真数型: **decimal**、**numeric**。概数値: **float**、**real**|  
|**String**|**varchar**、**nvarchar**、**char**|  
|**UInt32**|**int** (**int** は、使用可能なマッピングに最も近い **Uint32**)|  
|**UInt64**|**bigint** (**int** は、使用可能なマッピングに最も近い **Uint64**)|  
  
  
