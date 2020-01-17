---
title: 相互運用性と共存 (Integration Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 903afa9ef25afcba7818862bc73dc33bf677b47a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "67140818"
---
# <a name="interoperability-and-coexistence-integration-services"></a>相互運用性と共存 (Integration Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services (SSIS) は [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services および [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services と共存できます。  
  
## <a name="features-and-differences"></a>機能と相違点  
 次の表に、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]の現在のバージョンと以前のバージョンの相違点を示します。  
  
|機能|[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]|[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]|  
|-------------|-------------------------------|---------------------------------|---------------------------------|  
|開発環境|[以前のリリースの SQL Server Data Tools (SSDT と SSDT-BI)](https://docs.microsoft.com/sql/ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi?view=sql-server-2014)<br /><br /> [SQL Server 2014 Data Tools - Business Intelligence for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)|[SQL Server Data Tools for Visual Studio 2010](https://msdn.microsoft.com/library/hh500335\(v=vs.103\).aspx)<br /><br /> [SQL Server Data Tools - Business Intelligence for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)|Business Intelligence Development Studio ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)])|  
|管理環境|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|パッケージの格納に使用する msdb のメイン システム テーブル|sysssispackages|sysssispackages|sysssispackages|  
|パッケージの実行に使用するメイン コマンド プロンプト ユーティリティ|**dtexec** (dtexec.exe)、2014 バージョン|**dtexec** (dtexec.exe)、2012 バージョン|**dtexec** (dtexec.exe)、2008 バージョン|  
|既定のルート ファイル システム フォルダー|C:\Program Files\Microsoft SQL Server\120\DTS|C:\Program Files\Microsoft SQL Server\110\DTS|C:\Program Files\Microsoft SQL Server\100\DTS|  
|既定のルート レジストリ キー|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS|  
  
## <a name="side-by-side-compatibility-issues"></a>サイド バイ サイド実行の互換性に関する問題  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services を [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services および [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services とサイド バイ サイドでインストールしている場合、次の作業を実行できます。  
  
-   **SQL Server データ ツールでパッケージを設計する**。 対応するバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に基づくパッケージを開発および管理するには、次のツールを使用します。  
  
    -   使用して、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]開発および管理に基づくパッケージを Business Intelligence Development Studio のバージョン [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]  
  
    -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] に基づくパッケージを開発および管理するには、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] バージョンの [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]を使用します。  
  
    -   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] に基づくパッケージを開発および管理するには、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] バージョンの [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]を使用します。  
  
-   **パッケージを読み込んで実行する。** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] および [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]で開発したパッケージは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で読み込んで実行できます。 パッケージを既存のプロジェクトに追加すると、パッケージは [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services で使用される形式に永続的にアップグレードされます。 パッケージ ファイルを [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で開くと、パッケージは [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services で使用される形式に一時的にアップグレードされます。 パッケージの変更を保存すると、パッケージは永続的にアップグレードされます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services で使用される形式で保存すると、パッケージは、対応する [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] バージョンまたは [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] バージョンの Business Intelligence Development Studio で開くことも、対応する [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services ツールまたは [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services ツールで実行することもできなくなります。  
  
-   **SQL Server Management Studio でパッケージを管理する。** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンまたは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] バージョンの [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] からは [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] バージョンの [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]サービスのインスタンスに接続できません。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] バージョンの [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] からは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] バージョンまたは [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]サービスのインスタンスに接続できません。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] のインスタンスに保存されている [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]パッケージを管理できます。 サービス構成ファイルを変更して、サービスによって管理される場所の一覧に [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] のインスタンスを追加する必要があります。 詳細については、「 [Integration Services サービスの構成 (SSIS サービス)](../service/integration-services-service-ssis-service.md)との互換性を維持するために、このサービスをサポートしています。  
  
-   **SQL Server にパッケージを格納する。** パッケージは次のデータベースに保存できます。  
  
    |パッケージの形式|[データベース]|  
    |--------------------|--------------|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 統合サービス|インスタンスの msdb データベース [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 統合サービス|インスタンスの msdb データベース [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 統合サービス|インスタンスの msdb データベース [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインスタンスでは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]のインスタンスからパッケージをインポートできますが、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]のインスタンスにパッケージをエクスポートすることはできません。  
  
     [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]のインスタンスでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインスタンスとの間で、パッケージをインポートすることも、エクスポートすることもできません。  
  
-   **パッケージを実行する。** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services および [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services パッケージを実行するには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンまたは **dtexec** ユーティリティまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用します。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] で開発したパッケージを [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Integration Services ツールで読み込む場合、パッケージは常に、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] で使用されるパッケージ形式にメモリ内で一時的に変換されます。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] パッケージまたは [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] パッケージが問題により正常に変換できない場合、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services ツールでは、その問題が解決されるまでパッケージを実行できません。 詳細については、「 [Upgrade Integration Services Packages](upgrade-integration-services-packages.md)」を参照してください。  
  
  
