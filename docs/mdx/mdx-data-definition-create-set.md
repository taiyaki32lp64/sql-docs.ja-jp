---
title: CREATE SET ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6f8d522f7832a280aa8b280bbe912640b566974a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893740"
---
# <a name="mdx-data-definition---create-set"></a>MDX データ操作 - CREATE SET


  現在のキューブのセッションスコープを持つ名前付きセットを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE [SESSION] [ STATIC | DYNAMIC ] [HIDDEN] SET   
   CURRENTCUBE | Cube_Name  
      .Set_Name AS 'Set_Expression'  
      [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブの名前を指定する有効な文字列式です。  
  
 *Set_Name*  
 作成する名前付きセットの名前を指定する有効な文字列式です。  
  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Property_Name*  
 セットのプロパティの名前を指定する有効な文字列です。  
  
 *Property_Value*  
 セットのプロパティの値を定義する有効なスカラー式です。  
  
## <a name="remarks"></a>コメント  
 名前付きセットとは、再度使用するために作成するディメンションメンバー (またはセットを定義する式) のセットです。 たとえば、売上高上位 10 ストアのセットで構成されるディメンション メンバーのセットを名前付きセットとして定義するとします。 このセットは、静的に定義することも、 [TopCount](../mdx/topcount-mdx.md)のような関数を使用して定義することもできます。 この名前付きセットは、上位10個のストアのセットが必要な場所であればいつでも使用できます。  
  
 CREATE SET ステートメントは、セッション全体で使用できる名前付きセットを作成します。したがって、セッションの複数のクエリで使用できます。 詳細については、「[セッションスコープの計算&#40;さ&#41;れるメンバーの作成 MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members)」を参照してください。  
  
 1 つのクエリだけで使用する名前付きセットを定義することも可能です。 そのようなセットを定義する場合は、SELECT ステートメントで WITH 句を使用します。 WITH 句の詳細については、「[クエリスコープの名前付き&#40;セット&#41;を MDX として作成する](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets)」を参照してください。  
  
 *Set_Expression*句には、MDX 構文をサポートする任意の関数を含めることができます。 セッション句を指定しない CREATE SET ステートメントを使用して作成されたセットには、セッションスコープがあります。 クエリ スコープによるセットを作成するには、WITH 句を使用してください。  
  
 現在接続されているキューブ以外のキューブを指定すると、エラーが発生します。 したがって、現在のキューブを示すには、キューブ名の代わりに CURRENTCUBE を使用する必要があります。  
  
## <a name="scope"></a>スコープ  
 ユーザー定義セットは、次の表に示すいずれかのスコープ内で発生する可能性があります。  
  
 クエリ スコープ  
 セットの表示設定と有効期間は、クエリに限定されます。 セットは、個々のクエリで定義されます。 クエリスコープは、セッションスコープよりも優先されます。 詳細については、「[クエリスコープの名前&#40;付き&#41;セットの MDX の作成](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets)」を参照してください。  
  
 セッションスコープ  
 セットの可視性と有効期間は、そのセットが作成されたセッションに限定されます。 (Set で DROP SET ステートメントが実行された場合、有効期間はセッション継続時間よりも短くなります)。CREATE SET ステートメントは、セッションスコープを持つセットを作成します。 クエリ スコープによるセットを作成するには、WITH 句を使用してください。  
  
### <a name="example"></a>例  
 次の例では、Core Products というセットを作成します。 次に SELECT クエリによって、新しく作成されたセットの呼び出しを示しています。 CREATE SET ステートメントは、SELECT クエリを実行する前に実行する必要があります。同じバッチ内で実行することはできません。  
  
```  
CREATE SET [Adventure Works].[Core Products] AS '{[Product].[Category].[Bikes]}'  
  
SELECT [Core Products] ON 0  
  FROM [Adventure Works]  
```  
  
## <a name="set-evaluation"></a>評価の設定  
 セットの評価は異なる方法で定義できます。この設定は、セットの作成時に1回だけ実行するように定義することも、セットが使用されるたびに発生するように定義することもできます。  
  
 STATIC  
 CREATE SET ステートメントが評価されるときに、セットを一度だけ評価することを示します。  
  
 DYNAMIC  
 クエリでセットが使用されるたびに、セットを評価することを示します。  
  
## <a name="set-visibility"></a>可視性の設定  
 このセットは、キューブに対してクエリを実行する他のユーザーに表示するかどうかを指定できます。  
  
 HIDDEN  
 キューブに対してクエリを実行するユーザーに対して、セットを表示しないように指定します。  
  
## <a name="standard-properties"></a>標準プロパティ  
 セットには、それぞれ既定のプロパティのセットがあります。 クライアントアプリケーションがに[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]接続されている場合、管理者が選択すると、既定のプロパティがサポートされるか、サポートされるようになります。  
  
|プロパティの識別子|説明|  
|-------------------------|-------------|  
|キャプション|クライアントアプリケーションがセットのキャプションとして使用する文字列。|  
|DISPLAY_FOLDER|セットを表示するためにクライアント アプリケーションが使用する、表示フォルダーのパスを識別する文字列です。 フォルダー レベルの区切り記号は、クライアント アプリケーションによって定義されます。 によって[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]提供されるツールとクライアントでは\\、円記号 () がレベルの区切り記号です。 定義されたセットで複数の表示フォルダーを指定するには、セミコロン (;) を使用してフォルダーを区切ります。|  
  
## <a name="see-also"></a>関連項目  
 [DROP SET ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md)   
 [Mdx データ定義ステートメント&#40;mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
