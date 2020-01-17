---
title: パッケージの保存および実行 (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b1275f5cbb718f34ba1386d6d6313dd662901900
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284939"
---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>[パッケージの保存および実行]\(SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  データ ソースと宛先を指定して構成すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードによって **[パッケージの保存および実行]** が表示されます。 このページでは、コピー操作をすぐに実行するかどうかを指定します。 構成によっては、設定を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) パッケージとして保存して、それをカスタマイズし、後から再利用することができます。
  
**パッケージとは** ウィザードは SQL Server Integration Services (SSIS) を使用してデータをコピーします。 SSIS での基本単位はパッケージです。 ウィザードのページを進みながらオプションを指定すると、SSIS パッケージがメモリに作成されます。
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>[パッケージの保存および実行] ページのスクリーン ショット  
次のスクリーン ショットは、ウィザードの **[パッケージの保存および実行]** ページを示しています。 
   
![インポートおよびエクスポート ウィザードの [パッケージ] ページの保存と実行](../../integration-services/import-export-data/media/save-and-run.png "インポートおよびエクスポート ウィザードの [パッケージ] ページの保存と実行") 
  
## <a name="run-and-save-the-package"></a>パッケージの実行および保存 
 次に進むには、次の 2 つのオプションから少なくとも 1 つを選択する必要があります。  
  
 **Run immediately**  
 データのインポートとエクスポートをすぐに行うには、このオプションを選択します。 既定では、このチェック ボックスはオンになっており、操作はすぐに実行されます。
  
 **SSIS パッケージの保存**  
 設定を SSIS パッケージとして保存します。 後から、必要に応じてパッケージをカスタマイズして再実行できます。 パッケージの保存を選択すると、次のページ **[SSIS パッケージの保存]** にさらにオプションが表示されます。
 
パッケージを保存するオプションを選択できるのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition 以上のエディションをインストールしている場合のみです。   
  
> [!NOTE]
> ウィザードを終了し、操作を実行したが、実行が完了する前に操作が停止した場合は、 **[SSIS パッケージの保存]** チェック ボックスをオンにしていても、パッケージは保存されません。  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>Visual Studio からウィザードを起動した場合
SQL Server Data Tools (SSDT) がインストールされている Visual Studio で Integration Services プロジェクトからウィザードを起動した場合:
-   ウィザードを終了しないとパッケージを**実行**できません。 その場合、Visual Studio からパッケージを実行できます。
-   ウィザードを開始した Integration Services プロジェクトにパッケージが**保存**されます。

## <a name="specify-options-for-saving-the-package"></a>パッケージを保存する場合のオプションを指定する
**SQL Server**  
 このオプションを選択して、SQL Server で **msdb** データベースの **sysssispackages** テーブルにパッケージを保存します。
 
> [!IMPORTANT]
> このオプションでは、SSIS カタログ データベース (SSISDB) にパッケージを保存できません。  

 ターゲット サーバーを選択し、サーバーに接続するための資格情報を次のページ **[SSIS パッケージの保存]** で指定します。 詳細については、「 [[SSIS パッケージの保存] (SQL Server インポートおよびエクスポート ウィザード)](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)」を参照してください。  
  
 **ファイル システム**  
 **.dtsx** 拡張子を持つファイルとしてパッケージを保存するには、このオプションを選択します。  
  
 パッケージの対象フォルダーとファイル名を、次のページ **[SSIS パッケージの保存]** で選択します。 詳細については、「 [[SSIS パッケージの保存] (SQL Server インポートおよびエクスポート ウィザード)](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)」を参照してください。  
 
 ## <a name="specify-the-package-protection-level"></a>パッケージの保護レベルを指定する
 **パッケージの保護レベル**  
 パッケージのデータを保護するために、リストから保護レベルを選択します。  
  
 保護レベルによって、パッケージ保護の方法、パスワードまたはユーザー キー、適用範囲が決定されます。 保護対象には、すべてのデータを含めることも機密データのみを含めることもできます。 使用可能なオプションの詳細については、「 [パッケージ内の機微なデータへのアクセス制御](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)」を参照してください。  
  
 **パスワード**  
 パスワードを入力します。  
  
 **パスワードの再入力**  
 パスワードを再度入力します。  
  
> [!NOTE]
> このパスワード オプションは、パスワードが必要な **[パッケージの保護レベル]** を指定した場合 (つまり、 **[機微なデータをパスワードで暗号化する]** または **[すべてのデータをパスワードで暗号化する]** を指定した場合) にのみ使用できます。  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>パッケージを保存するためのオプションの 2 つのページについて  
 **[パッケージの保存および実行]** ページは、SSIS パッケージを保存するためのオプションを選択する 2 つのページの 1 つです。  
  
-   現在のページで、SQL Server またはファイルのどちらにパッケージを保存するかを選択します。 保存されたパッケージのセキュリティ設定も選択します。  
  
-   次に、 **[SSIS パッケージの保存]** ページで、パッケージの名前および保存場所に関する詳細情報を指定します。 詳細については、「 [[SSIS パッケージの保存] (SQL Server インポートおよびエクスポート ウィザード)](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)」を参照してください。  
  
 これらのオプションを使用できるのは、このページで **[SSIS パッケージの保存]** オプションを選択する場合のみです。  
  
## <a name="whats-next"></a>次の操作  
 コピー操作をすぐに実行するかどうかと、パッケージを保存するかどうかを指定した場合は、選択したオプションに応じて次のページが変わります。  
  
-   パッケージをすぐに実行することを選択した場合、次のページは **[ウィザードの完了]** です。 このページでは、ウィザードで選択した内容を確認し、コピー操作を開始します。 詳細については、「 [[ウィザードの完了] (SQL Server インポートおよびエクスポート ウィザード)](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)」を参照してください。  
  
-   パッケージを保存するオプションを選択した場合、次のページは **[SSIS パッケージの保存]** です。 このページでは、パッケージを保存するための追加オプションを指定します。 (パッケージを保存すると、その後のページは **[ウィザードの完了]** になります。)詳細については、「[[SSIS パッケージの保存] (SQL Server インポートおよびエクスポート ウィザード)](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[パッケージを保存する](../../integration-services/save-packages.md)  
[Integration Services (SSIS) パッケージの実行](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  

