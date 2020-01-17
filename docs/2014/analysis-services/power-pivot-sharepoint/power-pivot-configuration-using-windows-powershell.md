---
title: Windows PowerShell を使用した PowerPivot の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4d83e53e-04f1-417d-9039-d9e81ae0483d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9282fce8e0004495ae8c10b0b3f75fec205d6b34
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782806"
---
# <a name="powerpivot-configuration-using-windows-powershell"></a>Windows PowerShell を使用した PowerPivot の構成
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] には、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]のインストールを構成するために使用できる Windows PowerShell コマンドレットが含まれています。 PowerShell によりインストールを完全に構成するには、SharePoint コマンドレットと PowerPivot for SharePoint コマンドレットの両方を使用する必要があります。 構成の大部分は [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ツールのいずれかを使用して実行することができます。 ツールの詳細については、「 [PowerPivot 構成ツール](power-pivot-configuration-tools.md)」を参照してください。  
  
> [!IMPORTANT]  
>  SharePoint 2010 ファームの場合、PowerPivot for SharePoint または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] データベース サーバーを使用する SharePoint ファームを構成する前に、SharePoint 2010 SP1 をインストールする必要があります。 サービス パックをインストールしていない場合は、サーバーの構成を始める前にインストールしてください。  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-powershell"></a>PowerShell を使用して PowerPivot for SharePoint を構成する利点  
 Windows  PowerShell スクリプト (.ps1) ファイルを作成して構成タスクを自動化できます。 この方法は、任意のサーバーで実行できるスクリプト化されたインストール手順および構成手順が必要な場合に推奨されます。 このようなスクリプトは、ハードウェア障害が発生したときにサーバーを再構築するディザスター リカバリー計画の一環として必要になる場合があります。  
  
## <a name="view-a-list-of-the-powerpivot-cmdlets-on-a-server"></a>サーバーで PowerPivot コマンドレットの一覧を表示する  
 @No__t_0 コマンドレットの内容と例については、「 [PowerShell Reference for PowerPivot for SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)」を参照してください。  
  
 PowerShell を使用して PowerPivot コマンドレットの一覧を表示するには  
  
1.  **[管理者として実行]** オプションを使用して SharePoint 管理シェルを開きます。  
  
2.  次のコマンドを入力します。  
  
    ```powershell
    Get-Help *powerpivot*  
    ```  
  
     コマンドレット名に PowerPivot を含むコマンドレットの一覧が表示されます。 たとえば、 `Get-PowerPivotServiceApplication`があります。 使用できるコマンドレットの数は、使用している Analysis Services のバージョンによって異なります。  
  
    -   SharePoint モードで構成された SQL Server 2012 SP1 Analysis Services サーバーおよび SharePoint 2013 では、10 個のコマンドレットを使用できます。 2012 SP1 バージョンで使用される新しいアーキテクチャでは、分析サーバーを SharePoint ファームの外部で実行できるため、必要な管理 Windows PowerShell コマンドレットが少なくて済みます。  
  
    -   SharePoint モードで構成された SQL Server 2012 Analysis Services サーバーおよび SharePoint 2010 では、17 個のコマンドレットを使用できます。  
  
     一覧にコマンドが返されない場合、または "`get-help could not find *powerpivot* in a help file in this session.`" のようなエラーメッセージが表示される場合は、このトピックの次のセクションを参照して、サーバーで PowerPivot コマンドレットを有効にする方法を確認してください。  
  
     すべてのコマンドレットに、オンライン ヘルプが用意されています。 `New-PowerPivotServiceApplication` コマンドレットのオンライン ヘルプを表示する方法を次の例に示します。  
  
    ```powershell
    Get-Help new-powerpivotserviceapplication -Full  
    ```  
  
     また、例のみを表示するには、次の構文を使用します。  
  
    ```powershell
    Get-Help new-powerpivotserviceapplication -Example  
    ```  
  
## <a name="enable-powerpivot-cmdlets-on-a-server"></a>サーバーで PowerPivot コマンドレットを有効にする  
 PowerPivot コマンドレットは、PowerPivot for SharePoint のインストールとファーム ソリューションの配置が完了した後で利用できるようになります。 ソリューションは、PowerPivot 構成ツールを実行すると配置されます。 コマンドレットの使用を有効にするには、次の手順を実行します。  
  
1.  **[管理者として実行]** オプションを使用して SharePoint 管理シェルを開きます。  
  
2.  最初のコマンドレットを実行します。  
  
    ```powershell
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     コマンドレットにより、ソリューション名、ソリューション ID、および Deployed=False が返されます。 次の手順では、ソリューションを配置します。  
  
3.  2 番目のコマンドレットを実行してソリューションを配置します。  
  
    ```powershell
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
4.  ウィンドウを閉じます。 **[管理者として実行]** を使用してもう一度ウィンドウを開きます。  
  
## <a name="related-content"></a>関連コンテンツ  
 [サーバーの全体管理での PowerPivot サーバーの管理と構成](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [PowerPivot 構成ツール](power-pivot-configuration-tools.md)  
  
 [PowerPivot for SharePoint の PowerShell リファレンス](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
