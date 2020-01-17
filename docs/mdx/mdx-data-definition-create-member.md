---
title: CREATE MEMBER ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 220741cb2103c3428737cdcb9def9463381db900
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69494074"
---
# <a name="mdx-data-definition---create-member"></a>MDX データ操作 - CREATE MEMBER


  計算されるメンバーを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE [ SESSION ] [HIDDDEN] [ CALCULATED ] MEMBER CURRENTCUBE | Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 メンバーが作成されるキューブの名前を指定する有効な文字列式です。  
  
 *Member_Name*  
 メンバー名を指定する有効な文字列式です。 メジャーディメンション以外のディメンション内にメンバーを作成するには、完全修飾名を指定します。 完全修飾メンバー名を指定しない場合、メンバーは Measures ディメンションに作成されます。  
  
 *MDX_Expression*  
 有効な多次元式 (MDX) 式です。  
  
 *Property_Name*  
 計算されるメンバープロパティの名前を指定する有効な文字列です。  
  
 *Property_Value*  
 計算されるメンバープロパティの値を定義する有効なスカラー式です。  
  
## <a name="remarks"></a>コメント  
 CREATE MEMBER ステートメントでは、セッション全体で使用できる計算されるメンバーを定義します。そのため、セッション中に複数のクエリで使用できます。 詳細については、「[セッションスコープの計算&#40;さ&#41;れるメンバーの作成 MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members)」を参照してください。  
  
 1 つのクエリだけで使用する計算されるメンバーを定義することも可能です。 1 つのクエリに限定される計算されるメンバーを定義するには、SELECT ステートメントで WITH 句を使用します。 詳細については、「[クエリスコープの計算&#40;さ&#41;れるメンバーを作成する MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members)」を参照してください。  
  
 *Property_Name*は、標準またはオプションの計算されるメンバープロパティを参照できます。 標準メンバープロパティについては、このトピックの後半で説明します。 **セッション**値のない CREATE MEMBER を使用して作成された計算されるメンバーには、セッションスコープがあります。 さらに、計算されるメンバーの定義内の文字列は、二重引用符で区切られます。 これは OLE DB で定義されたメソッドとは異なります。これは、文字列を単一引用符で区切る必要があることを指定します。  
  
 現在接続されているキューブ以外のキューブを指定すると、エラーが発生します。 したがって、現在のキューブを示すには、キューブ名の代わりに CURRENTCUBE を使用する必要があります。  
  
 OLE DB によって定義されるメンバープロパティの詳細については、OLE DB のドキュメントを参照してください。  
  
## <a name="scope"></a>スコープ  
 計算されるメンバーは、次の表に示すいずれかのスコープ内で発生する可能性があります。  
  
 クエリ スコープ  
 計算されるメンバーの表示設定と有効期間は、クエリに限定されます。 そのような計算されるメンバーは、個々のクエリの中で定義します。 クエリスコープは、セッションスコープよりも優先されます。 詳細については、「[クエリスコープの計算&#40;さ&#41;れるメンバーを作成する MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members)」を参照してください。  
  
 セッションスコープ  
 計算されるメンバーの可視性と有効期間は、そのメンバーが作成されたセッションに限定されます。 (計算されるメンバーに対して DROP MEMBER ステートメントが実行された場合、有効期間はセッションの継続時間よりも短くなります)。CREATE MEMBER ステートメントは、セッションスコープを持つ計算されるメンバーを作成します。  
  
### <a name="scope-isolation"></a>スコープの分離  
 キューブ多次元式 (MDX) スクリプトに計算されるメンバーが含まれている場合、既定では、計算されるメンバーは、セッションスコープの計算が解決される前、およびクエリ定義の計算が解決される前に解決されます。  
  
> [!NOTE]  
>  特定のシナリオでは、[集計 (mdx)](../mdx/aggregate-mdx.md)関数と[VISUALTOTALS (mdx)](../mdx/visualtotals-mdx.md)関数ではこの動作が発生しません。  
  
 この動作によって、汎用的なクライアント アプリケーションでは計算の実装方法を気にせずに複雑な計算を含むキューブを処理できます。 ただし、特定のシナリオでは、キューブ内の特定の計算の前に、セッションスコープまたはクエリスコープの計算されるメンバーを実行する必要があり、**集計**関数も**visualtotals**関数も適用されません。 これを実現するには、SCOPE_ISOLATION 計算プロパティを使用します。  
  
#### <a name="example"></a>例  
 次のスクリプトは、正しい結果を生成するために SCOPE_ISOLATION 計算プロパティが必要なシナリオの例です。  
  
 **キューブの MDX スクリプト:**  
  
```  
CREATE MEMBER CURRENTCUBE.Measures.ProfitRatio AS 'Measures.[Store Sales]/Measures.[Store Cost]', SOLVE_ORDER = 10  
```  
  
 **MDX クエリ:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
 上のクエリでは、WA を除く USA の、出店コストに対する売上の比率を求めようとしています。 上のクエリでは目的の結果が返されず、USA の比率から WA の比率を引くという無意味な結果が返されます。 目的の結果を得るには、SCOPE_ISOLATION 計算プロパティを使用します。  
  
 **SCOPE_ISOLATION 計算プロパティを使用した MDX クエリ:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
,SCOPE_ISOLATION=CUBE  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
## <a name="standard-properties"></a>標準プロパティ  
 計算されるメンバーには、それぞれ既定のプロパティのセットがあります。 クライアントアプリケーションがに[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]接続されている場合、管理者が選択すると、既定のプロパティがサポートされるか、サポートされるようになります。  
  
 キューブの定義によっては、追加のメンバープロパティを使用できる場合があります。 以下のプロパティは、キューブ内のディメンション レベルに関係する情報を表します。  
  
|プロパティの識別子|説明|  
|-------------------------|-------------|  
|SOLVE_ORDER|計算されるメンバーがもう 1 つの他の計算されるメンバーを参照する場合 (つまり、計算されるメンバーが互いに交差する場合) に、計算されるメンバーが解決される順序です。|  
|FORMAT_STRING|クライアントアプリケーションがセル値を表示するときに使用できる Office スタイルの書式指定文字列。|  
|さ|計算されるメンバーがスキーマ行セットに表示されるかどうかを示す値です。 表示される計算されるメンバーは、 [Add演算メンバー](../mdx/addcalculatedmembers-mdx.md)関数を使用してセットに追加できます。 0以外の値は、計算されるメンバーが表示されることを示します。 このプロパティの既定値が*表示*されます。<br /><br /> 表示されない計算されるメンバー (この値がゼロに設定されている場合) は、一般に、より複雑な計算されるメンバーの中間手順として使用されます。 これらの計算されるメンバーは、メジャーなど、他の種類のメンバーによって参照することもできます。|  
|NON_EMPTY_BEHAVIOR|空のセルを解決するときの計算されるメンバーの動作を決定するために使用されるメジャーまたはセットです。<br /><br /> **警告このプロパティ\*は非推奨とされます。\* \* \*** これを設定しないでください。 詳細については、「 [SQL Server 2014 の非推奨の Analysis Services 機能](/sql/analysis-services/deprecated-analysis-services-features-in-sql-server-2014)」を参照してください。|  
|キャプション|メンバーのキャプションとしてクライアント アプリケーションが使用する文字列です。|  
|DISPLAY_FOLDER|クライアントアプリケーションがメンバーを表示するために使用する表示フォルダーのパスを識別する文字列。 フォルダー レベルの区切り記号は、クライアント アプリケーションによって定義されます。 によって[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]提供されるツールとクライアントでは\\、円記号 () がレベルの区切り記号です。 定義されたメンバーで複数の表示フォルダーを指定するには、セミコロン (;) を使用してフォルダーを区切ります。|  
|ASSOCIATED_MEASURE_GROUP|このメンバーが関連付けられているメジャー グループの名前です。|  
  
## <a name="see-also"></a>関連項目  
 [DROP MEMBER ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [メンバーステートメント&#40;MDX の更新&#41;](../mdx/mdx-data-definition-update-member.md)   
 [Mdx データ定義ステートメント&#40;mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
