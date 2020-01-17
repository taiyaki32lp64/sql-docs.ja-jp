---
title: パーティションおよびロールの配置オプションの指定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- partitions [Analysis Services], deployment options
- Analysis Services deployments, roles
- Analysis Services deployments, partitions
- Analysis Services Deployment Wizard, roles
- Analysis Services Deployment Wizard, partitions
- deploying [Analysis Services], roles
- roles [Analysis Services], deployment options
- deploying [Analysis Services], partitions
- modifying role deployments
- modifying partition deployments
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9b36013f13360a2afcf9546cd1e286b35ae4acd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075352"
---
# <a name="specifying-partition-and-role-deployment-options"></a>パーティションおよびロールの配置オプションの指定
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]展開ウィザードからのパーティションおよびロールの配置オプションを読み取り、 \<*プロジェクト名*> >.deploymentoptions ファイル。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの作成時にこのファイルを作成します。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 使用して、現在のパーティションおよびロールの配置オプション時にプロジェクト、 \<*プロジェクト名*> >.deploymentoptions ファイルを作成します。 構成設定の詳細については、「 [配置スクリプトを作成するための入力ファイルについて](deployment-script-files-input-used-to-create-deployment-script.md)」を参照してください。  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>パーティションおよびロールの配置オプションの確認  
 配置オプション、 \<*プロジェクト名*> >.deploymentoptions ファイルには、次が含まれます。  
  
 **パーティション配置オプション**  
 \<*プロジェクト名*> >.deploymentoptions ファイルは、転送先データベースで既存のパーティションを保持するかどうか、または上書きする (既定) を指定します。 既存のパーティションを保持する場合、新しいパーティションのみが配置され、既存のすべてのメジャー グループのパーティションおよび集計デザインはそのまま残されます。  
  
> [!NOTE]  
>  パーティションが含まれているメジャー グループを削除すると、パーティションも自動的に削除されます。  
  
 **ロール配置オプション**  
 \<*プロジェクト名*> >.deploymentoptions ファイルでは、次のロール配置オプションのいずれかを指定します。  
  
-   配置先データベースの既存のロールおよびロール メンバーは保持され、新しいロールおよびロール メンバーのみが配置されます。  
  
-   配置先データベースの既存のすべてのロールおよびメンバーは、配置するロールおよびメンバーに置き換えられます。  
  
-   配置先データベースの既存のロールおよびロール メンバーは保持され、新しいロールは配置されません。  
  
-   **注** 既存のロールおよびメンバーが保持される場合、これらのロールに関連付けられた権限はリセットされてなくなります。 セキュリティ権限は、オブジェクトが関連付けられているセキュリティ ロールではなく、オブジェクト自体に含まれています。 分析サービスの展開ウィザードを使用してこの動作を操作する方法の詳細についてを参照してください 'ロールの保持とメンバー' では、マイクロソフト サポート技術情報。  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>パーティションおよびロールの配置オプションの変更  
 展開する必要があります、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]プロジェクトに保存されているものの別のパーティションおよびロール オプションを使用して、 \<*プロジェクト名*> >.deploymentoptions ファイル。 たとえば、既存のパーティション、ロール、およびに記載されているすべての既存のパーティション、ロール、およびメンバーを置換ではなく、ロールのメンバーを保持するたい場合があります、 \<*プロジェクト名*> >.deploymentoptions ファイル。  
  
 パーティションおよびロールの配置を変更する、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]プロジェクト、プロジェクト内のパーティションおよびロールの設定を変更することはできませんので、 *\<プロジェクト名 >* **プロパティ ページ**  ダイアログ ボックスで[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]これらのオプションは表示されません。 ロールおよびパーティションの配置オプションを変更する場合は、内のこの情報を変更する必要があります、 \<*プロジェクト名*> >.deploymentoptions ファイル。 次の手順の説明内のパーティションおよびロールの配置オプションを変更する方法、 \<*プロジェクト名*> >.deploymentoptions ファイル。  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>入力ファイルの生成後にパーティションまたはロールの配置を変更するには  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードを対話形式で実行し、 **[パーティションとロールのオプションの指定]** ページで、パーティションおよびロールの新しい配置オプションを指定します。  
  
     \- または -  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードをコマンド プロンプトで実行し、ウィザードを応答ファイル モードで実行するように設定します。 (応答ファイル モードの詳細については、「 [Analysis Services 配置ウィザードの実行](running-the-analysis-services-deployment-wizard.md)」を参照してください。)  
  
     \- または -  
  
-   開く、 \<*プロジェクト名*> >.deploymentoptions 任意のテキスト エディターを手動でオプションを変更します。  
  
## <a name="see-also"></a>関連項目  
 [インストール先の指定](deployment-script-files-specifying-the-installation-target.md)   
 [ソリューションの配置に関する構成設定の指定](deployment-script-files-solution-deployment-config-settings.md)   
 [処理オプションの指定](deployment-script-files-specifying-processing-options.md)  
  
  
