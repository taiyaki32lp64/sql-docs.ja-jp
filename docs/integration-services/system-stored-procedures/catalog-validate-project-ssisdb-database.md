---
title: catalog.validate_project (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 5270689a-46d4-4847-b41f-3bed1899e955
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 618499b25914ea4f521fa694ac14b9e9049ca330
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296696"
---
# <a name="catalogvalidate_project-ssisdb-database"></a>catalog.validate_project (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトを非同期的に検証します。  
  
## <a name="syntax"></a>構文  
  
```sql
catalog.validate_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @validate_type = ] validate_type  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @environment_scope = ] environment_scope ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>引数  
 [ @folder_name = ] *folder_name*  
 プロジェクトを含むフォルダーの名前。 *folder_name* は **nvarchar(128)** です。  
  
 [ @project_name = ] *project_name*  
 プロジェクトの名前。 *project_name* は **nvarchar(128)** です。  
  
 [ @validate_type = ] *validate_type*  
 実行する検証の種類を示します。 文字 `F` を使用すると、完全な検証を実行します。 このパラメーターは省略可能です。文字 `F` が既定で使用されます。 *validate_type* は **char (1)** です。  
  
 [ @validation_id = ] *validation_id*  
 検証の一意識別子 (ID) を返します。 *validation_id* は **bigint** です。  
  
 [ @use32bitruntime = ] *use32bitruntime*  
 64 ビット オペレーティング システムで 32 ビットのランタイムを使用してパッケージを実行すべきかどうかを示します。 値 `1` を使用して 64 ビットのオペレーティング システムで実行されているときに、32 ビット ランタイムを使用してパッケージを実行します。 値 `0` を使用すると、64 ビット オペレーティング システムで実行しているときに、64 ビット ランタイムでパッケージが実行されます。 このパラメーターはオプションです。 *use32bitruntime* は **bit** です。  
  
 [ @environment_scope = ] *environment_scope*  
 検証が考慮する環境参照を示します。 値が `A` の場合は、プロジェクトに関連するすべての環境参照が検証に含まれます。 値が `S` の場合は、1 つの環境参照のみが含まれます。 値が `D` の場合、環境参照は含まれず、各パラメーターには、検証に合格するため、既定のリテラル値を指定する必要があります。 このパラメーターは省略可能です。文字 `D` が既定で使用されます。 *environment_scope* は **char(1)** です。  
  
 [ @reference_id = ] *reference_id*  
 環境参照の一意の ID。 このパラメーターは、検証に 1 つの環境参照が含まれていて、*environment_scope* が `S` の場合にのみ必要です。 *reference_id* は **bigint** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 検証手順の出力は、結果セットの異なるセクションとして返されます。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   プロジェクトの READ 権限と、該当する場合は、参照先の環境での READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   プロジェクト内の 1 つまたは複数のパッケージの検証の失敗  
  
-   検証に含まれる 1 つまたは複数の参照先の環境が、参照先の変数を含まない場合の検証の失敗  
  
-   指定した検証の種類が無効  
  
-   プロジェクト名または環境参照の ID が無効  
  
-   ユーザーに適切な権限がない  
  
## <a name="remarks"></a>Remarks  
 検証では、プロジェクトのパッケージが正常に実行されない問題を特定することができます。 検証の状態を監視するには、[catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) または [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) ビューを使用します。  
  
 検証で使用できるのは、ユーザーがアクセスできる環境のみです。 検証の出力は結果セットとしてクライアントに送信されます。  
  
 このリリースでは、プロジェクトの検証は、依存関係の検証をサポートしていません。  
  
 完全な検証では、すべての参照先の環境変数が、検証に含まれていたすべての参照先の環境内で見つかることを確認します。 完全な検証結果では、検証に含まれていた参照先の環境で見つからなかった、有効な参照先の環境変数ではない環境参照を一覧表示します。  
  
  
