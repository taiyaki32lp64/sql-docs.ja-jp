---
title: OLE DB ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbsource.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1a89632ad5502cee9599d1eea6e1cd0a0bebe7d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770998"
---
# <a name="ole-db-source"></a>OLE DB ソース
  OLE DB ソースは、データベース テーブル、ビュー、または SQL コマンドを使用して、OLE DB に準拠するさまざまなリレーショナル データベースからデータを抽出します。 たとえば、OLE DB ソースにより、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブルからデータを抽出できます。  
  
 OLE DB ソースには、データを抽出するために、次の 4 つの異なるデータ アクセス モードが用意されています。  
  
-   テーブルまたはビュー。  
  
-   変数で指定されたテーブルまたはビュー。  
  
-   SQL ステートメントの結果。 クエリにはパラメーター化クエリを使用できます。  
  
-   変数に格納された SQL ステートメントの結果。  
  
> [!NOTE]  
>  SQL ステートメントを使用して、一時テーブルから結果を返すストアド プロシージャが呼び出す場合は、WITH RESULT SETS オプションを使用して結果セットのメタデータを定義します。  
  
 パラメーター化クエリを使用すると、変数をパラメーターにマップして、SQL ステートメント内の個別のパラメーターの値を指定できます。  
  
 OLE DB ソースは、OLE DB 接続マネージャーを使用してデータ ソースに接続します。OLE DB 接続マネージャーは、使用する OLE DB プロバイダーを指定します。 詳細については、「 [OLE DB 接続マネージャー](../connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトでは、OLE DB 接続マネージャーを作成できるデータ ソース オブジェクトも用意されています。このオブジェクトは、データ ソースとデータ ソース ビューを OLE DB ソースで使用できるようにします。  
  
 OLE DB プロバイダーによっては、OLE DB ソースに次のような制限が生じる場合があります。  
  
-   Oracle 用の [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB プロバイダーは、Oracle データ型の BLOB、CLOB、NCLOB、BFILE、および UROWID 型をサポートしていないため、OLE DB ソースは、これらのデータ型の列が含まれるテーブルからデータを抽出できません。  
  
-   IBM OLE DB DB2 プロバイダーおよび [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 プロバイダーは、ストアド プロシージャを呼び出す SQL コマンドの使用をサポートしていません。 この種類のコマンドを使用すると、OLE DB ソースは列のメタデータを作成できません。その結果、データ フロー内で OLE DB ソースの後に実行されるデータ フロー コンポーネントでは、使用できる列データがないため、データ フローの実行が失敗します。  
  
 OLE DB ソースは、1 つの標準出力と 1 つのエラー出力をとります。  
  
## <a name="using-parameterized-sql-statements"></a>パラメーター化された SQL ステートメントの使用  
 OLE DB ソースは、SQL ステートメントを使用してデータを抽出できます。 使用できるのは、SELECT ステートメントまたは EXEC ステートメントです。  
  
 OLE DB ソースは、OLE DB 接続マネージャーを使用して、データの抽出元からデータ ソースに接続します。 OLE DB 接続マネージャーが使用するプロバイダー、および接続マネージャーの接続先であるリレーショナル データベース管理システム (RDBMS) によって、異なる規則がパラメーターの名前付けや一覧表示に適用されます。 パラメーター名が RDBMS から返される場合、パラメーター名を使用して、パラメーター リストのパラメーターを SQL ステートメントのパラメーターにマップできます。それ以外の場合は、パラメーターがパラメーター リストの序数位置によって SQL ステートメントのパラメーターにマップされます。 サポートされるパラメーター名の種類は、プロバイダーによって異なります。 たとえば、変数名または列名の使用を必要とするプロバイダーや、0 や Param0 などのシンボルの名前の使用を必要とするプロバイダーがあります。 SQL ステートメントで使用するパラメーター名の詳細については、プロバイダー固有のマニュアルを参照してください。  
  
 OLE DB 接続マネージャーを使用する場合、パラメーター化サブクエリは使用できません。これは、OLE DB ソースが OLE DB プロバイダーを介してパラメーター情報を取得できないからです。 ただし、式を使用することで、パラメーター値をクエリ文字列に連結したり、ソースの SqlCommand プロパティを設定したりできます。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、 **[OLE DB ソース エディター]** ダイアログ ボックスを使用して OLE DB ソースを構成し、 **[クエリ パラメーターの設定]** ダイアログ ボックスで変数にパラメーターをマップします。  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>序数位置を使用したパラメーターの指定  
 パラメーター名が返されない場合は、 **[クエリ パラメーターの設定]** ダイアログ ボックスの **[パラメーター]** ボックスの一覧にパラメーターが表示されている順序で、実行時にパラメーターがどのパラメーター マーカーにマップされるかが決まります。 一覧に表示されている最初のパラメーターは SQL ステートメントの最初の ? にマップされ、 2 番目のパラメーターは 2 番目の ? にマップされ、それ以降同様にマップされます  
  
 次の SQL ステートメントは、 **データベースの** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] テーブルから行を選択します。 **[マッピング]** ボックスの一覧に表示される最初のパラメーターは **Color** 列の最初のパラメーターに、2 番目のパラメーターは **Size** 列にマップされます。  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 パラメーター名は順序に影響しません。 たとえば、パラメーターの名前が適用先の列と同じ名前で、そのパラメーターが **[パラメーター]** ボックス内の正しい序数位置にない場合も、実行時に行われるパラメーター マッピングには、パラメーター名ではなく、パラメーターの序数位置が使用されます。  
  
 通常、EXEC コマンドでは、プロシージャのパラメーター値を指定する変数の名前をパラメーター名として使用する必要があります。  
  
### <a name="specifying-parameters-by-using-names"></a>名前を使用したパラメーターの指定  
 実際のパラメーター名が RDBMS から返される場合、SELECT ステートメントと EXEC ステートメントで使用されるパラメーターは名前によってマップされます。 このパラメーター名は、SELECT ステートメントまたは EXEC ステートメントによって実行されるストアド プロシージャで必要な名前と一致する必要があります。  
  
 次の SQL ステートメントは、 **データベースで利用できる** uspGetWhereUsedProductID [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] ストアド プロシージャを実行します。  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 このストアド プロシージャでは、パラメーター値を指定するために変数 `@StartProductID` と `@CheckDate`を必要としています。 パラメーターが **[マッピング]** ボックスの一覧に表示される順序は関係ありません。 ここで必要となるのは、パラメーター名が、\@ 記号を含めて、ストアド プロシージャの変数名と一致することのみです。  
  
### <a name="mapping-parameters-to-variables"></a>パラメーターの変数へのマッピング  
 パラメーターは、実行時にパラメーター値を提供する変数にマップされます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に用意されているシステム変数を使用することもできますが、通常はユーザー定義変数を使用します。 ユーザー定義変数を使用する場合、この変数に設定するデータ型は、パラメーター参照がマップされている列のデータ型との互換性があることを確認してください。 詳細については、「 [Integration Services &#40;SSIS&#41; の変数](../integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="troubleshooting-the-ole-db-source"></a>OLE DB ソースのトラブルシューティング  
 OLE DB ソースによる外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、OLE DB ソースによる外部データ ソースからのデータ読み込みに関するトラブルシューティングを行うことができます。 OLE DB ソースによる外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択します。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。  
  
## <a name="configuring-the-ole-db-source"></a>OLE DB ソースの構成  
 プロパティはプログラムによって設定するか、または [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。  
  
 **[OLE DB ソース エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [OLE DB ソース エディター &#40;[接続マネージャー] ページ&#41;](../ole-db-source-editor-connection-manager-page.md)  
  
-   [OLE DB ソース エディター &#40;[列] ページ&#41;](../ole-db-source-editor-columns-page.md)  
  
-   [OLE DB ソース エディター &#40;[エラー出力] ページ&#41;](../ole-db-source-editor-error-output-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [OLE DB カスタム プロパティ](ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [OLE DB ソースを使用してデータを抽出する](ole-db-source.md)  
  
-   [クエリ パラメーターをデータ フロー コンポーネントの変数にマップする](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)  
  
-   [マージ変換およびマージ結合変換用にデータを並べ替える](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 social.technet.microsoft.com の Wiki の記事「 [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670)(SSIS から Oracle への接続)」  
  
## <a name="see-also"></a>関連項目  
 [OLE DB 変換先](ole-db-destination.md)   
 [Integration Services &#40;SSIS&#41; の変数](../integration-services-ssis-variables.md)   
 [データ フロー](data-flow.md)  
  
  
