---
title: パッケージの管理 (SSIS サービス) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dtsserver.importpackage.f1
- sql13.dts.dtsserver.exportpackage.f1
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 33ce0a748381e425371b6f36c1ceeaaba4b62501
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296876"
---
# <a name="package-management-ssis-service"></a>パッケージの管理 (SSIS サービス)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  パッケージの管理には、パッケージの監視、管理、インポートおよびエクスポートが含まれます。  
 
 ## <a name="package-store"></a>パッケージ ストア  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、パッケージにアクセスするための次の 2 つの最上位フォルダーが提供されます。 
 - **パッケージの実行** 
 - **[格納されたパッケージ]**

 **[実行中のパッケージ]** フォルダーには、サーバーで現在実行中のパッケージが一覧表示されます。 **[格納されたパッケージ]** フォルダーには、パッケージ ストアに保存されたパッケージが一覧表示されます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理するパッケージは、これらのパッケージのみです。 パッケージ ストアは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルで一覧されている msdb データベースとファイル システム フォルダーのいずれかまたは両方で構成することができます。 この構成ファイルは、管理する msdb とファイル システム フォルダーを指定します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理していないパッケージは、ファイル システム内の他の場所に保存することもできます。  
  
 msdb に保存するパッケージは、sysssispackages というテーブルに格納されます。 パッケージを msdb に保存するときに、論理フォルダーにグループ化できます。 論理フォルダーを使用すると、パッケージを目的別に整理したり、sysssispackages テーブルでパッケージをフィルター処理したりするのに役立ちます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で新しい論理フォルダーを作成します。 既定では、msdb に追加する論理フォルダーは自動的にパッケージ ストアに含まれます。  
  
 作成する論理フォルダーは、msdb 内の sysssispackagefolders テーブルの行として表されます。 sysssispackagefolders の folderid 列と parentfolderid 列は、フォルダー階層を定義します。 msdb のルート論理フォルダーは、parentfolderid 列が NULL 値である sysssispackagefolders の行です。 詳細については、「[sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md)」および「[sysssispackagefolders (Transact-SQL)](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)」を参照してください。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開いて [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]に接続すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理する msdb フォルダーが、[格納されたパッケージ] フォルダー内に一覧表示されます。 構成ファイルでルート ファイル システム フォルダーを指定している場合は、[格納されたパッケージ] フォルダーにファイル システムのルート フォルダーとすべてのサブフォルダーに保存されているパッケージも一覧表示されます。  
  
 パッケージは任意のファイル システム フォルダーに保存できますが、そのフォルダーをパッケージ ストアの構成ファイルのフォルダー一覧に追加していない場合、 **[格納されたパッケージ]** フォルダーのサブフォルダーにはパッケージが一覧表示されません。 構成ファイルの詳細については、「 [Integration Services サービス (SSIS サービス)](../../integration-services/service/integration-services-service-ssis-service.md)との互換性を維持するために、このサービスをサポートしています。  
  
 **[実行中のパッケージ]** フォルダーにはサブフォルダーがなく、拡張もできません。  
  
 既定では、 **[格納されたパッケージ]** フォルダーには、 **[ファイル システム]** と **[MSDB]** の 2 つのフォルダーがあります。 **[ファイル システム]** フォルダーには、ファイル システムに保存されるパッケージが一覧表示されます。 これらのファイルの場所は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルで指定されます。 既定のフォルダーは、%Program Files%\Microsoft SQL Server\100\DTS の Packages フォルダーです。 **[MSDB]** フォルダーには、サーバーの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] msdb データベースに保存されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パッケージが一覧表示されます。 sysssispackages テーブルには、msdb に保存されるパッケージが格納されています。  
  
 パッケージ ストア内のパッケージの一覧を表示するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]に接続する必要があります。  
  
## <a name="monitor-running-packages"></a>実行中のパッケージの監視  
 **[実行中のパッケージ]** フォルダーには、現在実行中のパッケージが一覧表示されます。 **の** [概要] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ページに現在のパッケージ情報を表示するには、 **[実行中のパッケージ]** フォルダーをクリックします。 実行中のパッケージの実行時間などの情報が **[概要]** ページに一覧表示されます。 必要に応じて、フォルダーを更新して、最新の情報を表示します。  
  
 実行中の単一のパッケージに関する情報を **[概要]** ページに表示するには、該当するパッケージをクリックします。 **[概要]** ページには、パッケージのバージョンや説明などの情報が表示されます。  
  
