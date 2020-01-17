---
title: 用語参照変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termlookuptrans.f1
helpviewer_keywords:
- extracting data [Integration Services]
- match extracted terms [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- lookups [Integration Services]
- counting extracted items
- Term Lookup transformation
ms.assetid: 3c0fa2f8-cb6a-4371-b184-7447be001de1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 01b6388dbec5ed563dd8e7fa4476335a3ace998d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770318"
---
# <a name="term-lookup-transformation"></a>用語参照変換
  用語参照変換は、変換入力列内のテキストから抽出された用語を、参照テーブルの用語と照合します。 次に、入力データセットで参照テーブル内の用語が検出された回数をカウントし、その数を参照テーブルの用語と共に変換出力の列に書き込みます。 この変換は、単語の使用頻度を示す統計付きのユーザー定義の単語一覧を、入力テキストから作成する場合に便利です。  
  
 用語参照変換は、用語抽出変換と同じ次の方法を使用して、参照を実行する前に入力列のテキストから単語を抽出します。  
  
-   テキストは文に分けられます。  
  
-   文は単語に分けられます。  
  
-   単語は正規化されます。  
  
 用語の照合方法を詳細にカスタマイズするには、大文字と小文字を区別して照合するように用語参照変換を構成できます。  
  
## <a name="matches"></a>次と一致する  
 用語参照変換は参照を実行し、次の規則を使用して値を返します。  
  
-   大文字と小文字を区別して照合するように変換が構成されている場合、大文字と小文字を比較して一致しない場合は破棄されます。 たとえば、 *student* と *STUDENT* は別の単語として扱われます。  
  
    > [!NOTE]  
    >  文の先頭で 1 文字目が大文字になっている単語は小文字の単語と見なされます。 たとえば、 *Student* が文の最初の単語である場合、 *student* と *Student* の照合は成功します。  
  
-   名詞または名詞句の複数形が参照テーブルに存在する場合、参照により一致するのは、名詞または名詞句の複数形のみです。 たとえば、 *students* のすべてのインスタンスは、 *student*のインスタンスとは別にカウントされます。  
  
-   単語の単数形のみが参照テーブルにある場合、単語または語句の単数形および複数形の両方が単数形と一致します。 たとえば、参照テーブルに *student*が含まれ、変換が *student* と *students*を検出した場合、両方の単語が、参照用語の *student*に一致するものとしてカウントされます。  
  
-   入力列のテキストが、見出し語付きの名詞句の場合、名詞句の最後の単語のみが正規化されます。 たとえば、 *doctors appointments* の見出し語付き名詞句は、 *doctors appointment*になります。  
  
 参照セット内で重複している用語が参照項目に含まれる場合、つまりサブ用語が複数の参照レコード内に存在する場合、用語参照変換は参照結果を 1 つだけ返します。 次の例は、重複するサブ用語が参照項目に含まれる場合の結果を示しています。 この場合、重複するサブ用語は *Windows*で、2 つの参照用語内に存在します。 ただし、変換は結果を 2 つ返さず、参照用語の 1 つ *Windows*のみを返します。 2 番目の参照用語である *Windows 7 Professional*は返されません。  
  
|アイテム|値|  
|----------|-----------|  
|入力用語|Windows 7 Professional|  
|参照用語|Windows, Windows 7 Professional|  
|[出力]|Windows|  
  
 用語参照変換は、特殊文字が含まれる名詞および名詞句を照合でき、参照テーブルのデータにもこれらの文字を含めることができます。 特殊文字とは、%、@、&、$、#、\*、:、;、.、 **,** 、!、?、\<、>、+、=、^、~、|、\\、/、(、)、[、]、{、}、“、‘ です。  
  
## <a name="data-types"></a>データ型  
 用語参照変換で使用できる列は、DT_WSTR または DT_NTEXT データ型のどちらかの列のみです。 列にテキストが含まれていても、これらのデータ型ではない場合、データ変換の変換では、DT_WSTR または DT_NTEXT データ型の列をデータ フローに追加し、列の値を新しい列にコピーできます。 その後、データ変換の変換からの出力を、用語参照変換への入力として使用できます。 詳細については、「 [Data Conversion Transformation](data-conversion-transformation.md)」を参照してください。  
  
## <a name="configuration-the-term-lookup-transformation"></a>用語参照変換の構成  
 用語参照変換の入力列には、InputColumnType プロパティが含まれ、このプロパティにより、列の使用方法を指定します。 InputColumnType は次の値を含むことができます。  
  
-   値 0 は、列が出力のみに渡され、参照で使用されないことを示します。  
  
-   値 1 は、列が参照のみで使用されることを示します。  
  
-   値 2 は、列が出力に渡され、参照内でも使用されることを示します。  
  
 変換出力列の InputColumnType プロパティが 0 または 2 に設定されている場合、1 つの列に CustomLineageID プロパティが含まれます。このプロパティには、上流のデータ フロー コンポーネントによって列に割り当てられた、系列 ID が含まれます。  
  
 用語参照変換は、`Term` と `Frequency` という既定の名前野付いた 2 つの列を変換出力に追加します。 `Term` 列には参照テーブルからの用語が含まれ、`Frequency` 列には、入力データセットで参照テーブル内の用語が検出された回数が含まれます。 これらの列には、CustomLineageID プロパティは含まれません。  
  
 参照テーブルは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] または Access データベースのテーブルである必要があります。 用語抽出変換の出力がテーブルに保存されている場合、このテーブルを参照テーブルとして使用できます。ただし、他のテーブルを使用することもできます。 フラット ファイルのテキスト、Excel ブック、または他の変換元を用語参照変換で使用するには、これらを、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースまたは Access データベースにインポートする必要があります。  
  
 用語参照変換は、個別の OLE DB 接続を使用して、参照テーブルに接続します。 詳細については、「 [OLE DB 接続マネージャー](../../connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
 用語参照変換は、完全な事前キャッシュ モードで動作します。 用語参照変換は、実行時に参照テーブルの用語を読み取って独自のメモリに格納してから、変換入力行を処理します。  
  
 入力列の行の用語は繰り返して使用する場合があるため、用語参照変換の出力には、通常、変換入力よりも多くの行があります。  
  
 この変換は、1 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[用語参照変換エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [用語参照変換エディター ([参照テーブル] タブ)](../../term-lookup-transformation-editor-reference-table-tab.md)  
  
-   [用語参照変換エディター ([用語参照] タブ)](../../term-lookup-transformation-editor-term-lookup-tab.md)  
  
-   [用語参照変換エディター ([詳細設定] タブ)](../../term-lookup-transformation-editor-advanced-tab.md)  
  
 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
  
