---
title: catalog.grant_permission (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- grant_permission stored procedure [Integration Services]
- catalog.grant_permission stored procedure [Integration Services]
ms.assetid: e72cfd52-de66-45e9-98b9-b8580ac7b956
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9053a5ab4ac64bea8104ce7d9079bf891ffa887a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296771"
---
# <a name="cataloggrant_permission-ssisdb-database"></a>catalog.grant_permission (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのセキュリティ保護可能なオブジェクトに対するアクセス許可を許可します。  
  
## <a name="syntax"></a>構文  
  
```sql
catalog.grant_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>引数  
 [ @object_type = ] *object_type*  
 セキュリティ保護可能なオブジェクトの種類。 セキュリティ保護可能なオブジェクトの種類には、フォルダー (`1`)、プロジェクト (`2`)、環境 (`3`)、操作 (`4`) があります。*object_type* は **smallint** _です。_  
  
 [ @object_id = ] *object_id*  
 セキュリティ保護可能なオブジェクトの一意識別子 (ID)。 *object_id* は **bigint** です。  
  
 [ @principal_id = ] *principal_id*  
 権限を許可するプリンシパルの ID。 *principal_id* は **int** です。  
  
 [ @permission_type = ] *permission_type*  
 許可されるプリンシパルの種類。 *permission_type* は **smallint** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0 を返します。  
  
 1 (object_class が有効な)  
  
 2 (object_id が存在しない)  
  
 3 (プリンシパルが存在しない)  
  
 4 (アクセス許可が有効な)  
  
 5 (その他のエラー)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   オブジェクトに対する ASSIGN_PERMISSIONS 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  

この手順は、SQL Server で認証されたログインで呼び出すことはできません。 sa ログインから呼び出すことはできません。
  
## <a name="remarks"></a>Remarks  
 このストアド プロシージャを使用すると、次の表に記載されている権限の種類を許可できます。  
  
|permission_type 値|権限名|権限の説明|該当するオブジェクトの種類|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|プロパティなど、オブジェクトの一部と見なされる情報をプリンシパルが読み取ることができるようにします。 プリンシパルがオブジェクト内に含まれるその他のオブジェクトのコンテンツを列挙したり、読み取ったりすることはできません。|フォルダー、プロジェクト、環境、操作|  
|`2`|MODIFY|プロパティなど、オブジェクトの一部と見なされる情報をプリンシパルが変更できるようにします。 プリンシパルがオブジェクト内に含まれるその他のオブジェクトを修正することはできません。|フォルダー、プロジェクト、環境、操作|  
|`3`|EXECUTE|プリンシパルがプロジェクトのすべてのパッケージを実行できるようにします。|プロジェクト|  
|`4`|MANAGE_PERMISSIONS|プリンシパルがオブジェクトに権限を割り当てることができるようにします。|フォルダー、プロジェクト、環境、操作|  
|`100`|CREATE_OBJECTS|プリンシパルがフォルダーでオブジェクトを作成できるようにします。|フォルダー|  
|`101`|READ_OBJECTS|プリンシパルがフォルダーのすべてのオブジェクトを読み取ることができるようにします。|フォルダー|  
|`102`|MODIFY_OBJECTS|プリンシパルがフォルダーのすべてのオブジェクトを変更できるようにします。|フォルダー|  
|`103`|EXECUTE_OBJECTS|プリンシパルがフォルダーのすべてのプロジェクトからすべてのパッケージを実行できるようにします。|フォルダー|  
|`104`|MANAGE_OBJECT_PERMISSIONS|プリンシパルがフォルダー内のすべてのオブジェクトに対する権限を管理できるようにします。|フォルダー|  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 関連するエラーとメッセージについては、「リターン コードの値」を参照してください。  
  
  
