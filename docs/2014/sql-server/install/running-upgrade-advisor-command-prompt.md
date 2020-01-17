---
title: アップグレード アドバイザー (コマンド プロンプト) を実行している |。Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], running
- command prompt [Upgrade Advisor]
- UpgradeAdvisorWizardCmd utility
- XML formats [Upgrade Advisor]
ms.assetid: 7c83049b-9227-4723-9b7f-66288bc6bd1d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 997d637d109c04dbecb3105538f51fa6ece0518f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092441"
---
# <a name="running-upgrade-advisor-command-prompt"></a>アップグレード アドバイザーの実行 (コマンド プロンプト)
  使用して、 **UpgradeAdvisorWizardCmd**ユーティリティをコマンド プロンプトからアップグレード アドバイザーを実行します。 結果を XML 形式で受け取るか、コンマ区切り値のファイルで受け取るかを選択できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
      UpgradeAdvisorWizardCmd [ -? ]  |   
    [ -ConfigFilefilename | <server_info> ]  
    [ -SqlUserlogin_id-SqlPasswordpassword ]  
    [ -CSV ]  
  
where <server_info> is any combination of the following:  
        -Serverserver_name-Instanceinstance_name-ASInstanceAS_instance_name-RSInstanceRS_instance_name  
```  
  
## <a name="arguments"></a>引数  
 **-?**  
 コマンドの構文を表示します。  
  
 **-ConfigFile** _filename_  
 実行するときに使用する設定を含む XML ファイルのファイル名とパスの名前には、 **UpgradeAdvisorWizardCmd**ユーティリティ。  
  
 *<server_info>*  
 分析するコンピューターとインスタンスを指定します。 構成ファイルを使用していない場合に、これらのオプションを使用します。  
  
 *< server_info >* 次の 4 つの引数の組み合わせにすることができます。  
  
 **-Server** _server_name_  
 分析するコンピューターの名前を指定します。 ローカル コンピューター (既定値) またはリモート コンピューターのどちらでも指定できます。  
  
 **-Instance** _instance_name_  
 分析するインスタンスの名前を指定します。 既定値はありません。 このパラメーターを指定しない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]はスキャンされません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスの値は MSSQLSERVER です。 名前付きインスタンスの場合は、インスタンス名を使用します。  
  
 **-ASInstance**  _AS_instance_name_  
 分析する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスの名前を指定します。 既定値はありません。 この値を指定しない場合、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] はスキャンされません。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の既定のインスタンスの値は MSSQLServerOLAPService です。 名前付きインスタンスの場合は、インスタンス名を使用します。  
  
 **-RSInstance**  _RS_instance_name_  
 分析する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインスタンスの名前を指定します。 既定値はありません。 この値を指定しない場合、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] はスキャンされません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の既定のインスタンスの値は ReportServer です。 名前付きインスタンスの場合は、インスタンス名を使用します。  
  
 **-SqlUser** _login_id_  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、この値に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。アップグレード アドバイザーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへの接続にこのログインを使用します。 ログインを指定しないと、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続に Windows 認証が使用されます。  
  
 **-SqlPassword** _パスワード_  
 使用する場合、 **- SqlUser**引数では、この引数を使用して、パスワードを指定する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインします。  
  
 **-CSV**  
 標準的な XML の結果に加え、コンマ区切り値の結果を .csv ファイルに出力する場合に指定します。 My Documents に結果が書き込まれる\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade advisor \110\reports フォルダー。  
  
## <a name="return-values"></a>戻り値  
 次の表は、値を**UpgradeAdvisorWizardCmd**を返します。  
  
|値|Description|  
|-----------|-----------------|  
|0|分析が正常に完了し、アップグレードの問題は見つかりませんでした。|  
|正の整数|分析が正常に完了し、アップグレードの問題が見つかりました。|  
|負の整数|分析が失敗しました。|  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のユーザー名とパスワード以外は、分析の実行に必要なすべての情報を XML 構成ファイルに出力できます。 この XML 構成ファイルはテンプレートに記述されています。 構成ファイルを使用しない場合は、既定の設定でコンピューター名とインスタンス名を指定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにインストールされているコンポーネントすべてを分析できます。 既定の構成ファイル設定の詳細については、「要素の説明」の一覧を参照してください。  
  
## <a name="configuration-file-template"></a>構成ファイルのテンプレート  
 独自の構成ファイルを作成する場合は、次の XML をテンプレートとして使用してください。 テンプレートは必要に応じて変更できます。  
  
```xml  
<Configuration>  
    <Server> </Server>  
    <Instance></Instance>  
    <Components>  
        <SQLServer>  
            <Databases>  
                <Database></Database>  
            </Databases>  
            <TraceFiles>  
                <TraceFile></TraceFile>  
            </TraceFiles>  
            <BatchFiles>  
                <BatchFile></BatchFile>  
            </BatchFiles>  
            <BatchSeparator></BatchSeparator>  
        </SQLServer>  
        <AnalysisServices>  
            <ASInstance></ASInstance>  
            <Databases>  
                <Database></Database>  
            </Databases>  
        </AnalysisServices>  
        <ReportingServices>  
            <RSInstance></RSInstance>  
        </ReportingServices>  
        <IntegrationServices>  
            <PackagePath></PackagePath>  
        </IntegrationServices>  
    </Components>  
