---
title: '[SSIS パッケージの保存] (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 63cc8413175555e37a29caf288a72815824c3778
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296260"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>[SSIS パッケージの保存]\(SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[パッケージの保存および実行]** ページで、設定を SQL Server Integration Services (SSIS) パッケージとして保存することを指定した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードは **[SSIS パッケージの保存]** を表示します。 このページでは、ウィザードで作成されたパッケージを保存するための追加オプションを指定します。  

**[SSIS パッケージの保存]** ページに表示されるオプションは、SQL Server またはファイル システムにパッケージを保存するために **[パッケージの保存および実行]** ページで以前に行った選択によって異なります。 **[パッケージの保存および実行]** ページについては、「 [Save and Run Package](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)」 ([パッケージの保存および実行]) を参照してください。
 
**パッケージとは** ウィザードは SQL Server Integration Services (SSIS) を使用してデータをコピーします。 SSIS での基本単位はパッケージです。 ウィザードのページを進みながらオプションを指定すると、SSIS パッケージがメモリに作成されます。

## <a name="screen-shot---common-options"></a>スクリーン ショット - 共通オプション
次のスクリーンショットは、ウィザードの **[SSIS パッケージの保存]** ページの最初の部分を示しています。 ページの残りの部分には、選択したパッケージの保存先に応じて変わるさまざまなオプションがあります。

![パッケージの保存 - 共通オプション](../../integration-services/import-export-data/media/save-package-common-options.png)

## <a name="provide-a-name-and-description-for-the-package"></a>パッケージの名前と説明を指定します。  
 **[名前]**  
 パッケージの一意な名前を指定します。  
  
 **[説明]**  
 パッケージの説明を指定します。 パッケージを見るだけでその内容がわかり、保守が容易になるように、パッケージの目的について記述することをお勧めします。  
  
 **移行先**  
 パッケージに対して以前に指定した保存先です ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはファイル システム)。 別の保存先にパッケージを保存する場合は、 **[パッケージの保存および実行]** ページに戻ります。

## <a name="screen-shot---save-the-package-in-sql-server"></a>スクリーン ショット - SQL Server にパッケージを保存する

 次のスクリーンショットは、 **[パッケージの保存および実行]** ページで **[SQL Server]** を選択した場合のウィザードの **[SSIS パッケージの保存]** ページです。 
  
![インポートおよびエクスポート ウィザードの [SSIS パッケージの保存] ページ](../../integration-services/import-export-data/media/save-package2.png "インポートおよびエクスポート ウィザードの [SSIS パッケージの保存] ページ")  

## <a name="options-to-specify-target--sql-server"></a>指定するオプション (ターゲット = SQL Server) 

 > [!NOTE]
 > ウィザードは、**msdb** データベースの **sysssispackages** テーブルにパッケージを保存します。 このオプションでは、SSIS カタログ データベース (SSISDB) にパッケージを保存**できません**。  
 
 **サーバー名**  
 保存先のサーバー名を入力または選択します。  
   
 **Windows 認証を使用する**  
Windows 統合認証を使用してサーバーに接続します。 これは、推奨される認証方法です。  
  
 **SQL Server 認証を使用する**  
SQL Server 認証を使用してサーバーに接続します。  
  
 **User name**  
SQL Server 認証を指定した場合は、ユーザー名を入力します。  
  
 **パスワード**  
SQL Server 認証を指定した場合は、パスワードを入力します。  
    
## <a name="screen-shot---save-the-package-in-the-file-system"></a>スクリーン ショット - ファイル システムにパッケージを保存する
 
次のスクリーンショットは、 **[パッケージの保存および実行]** ページで **[ファイル システム]** を選択した場合のウィザードの **[SSIS パッケージの保存]** ページです。 
  
![インポートおよびエクスポート ウィザードの [SSIS パッケージの保存] ページ](../../integration-services/import-export-data/media/save-package1.png "インポートおよびエクスポート ウィザードの [SSIS パッケージの保存] ページ")  

## <a name="options-to-specify-target--file-system"></a>指定するオプション (ターゲット = ファイル システム)

 **[ファイル名]**  
 保存先ファイルのパスとファイル名を入力するか、 **[参照]** ボタンを使用して保存先を指定します。  
  
> [!TIP]
> 保存先フォルダーは、入力するか参照して、必ず指定してください。 ファイル名のみを入力し、パスを入力しないと、ウィザードがパッケージをどこに保存するかわかりません。 また、ウィザードはユーザーがファイル保存権限を持っていない場所にパッケージを保存しようとして、エラーが発生する可能性があります。  
>   
>  パッケージ ファイルの保存場所を忘れないでください。  
  
 **[参照]**  
 必要に応じて、 **[パッケージの保存]** ダイアログ ボックスで保存先ファイルのパスを参照して選択します。  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>パッケージを保存するためのオプションの 2 つのページについて  
 **[SSIS パッケージの保存]** ページは、SSIS パッケージを保存するためのオプションを選択する 2 つのページの 1 つです。  
  
-   前の **[パッケージの保存および実行]** ページでは、SQL Server またはファイルのどちらにパッケージを保存するかを選択します。 保存されたパッケージのセキュリティ設定も選択します。 **[パッケージの保存および実行]** ページについては、「 [Save and Run Package](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)」 ([パッケージの保存および実行]) を参照してください。  
  
-   このページでは、パッケージの名前および保存場所に関する詳細情報を指定します。  
 
## <a name="run-the-saved-package-again-later"></a>保存したパッケージを後で再び実行する  
 保存したパッケージを後で再び実行する方法については、以下のトピックを参照してください。  
  
-   使い慣れたユーティリティ プログラムを使用してパッケージを実行するには、「[パッケージ実行ユーティリティ (DtExecUI) の UI リファレンス](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)」を参照してください。  
  
-   コマンドラインまたはバッチ ファイルからパッケージを実行するには、「 [dtexec ユーティリティ](../../integration-services/packages/dtexec-utility.md)」を参照してください。  
  
-   SQL Server の **msdb** データベースにパッケージを保存した場合は、Integration Services サービスに接続します。 次に、SQL Server Management Studio のオブジェクト エクスプローラーで **[格納済みパッケージ]、[MSDB]** に移動し、パッケージを右クリックして、 **[パッケージの実行]** を選択します。

-   ファイル システムにパッケージを保存した場合、開発環境でパッケージを実行するには、「 [Integration Services (SSIS) パッケージの実行](../../integration-services/packages/run-integration-services-ssis-packages.md) 」を参照してください。 パッケージを開いて実行する前に、パッケージを Integration Services プロジェクトに追加する必要があります。  

## <a name="customize-the-saved-package"></a>保存されたパッケージをカスタマイズする  
 保存されたパッケージをカスタマイズする方法については、「[Integration Services (SSIS) パッケージ](../../integration-services/integration-services-ssis-packages.md)」を参照してください。  
  
## <a name="whats-next"></a>次の操作  
 パッケージ保存の追加オプションを指定した後、次のページは **[ウィザードの完了]** です。 このページでは、ウィザードで選択した内容を確認し、操作を開始します。 詳細については、「 [[ウィザードの完了] (SQL Server インポートおよびエクスポート ウィザード)](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)」を参照してください。  
 
## <a name="see-also"></a>参照  
[パッケージを保存する](../../integration-services/save-packages.md)  
[Integration Services (SSIS) パッケージの実行](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 
