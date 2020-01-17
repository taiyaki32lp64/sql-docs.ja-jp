---
title: 識別子 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- regular identifiers [Integration Services]
- variables [Integration Services], expressions
- identifiers [Integration Services]
- expressions [Integration Services], variables
- lineage identifiers
- columns [Integration Services], identifiers
- names [Integration Services]
- expressions [Integration Services], identifiers
- qualified identifiers [Integration Services]
ms.assetid: 56af984d-88b4-4db8-b6a2-6b07315a699e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ddde15e9ca4fac2fd98b598ee8334f3ff28d6df
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297555"
---
# <a name="identifiers-ssis"></a>識別子 (SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  識別子とは、式の内部で演算に使用できる列および変数のことです。 式では、標準識別子と修飾された識別子を使用できます。  
  
## <a name="regular-identifiers"></a>標準識別子  
 標準識別子とは、追加の修飾子を必要としない識別子のことです。 たとえば、 **MiddleName**は、 **AdventureWorks** データベースの **Contacts** テーブルの列ですが、これは標準識別子です。  
  
 標準識別子の名前付けは、次の規則に従う必要があります。  
  
-   名前の最初の文字は、Unicode Standard 2.0 で定義されている文字か、アンダースコア (_) である必要があります。  
  
-   2 番目以降の文字では、Unicode Standard 2.0 に定義されている文字または数字と、アンダースコア (_)、\@、$、および # 文字を使用できます。  
  
> [!IMPORTANT]  
>  埋め込み型スペース、および上記の一覧に表示されていない特殊文字は、標準識別子では無効です。 スペースや特殊文字を使用するには、標準識別子ではなく修飾された識別子を使用する必要があります。  
  
## <a name="qualified-identifiers"></a>修飾された識別子  
 修飾された識別子とは、角かっこで区切られた識別子のことです。 識別子の名前にスペースが含まれていたり、識別子名の最初の文字が英字でなかったり、アンダースコアの場合、識別子には区切り記号が必要になります。 たとえば、列名 **Middle Name** は角かっこで修飾し、式では [Middle Name] と記述する必要があります。  
  
 識別子の名前にスペースが含まれる場合、または標準識別子の名前が有効でない場合は、識別子を修飾する必要があります。 式エバリュエーターは、角かっこ ([]) を使用して識別子を修飾します。 角かっこは、文字列の最初と最後に配置します。 たとえば、識別子 5$> は [5$>] になります。 角かっこは、列名、変数名、関数名で使用できます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーのダイアログ ボックスを使用して式を構築する場合、標準識別子は、自動的に角かっこで囲まれます。 ただし、角かっこが必要となるのは、名前に無効な文字が含まれている場合のみです。 たとえば、 **MiddleName** という名前の列は、角かっこなしでも有効です。  
  
 式の内部では、角かっこが含まれる列名を参照できません。 たとえば、列名 **Column[1]** は、式では使用できません。 この列を式で使用するには、角かっこなしの名前に変更する必要があります。  
  
