---
title: ADO (SQLXML 4.0) を使用した、DiffGram の実行 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], SQLOLEDB Provider
- ADO [SQLXML]
- SQLXMLOLEDB Provider, DiffGrams
- data providers [SQLXML], SQLOLEDB Provider
- DiffGrams [SQLXML], ADO
ms.assetid: 741fce82-de83-4923-86eb-30acb5b9a5e6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac11a4f5f697e2b2cd0c27a56940a7183c6231da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012478"
---
# <a name="executing-a-diffgram-by-using-ado-sqlxml-40"></a>ADO を使用した、DiffGram の実行 (SQLXML 4.0)
  この [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic アプリケーションでは、ADO を使用して Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスへの接続を確立した後、DiffGram を実行します。 このアプリケーションでは、DiffGram と XSD スキーマは 1 つのファイルに格納されており、 ファイルを指定して DiffGram を読み込みます。 Diffgram (と関連する XSD スキーマ) のいずれかを使用することで説明されている[DiffGram の例](diffgram-examples-sqlxml-4-0.md)します。  
  
 これは、サンプル アプリケーションのプロセスです。  
  
-   **Conn**オブジェクト (**ADODB します。接続**) 特定のサーバーで実行中の SQL Server のインスタンスへの接続を確立します。  
  
-   **Cmd**オブジェクト (**ADODB.Command**) で確立された接続を実行します。  
  
-   コマンド言語が DBGUID_MSSQLXML に設定されます。  
  
-   DiffGram がコマンド ストリームにコピーされます (**strmIn**) ファイルから。  
  
-   設定されているコマンドの出力ストリーム、 **StrmOut**オブジェクト (**ADODB します。Stream**) が表示されるデータが返されます。  
  
-   SQLOLEDB プロバイダーを使用する場合、既定では Sqlxmlx.dll により Microsoft SQLXML の機能が提供されます。 SQLOLEDB プロバイダーで Sqlxml4.dll を使用する、 **SQLXML Version**にプロパティを設定する必要があります**SQLXML.4.0** SQLOLEDB プロバイダーで**接続**オブジェクト。  
  
-   コマンド (DiffGram) が実行されます。  
  
 サンプル アプリケーションのコードを次に示します。  
  
> [!NOTE]  
>  コードでは、接続文字列に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名を含める必要があります。  
  
```  
Private Sub Command1_Click()  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmOut As New ADODB.Stream  
  Dim strmIn As New ADODB.Stream  
  
  'Open a connection to SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=SqlServerName; database=tempdb; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  strmIn.Open  
  strmIn.Charset = "UTF-8"  
  strmIn.LoadFromFile "C:\SomeFilePath\SampleDiffGram.xml"  
  strmIn.Position = 0  
  Set cmd.CommandStream = strmIn  
  
  strmOut.Open  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  cmd.Properties("Mapping Schema") = "C:\SomeFilePath\SampleDiffGram.xml"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Set cmd = Nothing  
  strmOut.Charset = "UTF-8"  
  strmOut.SaveToFile "C:\DropIt.txt", adSaveCreateOverWrite  
  strmOut.Close  
  Set strmOut = Nothing  
  
End Sub  
```  
  
### <a name="to-test-the-diffgram"></a>DiffGram をテストするには  
  
1.  コンピューター上のフォルダー、するには、例では、いずれかから、Diffgram と対応する XSD スキーマのいずれかをコピー [DiffGram の例](diffgram-examples-sqlxml-4-0.md)します。  
  
2.  Visual Basic を開き、標準 EXE プロジェクトを作成します。  
  
3.  プロジェクトに次の参照を追加します。  
  
    ```  
    Microsoft ActiveX Data Objects 2.8 Library  
    ```  
  
4.  ツールボックス、 **CommandButton**フォームにボタンを描画します。  
  
5.  ボタンをダブルクリックしてコードを編集し、トピックで提供されるアプリケーション コードを追加します。  
  
6.  コードに DiffGram と XSD ファイルの名前を指定し、 接続文字列も適宜変更します。  
  
7.  アプリケーションを実行します。 実行結果は、実行する DiffGram によって変わります。  
  
  
