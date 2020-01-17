---
title: インポートおよびエクスポート パッケージ (SSIS サービス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], importing
- packages [Integration Services], exporting
- importing packages
- exporting packages
ms.assetid: ef18ec11-b536-47d9-abd1-794099f43486
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a1d50afde56843942c470017a8534ffa797eb69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058151"
---
# <a name="import-and-export-packages-ssis-service"></a>パッケージをインポートおよびエクスポートする (SSIS サービス)
    
> [!IMPORTANT]  
>  このトピックでは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを管理するための Windows サービスである [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスについて説明します。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] では、以前のリリースの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]との互換性を維持するために、このサービスをサポートしています。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]以降では、Integration Services サーバー上のパッケージなどのオブジェクトを管理できます。  
  
 パッケージは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb データベースの sysssispackages テーブルまたはファイル システムに保存できます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスによって監視および管理される論理ストレージであるパッケージ ストアには、msdb データベースと、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスの構成ファイルに指定されているファイル システム フォルダーの両方を格納できます。  
  
 パッケージは、次の種類のストレージ間でインポートおよびエクスポートできます。  
  
-   ファイル システム上の任意の場所にあるファイル システム フォルダー。  
  
-   SSIS パッケージ ストア内のフォルダー。 [ファイル システム] と [MSDB] の 2 つの既定のフォルダーがあります。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb データベース。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、パッケージをインポートおよびエクスポートできます。これは、パッケージの保存形式と位置が変わることを意味します。 インポートおよびエクスポート機能を使用すると、ファイル システム、パッケージ ストア、または msdb データベースにパッケージを追加したり、いずれかの保存形式から別の保存形式にパッケージをコピーしたりできます。 たとえば、msdb に保存されているパッケージをファイル システムにコピーしたり、その逆の操作を行うことができます。  
  
 **dtutil** コマンド プロンプト ユーティリティ (dtutil.exe) を使用してパッケージを別の形式にコピーすることもできます。 詳細については、「[dtutil ユーティリティ](dtutil-utility.md)」を参照してください。  
  
## <a name="to-import-or-export-a-package"></a>パッケージをインポートまたはエクスポートするには  
  
