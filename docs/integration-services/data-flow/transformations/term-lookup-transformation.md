---
title: 用語参照変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.termlookuptrans.f1
- sql13.dts.designer.termlookup.termlookup.f1
- sql13.dts.designer.termlookup.referencetable.f1
- sql13.dts.designer.termlookup.advanced.f1
helpviewer_keywords:
- extracting data [Integration Services]
- match extracted terms [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- lookups [Integration Services]
- counting extracted items
- Term Lookup transformation
ms.assetid: 3c0fa2f8-cb6a-4371-b184-7447be001de1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 61dad85fb7857b8694712f79b860f58d88e7d650
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291202"
---
# <a name="term-lookup-transformation"></a>用語参照変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
|アイテム|[値]|  
|----------|-----------|  
|入力用語|Windows 7 Professional|  
|参照用語|Windows, Windows 7 Professional|  
|[出力]|Windows|  
  
 用語参照変換は、特殊文字が含まれる名詞および名詞句を照合でき、参照テーブルのデータにもこれらの文字を含めることができます。 特殊文字とは、%、@、&、$、#、\*、:、;、.、 **,** 、!、?、\<、>、+、=、^、~、|、\\、/、(、)、[、]、{、}、“、‘ です。  
  
## <a name="data-types"></a>データ型  
 用語参照変換で使用できる列は、DT_WSTR または DT_NTEXT データ型のどちらかの列のみです。 列にテキストが含まれていても、これらのデータ型ではない場合、データ変換の変換では、DT_WSTR または DT_NTEXT データ型の列をデータ フローに追加し、列の値を新しい列にコピーできます。 その後、データ変換の変換からの出力を、用語参照変換への入力として使用できます。 詳細については、「 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)」を参照してください。  
  
## <a name="configuration-the-term-lookup-transformation"></a>用語参照変換の構成  
 用語参照変換の入力列には、InputColumnType プロパティが含まれ、このプロパティにより、列の使用方法を指定します。 InputColumnType は次の値を含むことができます。  
  
-   値 0 は、列が出力のみに渡され、参照で使用されないことを示します。  
  
-   値 1 は、列が参照のみで使用されることを示します。  
  
-   値 2 は、列が出力に渡され、参照内でも使用されることを示します。  
  
 変換出力列の InputColumnType プロパティが 0 または 2 に設定されている場合、1 つの列に CustomLineageID プロパティが含まれます。このプロパティには、上流のデータ フロー コンポーネントによって列に割り当てられた、系列 ID が含まれます。  
  
 用語参照変換は、 **用語** と **頻度**という既定の名前の付いた 2 つの列を変換出力に追加します。 **用語** 列には参照テーブルからの用語が含まれ、 **頻度** 列には、入力データセットで参照テーブル内の用語が検出された回数が含まれます。 これらの列には、CustomLineageID プロパティは含まれません。  
  
 参照テーブルは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] または Access データベースのテーブルである必要があります。 用語抽出変換の出力がテーブルに保存されている場合、このテーブルを参照テーブルとして使用できます。ただし、他のテーブルを使用することもできます。 フラット ファイルのテキスト、Excel ブック、または他の変換元を用語参照変換で使用するには、これらを、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースまたは Access データベースにインポートする必要があります。  
  
 用語参照変換は、個別の OLE DB 接続を使用して、参照テーブルに接続します。 詳細については、「 [OLE DB 接続マネージャー](../../../integration-services/connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
 用語参照変換は、完全な事前キャッシュ モードで動作します。 用語参照変換は、実行時に参照テーブルの用語を読み取って独自のメモリに格納してから、変換入力行を処理します。  
  
 入力列の行の用語は繰り返して使用する場合があるため、用語参照変換の出力には、通常、変換入力よりも多くの行があります。  
  
 この変換は、1 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="term-lookup-transformation-editor-term-lookup-tab"></a>[用語参照変換エディター] ([用語参照] タブ)
  **[用語参照変換エディター]** ダイアログ ボックスの **[用語参照]** タブを使用すると、入力列を参照テーブルの参照列にマップし、各出力列の別名を提供できます。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 チェック ボックスを使用して、出力にそのまま渡す入力列を選択します。 **[使用できる参照列]** の一覧に入力列をドラッグして、入力列を参照テーブル内の参照列にマップします。 入力列と参照列は、DT_NTEXT または DT_WSTR のサポートされるデータ型が同じである必要があります。 マッピングする行を選択して右クリックし、 [[リレーションシップの作成]](../../../integration-services/data-flow/transformations/create-relationships.md) ダイアログ ボックスでマッピングを編集します。  
  
 **[使用できる参照列]**  
 参照テーブル内の使用できる列を表示します。 一致させる用語の一覧を含む列を選択します。  
  
 **[パススルー列]**  
 使用できる入力列の一覧から選択します。 選択内容が **[使用できる入力列]** テーブルのチェック ボックスに反映されます。  
  
 **[出力列の別名]**  
 各出力列の別名を入力します。 既定では列の名前が使用されますが、一意なわかりやすい名前を自由に付けることができます。  
  
 **エラー出力の構成**  
 [[エラー出力の構成]](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ダイアログ ボックスは、エラーが発生した行に対するエラー処理オプションを指定するために使用します。  
  
## <a name="term-lookup-transformation-editor-reference-table-tab"></a>[用語参照変換エディター] ([参照テーブル] タブ)
  **[用語参照変換エディター]** ダイアログ ボックスの **[参照テーブル]** タブを使用すると、参照テーブルへの接続を指定できます。  
  
### <a name="options"></a>オプション  
 **OLE DB 接続マネージャー**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続を作成します。  
  
 **[参照テーブル名]**  
 一覧から項目を選択することにより、データベースからの参照テーブルまたはビューを選択します。 テーブルまたはビューは、変換元の列のテキストとの比較に使用できる、既存の一覧が含まれた列を含んでいる必要があります。  
  
 **エラー出力の構成**  
 [[エラー出力の構成]](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ダイアログ ボックスは、エラーが発生した行に対するエラー処理オプションを指定するために使用します。  
  
## <a name="term-lookup-transformation-editor-advanced-tab"></a>[用語参照変換エディター] ([詳細設定] タブ)
  **[用語参照変換エディター]** ダイアログ ボックスの **[詳細設定]** タブを使用すると、参照で大文字と小文字を区別するかどうかを指定できます。  
  
### <a name="options"></a>オプション  
 **[用語参照で大文字と小文字を区別する]**  
 参照で大文字と小文字が区別されるかどうかを示します。 既定値は **False**です。  
  
 **エラー出力の構成**  
 [[エラー出力の構成]](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ダイアログ ボックスは、エラーが発生した行に対するエラー処理オプションを指定するために使用します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../../integration-services/integration-services-error-and-message-reference.md)   
 [用語抽出変換](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
