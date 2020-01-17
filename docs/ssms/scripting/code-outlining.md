---
title: コードのアウトライン表示 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], outlining code
- Query Editor [SQL Server Management Studio], hiding code
ms.assetid: 556c7dfe-7bc8-4cab-a36f-2b753a05d3f1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c718d4f6ff1d057c23f8041be755da54f9b5da58
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68256640"
---
# <a name="code-outlining"></a>コードのアウトライン表示
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のクエリ エディターのアウトライン機能を使用して、クエリの編集時にコードを選択して非表示にすることができます。 これにより、特に大きなクエリ ファイルでは、作業中のコードを見やすくすることができます。  
  
## <a name="outlining-overview"></a>アウトラインの概要  
 既定では、クエリ エディター ウィンドウを開くとすべてのコードが表示されます。 コード領域は折りたたんで非表示にすることができます。 エディター ウィンドウの左端にある垂直線では負符号 (-) の付いた正方形を使用して、折りたたむことができるコード領域の先頭をそれぞれ識別します。 負符号をクリックすると、コード領域のテキストが 3 つのピリオド (...) の付いたボックスに置き換わり、負符号が正符号 (+) に変わります。 正符号をクリックすると、折りたたまれていたコードが表示され、正符号が負符号に変わります。 ポインターを 3 つのピリオドの付いたボックス上に移動すると、折りたたまれているセクションのコードを示すツールヒントが表示されます。  
  
## <a name="system-outline-regions"></a>システムのアウトライン領域  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の各エディターでは、システム定義のアウトライン領域の既定のセットが生成されます。  
  
 MDX と DMX のコード エディターでは、複数行にわたるステートメントごとにアウトライン領域が作成されます。 これは、このようなエディターがサポートする唯一のアウトライン レベルです。  
  
### <a name="analysis-services-xmla-query-editor-regions"></a>Analysis Services の XMLA クエリ エディターの領域  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の XMLA クエリ エディターでは、複数行にわたる XML 属性ごとにアウトライン領域が生成されます。 エディターは、入れ子になったタグのアウトライン領域は入れ子にします。 たとえば、XMLA エディターでは次のドキュメントに対して 3 つのアウトライン領域を作成します。  
  
 ![XML コードのアウトライン表示](../../ssms/scripting/media/editoutlinexmlfull.gif "XML code showing outlining")  
  
 \<InnerTag> 行の負符号をクリックすると、次の図に示すように InnerTag だけが折りたたまれます。  
  
 ![内部ノードが非表示の XML コード](../../ssms/scripting/media/editoutlinexmlinnercol.gif "XML code with inner node hidden")  
  
 ポインターを 3 つのピリオド (...) の付いたボックス上に移動すると、次の図に示すように、折りたたまれた領域のコードがツールヒントに表示されます。  
  
 ![非表示コードを示すツールヒント付きの XML コード](../../ssms/scripting/media/editoutlinexmlmouse.gif "XML code with tooltip showing hidden code")  
  
 \<MiddleTag> 行の負符号をクリックすると、次の図に示すように MiddleTag と InnerTag の両方が折りたたまれます。  
  
 ![内部タグと中間タグが非表示の XML コード](../../ssms/scripting/media/editoutlinexmlmiddlecol.gif "XML code with inner and middle tags hidden")  
  
 \<OuterTag> 行の負符号をクリックすると、次の図に示すように 3 行すべてが折りたたまれます。  
  
 ![3 つのタグがすべて非表示の XML コード](../../ssms/scripting/media/editoutlinexmloutercol.gif "XML code showing all three tags hidden")  
  
### <a name="database-engine-query-editor-regions"></a>データベース エンジンのクエリ エディターの領域  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディターでは、次の階層で要素ごとにアウトライン領域が生成されます。  
  
1.  バッチ。 最初のバッチは、ファイルの先頭から最初の GO コマンドまでのコードか、GO コマンドがなければファイルの末尾までのコードです。 最初の GO の後は、各 GO コマンドから次の GO コマンドまで、またはファイルの末尾までが 1 つのバッチです。  
  
2.  次のキーワードで区切られるブロック。  
  
    -   BEGIN - END  
  
    -   BEGIN TRY - END TRY  
  
    -   BEGIN CATCH - END CATCH  
  
3.  複数行にわたるステートメント。  
  
 たとえば、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディターでは、次のクエリに対して 3 つのアウトライン領域が作成されます。  
  
```  
CREATE PROCEDURE Sales.SampleProc --Outline region 1  
AS  
BEGIN --Outline region 2   
  SELECT GETDATE() AS TimeOfQuery;  
  SELECT * --Outline region 3  
  FROM sys.transmission_queue;  
  SELECT @@VERSION;  
END;  
GO  
```  
  
 `SELECT *` 行の負符号をクリックして、その `SELECT` ステートメントのみを折りたたむことができます。 `BEGIN - END` ブロック全体を折りたたむには、 `BEGIN` 行の負符号をクリックします。 `GO` コマンドまでのバッチ全体を折りたたむには、 `CREATE PROCEDURE` 行の負符号をクリックします。 `SELECT GETDATE()` 行または `SELECT @@VERSION` 行は、単一行のステートメントでアウトライン領域にはならないため、個別に折りたたむことはできません。  
  
  