**[実行中のパッケージ]** フォルダーで実行中のパッケージを停止する場合は、パッケージを右クリックしてから **[停止]** をクリックします。  
  
## <a name="view-packages-in-ssms"></a>SSMS でのパッケージの表示
    
 この手順では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] に接続して、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理するパッケージの一覧を表示する方法について説明します。  
  
### <a name="to-connect-to-integration-services"></a>Integration Services に接続するには  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** の順にポイントし、 **[SQL Server Management Studio]** をクリックします。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、 **[サーバーの種類]** 一覧の **[Integration Services]** を選択し、 **[サーバー名]** ボックスにサーバー名を入力して **[接続]** をクリックします。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]に接続できない場合は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが実行されていない可能性があります。 このサービスの状態を調べるには、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** 、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。 左ペインで、 **[SQL Server のサービス]** をクリックします。 右ペインで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを見つけます。 サービスがまだ実行されていない場合は開始します。  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] が開きます。 既定では、Management Studio の左下隅にオブジェクト エクスプローラーが開きます。 オブジェクト エクスプローラーが開いていない場合は、 **[表示]** メニューの **[オブジェクト エクスプローラー]** をクリックします。  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>Integration Services サービスが管理するパッケージを表示するには  
  
1.  オブジェクト エクスプローラーで、[格納されたパッケージ] フォルダーを展開します。  
  
2.  [格納されたパッケージ] サブフォルダーを展開して、パッケージを表示します。  

## <a name="import-and-export-packages"></a>パッケージのインポートとエクスポート
 
 パッケージは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb データベースの sysssispackages テーブルまたはファイル システムに保存できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスによって監視および管理される論理ストレージであるパッケージ ストアには、msdb データベースと、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルに指定されているファイル システム フォルダーの両方を格納できます。  
  
 パッケージは、次の種類のストレージ間でインポートおよびエクスポートできます。  
  
-   ファイル システム上の任意の場所にあるファイル システム フォルダー。  
  