</Configuration>  
```  
  
## <a name="element-descriptions"></a>要素の説明  
  
|Tag|定義|個数|  
|---------|----------------|----------------|  
|`Configuration`|アップグレード アドバイザー構成ファイルの親要素です。|必須。構成ファイルにつき 1 個。|  
|`Server`|分析するサーバーの名前です。|省略可。構成ファイルにつき 1 個。 既定値はローカル コンピューターです。|  
|`Instance`|分析する[!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスの名前です。|省略可。構成ファイルにつき 1 個。 既定値は既定のインスタンスです。<br /><br /> サーバー上に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 要素または `IntegrationServices` 要素が存在する場合は必須。構成ファイルにつき 1 個。|  
|`Components`|分析するコンポーネントを指定する要素を含みます。|必須。構成ファイルにつき 1 個。|  
|`SQLServer`|[!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスの分析設定を含みます。|省略可。構成ファイルにつき 1 個。 指定しないと、[!INCLUDE[ssDE](../../includes/ssde-md.md)] データベースが分析されません。|  
|`Databases` 要素の `SQLServer`|分析するデータベースの一覧を含みます。|省略可能な 1 回`SQLServer`要素。 この要素が存在しない場合、インスタンスのすべてのデータベースが分析されます。|  
|`Database` 要素の `SQLServer`|分析するデータベースの名前を指定します。|必須。`Databases` 要素が存在する場合に 1 個以上。 `Database` 要素に値 "*" が含まれている場合は、インスタンスのすべてのデータベースが分析されます。 既定値はありません。|  
|`TraceFiles`|分析するトレース ファイルの一覧を含みます。|省略可能な 1 回`SQLServer`要素。|  
|`TraceFile`|分析するトレース ファイルのパスと名前を指定します。|必須。`TraceFiles` 要素が存在する場合に 1 個以上。 既定値はありません。|  
|`BatchFiles`|分析するバッチ ファイルの一覧を含みます。|省略可能な 1 回`SQLServer`要素。|  
|`BatchFile`|分析するバッチ ファイルを指定します。 複数指定することもできます。|必須。`BatchFiles` 要素が存在する場合に 1 個以上。 既定値はありません。|  
|`BatchSeparator`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バッチ ファイルに使用されるバッチ区切り記号を指定します。|省略可能な 1 回`SQLServer`要素。 既定値は、GO です。|  
|`AnalysisServices`|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の分析設定を含みます。|省略可。構成ファイルにつき 1 個。 指定しないと、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースが分析されません。|  
|`ASInstance`|インスタンスの名前を示す[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]します。|必須。`AnalysisServices` 要素につき 1 個。 既定値はありません。|  
|`Databases` 要素の `Analysis Services`|分析するデータベースの一覧を含みます。|省略可能な 1 回`AnalysisServices`要素。 この要素が存在しない場合、インスタンスのすべてのデータベースが分析されます。|  
|`Database` 要素の `AnalysisServices`|分析するデータベースの名前を指定します。|必須。`Databases` 要素が存在する場合に 1 個以上。 `Database` 要素に値 "*" が含まれている場合は、インスタンスのすべてのデータベースが分析されます。 既定値はありません。|  
|`ReportingServices`|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に対して分析を実行することを指定します。|省略可。構成ファイルにつき 1 個。 指定しなかった場合、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は分析されません。|  
|`RSInstance`|インスタンスの名前を示す[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]します。|必須。`ReportingServices` 要素につき 1 個。 既定値はありません。|  
|`IntegrationServices`|分析の設定を含む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]します。|省略可。構成ファイルにつき 1 個。 指定しなかった場合、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は分析されません。|  
|`PackagePath`|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのセットのパスを指定します。|省略可能な 1 回`IntegrationServices`要素。 この要素が存在しない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して分析が行われ、外部に格納されたパッケージは分析されません。 既定値はありません。|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-run-upgrade-advisor-using-a-configuration-file"></a>A. 構成ファイルを使用したアップグレード アドバイザーの実行  
 次の例は、分析対象を指定する構成ファイルを使用したコマンド プロンプトからのアップグレード アドバイザーの実行方法を示しています。 この例では、Windows 認証を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続します。  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"  
```  
  
### <a name="b-run-upgrade-advisor-using-default-configuration-settings"></a>B. 既定の構成設定を使用したアップグレード アドバイザーの実行  
 次の例は、既定の構成設定と Windows 認証を使用したコマンド プロンプトからのアップグレード アドバイザーの実行方法を示しています。  
  
```  
UpgradeAdvisorWizardCmd -Server MyServer -Instance MyInst   
```  
  
### <a name="c-run-upgrade-advisor-using-includessnoversionincludesssnoversion-mdmd-authentication"></a>C. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用したアップグレード アドバイザーの実行  
 次の例は、構成ファイルを使用したコマンド プロンプトからのアップグレード アドバイザーの実行方法を示しています。 この例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続するための [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー名とパスワードを指定します。  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"   
    -SqlUser "MyUserName" -SqlPassword "QweRTy-55"  
```  
  
## <a name="see-also"></a>参照  
 [アップグレードの問題を解決します。](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [アップグレード アドバイザーを実行している&#40;ユーザー インターフェイス&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)  
  
  
