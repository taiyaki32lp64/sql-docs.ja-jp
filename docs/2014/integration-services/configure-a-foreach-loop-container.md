---
title: Foreach ループ コンテナーの構成 |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Foreach Loop containers
- containers [Integration Services], Foreach Loop
ms.assetid: 519c6f96-5e1f-47d2-b96a-d49946948c25
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 461a652999e97907962486cfc05e5b6668f5590d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060876"
---
# <a name="configure-a-foreach-loop-container"></a>Foreach ループ コンテナーを構成する
  この手順では、列挙子レベルおよびコンテナー レベルでのプロパティ式など、Foreach ループ コンテナーを構成する方法について説明します。  
  
### <a name="to-configure-the-foreach-loop-container"></a>Foreach ループ コンテナーを構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  **[制御フロー]** タブをクリックし、Foreach ループをダブルクリックします。  
  
3.  **[Foreach ループ エディター]** ダイアログ ボックスで **[全般]** をクリックし、必要に応じて Foreach ループの名前と説明を変更します。  
  
4.  **[コレクション]** をクリックし、 **[Enumerator]** 一覧から列挙子の型を選択します。  
  
5.  列挙子を指定し、列挙子のオプションを次のように設定します。  
  
    -   Foreach File 列挙子を使用するには、列挙するファイルが含まれるフォルダーを指定し、ファイル名と種類に対するフィルターを指定します。次に、完全修飾ファイル名を返すかどうかを指定します。 また、サブフォルダーを再帰的に使用して、より多くのファイルを列挙するかどうかを指定します。  
  
    -   Foreach Item 列挙子を使用するには、 **[列]** をクリックし、 **[For Each Item 列]** ダイアログ ボックスで **[追加]** をクリックして列を追加します。 **[データ型]** 一覧で各列のデータ型を選択し、 **[OK]** をクリックします。  
  
         列の値を入力するか、一覧から値を選択します。  
  
        > [!NOTE]  
        >  新しい行を追加するには、入力したセルの外側の任意の場所をクリックします。  
  
        > [!NOTE]  
        >  値が列のデータ型と互換性がない場合、テキストが強調表示されます。  
  
    -   Foreach ADO 列挙子を使用するには、 **[ADO オブジェクト ソース変数]** の一覧で既存の変数を選択するか、または **[新しい変数]** をクリックして、列挙する ADO オブジェクトの名前を保持する変数を指定します。次に、列挙モードのオプションを選択します。  
  
         新しい変数を作成する場合、 **[変数の追加]** ダイアログ ボックスで変数のプロパティを設定します。  
  
    -   Foreach ADO.NET Schema Rowset 列挙子を使用するには、 **[接続]** 一覧で既存の ADO.NET 接続を選択するか、または **[新しい接続]** をクリックします。次に、スキーマを選択します。  
  
         必要に応じて、 **[制限の設定]** をクリックしてスキーマの制限を選択するか、制限値が含まれる変数を選択するか、または制限値を入力します。次に、 **[OK]** をクリックします。  
  
    -   Foreach From Variable 列挙子を使用するには、 **[変数]** 一覧で変数を選択します。  
  
    -   Foreach NodeList 列挙子を使用するには、[DocumentSourceType] をクリックし、リストからソースの種類を選択し、[DocumentSource] をクリックします。 選択した DocumentSourceType の値に応じて、一覧から変数またはファイル接続を選択するか、新しい変数またはファイル接続を作成するか、 **[ドキュメント ソース エディター]** で XML ソースを入力します。  
  
         次に、[EnumerationType] をクリックし、一覧から列挙型を選択します。 [EnumerationType] が **[Navigator]、[Node]、または [NodeText]** の場合、[OuterXPathStringSourceType] をクリックし、ソースの種類を選択し、[OuterXPathString] をクリックします。 設定した OuterXPathStringSourceType の値に応じて、一覧から変数またはファイル接続を選択するか、新しい変数またはファイル接続を作成するか、外部の XML パス言語 (XPath) 式の文字列を入力します。  
  
         [EnumerationType] が **[ElementCollection]** の場合、前述のように [OuterXPathStringSourceType] と [OuterXPathString] を設定します。 次に [InnerElementType] をクリックし、内部要素の 列挙型を選択し、[InnerXPathStringSourceType] をクリックします。 設定した InnerXPathStringSourceType の値に応じて、変数またはファイル接続を選択するか、新しい変数またはファイル接続を作成するか、内部の XPath 式の文字列を入力します。  
  
    -   Foreach SMO 列挙子を使用するには、 **[接続]** 一覧で既存の ADO.NET 接続を選択するか、 **[新しい接続]** をクリックします。次に、使用する文字列を入力するか、 **[参照]** をクリックします。 **[参照]** をクリックした場合は、 **[SMO 列挙の選択]** ダイアログ ボックスで、列挙するオブジェクトの種類と列挙型を選択し、 **[OK]** をクリックします。  
  
6.  必要に応じて、 **[コレクション]** ページの **[式]** テキスト ボックスにある参照ボタン ( **[...]** ) をクリックし、プロパティ値を更新する式を作成します。 詳細については、「 [プロパティ式を追加または変更する](expressions/add-or-change-a-property-expression.md)」を参照してください。  
  
    > [!NOTE]  
    >  **[プロパティ]** 一覧に表示されるプロパティは、列挙子ごとに異なります。  
  
7.  必要に応じて、 **[変数のマッピング]** をクリックし、オブジェクトのプロパティをコレクションの値にマップします。その後、次の操作を行います。  
  
    1.  **[変数]** 一覧で変数を選択するか、 **[\<新しい変数>]** をクリックして新しい変数を作成します。  
  
    2.  新しい変数を追加する場合、 **[変数の追加]** ダイアログ ボックスで変数のプロパティを設定し、 **[OK]** をクリックします。  
  
    3.  Foreach Item 列挙子を使用する場合、 **[インデックス]** の一覧で、インデックス値を更新できます。  
  
        > [!NOTE]  
        >  インデックス値は、アイテム内のどの列が変数にマップされるかを示します。 0 以外のインデックス値を使用できるのは、Foreach Item 列挙子だけです。  
  
8.  必要に応じて **[式]** をクリックし、 **[式]** ページで Foreach ループ コンテナーのプロパティ用のプロパティ式を作成します。 詳細については、「 [プロパティ式を追加または変更する](expressions/add-or-change-a-property-expression.md)」を参照してください。  
  
9. **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Foreach ループ コンテナー](control-flow/foreach-loop-container.md)  
  
  
