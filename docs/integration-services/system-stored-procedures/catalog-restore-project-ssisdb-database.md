---
title: catalog.restore_project (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 8adee525-579b-4d2f-b807-e2ecc07fb2e9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d131ebd8d532e0844774fc675165750832f964c9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295457"
---
# <a name="catalogrestore_project-ssisdb-database"></a>catalog.restore_project (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトを前のバージョンに復元します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.restore_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project _name  
    , [ @object_version_lsn = ] object_version_lsn  
  
```  
  
## <a name="arguments"></a>引数  
 [ @folder_name = ] *folder_name*  
 プロジェクトを含むフォルダーの名前。 *folder_name* は **nvarchar(128)** です。  
  
 [ @project _name = ] *project_name*  
 プロジェクトの名前。 *project_name* は **nvarchar(128)** です。  
  
 [ @object_version_lsn = ] *object_version_lsn*  
 プロジェクトのバージョン。 *object_version_lsn* は **bigint** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 *project_name* が見つかった場合、結果セットの一部として、プロジェクトの詳細が **varbinary(MAX)** として返されます。  
  
 指定のフォルダーにプロジェクトを復元できない場合、**NO RESULT SET** が返されます。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   プロジェクトの READ および MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   プロジェクトのバージョンが存在しないか、プロジェクト名と一致しない  
  
-   プロジェクトが存在しない  
  
-   ユーザーに適切な権限がない  
  
## <a name="remarks"></a>Remarks  
 プロジェクトを復元すると、すべてのパラメーターが既定値としてが割り当てられ、すべての環境参照は変更されないままになります。 カタログに保持されるプロジェクト バージョンの最大数は、カタログ プロパティ **MAX_VERSIONS_PER_PROJECT** によって決まります。[catalog_property](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) ビューに表示されます。  
  
> [!WARNING]  
>  プロジェクトの復元後は、環境参照が有効ではなくなる場合があります。  
  
  
