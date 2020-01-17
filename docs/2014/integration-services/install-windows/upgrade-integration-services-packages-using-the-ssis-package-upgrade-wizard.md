---
title: SSIS パッケージ アップグレード ウィザードを使用した Integration Services パッケージのアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, upgrading
- upgrading Integration Services packages
ms.assetid: 9359275a-48f5-4d1e-8ae7-e797759e3ccf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e44b755748dcbda6af30e0570b667f9ba3ee75a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767891"
---
# <a name="upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard"></a>SSIS パッケージ アップグレード ウィザードを使用した Integration Services パッケージのアップグレード
  以前のバージョンの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で作成したパッケージは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で使用される [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 形式にアップグレードできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、このプロセスを容易に行うための [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードが用意されています。 このウィザードは元のパッケージをバックアップするように構成できるため、アップグレードが難しい場合は、元のパッケージを引き続き使用できます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインストール時にインストールされます。  
  
> [!NOTE]  
>  [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の Standard Edition、Enterprise Edition、および Developer Edition で使用できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのアップグレード方法については、「 [Integration Services パッケージのアップグレード](upgrade-integration-services-packages.md)」をご覧ください。  
  
 以降では、ウィザードの実行方法と元のパッケージのバックアップ方法について説明します。  
  
## <a name="running-the-ssis-package-upgrade-wizard"></a>SSIS パッケージ アップグレード ウィザードの実行  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、またはコマンド プロンプトから実行できます。  
  
#### <a name="to-run-the-wizard-from-sql-server-data-tools"></a>SQL Server データ ツールからウィザードを実行するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを作成または開きます。  
  
2.  ソリューション エクスプローラーで、 **[SSIS パッケージ]** ノードを右クリックして **[すべてのパッケージをアップグレード]** をクリックし、このノードの下のすべてのパッケージをアップグレードします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージまたは [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] パッケージが含まれる [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] プロジェクトを開いた場合、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードが自動的に開きます。  
  
#### <a name="to-run-the-wizard-from-sql-server-management-studio"></a>SQL Server Management Studio からウィザードを実行するには  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]に接続し、 **[格納されたパッケージ]** ノードを展開して **[ファイル システム]** ノードまたは **[MSDB]** ノードを右クリックし、 **[パッケージのアップグレード]** をクリックします。  
  
#### <a name="to-run-the-wizard-at-the-command-prompt"></a>コマンド プロンプトでウィザードを実行するには  
  
-   コマンド プロンプトから SSISUpgrade.exe ファイルを実行、 **C:\Program files \microsoft SQL server \120\dts\binn**フォルダー。  
  
## <a name="backing-up-the-original-packages"></a>元のパッケージのバックアップ  
 元のパッケージをバックアップするには、元のパッケージとアップグレードされたパッケージの両方をファイル システム内の同一フォルダーに格納する必要があります。 この格納場所は、ウィザードの実行方法に応じて、自動的に選択される場合があります。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードを [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]から実行すると、元のパッケージとアップグレードされたパッケージの両方がファイル システム内の同一フォルダーに自動的に格納されます。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードを [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] またはコマンド プロンプトから実行すると、元のパッケージとアップグレードされたパッケージに異なる格納場所を指定することができます。 元のパッケージをバックアップするには、元のパッケージとアップグレードされたパッケージの両方がファイル システム内の同一フォルダーに格納されるように指定する必要があります。 他の格納オプションを指定すると、元のパッケージをバックアップできません。  
  
 ウィザードで元のパッケージをバックアップすると、元のパッケージのコピーが **SSISBackupFolder** フォルダーにバックアップされます。 この **SSISBackupFolder** フォルダーは、元のパッケージとアップグレードされたパッケージが格納されるフォルダーのサブフォルダーとして作成されます。  
  
#### <a name="to-back-up-the-original-packages-in-sql-server-management-studio-or-at-the-command-prompt"></a>SQL Server Management Studio またはコマンド プロンプトで元のパッケージをバックアップするには  
  
1.  元のパッケージをファイル システム上の場所に保存します。  
  
    > [!NOTE]  
    >  ウィザードのバックアップ オプションは、ファイル システムに格納されているパッケージに対してのみ機能します。  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] またはコマンド プロンプトで、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードを実行します。  
  
3.  ウィザードの **[アップグレード元の場所の選択]** ページで、 **[パッケージのアップグレード元]** プロパティを **[ファイル システム]** に設定します。  
  
4.  ウィザードの **[アップグレード先の場所の選択]** ページで、 **[アップグレード元の場所に保存する]** をクリックして、アップグレードされたパッケージを、元のパッケージと同じ場所に保存します。  
  
    > [!NOTE]  
    >  ウィザードのバックアップ オプションを使用できるのは、アップグレードされたパッケージが元のパッケージと同じフォルダーに格納されている場合のみです。  
  
5.  ウィザードの **[パッケージ管理オプションの選択]** ページで、 **[元のパッケージをバックアップする]** チェック ボックスをオンにします。  
  
#### <a name="to-back-up-the-original-packages-in-sql-server-data-tools"></a>SQLServer データ ツールの元のパッケージをバックアップするには  
  
1.  元のパッケージをファイル システム上の場所に保存します。  
  
2.  ウィザードの **[パッケージ管理オプションの選択]** ページで、 **[元のパッケージをバックアップする]** チェック ボックスをオンにします。  
  
    > [!WARNING]  
    >  **元のパッケージをバックアップ**を開くと、オプションは表示されませんが、[!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]または[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]プロジェクト[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、自動的にウィザードを起動します。  
  
3.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードを実行します。  
  
  