-   SSIS パッケージ ストア内のフォルダー。 [ファイル システム] と [MSDB] の 2 つの既定のフォルダーがあります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb データベース。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、パッケージをインポートおよびエクスポートできます。これは、パッケージの保存形式と位置が変わることを意味します。 インポートおよびエクスポート機能を使用すると、ファイル システム、パッケージ ストア、または msdb データベースにパッケージを追加したり、いずれかの保存形式から別の保存形式にパッケージをコピーしたりできます。 たとえば、msdb に保存されているパッケージをファイル システムにコピーしたり、その逆の操作を行うことができます。  
  
 **dtutil** コマンド プロンプト ユーティリティ (dtutil.exe) を使用してパッケージを別の形式にコピーすることもできます。 詳細については、「 [dtutil ユーティリティ](../../integration-services/dtutil-utility.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、次の場所からインポートしたり、次の場所にエクスポートしたりできます。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス、ファイル システム、または [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアに格納されているパッケージをインポートできます。 インポートしたパッケージは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、または [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストア内のフォルダーに保存されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス、ファイル システム、または [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアに格納されているパッケージを異なるストレージ形式および場所にエクスポートできます。  
  
 ただし、異なるバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]間でパッケージをインポートおよびエクスポートするには、いくつかの制限があります。  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]のインスタンスでは、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のインスタンスからパッケージをインポートできますが、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のインスタンスにパッケージをエクスポートすることはできません。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のインスタンスでは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]のインスタンスとの間で、パッケージをインポートすることも、エクスポートすることもできません。  
  
 次の手順では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してパッケージをインポートまたはエクスポートする方法について説明します。  
  
### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してパッケージをインポートするには  
  
1.  **[スタート]** ボタンをクリックし、 **[Microsoft** ][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をポイントして、 **[SQL Server Management Studio]** をクリックします。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、次のオプションを設定します。  
  
    -   **[サーバーの種類]** ボックスの一覧の **[Integration Services]** をクリックします。  
  
    -   **[サーバー名]** ボックスでサーバー名を入力するか、 **[\<参照...>]** をクリックして使用するサーバーを見つけます。  
  
3.  オブジェクト エクスプローラーが開いていない場合は、 **[表示]** メニューの **[オブジェクト エクスプローラー]** をクリックします。  
  
4.  オブジェクト エクスプローラーで、 **[格納されたパッケージ]** フォルダーを展開します。  
  
5.  サブフォルダーを展開し、パッケージのインポート先のフォルダーを探します。  
  
6.  フォルダーを右クリックし、 **[パッケージのインポート]** をクリックして、 次のいずれかの操作を行います。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスからインポートするには、 **[SQL Server]** をクリックし、サーバーを指定して認証モードを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を選択した場合は、ユーザー名とパスワードを指定します。  
  
         参照ボタン **[...]** をクリックし、インポートするパッケージを選択します。次に、 **[OK]** をクリックします。  
  
    -   ファイル システムからインポートするには、 **[ファイル システム]** をクリックします。  
  
         参照ボタン **[...]** をクリックし、インポートするパッケージを選択します。次に、 **[開く]** をクリックします。  
  
    -   [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアからインポートするには、 **[SSIS パッケージ ストア]** をクリックし、サーバーを指定します。  
  
         参照ボタン **[...]** をクリックし、インポートするパッケージを選択します。次に、 **[OK]** をクリックします。  
  
7.  必要に応じて、パッケージ名を更新します。  
  
8.  パッケージの保護レベルを更新するには、参照ボタン **[...]** をクリックし、 **[パッケージの保護レベル]** ダイアログ ボックスで別の保護レベルを選択します。 **[機微なデータをパスワードで暗号化する]** または **[すべてのデータをパスワードで暗号化する]** をクリックした場合は、パスワードを入力して確認します。  
  
9. **[OK]** をクリックすると、インポートが完了します。  
  
### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してパッケージをエクスポートするには  
  
1.  **[スタート]** ボタンをクリックし、 **[Microsoft** ][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をポイントして、 **[SQL Server Management Studio]** をクリックします。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、次のオプションを設定します。  
  
    -   **[サーバーの種類]** ボックスの一覧の **[Integration Services]** をクリックします。  
  
    -   **[サーバー名]** ボックスでサーバー名を入力するか、 **[\<参照...>]** をクリックして使用するサーバーを見つけます。  
  
3.  オブジェクト エクスプローラーが開いていない場合は、 **[表示]** メニューの **[オブジェクト エクスプローラー]** をクリックします。  
  
4.  オブジェクト エクスプローラーで、 **[格納されたパッケージ]** フォルダーを展開します。  
  
5.  サブフォルダーを展開し、エクスポートするパッケージを探します。  
  
6.  パッケージを右クリックして **[エクスポート]** をクリックし、次のいずれかの操作を行います。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスにエクスポートするには、 **[SQL Server]** をクリックし、サーバーを指定して認証モードを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を選択した場合は、ユーザー名とパスワードを指定します。  
  
         参照ボタン **[...]** をクリックして **[SSIS パッケージ]** フォルダーを展開し、パッケージを保存するフォルダーを探します。 必要に応じて、パッケージの既定の名前を更新し、 **[OK]** をクリックします。  
  
    -   ファイル システムにエクスポートするには、 **[ファイル システム]** をクリックします。  
  
         参照ボタン **[...]** をクリックし、パッケージのエクスポート先のフォルダーを探します。次に、パッケージ ファイルの名前を入力して **[保存]** をクリックします。  
  
    -   [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアにエクスポートするには、 **[SSIS パッケージ ストア]** をクリックしてサーバーを指定します。  
  
         参照ボタン **[...]** をクリックして **[SSIS パッケージ]** フォルダーを展開し、パッケージを保存するフォルダーを選択します。 必要に応じて、パッケージの新しい名前を **[パッケージ名]** テキスト ボックスに入力します。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  パッケージの保護レベルを更新するには、参照ボタン **[...]** をクリックし、 **[パッケージの保護レベル]** ダイアログ ボックスで別の保護レベルを選択します。 **[機微なデータをパスワードで暗号化する]** または **[すべてのデータをパスワードで暗号化する]** をクリックした場合は、パスワードを入力して確認します。  
  
8.  **[OK]** をクリックすると、エクスポートが完了します。  

## <a name="import-package-dialog-box-ui-reference"></a>[パッケージのインポート] ダイアログ ボックスの UI リファレンス
  **の** [パッケージのインポート] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ダイアログ ボックスを使用すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージをインポートしたり、パッケージの保護レベルの設定や変更を行ったりできます。  
  
### <a name="options"></a>オプション  
 **[パッケージの場所]**  
 パッケージをインポートする格納場所の種類を選択します。 使用できるオプションは以下のとおりです。  
  
 **SQL Server**  
  
 **[ファイル システム]**  
  
 **[SSIS パッケージ ストア]**  
  
 **[サーバー]**  
 サーバー名を入力するか、サーバーを一覧から選択します。  
  
 **[認証]**  
 Windows 認証または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を選択します。 このオプションは、格納場所が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の場合のみ使用できます。  
  
> [!IMPORTANT]  
>  可能であれば、Windows 認証を使用します。  
  
 **認証の種類**  
 認証の種類を選択します。  
  
 **User name**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、ユーザー名を指定します。  
  
 **パスワード**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、パスワードを指定します。  
  
 **[パッケージのパス]**  
 パッケージのパスを入力するか、参照ボタン **[...]** をクリックしてパッケージを指定します。  
  
 **パッケージ名**  
 オプションでパッケージの名前を変更できます。 既定の名前は、インポートするパッケージの名前です。  
  
 **保護レベル**  
 参照ボタン **[...]** をクリックし、 **[パッケージの保護レベル]** ダイアログ ボックスで保護レベルを更新します。 詳細については、「 [[パッケージの保護レベル] ダイアログ ボックス](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog)」を参照してください。  

## <a name="export-package-dialog-box-ui-reference"></a>[パッケージのエクスポート] ダイアログ ボックスの UI リファレンス
  **の** [パッケージのエクスポート] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ダイアログ ボックスを使用すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを別の場所にエクスポートしたり、必要に応じてパッケージの保護レベルを変更したりできます。  
  
### <a name="options"></a>オプション  
 **[パッケージの場所]**  
 パッケージをエクスポートする格納場所の種類を選択します。 使用できるオプションは以下のとおりです。  
  
 **SQL Server**  
  
 **[ファイル システム]**  
  
 **[SSIS パッケージ ストア]**  
  
 **[サーバー]**  
 サーバー名を入力するか、サーバーを一覧から選択します。  
  
 **[認証]**  
 Windows 認証または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を選択します。 このオプションは、格納場所が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の場合のみ使用できます。  
  
> [!IMPORTANT]  
>  可能であれば、Windows 認証を使用します。  
  
 **認証の種類**  
 認証の種類を選択します。  
  
 **User name**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、ユーザー名を指定します。  
  
 **パスワード**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、パスワードを指定します。  
  
 **[パッケージのパス]**  
 パッケージのパスを入力するか、参照ボタン **[...]** をクリックしてパッケージを格納するフォルダーを指定します。  
  
 **保護レベル**  
 参照ボタン **[...]** をクリックして、 **[パッケージの保護レベル]** ダイアログ ボックスで保護レベルを更新します。 詳細については、「 [[パッケージの保護レベル] ダイアログ ボックス](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog)」を参照してください。  

## <a name="back-up-and-restore-packages"></a>パッケージのバックアップと復元
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、ファイル システムや [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム データベースの msdb に保存できます。 msdb に保存されたパッケージは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップおよび復元機能を使用してバックアップおよび復元できます。  
  
 msdb データベースのバックアップおよび復元の詳細については、次のトピックのいずれかを参照してください。  
  
-   [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [システム データベースのバックアップと復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージの管理に使用する **dtutil** コマンド プロンプト ユーティリティ (dtutil.exec) が付属しています。 詳細については、「 [dtutil ユーティリティ](../../integration-services/dtutil-utility.md)」を参照してください。  
  
### <a name="configuration-files"></a>構成ファイル  
 パッケージに含まれるすべての構成ファイルはファイル システムに格納されています。 msdb データベースをバックアップするとき、これらのファイルはバックアップされません。したがって、msdb に保存されたパッケージの安全を確保するための計画の一部として、構成ファイルを定期的にバックアップする必要があります。 msdb データベースのバックアップに構成を含めるには、ファイル ベースの構成の代わりに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の構成の種類の使用を検討してください。  
  
### <a name="packages-stored-in-the-file-system"></a>ファイル システムに保存されたパッケージ  
 サーバーのファイル システムのバックアップ計画には、ファイル システムに保存されるパッケージのバックアップも含める必要があります。 既定で MsDtsSrvr.ini.xml という名前を持つ [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービス構成ファイルには、このサービスで監視されるサーバー上のフォルダーが定義されています。 これらのフォルダーを必ずバックアップしてください。 さらに、パッケージをサーバー上の他のフォルダーに格納している場合は、これらのフォルダーもバックアップに含める必要があります。  

## <a name="see-also"></a>参照  
 [Integration Services サービス (SSIS サービス)](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  
