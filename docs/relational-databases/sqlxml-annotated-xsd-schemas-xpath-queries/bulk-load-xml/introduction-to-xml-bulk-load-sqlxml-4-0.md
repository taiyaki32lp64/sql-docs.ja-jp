---
title: XML 一括読み込みの概要 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4116bef21a70e6de699046019fd404798826bf18
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246742"
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>XML 一括読み込みの概要 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 一括読み込みは、半構造化 XML データを Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]テーブルに読み込むことができるスタンドアロンの COM オブジェクトです。  
  
 INSERT ステートメントと OPENXML 関数を使用すれば、XML データを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに挿入できますが、大量の XML データを挿入する必要があるときには、一括読み込みユーティリティを使用すると効率的です。  
  
 XML 一括読み込みオブジェクトモデルの Execute メソッドには、次の2つのパラメーターがあります。  
  
-   注釈付き XML Schema Definition (XSD) または XML-Data Reduced (XDR) スキーマ。 XML 一括読み込みユーティリティでは、このスキーマで指定されたマッピング スキーマと注釈が解釈され、XML データを挿入する SQL Server テーブルが特定されます。  
  
-   XML ドキュメント、またはドキュメント フラグメント (単一の最上位要素がないドキュメント)。 XML 一括読み込みで読み込むことができるファイル名またはストリームを指定できます。  
  
 XML 一括読み込みではマッピング スキーマが解釈されて、XML データを挿入するテーブルが特定されます。  
  
 ユーザーは、次の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能について理解していることを前提としています。  
  
-   注釈付き XSD および XDR スキーマ。 注釈付き XSD スキーマの詳細については、「[注釈付き Xsd スキーマの概要 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)」を参照してください。 注釈付き XDR スキーマの詳細については、「 [SQLXML 4.0&#41;で非推奨とされた注釈付き Xdr スキーマ &#40;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)」を参照してください。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の BULK INSERT ステートメント、bcp ユーティリティなどの [!INCLUDE[tsql](../../../includes/tsql-md.md)] 一括挿入メカニズム。 詳細については、「 [BULK INSERT &#40;transact-sql&#41;](../../../t-sql/statements/bulk-insert-transact-sql.md)および[bcp ユーティリティ](../../../tools/bcp-utility.md)」を参照してください。  
  
## <a name="streaming-of-xml-data"></a>XML データのストリーミング  
 ソースの XML ドキュメントは大きい可能性があるため、一括読み込み処理では、メモリにドキュメント全体は読み込まれません。 代わりに、XML 一括読み込みでは XML データがストリームとして解釈され読み取られます。 データが読み取られるとき、このユーティリティではデータベース テーブルが特定され、XML データ ソースを基に適切なレコードが生成された後、そのレコードが挿入のため [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。  
  
 たとえば、次のソース XML ドキュメントは、 ** \<Customer>** の要素と** \<順序>** 子要素で構成されています。  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 XML 一括読み込みでは、 ** \<Customer>** 要素が読み取られ、ユーザーテーブルのレコードが生成されます。 /Customer>終了タグを読み取ると、XML 一括読み込みでは、そのレコードがの[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]テーブルに挿入されます。 ** \<** 同様に、 ** \<Order>** 要素を読み取ると、XML 一括読み込みでは ordertable のレコードが生成されます。その後、 ** \</order>** 終了[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]タグの読み取り時に、そのレコードがテーブルに挿入されます。  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>トランザクション モードとトランザクション以外のモードでの XML 一括読み込みの操作  
 XML 一括読み込みは、トランザクション モードまたはトランザクション以外のモードで操作できます。 トランザクション以外のモードで一括読み込みを行う場合は、通常、次のいずれかの条件に該当する場合に、パフォーマンスが最適です。  
  
-   データの一括読み込みの対象テーブルが空で、インデックスが作成されていない。  
  
-   テーブルにデータと一意のインデックスが格納されている。  
  
 トランザクション以外のモードで一括読み込みを実行する場合は、一括読み込み中に問題が発生したとしてもロールバックは保証されません (ただし、部分ロールバックは実行されることがあります)。 トランザクション以外のモードでの一括読み込みは、データベースが空の場合に適しています。 この場合、問題が発生したらデータベースの内容を消去して、XML 一括読み込みを再実行できます。  
  
> [!NOTE]  
>  トランザクション以外のモードの場合、XML 一括読み込みでは既定の内部トランザクションが使用され、そのトランザクションがコミットされます。 Transaction プロパティが TRUE に設定されている場合、XML 一括読み込みではこのトランザクションで commit が呼び出されません。  
  
 Transaction プロパティが TRUE に設定されている場合、XML 一括読み込みでは、マッピングスキーマで指定されている各テーブルに1つずつ、一時ファイルが作成されます。 ソース XML ドキュメントからのレコードは、最初に XML 一括読み込みによってこれらの一時ファイルに保存され、 次に [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT ステートメントによって一時ファイルから取得されて、対応するテーブルに保存されます。 一時ファイルの場所は、TempFilePath プロパティを使用して指定できます。 XML 一括読み込みで使用される [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アカウントからは、このパスにアクセスできる必要があります。 TempFilePath プロパティが指定されていない場合は、TEMP 環境変数で指定されている既定のファイルパスを使用して一時ファイルが作成されます。  
  
 Transaction プロパティが FALSE (既定の設定) に設定されている場合、XML 一括読み込みでは OLE DB インターフェイス IRowsetFastLoad を使用してデータの一括読み込みを行います。  
  
 ConnectionString プロパティによって接続文字列が設定され、Transaction プロパティが TRUE に設定されている場合、XML 一括読み込みは独自のトランザクションコンテキストで動作します。 たとえば、XML 一括読み込みでは自身のトランザクションが開始され、必要に応じてコミットまたはロールバックが行われます。  
  
 ConnectionCommand プロパティによって接続が既存の接続オブジェクトに設定されていて、Transaction プロパティが TRUE に設定されている場合、XML 一括読み込みでは、成功または失敗の場合、それぞれ COMMIT ステートメントまたは ROLLBACK ステートメントは発行されません。 エラーが発生した場合、XML 一括読み込みでは適切なエラー メッセージが返されます。 COMMIT または ROLLBACK ステートメントを発行するかどうかは、一括読み込みを実行したクライアントで決定されます。 XML 一括読み込みに使用される接続オブジェクトは、ICommand 型であるか、または ADO コマンドオブジェクトである必要があります。  
  
 SQLXML 4.0 では、ConnectionObject は、Transaction プロパティを FALSE に設定して使用することはできません。 非トランザクションモードは、渡されたセッションで複数の IRowsetFastLoad インターフェイスを開くことができないため、ConnectionObject ではサポートされていません。  
  
  