## <a name="lineage-identifiers"></a>系列 ID  
 式では、系列 ID を使用して列を参照できます。 系列 ID は、最初にパッケージを作成する際に自動的に割り当てられます。 列の系列 ID は、 **デザイナーにある、** [詳細エディター] **ダイアログ ボックスの** [列のプロパティ] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブで表示できます。  
  
 列の系列 ID を使用してその列を参照する場合、系列 ID に、ポンド (#) 記号のプレフィックスを含める必要があります。 たとえば、系列 ID が 147 の列は、#147 として参照する必要があります。  
  
 式が正常に解析された場合、式エバリュエーターは、ダイアログ ボックス内の系列 ID を列名に置き換えます。  
  
## <a name="unique-column-names"></a>一意の列名  
 パッケージで使用される複数のコンポーネントは、列を同じ名前で公開する場合があります。 これらの列を式で使用する場合、列を明確に識別しなければ、式は正常に解析されません。 式エバリュエーターでは、元の列を識別するためのドット付き表記がサポートされています。 たとえば、 **Age** という名前の 2 つの列が **FlatFileSource.Age** と **OLEDBSource.Age**になり、これらの列がそれぞれ FlatFileSource と OLEDBSource に含まれていることを表します。 パーサーでは、完全修飾名が 1 つの列名として扱われます。  
  
 基となるコンポーネント名や列名は、個別に修飾されます。 次の例では、ドット付き表記を使用した角かっこの有効な使用例を示します。  
  
-   基となるコンポーネント名にスペースが含まれる場合。  
  
    ```  
    [MySo urce].Age  
    ```  
  
-   列名の最初の文字が、有効でない場合。  
  
    ```  
    MySource.[#Age]  
    ```  
  
-   基となるコンポーネント名と列名に、無効な文字が含まれる場合。  
  
    ```  
    [MySource?].[#Age]  
    ```  
  
> [!IMPORTANT]  
>  ドット付き表記の両方の要素が 1 組の角かっこで囲まれている場合、式エバリュエーターは、その組を、元の列の組み合わせとしてではなく、単一の識別子として解釈します。  
  
## <a name="variables-in-expressions"></a>式内部の変数  
 変数が式の内部で参照される場合、変数には \@ プレフィックスを含める必要があります。 たとえば、**Counter** 変数を参照する場合、\@Counter を使用します。 \@ 文字は、変数名の一部ではなく、式の評価において変数を識別するためのものにすぎません。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで用意されているダイアログ ボックスを使用して式を構築する場合、\@ 文字が自動的に変数名に追加されます。 \@ 文字と変数名の間にスペースが含まれる場合は、無効になります。  
  
 変数名は、他の標準識別子の規則と同じく、次の規則に従います。  
  
-   名前の最初の文字は、Unicode Standard 2.0 で定義されている文字か、アンダースコア (_) である必要があります。  
  
-   2 番目以降の文字では、Unicode Standard 2.0 に定義されている文字または数字と、アンダースコア (_)、\@、$、および # 文字を使用できます。  
  
 上記の一覧に表示されていない文字が変数名に含まれる場合、変数を角かっこで囲む必要があります。 たとえば、スペースが含まれる変数名は角かっこで囲みます。 左角かっこは、\@ 文字の後ろに付けます。 たとえば、**My Name** 変数は、\@[My Name] として参照されます。 変数名と角かっこの間にスペースが含まれる場合は、無効になります。  
  
> [!NOTE]  
>  ユーザー定義変数およびシステム変数の名前では、大文字と小文字が区別されます。  
  
## <a name="unique-variable-names"></a>一意の変数名  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ではカスタム変数がサポートされ、さらにシステム変数のセットが用意されています。 既定では、カスタム変数は **User** 名前空間に属し、システム変数は **System** 名前空間に属します。 カスタム変数用に別の名前空間を作成し、名前空間の名前をアプリケーションのニーズに合わせて更新できます。 式ビルダーでは、すべての名前空間にあるスコープ内の変数が一覧表示されます。  
  
 すべての変数はスコープを持ち、名前空間に属します。 変数は、パッケージ スコープまたは、パッケージ内のコンテナーあるいはタスクのスコープを持ちます。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの式ビルダーでは、スコープ内の変数のみが一覧表示されます。 詳細については、「[Integration Services (SSIS) の変数](../../integration-services/integration-services-ssis-variables.md)」および「[パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)」を参照してください。  
  
 式で使用される変数名は、式エバリュエーターが式を正しく評価できるよう、一意である必要があります。 パッケージで複数の変数を同じ名前で使用する場合、その変数は、それぞれ別の名前空間に属する必要があります。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、2 つのコロン (::) から成る、名前空間を解決する演算子が用意され、変数は名前空間で修飾されます。 たとえば、次の式では、 **Count**という名前の 2 つの変数が使用されています。変数の 1 つは **User** 名前空間、もう 1 つの変数は **MyNamespace** 名前空間に属します。  
  
```  
@[User::Count] > @[MyNamespace::Count]  
```  
  
> [!IMPORTANT]  
>  名前空間の組み合わせおよび修飾された変数名は、式エバリュエーターが変数を認識できるよう、角かっこで囲む必要があります。  
  
 **User** 名前空間の **Count** の値が 10、 **MyNamespace** 名前空間の **Count** の値が 2 の場合、式エバリュエーターが 2 つの異なる変数を認識したため、式は **true** に評価されます。  
  
 変数名が一意でない場合でもエラーは発生せず、 式エバリュエーターは、変数のインスタンスを 1 つのみ使用して式を評価し、間違った結果を返します。 たとえば、次の式は 2 つの個別の **Count** 変数の値 (10 および 2) を比較することを目的としています。ただし、式エバリュエーターでは、 **Count** 変数の同じインスタンスが 2 回使用されているので、 **false** と評価されます。  
  
```  
@Count > @Count  
```  
  
## <a name="related-content"></a>関連コンテンツ  
 pragmaticworks.com の技術記事「 [SSIS 式チート シート](https://go.microsoft.com/fwlink/?LinkId=746575)」  
  
  
