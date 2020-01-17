---
title: パッケージの管理 (SSIS サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, managing
- packages [Integration Services], managing
- Integration Services packages, managing
- storing packages
- Stored Packages folder
- current packages
- Running Packages folder
- status information [Integration Services]
- SSIS packages, managing
- storage [Integration Services]
- monitoring [Integration Services], packages
- Integration Services service, package management
- services [Integration Services], package management
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 89e925d72b4ca4815c05e9f4ab67211a1a7ea980
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62766630"
---
# <a name="package-management-ssis-service"></a>パッケージの管理 (SSIS サービス)
  パッケージの管理には、次のタスクを含むいくつかのタスクを伴います。  
  
-   実行中のパッケージの監視  
  
-   パッケージ ストレージの管理  
  
-   パッケージのインポートおよびエクスポート  
  
> [!IMPORTANT]  
>  このトピックでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを管理するための Windows サービスである [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスについて説明します。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、以前のリリースの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]との互換性を維持するために、このサービスをサポートしています。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降では、Integration Services サーバー上のパッケージなどのオブジェクトを管理できます。  
  
## <a name="package-store"></a>パッケージ ストア  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 2 つの最上位フォルダーにアクセスするには、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]パッケージ。**パッケージを実行している**と**パッケージが格納されている**します。 **[実行中のパッケージ]** フォルダーには、サーバーで現在実行中のパッケージが一覧表示されます。 **[格納されたパッケージ]** フォルダーには、パッケージ ストアに保存されたパッケージが一覧表示されます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理するパッケージは、これらのパッケージのみです。 パッケージ ストアは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルで一覧されている msdb データベースとファイル システム フォルダーのいずれかまたは両方で構成することができます。 この構成ファイルは、管理する msdb とファイル システム フォルダーを指定します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理していないパッケージは、ファイル システム内の他の場所に保存することもできます。  
  
 msdb に保存するパッケージは、sysssispackages というテーブルに格納されます。 パッケージを msdb に保存するとき、論理フォルダーに格納してグループ化できます。 論理フォルダーを使用することで、パッケージを目的別に整理したり、sysssispackages テーブルでパッケージをフィルター処理したりできます。 新しい論理フォルダーを作成するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用します。 既定では、msdb に追加する論理フォルダーは自動的にパッケージ ストアに含まれます。  
  
 msdb 内のパッケージをグループ化するために作成する論理フォルダーは、msdb 内の sysssispackagefolders テーブルの行として表現されます。 sysssispackagefolders の folderid 列と parentfolderid 列は、フォルダー階層を定義します。 msdb のルート論理フォルダーは、parentfolderid 列が NULL 値である sysssispackagefolders の行です。 詳細については、「[sysssispackages (Transact-SQL)](/sql/relational-databases/system-tables/sysssispackages-transact-sql)」および「[sysssispackagefolders (Transact-SQL)](/sql/relational-databases/system-tables/sysssispackagefolders-transact-sql)」を参照してください。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開いて [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に接続すると、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理する msdb フォルダーが、[格納されたパッケージ] フォルダー内に一覧表示されます。 構成ファイルでルート ファイル システム フォルダーを指定している場合は、[格納されたパッケージ] フォルダーにファイル システムのルート フォルダーとすべてのサブフォルダーに保存されているパッケージも一覧表示されます。  
  
 パッケージは任意のファイル システム フォルダーに保存できますが、そのフォルダーをパッケージ ストアの構成ファイルのフォルダー一覧に追加していない場合、 **[格納されたパッケージ]** フォルダーのサブフォルダーにはパッケージが一覧表示されません。 構成ファイルの詳細については、「[Integration Services サービスの構成 (SSIS サービス)](integration-services-service-ssis-service.md)」を参照してください。  
  
 **[実行中のパッケージ]** フォルダーにはサブフォルダーがなく、拡張もできません。  
  
 既定では、 **[格納されたパッケージ]** フォルダーには、 **[ファイル システム]** と **[MSDB]** の 2 つのフォルダーがあります。 **[ファイル システム]** フォルダーには、ファイル システムに保存されるパッケージが一覧表示されます。 これらのファイルの場所は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルで指定されます。 既定のフォルダーは、%Program Files%\Microsoft SQL Server\100\DTS の Packages フォルダーです。 **[MSDB]** フォルダーには、サーバーの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] msdb データベースに保存されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パッケージが一覧表示されます。 sysssispackages テーブルには、msdb に保存されるパッケージが格納されています。  
  
 パッケージ ストア内のパッケージの一覧を表示するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]に接続する必要があります。 詳細については、「 [SQL Server Management Studio で Integration Services パッケージを表示する (SSIS サービス)](../view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)との互換性を維持するために、このサービスをサポートしています。  
  
## <a name="monitoring-running-packages"></a>実行中のパッケージの監視  
 **[実行中のパッケージ]** フォルダーには、現在実行中のパッケージが一覧表示されます。 **の** [概要] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ページに現在のパッケージ情報を表示するには、 **[実行中のパッケージ]** フォルダーをクリックします。 実行中のパッケージの実行時間などの情報が **[概要]** ページに一覧表示されます。 必要に応じて、フォルダーを更新して、最新の情報を表示します。  
  
 実行中の単一のパッケージに関する情報を **[概要]** ページに表示するには、該当するパッケージをクリックします。 **[概要]** ページには、パッケージのバージョンや説明などの情報が表示されます。  
  
 **[実行中のパッケージ]** フォルダーで実行中のパッケージを右クリックしてから、 **[停止]** をクリックすると、実行中のパッケージを停止できます。  
  
## <a name="managing-package-storage"></a>パッケージ ストレージの管理  
 パッケージを整理するために、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスによって構成ファイルに一覧表示されるルート パッケージ ストア フォルダーにカスタム フォルダーを追加できます。 既定では、ルート フォルダーは **[ファイル システム]** フォルダーと **[MSDB]** フォルダーです。 たとえば、 **[ファイル システム]** フォルダーに、データ クリーンに使用するすべてのパッケージを格納する **[データ クリーン]** フォルダーを追加できます。 カスタム フォルダー内にカスタム フォルダーを追加して、必要に合わせて入れ子にしたフォルダー階層を作成できます。 カスタム フォルダーは削除や名前の変更が可能ですが、構成ファイルで指定されているルート フォルダーの名前の変更や削除はできません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で一覧表示されるルート フォルダーを更新するには、構成ファイルを更新する必要があります。  
  
 詳細については、「 [Integration Services サービスの構成 (SSIS サービス)](../configuring-the-integration-services-service-ssis-service.md)との互換性を維持するために、このサービスをサポートしています。  
  
## <a name="importing-and-exporting-packages"></a>パッケージのインポートおよびエクスポート  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、msdb データベースまたはファイル システムに保存できます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインポートまたはエクスポート機能を使用して、一方のストレージ型から別のストレージ型にパッケージをコピーできます。 また、同じストレージ型にパッケージをインポートして別の名前を付け、パッケージのコピーを作成することもできます。 パッケージのインポートおよびエクスポートには、 **dtutil** コマンド プロンプト ユーティリティ (dtutil.exe) も使用できます。  
  
 詳細については、「 [dtutil ユーティリティ](../dtutil-utility.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [パッケージをインポートおよびエクスポートする &#40;SSIS サービス&#41;](../import-and-export-packages-ssis-service.md)  
  
-   [SQL Server Management Studio で Integration Services パッケージを表示する (SSIS サービス)](../view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)  
  
## <a name="see-also"></a>参照  
 [Integration Services サービス (SSIS サービス)](integration-services-service-ssis-service.md)  
  
  
