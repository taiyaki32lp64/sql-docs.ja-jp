---
title: ADO を使用した、SQLXML 4.0 クエリの実行
ms.custom: ''
ms.date: 12/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- query testers [SQLXML]
- test scripts
- ADO [SQLXML]
- queries [SQLXML], ADO
- SQLXML, ADO
ms.assetid: 3d54e3bb-7c5f-427e-82f8-1403a54c4f53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02dfe2bfe1a5893a2ef121f279648c5962d6cce9
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251417"
---
# <a name="using-ado-to-execute-sqlxml-40-queries"></a>ADO を使用した、SQLXML 4.0 クエリの実行
  以前のバージョンの SQLXML では、SQLXML IIS 仮想ディレクトリと SQLXML ISAPI フィルターを使用して、HTTP ベースのクエリを実行することができました。 SQLXML 4.0 では、重複する類似の機能が [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のネイティブ XML Web サービスに付属しているため、これらのコンポーネントが削除されました。  
  
 SQLXML 4.0 では、代わりに Microsoft Data Access Components (MDAC) 2.6 以降で最初に導入された ADO (ActiveX Data Objects) への SQLXML 拡張を使用して、COM ベースのアプリケーションで SQLXML 4.0 を使用してクエリを実行することができます。  
  
 ここでは、Visual Basic Scripting Edition (VBScript) アプリケーション (ファイル拡張子が .vbs のスクリプト) の一部として、SQLXML と ADO を使用する方法を紹介します。 SQLXML 4.0 のドキュメントにあるサンプル クエリを作成しテストするときには、ここで紹介する最初の設定手順を参考にしてください。  
  
## <a name="creating-the-sqlxml-40-test-script"></a>SQLXML 4.0 テスト スクリプトの作成  
 ここでは、VBScript (.vbs) ファイル Sqlxml4test.vbs を作成します。このファイルを使用すると、ADO 2.6 以降の SQLXML ADO 拡張を使用して SQLXML クエリを実行できます。  
  
#### <a name="to-create-the-sqlxml-40-query-tester-using-ado-vbscript"></a>ADO を使用した SQLXML 4.0 クエリのテスト スクリプト (VBScript) を作成するには  
  
1.  次の VBScript コードをコピーし、テキストファイルに貼り付けます。 Sqlxml4test.vbs として保存します。  
  
    ```vb
    WScript.Echo "Query process may take a few seconds to complete. Please be patient."  
  
    ' Note that for SQL Server Native Client to be used as the data provider,  
    ' it needs to be installed on the client computer first. Also, SQLXML extensions   
    ' for ADO are used and available in MDAC 2.6 or later.  
  
    'Set script variables.  
    inputFile = "@@FILE_NAME@@"  
    strServer = "@@SERVER_NAME@@"  
    strDatabase = "@@DATABASE_NAME@@"  
    dbGuid = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
    ' Establish ADO connection to SQL Server and   
    ' create an instance of the ADO Command object.  
    Set conn = CreateObject("ADODB.Connection")  
    Set cmd = CreateObject("ADODB.Command")  
    conn.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Server=" & strServer & _  
              ";Database=" & strDatabase & ";Integrated Security=SSPI"  
    Set cmd.ActiveConnection = conn  
  
    ' Create the input stream as an instance of the ADO Stream object.  
    Set inStream = CreateObject("ADODB.Stream")  
    inStream.Open  
    inStream.Charset = "utf-8"  
    inStream.LoadFromFile inputFile  
  
    ' Set ADO Command instance to use input stream.  
    Set cmd.CommandStream = inStream  
  
    ' Set the command dialect.  
    cmd.Dialect = dbGuid  
  
    ' Set a second ADO Stream instance for use as a results stream.   
    Set outStream = CreateObject("ADODB.Stream")  
    outStream.Open  
  
    ' Set dynamic properties used by the SQLXML ADO command instance.   
    cmd.Properties("XML Root").Value = "ROOT"  
    cmd.Properties("Output Encoding").Value = "UTF-8"  
  
    ' Connect the results stream to the command instance and execute the command.  
    cmd.Properties("Output Stream").Value = outStream  
    cmd.Execute , , 1024  
  
    ' Echo cropped/partial results to console.  
    WScript.Echo Left(outStream.ReadText, 1023)  
  
    inStream.Close  
    outStream.Close  
    ```  
  
2.  テストするサンプルとテスト環境に合わせて、次のスクリプト値を更新します。  
  
    -   "`@@FILE_NAME@@`" をテンプレート ファイルの名前に置き換えます。  
  
    -   "`@@SERVER_NAME@@`" を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前 (`(local)` をローカルで実行している場合は "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" など) に置き換えます。  
  
    -   "`@@DATABASE_NAME@@`" をデータベースの名前 ("`AdventureWorks2012`" や "`tempdb`" など) に置き換えます。  
  
     ローカル コンピューターに作成するサンプル用の具体的な指示に従って、必要であれば他の値も更新します。  
  
3.  ファイルを保存して閉じます。  
  
4.  ローカル コンピューターに作成するサンプル ファイルの一部として、XML テンプレートやスキーマなどの必要な追加ファイルが作成されたことを確認します。 これらのファイルは、テスト スクリプト ファイル (Sqlxml4test.vbs) を保存したディレクトリに置く必要があります。  
  
5.  次に、SQLXML 4.0 テスト スクリプトの使用方法について説明します。  
  
## <a name="using-the-sqlxml-40-test-script"></a>SQLXML 4.0 テスト スクリプトの使用  
 Sqlxml4test.vbs ファイルを使用して、このドキュメントで提供されるサンプル クエリをテストするには、次の手順に従います。  
  
#### <a name="to-use-the-sqlxml-40-query-tester"></a>SQLXML 4.0 クエリのテスト スクリプトの使用  
  
1.  次の方法で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client がインストールされていること確認します。  
  
    1.  [**スタート**] メニューの [**設定**] をポイントし、[**コントロールパネル**] をクリックします。  
  
    2.  コントロールパネルで、[**プログラムの追加と削除**] を開きます。  
  
    3.  現在インストールされているプログラムの一覧で、[ **Microsoft SQL Server Native Client** ] が一覧に表示されていることを確認します。  
  
        > [!NOTE]  
        >  Native Client をインストール[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する必要がある場合は、「SQL Server Native Client の[インストール](../native-client/applications/installing-sql-server-native-client.md)」を参照してください。  
  
2.  クライアント コンピューターにインストールされている MDAC のバージョンが 2.6 以降であることを確認します。 MDAC のバージョン情報を確認する必要がある場合は、MDAC コンポーネントチェッカーツールを使用できます。このツールは、Microsoft Web サイト[https://www.microsoft.com/](https://www.microsoft.com/)から無料でダウンロードできます。 詳細については、Microsoft Web サイトの「MDAC Component Checker」を検索してください。  
  
3.  スクリプトを実行します。  
  
     VBScript ファイルを実行するには、コマンド ラインで Cscript.exe を指定するか、Sqlxml4test.vbs ファイルをダブルクリックして Windows Script Host (WScript.exe) を呼び出します。  
  
     スクリプトを実行すると、警告メッセージが表示され、返されたクエリの結果を出力として表示するまでには時間がかかる場合があることが示されます。 出力が表示されたら、サンプルの結果例と内容を比較します。  
  
  
