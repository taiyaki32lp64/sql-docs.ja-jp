---
title: Integration Services パッケージのアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, migrating
- migrating packages [Integration Services]
ms.assetid: 68dbdf81-032c-4a73-99f6-41420e053980
author: MikeRayMSFT
ms.author: mikeray
manager: erikre
ms.openlocfilehash: 3d458e7696719c383b03a5cc3f259de08e4b8c37
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262780"
---
# <a name="upgrade-integration-services-packages"></a>Integration Services パッケージのアップグレード

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] のインスタンスを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の現在のリリースにアップグレードするとき、既存の [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] パッケージは、現在のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で使用されるパッケージ形式に自動的にアップグレードされません。 アップグレード方法を選択して、パッケージを手動でアップグレードする必要があります。  
  
 プロジェクトをプロジェクトの配置モデルに変換するときのパッケージのアップグレードについては、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」をご覧ください。
  
## <a name="selecting-an-upgrade-method"></a>アップグレード方法の選択  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、または [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] パッケージは、さまざまな方法でアップグレードできます。 その方法によって、アップグレードが一時的な場合と 永続的な場合があります。 次の表に、それらの各方法とアップグレードが一時的か永続的かを示します。  
  
> [!NOTE]  
>  現在のリリースの [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]と共にインストールされる [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]dtexec [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ユーティリティ (dtexec.exe) を使用して [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 、 **、** 、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パッケージを実行すると、一時パッケージのアップグレードが行われることで、実行時間が増加します。 パッケージ実行時間の増加比率は、パッケージのサイズに応じて異なります。 実行時間が増加しないようにするには、パッケージの実行前にアップグレードしておくことをお勧めします。  
  
|アップグレード方法|アップグレードの種類|  
|--------------------|---------------------|  
|現在のリリースの **と共にインストールされる** dtexec [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ (dtexec.exe) を使用して、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、または [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] パッケージを実行します。<br /><br /> 詳細については、「 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)」を参照してください。|パッケージのアップグレードは一時的です。<br /><br /> 変更を保存することはできません。|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]で [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 、または [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]パッケージ ファイルを開きます。|パッケージのアップグレードは、パッケージを保存した場合は永続的になり、パッケージを保存しなかった場合は一時的になります。|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、または [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] パッケージを [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]の既存のプロジェクトに追加します。|パッケージのアップグレードは永続的です。|  
|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] で [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]以降のプロジェクト ファイルを開き、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードを使用してプロジェクト内の複数のパッケージをアップグレードします。<br /><br /> 詳細については、「 [SSIS パッケージ アップグレード ウィザードを使用した Integration Services パッケージのアップグレード](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md) 」および [SSIS パッケージ アップグレード ウィザードの F1 ヘルプ](../../integration-services/ssis-package-upgrade-wizard-f1-help.md)」を参照してください。|パッケージのアップグレードは永続的です。|  
|現在のリリースの <xref:Microsoft.SqlServer.Dts.Runtime.Application.Upgrade%2A> メソッドを使用して、1 つまたは複数の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、さまざまな方法でアップグレードできます。|パッケージのアップグレードは永続的です。|  
  
## <a name="custom-applications-and-custom-components"></a>カスタム アプリケーションおよびカスタム コンポーネント  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 現在のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、 カスタム コンポーネントが動作しません。  
  
 現在のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ツールを使用して、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 or [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssIS](../../includes/ssis-md.md)] カスタム コンポーネントが含まれているパッケージを実行および管理することができます。 ランタイム アセンブリを Version 10.0.0.0 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)])、Version 11.0.0.0 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])、または Version 12.0.0.0 ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) から Version 13.0.0.0 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) にリダイレクトする際に役立つ 4 つのバインド リダイレクト ルールが次のファイルに追加されました。  
  
-   DTExec.exe.config  
  
-   dtshost.exe.config  
  
-   DTSWizard.exe.config  
  
