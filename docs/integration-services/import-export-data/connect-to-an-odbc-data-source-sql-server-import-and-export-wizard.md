---
title: ODBC データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
description: SQL Server インポートおよびエクスポート ウィザードで使用する目的で ODBC DSN を構成するか、ODBC 接続文字列を作成する方法
ms.custom: ''
ms.date: 12/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2b9979f7d82ef153ed3c447b5d47bf7424ca9443
ms.sourcegitcommit: ab7209b5856537bfef0a6e9d0527d9002bd0a528
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75608031"
---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>ODBC データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このトピックでは、SQL Server インポートおよびエクスポート ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページから **ODBC** データ ソースに接続する方法を説明します。

Microsoft またはサード パーティから必要な ODBC ドライバーをダウンロードすることが必要な場合があります。

また、指定する必要がある必要な接続情報を調べることも必要な場合があります。 このサード パーティのサイト「[The Connection Strings Reference](https://www.connectionstrings.com/)」(接続文字列リファレンス) には、接続文字列のサンプルと、データ プロバイダーおよび必要な接続情報に関する詳細な情報が記載されています。

## <a name="make-sure-the-driver-you-want-is-installed"></a>必要なドライバーがインストールされていることを確認する
1.  スタート メニューまたはコントロール パネルの **[ODBC データ ソース (64 ビット)]** アプレットを検索または参照します。 32 ビット ドライバーしかない場合、または 32 ビット ドライバーを使う必要があることがわかっている場合は、代わりに **[ODBC データ ソース (32 ビット)]** を検索または参照します。
2.  アプレットを起動します。 **[ODBC データ ソース アドミニストレーター]** ウィンドウが開きます。
3.  **[ドライバー]** タブで、お使いのコンピューターにインストールされているすべての ODBC ドライバーの一覧を見ることができます (一部のドライバーの名前は、複数の言語で表示される場合があります)。

    インストールされている 64 ビット ドライバーの一覧の例を次に示します。

    ![インストールされている 64 ビット ODBC ドライバー](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> ドライバーがインストールされていることがわかっていて、64 ビット アプレットに表示されない場合は、代わりに 32 ビット アプレットを調べてください。 これを見ると、64 ビットまたは 32 ビットどちらの SQL Server インポートおよびエクスポート ウィザードを実行する必要があるかもわかります。
>
> 64 ビット バージョンの SQL Server インポートおよびエクスポート ウィザードを使用するには、SQL Server をインストールする必要があります。 SQL Server Data Tools (SSDT) および SQL Server Management Studio (SSMS) は 32 ビット アプリケーションであり、32 ビット バージョンのウィザードを含む、32 ビット ファイルのみがインストールされます。
    
## <a name="step-1---select-the-data-source"></a>ステップ 1 - データ ソースを選択する
お使いのコンピューターにインストールされている ODBC ドライバーは、データ ソースのドロップダウン リストに表示されません。 ODBC ドライバーを使って接続するには、最初にウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページで、データ ソースとして **[.NET Framework Data Provider for ODBC]** を選びます。 このプロバイダーは、ODBC ドライバーのラッパーとして機能します。

下の図は、.NET Framework Data Provider for ODBC を選んだ直後に表示される一般的な画面です。

![ODBC を使って SQL に接続する (前)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>ステップ 2 - 接続情報を指定する
次に、ODBC ドライバーとデータ ソースの接続情報を指定します。 この場合、2 つの選択肢があります。
1.  既に存在している **DSN** (データ ソース名) または **[ODBC データ ソース アドミニストレーター]** アプレットで作成した DSN を指定します。 DSN は、ODBC データ ソースへの接続に必要な設定の保存されたコレクションです。

    既に DSN 名がわかっている場合、または新しい DSN の作成方法がわかっている場合は、このページの残りの部分を省略できます。 **[データ ソースの選択]** ページまたは **[変換先の選択]** ページの **[DSN]** フィールドに DSN 名を入力し、ウィザードの次のステップを続けます。

    [DSN を指定する](#odbc_dsn)
    
2.  **接続文字列** を指定します。接続文字列は、オンラインで調べることも、お使いのコンピューターで **[ODBC データ ソース アドミニストレーター]** アプレットを使って作成し、テストすることもできます。

    接続文字列が既にある場合、または接続文字列の作成方法がわかっている場合は、このページの残りの部分を省略できます。 **[データ ソースの選択]** ページまたは **[変換先の選択]** ページの **[ConnectionString]** フィールドに接続文字列を入力し、ウィザードの次のステップを続けます。

    [接続文字列を指定する](#odbc_connstring)

接続文字列を指定すると、 **[データ ソースの選択]** ページまたは **[変換先の選択]** ページに、ウィザードがデータ ソースへの接続に使うすべての接続情報 (サーバー名、データベース名、認証方法など) が表示されます。 DSN を指定した場合は、この情報は表示されません。

## <a name="odbc_dsn"></a> オプション 1 - DSN を指定する
DSN (データ ソース名) で接続情報を指定する場合は、 **[ODBC データ ソース アドミニストレーター]** アプレットを使って既存の DSN の名前を調べるか、新しい DSN を作成します。
1.  スタート メニューまたはコントロール パネルの **[ODBC データ ソース (64 ビット)]** アプレットを検索または参照します。 32 ビット ドライバーしかない場合、または 32 ビット ドライバーを使う必要がある場合は、代わりに **[ODBC データ ソース (32 ビット)]** を検索または参照します。
2.  アプレットを起動します。 **[ODBC データ ソース アドミニストレーター]** ウィンドウが開きます。 アプレットの表示は次のようになります。

    ![ODBC アドミニストレーター コントロール パネル アプレット](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  データ ソースに**既存の DSN を使う**場合は、 **[ユーザー DSN]** 、 **[システム DSN]** 、または **[ファイル DSN]** のどのタブに表示される DSN でも使うことができます。名前を確認してからウィザードに戻り、 **[データ ソースの選択]** ページまたは **[変換先の選択]** ページの **[DSN]** フィールドに入力します。 このページの残りの部分を省略し、ウィザードの次のステップを続けます。
4.  **新しい DSN を作成する**場合は、自分だけに表示されるようにするか (ユーザー DSN)、Windows サービスを含むコンピューターの全ユーザーに表示されるようにするか (システム DSN)、またはファイルに保存するか (ファイル DSN) を決めます。 この例では、新しいシステム DSN を作成します。
5. **[システム DSN]** タブで **[追加]** をクリックします。

    ![新しい ODBC システム DSN を追加する](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  **[新しいデータ ソースの作成]** ダイアログ ボックスでデータ ソースのドライバーを選んで、 **[完了]** をクリックします。

    ![新しいシステム DSN のドライバーを選ぶ](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. ドライバー固有の画面が表示されるので (複数の場合あり)、データ ソースに接続するために必要な情報を入力します (たとえば、SQL Server ドライバーの場合は、4 ページのカスタム設定があります)。完了すると、新しいシステム DSN が一覧に表示されます。

    ![一覧の新しいシステム DSN](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  ウィザードに戻り、 **[データ ソースの選択]** ページまたは **[変換先の選択]** ページの **[DSN]** フィールドに DSN 名を入力します。 ウィザードの次のステップに進みます。

## <a name="odbc_connstring"></a> オプション 2 - 接続文字列を指定する
接続文字列で接続情報を指定する場合は、このトピックの残りの部分を参考にして、必要な接続文字列を取得します。

この例では、Microsoft SQL Server に接続する次の接続文字列を使います。 使用されるデータベース例は **WideWorldImporters** であり、ローカル コンピューターで SQL Server に接続します。

    ```
    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;
    ```

**[データ ソースの選択]** ページまたは **[変換先の選択]** ページで、 **[ConnectionString]** フィールドに接続文字列を入力します。 接続文字列を入力すると、ウィザードによって文字列が解析され、個々のプロパティとその値が一覧に表示されます。

接続文字列を入力した後に表示される画面を次に示します。

![ODBC を使って SQL に接続する (後)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> ODBC ドライバーの接続オプションは、ソースまたは変換先のどちらを構成している場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

## <a name="get-the-connection-string-online"></a>オンラインで接続文字列を取得する
ODBC ドライバーの接続文字列をオンラインで調べるには、「[The Connection Strings Reference](https://www.connectionstrings.com/)」(接続文字列リファレンス) をご覧ください。 このサード パーティのサイトには、接続文字列のサンプルと、データ プロバイダーおよび必要な接続情報に関する詳細な情報が記載されています。

## <a name="get-the-connection-string-with-an-app"></a>アプリで接続文字列を取得する
お使いのコンピューターで ODBC ドライバーの接続文字列を作成してテストするには、コントロール パネルの **[ODBC データ ソース アドミニストレーター]** アプレットを使うことができます。 接続のファイル DSN を作成した後、ファイル DSN の設定をコピーして接続文字列を組み立てます。 これには複数の手順が必要ですが、接続文字列が有効であることを確認するのに役立ちます。

1.  スタート メニューまたはコントロール パネルの **[ODBC データ ソース (64 ビット)]** アプレットを検索または参照します。 32 ビット ドライバーしかない場合、または 32 ビット ドライバーを使う必要がある場合は、代わりに **[ODBC データ ソース (32 ビット)]** を検索または参照します。
2.  アプレットを起動します。 **[ODBC データ ソース アドミニストレーター]** ウィンドウが開きます。
3.  アプレットの **[ファイル DSN]** タブに移動します。 **[追加]** をクリックします。

    この例では、ユーザー DSN またはシステム DSN ではなくファイル DSN を作成します。これは、ファイル DSN では、接続文字列に必要な特定の形式で名前と値のペアが保存されるためです。

    ![新しい ODBC ファイル DSN を追加する](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  **[データ ソースの新規作成]** ダイアログ ボックスで、一覧からドライバーを選び、 **[次へ]** をクリックします。 この例では、Microsoft SQL Server に接続するために必要な接続文字列引数を含む DSN を作成します。

    ![新しい ODBC データ ソースを作成する](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  新しいファイル DSN の場所を選び、名前を入力して、 **[次へ]** をクリックします。 後のステップでファイルを探して開くことができるように、ファイルを保存した場所を覚えておきます。

    ![新しいファイル DSN を保存する](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  選択内容の概要を確認し、 **[完了]** をクリックします。

7.  **[完了]** をクリックすると、選んだドライバーに固有の画面が表示されて、接続に必要な情報が収集されます。 通常この情報には、サーバー ベースのデータ ソースの場合はサーバー、ログイン情報、データベースが含まれ、ファイル ベースのデータ ソースの場合はファイル、形式、バージョンが含まれます。

8. データ ソースを構成して **[完了]** をクリックすると、通常、選択内容の概要が表示されて、それらをテストすることができます。

    ![新しいファイル DSN をテストする](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. データ ソースをテストして、ダイアログ ボックスを閉じた後、ファイル システムで保存したファイル DSN を探します。 ファイル拡張子を変更していない場合、既定の拡張子は .DSN です。

10. メモ帳または他のテキスト エディターで、保存したファイルを開きます。 この SQL Server の例の内容を次に示します。

    ```   
    [ODBC]  
    DRIVER=ODBC Driver 13 for SQL Server  
    TrustServerCertificate=No  
    DATABASE=WideWorldImporters    
    WSID=<local computer name>  
    APP=MicrosoftÂ® WindowsÂ® Operating System  
    Trusted_Connection=Yes  
    SERVER=localhost   
    ```
        
11. 必要な値をコピーし、接続文字列に貼り付けます。接続文字列では、名前と値のペアをセミコロンで区切ります。

    サンプルのファイル DSN から必要な値を組み立てた後、接続文字列は次のようになります。
    
        ```
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes
        ```

    通常、動作する接続文字列を作成するために、ODBC データ ソース アドミニストレーターによって作成された DSN のすべての設定は必要はありません。  
    -   ODBC ドライバーは、常に指定する必要があります。
    -   SQL Server のようなサーバー ベースのデータ ソースの場合は、通常、サーバー、データベース、およびログイン情報が必要です。 サンプルの DSN では、TrustServerCertificate、WSID、APP は不要です。
    -   ファイル ベースのデータ ソースの場合は、少なくともファイルの名前と場所が必要です。
    
12. ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページで、 **[ConnectionString]** フィールドにこの接続文字列を貼り付けます。 ウィザードが文字列を解析し、続行する準備ができます。

    ![ODBC を使って SQL に接続する (後)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>参照
[データ ソースの選択](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[変換先の選択](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