> [!IMPORTANT]  
>  このトピックでは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] に含まれている [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]サービスについて説明します。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] との互換性を維持するために、 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]サービスをサポートしています。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] でのパッケージ管理の詳細については、「[Integration Services (SSIS) Server](catalog/integration-services-ssis-server-and-catalog.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージは、次の場所からインポートしたり、次の場所にエクスポートしたりできます。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンス、ファイル システム、または [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストアに格納されているパッケージをインポートできます。 インポートしたパッケージは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、または [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストア内のフォルダーに保存されます。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンス、ファイル システム、または [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストアに格納されているパッケージを異なるストレージ形式および場所にエクスポートできます。  
  
 ただし、異なるバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 間でパッケージをインポートおよびエクスポートするには、いくつかの制限があります。  
  
-   [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] のインスタンスでは、[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] のインスタンスからパッケージをインポートできますが、[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] のインスタンスにパッケージをエクスポートすることはできません。  
  
-   [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] のインスタンスでは、[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] のインスタンスとの間で、パッケージをインポートすることも、エクスポートすることもできません。  
  
 次の手順では、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を使用してパッケージをインポートまたはエクスポートする方法について説明します。  
  
#### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してパッケージをインポートするには  
  
1.  **[スタート]** ボタンをクリックし、 **[Microsoft** ][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をポイントして、 **[SQL Server Management Studio]** をクリックします。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、次のオプションを設定します。  
  
    -   **[サーバーの種類]** ボックスの一覧の **[Integration Services]** をクリックします。  
  
    -   **[サーバー名]** ボックスでサーバー名を入力するか、 **[\<参照...>]** をクリックして使用するサーバーを見つけます。  
  
3.  オブジェクト エクスプローラーが開いていない場合は、 **[表示]** メニューの **[オブジェクト エクスプローラー]** をクリックします。  
  
4.  オブジェクト エクスプローラーで、 **[格納されたパッケージ]** フォルダーを展開します。  
  
5.  サブフォルダーを展開し、パッケージのインポート先のフォルダーを探します。  
  
6.  フォルダーを右クリックし、 **[パッケージのインポート]** をクリックして、 次のいずれかの操作を行います。  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスからインポートするには、 **[SQL Server]** をクリックし、サーバーを指定して認証モードを選択します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を選択した場合は、ユーザー名とパスワードを指定します。  
  
         参照ボタン **[...]** をクリックし、インポートするパッケージを選択します。次に、 **[OK]** をクリックします。  
  
    -   ファイル システムからインポートするには、 **[ファイル システム]** をクリックします。  
  
         参照ボタン **[...]** をクリックし、インポートするパッケージを選択します。次に、 **[開く]** をクリックします。  
  
    -   [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストアからインポートするには、 **[SSIS パッケージ ストア]** をクリックし、サーバーを指定します。  
  
         参照ボタン **[...]** をクリックし、インポートするパッケージを選択します。次に、 **[OK]** をクリックします。  
  
7.  必要に応じて、パッケージ名を更新します。  
  
8.  パッケージの保護レベルを更新するには、参照ボタン **[...]** をクリックし、 **[パッケージの保護レベル]** ダイアログ ボックスで別の保護レベルを選択します。 **[機微なデータをパスワードで暗号化する]** または **[すべてのデータをパスワードで暗号化する]** をクリックした場合は、パスワードを入力して確認します。  
  
9. **[OK]** をクリックすると、インポートが完了します。  
  
#### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してパッケージをエクスポートするには  
  
1.  **[スタート]** ボタンをクリックし、 **[Microsoft** ][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をポイントして、 **[SQL Server Management Studio]** をクリックします。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、次のオプションを設定します。  
  
    -   **[サーバーの種類]** ボックスの一覧の **[Integration Services]** をクリックします。  
  
    -   **[サーバー名]** ボックスでサーバー名を入力するか、 **[\<参照...>]** をクリックして使用するサーバーを見つけます。  
  
3.  オブジェクト エクスプローラーが開いていない場合は、 **[表示]** メニューの **[オブジェクト エクスプローラー]** をクリックします。  
  
4.  オブジェクト エクスプローラーで、 **[格納されたパッケージ]** フォルダーを展開します。  
  
5.  サブフォルダーを展開し、エクスポートするパッケージを探します。  
  
6.  パッケージを右クリックして **[エクスポート]** をクリックし、次のいずれかの操作を行います。  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスにエクスポートするには、 **[SQL Server]** をクリックし、サーバーを指定して認証モードを選択します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を選択した場合は、ユーザー名とパスワードを指定します。  
  
         参照ボタン **[...]** をクリックして **[SSIS パッケージ]** フォルダーを展開し、パッケージを保存するフォルダーを探します。 必要に応じて、パッケージの既定の名前を更新し、 **[OK]** をクリックします。  
  
    -   ファイル システムにエクスポートするには、 **[ファイル システム]** をクリックします。  
  
         参照ボタン **[...]** をクリックし、パッケージのエクスポート先のフォルダーを探します。次に、パッケージ ファイルの名前を入力して **[保存]** をクリックします。  
  
    -   [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストアにエクスポートするには、 **[SSIS パッケージ ストア]** をクリックしてサーバーを指定します。  
  
         参照ボタン **[...]** をクリックして **[SSIS パッケージ]** フォルダーを展開し、パッケージを保存するフォルダーを選択します。 必要に応じて、パッケージの新しい名前を **[パッケージ名]** テキスト ボックスに入力します。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  パッケージの保護レベルを更新するには、参照ボタン **[...]** をクリックし、 **[パッケージの保護レベル]** ダイアログ ボックスで別の保護レベルを選択します。 **[機微なデータをパスワードで暗号化する]** または **[すべてのデータをパスワードで暗号化する]** をクリックした場合は、パスワードを入力して確認します。  
  
8.  **[OK]** をクリックすると、エクスポートが完了します。  
  
## <a name="see-also"></a>関連項目  
 [パッケージの管理 &#40;SSIS サービス&#41;](service/package-management-ssis-service.md)  
  
  