-   DTUtil.exe.config  
  
-   DTExecUI.exe.config  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] を使って、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、または [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] カスタム コンポーネントを含むパッケージを設計するには、\<*ドライブ*>:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE にある devenv.exe.config ファイルを変更する必要があります。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のランタイムで構築された顧客アプリケーションでこれらのパッケージを使用するには、実行可能ファイルに対応する *.exe.config ファイルの configuration セクションにリダイレクト ルールを含めます。 これらのルールにより、ランタイム アセンブリが Version 13.0.0.0 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) にリダイレクトされます。 アセンブリ バージョン リダイレクトについて詳しくは、「[\<runtime> の \<assemblyBinding> 要素](https://msdn.microsoft.com/library/twy1dw1e.aspx)」をご覧ください。  
  
### <a name="locating-the-assemblies"></a>アセンブリの場所  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] アセンブリが .NET 4 にアップグレードされました。 \<*ドライブ*>:\Windows\Microsoft.NET\assembly に、.NET 4 用の別のグローバル アセンブリ キャッシュが用意されています。 すべての [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] アセンブリは、通常、このパスの GAC_MSIL フォルダーにあります。  
  
 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と同様に、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のコア機能拡張 .dll ファイルは \<*ドライブ*>:\Program Files\Microsoft SQL Server\130\SDK\Assemblies にあります。  
  
## <a name="understanding-sql-server-package-upgrade-results"></a>SQL Server パッケージのアップグレード結果について  
 パッケージのアップグレード プロセス中に、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、または [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] パッケージ内のほとんどのコンポーネントと機能が、現在のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の対応するコンポーネントと機能にシームレスに変換されます。 ただし、いくつかのコンポーネントと機能については、アップグレードされないか、アップグレード結果に注意が必要です。 それらのコンポーネントと機能を次の表に示します。  
  
> [!NOTE]  
>  この表の一覧に示された問題を含むパッケージを識別するには、アップグレード アドバイザーを実行します。  
  
|コンポーネントまたは機能|アップグレード結果|  
|--------------------------|---------------------|  
|接続文字列|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、または [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] パッケージでは、特定のプロバイダーの名前が変更されているため、接続文字列の値を変更する必要があります。 接続文字列を更新するには、次のいずれかの手順を実行します。<br /><br /> [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ アップグレード ウィザードを使用してパッケージをアップグレードし、 **[新しいプロバイダー名を使用した接続文字列に更新する]** オプションを選択します。<br /><br /> [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、[オプション] ダイアログ ボックスの [全般] ページにある **[新しいプロバイダー名を使用した接続文字列に更新する]** オプションを選択します。 このオプションについて詳しくは、「[全般] ページ」をご覧ください。<br /><br /> [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でパッケージを開き、ConnectionString プロパティのテキストを手動で変更します。<br /><br /> 注:接続文字列が構成ファイルまたはデータ ソース ファイルに格納されている場合、または式で **ConnectionString** プロパティを設定する場合は、上記の手順を使用して接続文字列を更新することはできません。 このような場合に接続文字列を更新するには、ファイルまたは式を手動で更新する必要があります。<br /><br /> 使用できるデータ ソースの詳細については、「 [データ ソース](../../integration-services/connection-manager/data-sources.md)」を参照してください。|  
  
### <a name="scripts-that-depend-on-adodbdll"></a>ADODB.dll に依存するスクリプト  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] がインストールされていないコンピューターでは、ADODB.dll を明示的に参照するスクリプト タスクおよびスクリプト コンポーネントのスクリプトをアップグレードしたり、実行したりすることはできません。 このようなスクリプト タスクまたはスクリプト コンポーネントのスクリプトをアップグレードするには、ADODB.dll に対する依存関係を削除することをお勧めします。  また、VB や C# のスクリプトなどのマネージド コードの代わりに ADO.NET を使用することをお勧めします。  
  
  
