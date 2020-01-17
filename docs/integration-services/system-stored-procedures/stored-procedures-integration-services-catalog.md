---
title: ストアド プロシージャ (Integration Services カタログ) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- stored procedures [Integration Services]
ms.assetid: a6ccd884-108f-4fb6-95ad-00b9cb65d5d6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e1eea2f9e83069b18b47b1563e60a0c31c0bfcb0
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296687"
---
# <a name="stored-procedures-integration-services-catalog"></a>ストアド プロシージャ (Integration Services カタログ)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  このセクションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに配置されている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを管理できる [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャについて説明します。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ストアド プロシージャを呼び出して、**SSISDB** カタログに格納されているオブジェクトを追加、削除、変更、または実行します。  
  
 カタログの既定の名前は、SSISDB です。 カタログに格納されているオブジェクトには、プロジェクト、パッケージ、パラメーター、環境、操作履歴があります。  
  
 データベース ビューとストアド プロシージャを直接使用することも、マネージド API を呼び出すカスタム コードを記述することもできます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] およびマネージド API では、ビューに対してクエリを実行し、多くのタスクを実行するストアド プロシージャ (このセクションで説明) を呼び出します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
 パッケージ データ フロー内のコンポーネントの出力で、データ タップを追加します。  
  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
 パッケージ データ フロー内の特定のデータ フロー パスにデータ タップを追加します。  
  
 [catalog.check_schema_version](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)  
 SSISDB カタログ スキーマと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] バイナリ (ISServerExec および SQLCLR アセンブリ) に互換性があるかどうかを示します。  
  
 [catalog.clear_object_parameter_value &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)  
 サーバーに格納されている既存の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトまたはパッケージのパラメーターの値をクリアします。  
  
 [catalog.configure_catalog &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)  
 カタログ プロパティを特定の値に設定することによって [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログを構成します。  
  
 [catalog.create_environment &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログで環境を作成します。  
  
 [catalog.create_environment_reference &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトに環境参照を作成します。  
  
 [catalog.create_environment_variable &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログで環境変数を作成します。  
  
 [catalog.create_execution &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの実行のインスタンスを作成します。  
  
 [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
 実行中のパッケージを一時停止させ、ダンプ ファイルを作成します。  
  
 [catalog.create_folder &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのフォルダーを作成します。  
  
 [catalog.delete_environment &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのフォルダーから環境を削除します。  
  
 [catalog.delete_environment_reference &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
 環境参照を [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトから削除します。  
  
 [catalog.delete_environment_variable &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの環境から環境変数を削除します。  
  
 [catalog.delete_folder &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログからフォルダーを削除します。  
  
 [catalog.delete_project &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのフォルダーから既存のプロジェクトを削除します。  
  
 [catalog.deny_permission &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのセキュリティ保護可能なオブジェクトに対する権限を拒否します。  
  
 [catalog.deploy_project &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのフォルダーにプロジェクトを配置するか、以前に配置した既存のプロジェクトを更新します。  
  
 [catalog.get_parameter_values &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトおよび対応するパッケージの既定のパラメーター値を解決し、取得します。  
  
 [catalog.get_project &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの既存のプロジェクトのプロパティを取得します。  
  
 [catalog.grant_permission &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのセキュリティ保護可能なオブジェクトに対するアクセス許可を許可します。  
  
 [catalog.move_environment &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
 特定のフォルダーの環境を [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログ内の別のフォルダーに移動します。  
  
 [catalog.move_project &#40;&#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-move-project-ssisdb-database.md)  
 特定のフォルダーのプロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログ内の別のフォルダーに移動します。  
  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md)  
 実行内のコンポーネント出力からデータ タップを削除します。  
  
 [catalog.rename_environment &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの環境の名前を変更します。  
  
 [catalog.rename_folder &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのフォルダー名を変更します。  
  
 [catalog.restore_project &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトを前のバージョンに復元します。  
  
 [catalog.revoke_permission &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのセキュリティ保護可能なオブジェクトに対するアクセス許可を取り消します。  
  
 [catalog.set_environment_property &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの環境のプロパティを設定します。  
  
 [catalog.set_environment_reference_type &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトの既存の環境参照に関連付けられている参照の種類と環境名を設定します。  
  
 [catalog.set_environment_variable_property &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの環境変数のプロパティを設定します。  
  
 [catalog.set_environment_variable_protection &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの環境変数のセンシティビティ ビットを設定します。  
  
 [catalog.set_environment_variable_value &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの環境変数の値を設定します。  
  
 [catalog.set_execution_parameter_value &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの実行のインスタンスにパラメーターの値を設定します。  
  
 [catalog.set_execution_property_override_value](../../integration-services/system-stored-procedures/catalog-set-execution-property-override-value.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの実行のインスタンスにプロパティの値を設定します。  
  
 [catalog.set_folder_description &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのフォルダーの説明を設定します。  
  
 [catalog.set_object_parameter_value &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのパラメーターの値を設定します。 他の値が割り当てられていない場合は、値を環境変数に関連付けるか、または既定で使用されるリテラル値を割り当てます。  
  
 [catalog.start_execution &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの実行のインスタンスを起動します。  
  
 [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md)  
 SSISDB カタログに対する操作の状態のメンテナンスを実行します。  
  
 [catalog.stop_operation &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの実行の検証またはインスタンスを停止します。  
  
 [catalog.validate_package &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのパッケージを非同期的に検証します。  
  
 [catalog.validate_project &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトを非同期的に検証します。  
  
[catalog.add_execution_worker &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)   
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker を Scale Out 内の実行のインスタンスに追加します。

[catalog.enable_worker_agent &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)   
Scale Out Master でこの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログを操作する場合に Scale Out Worker を有効にします。

[catalog.disable_worker_agent &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)   
Scale Out Master でこの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログを操作する場合に Scale Out Worker を無効にします。


