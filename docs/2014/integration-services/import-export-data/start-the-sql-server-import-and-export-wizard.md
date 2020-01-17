---
title: 実行の SQL Server インポートおよびエクスポート ウィザード |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 824642cf50923aa7ec879bfedbbb8f4ceaa6d9f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768034"
---
# <a name="run-the-sql-server-import-and-export-wizard"></a>SQL Server インポートおよびエクスポート ウィザードを実行する
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを使用すると、最も簡単な方法でデータ ソース間でデータをコピーしたり、基本パッケージを構築したりすることができます。 ウィザードの詳細については、次を参照してください。 [SQL Server インポートおよびエクスポート ウィザード](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)します。  
  
 SQL Server インポートおよびエクスポート ウィザードを使用して、SQL Server データベースから Microsoft Excel スプレッドシートにデータをエクスポートするパッケージを作成する方法を示すビデオは、次を参照してください。 [Excel (SQL Server ビデオ) への SQL Server データのエクスポート](https://go.microsoft.com/fwlink/?LinkId=131024)します。  
  
### <a name="to-start-the-sql-server-import-and-export-wizard"></a>SQL Server インポートおよびエクスポート ウィザードを起動するには  
  
-   **開始**メニューで、**すべてのプログラム**、 をポイント**Microsoft SQL Server** 、順にクリックします**データ インポートおよびエクスポート**します。  
  
     \- または -  
  
     [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]を右クリックし、 **SSIS パッケージ**フォルダー、およびクリック**SSISImport およびエクスポート ウィザード**します。  
  
     \- または -  
  
     [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]の**プロジェクト** メニューのをクリックして**SSISImport およびエクスポート ウィザード**します。  
  
     \- または -  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]への接続、[!INCLUDE[ssDE](../../includes/ssde-md.md)]サーバーの種類のデータベースを展開し、データベースを右クリックをポイントして**タスク**、 をクリックし、**データのインポート**または**データをエクスポート**.  
  
     \- または -  
  
     コマンド プロンプト ウィンドウで、C:\Program Files\Microsoft SQL Server\100\DTS\Binn にある DTSWizard.exe を実行します。  
  
    > [!NOTE]  
    >  64 ビット コンピューターには、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって 64 ビット版の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザード (DTSWizard.exe) がインストールされます。 ただし、Access や Excel など、一部のデータ ソースは、32 ビット プロバイダーでしか使用できません。 これらのデータ ソースを操作するには、32 ビット版のウィザードをインストールして実行することが必要になる場合があります。 32 ビット版のウィザードをインストールするには、セットアップ中に [クライアント ツール] または [[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]] を選択します。  
  
### <a name="to-import-or-export-data-by-using-the-sql-server-import-and-export-wizard"></a>SQL Server インポートおよびエクスポート ウィザードを使用してデータをインポートまたはエクスポートするには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを起動します。  
  
2.  対応するウィザード ページで、データの変換元とデータの変換先を選択します。  
  
     利用できるデータの変換元は、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダー、OLE DB プロバイダー、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client プロバイダー、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] プロバイダー、Microsoft Office Excel、Microsoft Office Access およびフラット ファイル ソースです。 変換元に応じて、認証モード、サーバー名、データベース名、ファイル形式などのオプションを設定します。  
  
    > [!NOTE]  
    >  [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Oracle では、Oracle BLOB、CLOB、NCLOB、BFILE、および UROWID のデータ型はサポートされません。 したがって、OLE DB ソースで、これらのデータ型を使用する列が含まれるテーブルからデータを抽出することはできません。  
  
     利用できるデータの変換先は、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダー、OLE DB プロバイダー、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client、Excel、Access およびフラット ファイル変換先です。  
  
3.  選択した変換先の種類に対応するオプションを設定します。  
  
     変換先が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの場合、次のように指定できます。  
  
    -   新しいデータベースを作成してデータベース プロパティを設定するかどうかを指定します。 次のプロパティは構成できません。ウィザードは指定の既定値を使用します。  
  
        |プロパティ|値|  
        |--------------|-----------|  
        |照合順序|Latin1_General_CS_AS_KS_WS|  
        |復旧モデル|[完全]|  
        |フルテキスト インデックスを使用する|True|  
  
    -   テーブルまたはビューのデータをコピーするか、またはクエリ結果をコピーするかを選択します。  
  
         変換元のデータに対してクエリを実行し、その結果をコピーするには、Transact-SQL クエリを作成できます。 Transact-SQL クエリは、手動で入力するか、またはファイルに保存されたクエリを使用できます。 ウィザードにはファイルを探す参照機能があり、ファイルを選択すると、ウィザードは自動的にファイルを開き、その内容をウィザード ページに貼り付けます。  
  
         変換元が [!INCLUDE[vstecado](../../includes/vstecado-md.md)] プロバイダーの場合は、DBCommand 文字列をクエリとして提供し、クエリ結果をコピーするオプションも使用できます。  
  
         変換元のデータがビューの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードでは、変換先でビューがテーブルに自動的に変換されます。  
  
    -   変換先テーブルを削除して再作成するかどうか、および ID 挿入を許可するかどうかを示します。  
  
    -   既存の変換先テーブルの行を削除するか、または行を追加するかを示します。 テーブルが存在しない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードは自動的にテーブルを作成します。  
  
     変換先がフラット ファイル変換先の場合、次のように指定できます。  
  
    -   変換先ファイルの行区切り記号を指定します。  
  
    -   変換先ファイルの列区切り記号を指定します。  
  
4.  (省略可) テーブルを 1 つ選択して変換元列と変換先列間のマッピングを変更するか、または変換先列のメタデータを変更します。  
  
    -   変換元列を別の変換先列にマップします。  
  
    -   変換先列のデータ型を変更します。  
  
    -   文字データ型の列の長さを設定します。  
  
    -   数値データ型の列の有効桁数と小数点以下桁数を設定します。  
  
    -   列が null 値を含めるかどうかを指定します。  
  
5.  (省略可) 複数のテーブルを選択して、これらのテーブルに適用されるメタデータおよびオプションを更新します。  
  
    -   既存の変換先スキーマを選択するか、テーブルを割り当てる新しいスキーマを提供します。  
  
    -   変換先テーブルの ID 挿入を許可するかどうかを指定します。  
  
    -   変換先テーブルを削除して再作成するかどうかを指定します。  
  
    -   既存の変換先テーブルを切り捨てるかどうかを指定します。  
  
6.  保存し、パッケージを実行します。  
  
     ウィザードを [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] またはコマンド プロンプトから起動した場合、パッケージはすぐに実行されます。 パッケージを保存することができます必要に応じて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**データベースまたはファイル システム。 詳細については、 **msdb**データベースを参照してください[Package Management &#40;SSIS サービス&#41;](../service/package-management-ssis-service.md)します。  
  
     パッケージを保存する際に、パッケージの保護レベルを設定し、パスワードを使用する保護レベルの場合はパスワードを指定できます。 パッケージの保護レベルの詳細については、次を参照してください。[パッケージ内の機密データのアクセス制御](../security/access-control-for-sensitive-data-in-packages.md)します。  
  
     ウィザードを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] プロジェクトから起動した場合、ウィザードからパッケージを実行することはできません。 代わりに、ウィザードを起動した [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトにパッケージが追加されます。 パッケージは、その後、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] で実行できます。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]、ウィザードによって作成されたパッケージを保存するオプションは使用できません。  
  
## <a name="see-also"></a>参照  
 [SQL Server インポートおよびエクスポート ウィザード](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [SQL Server データ ツールでのパッケージの作成](../create-packages-in-sql-server-data-tools.md)  
  
  
