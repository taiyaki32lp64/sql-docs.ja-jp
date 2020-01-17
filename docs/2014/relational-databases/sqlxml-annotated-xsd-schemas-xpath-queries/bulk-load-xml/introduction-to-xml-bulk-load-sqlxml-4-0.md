---
title: XML 一括読み込み (SQLXML 4.0) の概要 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nontransacted XML Bulk Load operations
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
- transacted XML Bulk Load operations
- streaming XML data
ms.assetid: 38bd3cbd-65ef-4c23-9ef3-e70ecf6bb88a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d257b6eee1fb3adc0ba611f58a1d5eea5adf3f86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013388"
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>XML 一括読み込みの概要 (SQLXML 4.0)
  Microsoft に半構造化 XML データを読み込むことができるようにするスタンドアロンの COM オブジェクトは、XML 一括読み込み[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]テーブル。  
  
 INSERT ステートメントと OPENXML 関数を使用すれば、XML データを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに挿入できますが、大量の XML データを挿入する必要があるときには、一括読み込みユーティリティを使用すると効率的です。  
  
 XML 一括読み込みオブジェクト モデルの Execute メソッドは、2 つのパラメーターを受け取ります。  
  
-   注釈付き XML Schema Definition (XSD) または XML-Data Reduced (XDR) スキーマ。 XML 一括読み込みユーティリティでは、このスキーマで指定されたマッピング スキーマと注釈が解釈され、XML データを挿入する SQL Server テーブルが特定されます。  
  
-   XML ドキュメント、またはドキュメント フラグメント (単一の最上位要素がないドキュメント)。 XML 一括読み込みで読み込むことができるファイル名またはストリームを指定できます。  
  
 XML 一括読み込みではマッピング スキーマが解釈されて、XML データを挿入するテーブルが特定されます。  
  
 ユーザーは、次の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能について理解していることを前提としています。  
  
-   注釈付き XSD および XDR スキーマ。 注釈付き XSD スキーマの詳細については、次を参照してください。[注釈付き XSD スキーマの概要&#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)します。 注釈付き XDR スキーマについては、次を参照してください。[注釈付き XDR スキーマ&#40;SQLXML 4.0 では非推奨&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の BULK INSERT ステートメント、bcp ユーティリティなどの [!INCLUDE[tsql](../../../includes/tsql-md.md)] 一括挿入メカニズム。 詳細については、次を参照してください。 [BULK INSERT &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/bulk-insert-transact-sql)と[bcp ユーティリティ](../../../tools/bcp-utility.md)します。  
  
## <a name="streaming-of-xml-data"></a>XML データのストリーミング  
 ソースの XML ドキュメントは大きい可能性があるため、一括読み込み処理では、メモリにドキュメント全体は読み込まれません。 代わりに、XML 一括読み込みでは XML データがストリームとして解釈され読み取られます。 データが読み取られるとき、このユーティリティではデータベース テーブルが特定され、XML データ ソースを基に適切なレコードが生成された後、そのレコードが挿入のため [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。  
  
 たとえば、次のソース XML ドキュメントから成る **\<顧客 >** 要素と **\<順序 >** 子要素。  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 XML 一括読み込みが読み取られると、 **\<顧客 >** 要素、Customertable のレコードが生成されます。 読み取られる、  **\</Customer >** 終了タグ、XML 一括読み込みの挿入でテーブルに記録する[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]します。 同じで、それを読み取るとき、 **\<順序 >** 要素、XML 一括読み込み、Ordertable のレコードの生成し、には、そのレコードを挿入し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]読み取り時にテーブル、  **\</注文 >** 終了タグ。  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>トランザクション モードとトランザクション以外のモードでの XML 一括読み込みの操作  
 XML 一括読み込みは、トランザクション モードまたはトランザクション以外のモードで操作できます。 パフォーマンスは通常、トランザクション以外のモードで一括読み込みを行う場合に最適な: トランザクションのプロパティを FALSE に設定する、)、次の条件のいずれかが true と。  
  
-   データの一括読み込みの対象テーブルが空で、インデックスが作成されていない。  
  
-   テーブルにデータと一意のインデックスが格納されている。  
  
 トランザクション以外のモードで一括読み込みを実行する場合は、一括読み込み中に問題が発生したとしてもロールバックは保証されません (ただし、部分ロールバックは実行されることがあります)。 トランザクション以外のモードでの一括読み込みは、データベースが空の場合に適しています。 この場合、問題が発生したらデータベースの内容を消去して、XML 一括読み込みを再実行できます。  
  
> [!NOTE]  
>  トランザクション以外のモードの場合、XML 一括読み込みでは既定の内部トランザクションが使用され、そのトランザクションがコミットされます。 トランザクションのプロパティが TRUE に設定されている場合は、XML 一括読み込みはこのトランザクションのコミットを呼び出しません。  
  
 トランザクションのプロパティが TRUE に設定されている場合、XML 一括読み込みは、マッピング スキーマで識別されるテーブルごとに 1 つずつ一時ファイルを作成します。 ソース XML ドキュメントからのレコードは、最初に XML 一括読み込みによってこれらの一時ファイルに保存され、 次に [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT ステートメントによって一時ファイルから取得されて、対応するテーブルに保存されます。 TempFilePath プロパティを使用して、これらの一時ファイルの場所を指定できます。 XML 一括読み込みで使用される [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アカウントからは、このパスにアクセスできる必要があります。 TempFilePath プロパティが指定されていない場合は、TEMP 環境変数で指定されている既定のファイル パスが一時ファイルの作成に使用されます。  
  
 トランザクションのプロパティが FALSE (既定の設定) に設定されている場合は、一括読み込みデータを OLE DB インターフェイス IRowsetFastLoad を使用して XML 一括読み込み。  
  
 ConnectionString プロパティは、接続文字列を設定し、トランザクションのプロパティが TRUE に設定した場合、XML 一括読み込みは、独自のトランザクション コンテキストで動作します。 たとえば、XML 一括読み込みでは自身のトランザクションが開始され、必要に応じてコミットまたはロールバックが行われます。  
  
 ConnectionCommand プロパティが設定されている場合との接続を既存の接続オブジェクトとトランザクションのプロパティが TRUE に設定されて、XML 一括読み込みが成功または失敗の場合、COMMIT または ROLLBACK ステートメントをそれぞれ発行しません。 エラーが発生した場合、XML 一括読み込みでは適切なエラー メッセージが返されます。 COMMIT または ROLLBACK ステートメントを発行するかどうかは、一括読み込みを実行したクライアントで決定されます。 XML 一括読み込みに使用される接続オブジェクトは、ICommand 型のか、ADO コマンド オブジェクトである必要があります。  
  
 SQLXML 4.0 でのトランザクション プロパティが FALSE に設定する ConnectionObject は使用できません。 渡されたセッションで 1 つ以上の IRowsetFastLoad インターフェイスを開くことはないために、トランザクション以外のモードは、ConnectionObject でサポートされていません。  
  
  
