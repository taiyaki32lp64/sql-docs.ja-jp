---
title: パッケージ管理オプション (SSIS パッケージ アップグレード ウィザード) を選択します |。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectpackagemgtoptions.f1
ms.assetid: 810fc020-51cd-43ed-9f35-af99b4f35947
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c71f254b0d0fb79e3ee8135c10d2d9ed715d3437
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056027"
---
# <a name="select-package-management-options-ssis-package-upgrade-wizard"></a>[パッケージ管理オプションの選択] (SSIS パッケージ アップグレード ウィザード)
  **[パッケージ管理オプションの選択]** ページを使用すると、パッケージのアップグレードに関するオプションを指定できます。  
  
 **SSIS パッケージ アップグレード ウィザードを実行するには**  
  
-   [SSIS パッケージ アップグレード ウィザードを使用した Integration Services パッケージのアップグレード](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="options"></a>および  
 **[接続文字列を更新して新しいプロバイダー名を使用する]**  
 現在のリリースの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]の次のプロバイダーの名前を使用するように、接続文字列を更新します。  
  
-   OLE DB Provider for [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ アップグレード ウィザードは、接続マネージャーに格納されている接続文字列だけを更新します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の式言語またはスクリプト タスクのコードによって動的に構築される接続文字列は更新しません。  
  
 **[アップグレード パッケージの検証]**  
 アップグレード パッケージを検証し、検証に合格したアップグレード パッケージだけを保存します。  
  
 このオプションを選択しない場合、ウィザードでアップグレード パッケージの検証が行われません。 したがって、有効なパッケージかどうかにかかわらず、すべてのアップグレード パッケージが保存されます。 ウィザードの **[アップグレード先の場所を選択]** ページで指定したアップグレード先に、アップグレード パッケージが保存されます。  
  
 検証を行うと、アップグレード プロセスにかかる時間が長くなります。 アップグレードに成功する可能性の高い大規模なパッケージに対しては、このオプションを選択しないことをお勧めします。  
  
 **[新しいパッケージ ID を作成する]**  
 アップグレード パッケージの新しいパッケージ ID を作成します。  
  
 **[パッケージのアップグレードに失敗してもアップグレード処理を続行する]**  
 あるパッケージをアップグレードできなかった場合に、残りのパッケージのアップグレードを [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ アップグレード ウィザードで続行します。  
  
 **[パッケージ名の競合]**  
 同じ名前のパッケージをウィザードで処理する方法を指定します。 このオプションには、次の表に示す値があります。  
  
 **[既存のパッケージ ファイルを上書き]**  
 既存のパッケージを同じ名前のアップグレード パッケージで置き換えます。  
  
 **[アップグレード パッケージ名に数値サフィックスを追加]**  
 アップグレード パッケージの名前に数値サフィックスを追加します。  
  
 **[パッケージをアップグレードしない]**  
 そのパッケージのアップグレードを停止し、ウィザードの完了時にエラーを表示します。  
  
 ウィザードの **[アップグレード先の場所を選択]** ページで **[ソースの場所に保存]** オプションを選択した場合は、これらのオプションを使用できません。  
  
 **[構成を無視する]**  
 パッケージのアップグレード中にパッケージ構成を読み込みません。 このオプションを選択すると、パッケージのアップグレードに必要な時間が短縮されます。  
  
 **[元のパッケージをバックアップする]**  
 ウィザードで、元のパッケージを **SSISBackupFolder** フォルダーにバックアップします。 元のパッケージとアップグレード済みパッケージが格納されるフォルダーに、 **SSISBackupFolder** サブフォルダーが作成されます。  
  
> [!NOTE]  
>  このオプションを使用できるのは、元のパッケージとアップグレード済みパッケージをファイル システム内の同一フォルダーに格納するように指定した場合だけです。  
  
 詳細については、「[SSIS パッケージ アップグレード ウィザードを使用した Integration Services パッケージのアップグレード](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services パッケージのアップグレード](install-windows/upgrade-integration-services-packages.md)  
  
  
