---
title: レポート デザイナーでカスタム コードやアセンブリを式から参照する (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- items [Reporting Services], expressions
- data [Reporting Services], expressions
- expressions [Reporting Services], about expressions
- expressions [Reporting Services]
- SSRS, expressions
- formulas [Reporting Services]
- data manipulation [Reporting Services]
- SQL Server Reporting Services, expressions
ms.assetid: ae8a0166-2ccc-45f4-8d28-c150da7b73de
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df09ab032929de0eca51c9640f5c5cb23d1cde21
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106111"
---
# <a name="custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs"></a>レポート デザイナーでカスタム コードやアセンブリを式から参照する (SSRS)
  レポート内に埋め込まれたカスタム コードや、ビルドして自分のコンピューターに保存 (またはレポート サーバーに配置) したカスタム アセンブリは、レポート内から参照することができます。 カスタム定数、複雑な関数、または 1 レポート内で何度も使用される関数には、埋め込みコードを使用します。 コードを 1 か所で管理し、そのコードを複数のレポートで共有する場合は、カスタム コード アセンブリを使用します。 カスタム コードには、新しいカスタム定数、変数、関数、またはサブルーチンを含めることができます。 Parameters コレクションなど、組み込みコレクションへの読み取り専用の参照を含めることが可能です。 ただし、レポート データ値セットをカスタム関数に渡すことはできません。特に、カスタム集計はサポートされていません。  
  
> [!IMPORTANT]  
>  実行時にいったん評価し、レポート処理全体で同じ値を保持しておく必要のある、タイミングに依存するような計算の場合は、レポート変数とグループ変数のどちらを使用するかを検討してください。 詳細については、「[レポート変数コレクションとグループ変数コレクションの参照 (レポート ビルダーおよび SSRS)](built-in-collections-report-and-group-variables-references-report-builder.md)」を参照してください。  
  
 カスタム コードをレポートに追加するための作成環境としては、レポート デザイナーの使用をお勧めします。 レポート ビルダーでサポートされるのは、有効な式を含んだレポートの処理、またはレポート サーバー上のカスタム アセンブリへの参照を含んだレポートの処理です。 カスタム アセンブリへの参照を追加する手段は、レポート ビルダーには用意されていません。  
  
> [!NOTE]  
>  カスタム アセンブリに依存しているレポートについては、レポート サーバーのアップグレード時に注意が必要です。アップグレードを完了するまでに、追加の手順が必要となる場合があります。 詳細については、「 [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RB3"></a> レポート ビルダーでのカスタム コードの使用  
 レポート ビルダーでは、カスタム アセンブリを参照するレポートをレポート サーバーから取得して開くことができます。 たとえば、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のレポート デザイナーを使用して作成、配置されたレポートを編集することができます。 カスタム アセンブリは、レポート サーバーに配置されている必要があります。  
  
 次の操作は実行できません。  
  
1.  参照またはクラス メンバーのインスタンスをレポートに追加する。  
  
2.  カスタム アセンブリへの参照を含んだレポートをローカル モードでプレビューする。  
  
##  <a name="Common"></a> 使用頻度の高い関数への参照の追加  
 **[式]** ダイアログ ボックスを使用すると、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]に組み込まれている共通の関数の一覧がカテゴリ別に表示されます。 **[共通の関数]** を展開してカテゴリをクリックすると、式に含める関数の一覧が **[アイテム]** ペインに表示されます。 共通の関数には、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.Math> 名前空間と <xref:System.Convert> 名前空間のクラス、および [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ランタイム ライブラリ関数が含まれています。 便宜上、最もよく使用される関数を表示できます、**式** ダイアログ ボックスで、カテゴリ別一覧はどこで。テキスト、日付し、時刻、数学、検査、プログラム フロー、集計、財務、変換、およびその他。 使用頻度の低い関数は、一覧に表示されませんが、式で使用することはできます。  
  
 組み込み関数を使用するには、[アイテム] ペインで関数名をダブルクリックします。 関数の説明が説明ペインに表示され、関数呼び出しの例がサンプル ペインに表示されます。 コード ペインで、関数名の後に左かっこ **(** を入力すると、IntelliSense により、関数呼び出しの有効な各構文が表示されます。 たとえば、テーブルの `Quantity` という名前のフィールドの最大値を計算するには、 `=Max(` という単純な式をコード ペインに追加した後、スマート タグを使用して、関数呼び出しに使用できる有効な構文をすべて表示します。 この例を完成させるには、「 `=Max(Fields!Quantity.Value)`」と入力します。  
  
 各関数の詳細については、MSDN の「 <xref:System.Math>」、「 <xref:System.Convert>」、および「 [Visual Basic ランタイム ライブラリのメンバー](https://go.microsoft.com/fwlink/?LinkId=198941) 」を参照してください。  
  
##  <a name="NotCommon"></a> 使用頻度の低い関数への参照の追加  
 使用頻度の低い、その他の CLR 名前空間への参照を含めるには、 <xref:System.Text.StringBuilder>」を参照してください。 このような使用頻度の低い関数については、 **[式]** ダイアログ ボックスのコード ペインで IntelliSense がサポートされていません。  
  
 各関数の詳細については、MSDN の「 [Visual Basic ランタイム ライブラリのメンバー](https://go.microsoft.com/fwlink/?LinkId=198941) 」を参照してください。  
  
##  <a name="External"></a> 外部アセンブリへの参照の追加  
 外部アセンブリ内のクラスへの参照を含めるには、レポート プロセッサのアセンブリを特定する必要があります。 レポートに追加するアセンブリの完全修飾名を指定するには、 **[レポートのプロパティ]** ダイアログ ボックスの **[参照]** ページを使用します。 式では、アセンブリ内のクラスの完全修飾名を使用する必要があります。 外部アセンブリ内のクラスは、 **[式]** ダイアログ ボックスに表示されません。そのため、クラスの正しい名前を指定する必要があります。 完全修飾名には、名前空間、クラス名、およびメンバー名が含まれます。  
  
##  <a name="Embedded"></a> 埋め込みコードの追加  
 埋め込みコードをレポートに追加するには、 **[レポートのプロパティ]** ダイアログ ボックスの [コード] タブを使用します。 作成したコード ブロックでは、複数のメソッドを使用できます。 埋め込みコード内のメソッドは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] で記述されており、インスタンス ベースである必要があります。 レポート プロセッサは、System.Convert 名前空間および System.Math 名前空間の参照を自動的に追加します。 他のアセンブリ参照を追加するには、 **[レポートのプロパティ]** ダイアログ ボックスの **[参照]** ページを使用します。 詳細については、「 [レポートにアセンブリへの参照を追加する &#40;SSRS&#41;](add-an-assembly-reference-to-a-report-ssrs.md)」を参照してください。  
  
 埋め込みコード内のメソッドは、グローバルに定義されている `Code` メンバーを介して利用できます。 `Code` メンバーとメソッド名を参照することで、これらのメソッドにアクセスできます。 次の例では、`ToUSD` メソッドを呼び出します。これにより、`StandardCost` フィールドの値が米ドル単位に変換されます。  
  
```  
=Code.ToUSD(Fields!StandardCost.Value)  
```  
  
 カスタム コード内で組み込みコレクションを参照するには、組み込みの `Report` オブジェクトへの参照を含めます。  
  
```  
=Report.Parameters!Param1.Value  
```  
  
 次の例は、いくつかのカスタム定数と変数を定義する方法を示しています。  
  
```  
Public Const MyNote = "Authored by Bob"  
Public Const NCopies As Int32 = 2  
Public Dim  MyVersion As String = "123.456"  
Public Dim MyDoubleVersion As Double = 123.456  
```  
  
 **[式]** ダイアログ ボックスの **[定数]** カテゴリにはカスタム定数が表示されませんが (組み込み定数のみが表示されます)、次の例に示すように、任意の式からカスタム定数への参照を追加できます。 式の中では、カスタム定数が `Variant` として扱われます。  
  
```  
=Code.MyNote  
=Code.NCopies  
=Code.MyVersion  
=Code.MyDoubleVersion  
```  
  
 次の例には、関数 `FixSpelling` のコード参照およびコード実装の両方が含まれています。これにより、`"Bicycle"` フィールド内の "Bike" というテキストがすべて `SubCategory` に置き換えられます。  
  
 `=Code.FixSpelling(Fields!SubCategory.Value)`  
  
 レポート定義コード ブロックに埋め込んで使用する次のコードは、`FixSpelling` メソッドの実装を示しています。 この例は、完全修飾参照を使用する方法を示します、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] `StringBuilder`クラス。  
  
```vb  
Public Function FixSpelling(ByVal s As String) As String  
   Dim strBuilder As New System.Text.StringBuilder(s)  
   If s.Contains("Bike") Then  
      strBuilder.Replace("Bike", "Bicycle")  
      Return strBuilder.ToString()  
      Else : Return s  
   End If  
End Function  
```  
  
 組み込みのオブジェクト コレクションと初期化の詳細については、「[組み込み Globals および Users 参照 &#40;レポート ビルダーおよび SSRS&#41;](built-in-collections-built-in-globals-and-users-references-report-builder.md)」および「[カスタム アセンブリ オブジェクトの初期化](../custom-assemblies/initializing-custom-assembly-objects.md)」を参照してください。  
  
##  <a name="Parameters"></a> パラメーターへの参照の追加 (コード経由)  
 レポート定義のコード ブロックまたはユーザーが指定したカスタム アセンブリのカスタム コードを経由してグローバル パラメーター コレクションを参照できます。 パラメーター コレクションは読み取り専用で、パブリック反復子がありません。 使用することはできません、 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] `For Each`コレクションのステップ実行を作成します。 レポート定義内で定義されたパラメーターの名前をコード内で参照する前に、その名前を確認しておく必要があります。 ただし、複数の値を持つパラメーターのすべての値は、繰り返し処理することができます。  
  
 次の表には、カスタム コードから組み込みコレクション `Parameters` を参照する例を示しています。  
  
|説明|式での参照|カスタム コード定義|  
|-----------------|-----------------------------|----------------------------|  
|グローバル パラメーター コレクション全体をカスタム コードに渡します。<br /><br /> この関数は、特定のレポート パラメーター *MyParameter*の値を返します。|`=Code.DisplayAParameterValue(Parameters)`|`Public Function DisplayAParameterValue(`<br /><br /> `ByVal parameters as Parameters) as Object`<br /><br /> `Return parameters("MyParameter").Value`<br /><br /> `End Function`|  
|個別のパラメーターをカスタム コードに渡します。<br /><br /> この例では、渡されたパラメーターの値が返されます。 パラメーターが複数の値を持つパラメーターである場合、返される文字列はすべての値の連結になります。|`=Code.ShowParametersValues(Parameters!DayOfTheWeek)`|`Public Function ShowParameterValues(ByVal parameter as Parameter)` <br />  `as String` <br /> `Dim s as String`  <br />  `If parameter.IsMultiValue then` <br />  `s = "Multivalue: "`  <br /> `For i as integer = 0 to parameter.Count-1` <br />  `s = s + CStr(parameter.Value(i)) + " "`  <br />  `Next` <br /> `Else` <br /> `s = "Single value: " + CStr(parameter.Value)` <br /> `End If` <br />  `Return s` <br /> `End Function`|  
  
##  <a name="Custom"></a> コードへの参照の追加 (カスタム アセンブリ経由)  
 レポートでカスタム アセンブリを使用するには、まずアセンブリを作成して、これをレポート デザイナーが利用できるようにし、アセンブリへの参照をレポートに追加してから、レポート内の式を使用してこのアセンブリ内のメソッドを参照します。 レポートがレポート サーバーに配置される場合は、カスタム アセンブリもレポート サーバーに配置する必要があります。  
  
 カスタム アセンブリを作成して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で利用できるようにする方法については、「 [レポートでのカスタム アセンブリの使用](../custom-assemblies/using-custom-assemblies-with-reports.md)」を参照してください。  
  
 式の中でカスタム コードを参照するには、アセンブリ内のクラスのメンバーを呼び出す必要があります。 呼び出す方法は、メソッドが静的であるかインスタンス ベースであるかにより異なります。 カスタム アセンブリ内の静的メソッドは、レポート内でグローバルに利用できます。 静的メソッドには、名前空間、クラス、メソッド名を指定することによって、式からアクセスできます。 次の例は、メソッドを呼び出して`ToGBP`の値に変換、 **StandardCost**値をドルから英ポンドに換算に。  
  
```  
=CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
```  
  
 インスタンスベースのメソッドは、グローバルに定義されている `Code` メンバーを介して利用できます。 まず `Code` メンバーを参照し、続いてインスタンスとメソッド名を参照することで、これらのメソッドにアクセスできます。 次の例は、インスタンス メソッドを呼び出します`ToEUR`の値に変換**StandardCost**をドル ユーロから。  
  
```  
=Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
```  
  
> [!NOTE]  
>  レポート デザイナーでは、カスタム アセンブリが一度読み込まれると、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]を終了するまでアンロードされません。 レポートをプレビューして、レポートで使用するカスタム アセンブリに変更を加え、その後再びレポートをプレビューした場合、2 回目のプレビューでは行った変更が表示されません。 アセンブリを再度読み込むには、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] を終了してから再起動し、レポートをプレビューします。  
  
 コードへのアクセスの詳細については、「 [Accessing Custom Assemblies Through Expressions](../custom-assemblies/accessing-custom-assemblies-through-expressions.md)」を参照してください。  
  
##  <a name="collections"></a> カスタム アセンブリへの組み込みコレクションの引き渡し  
 組み込みコレクション ( *Globals* コレクションや *Parameters* コレクションなど) をカスタム アセンブリ内に渡して処理する場合は、コード プロジェクト内のアセンブリ参照を組み込みコレクションを定義するアセンブリに追加し、正しい名前空間にアクセスする必要があります。 開発しているカスタム アセンブリが、レポート サーバー上で実行されるレポート (サーバー レポート) 用のものなのか、それとも .NET アプリケーション内でローカルに実行されるレポート (ローカル レポート) 用のものなのかによって、参照する必要があるアセンブリは異なります。 詳細については、以下を参照してください。  
  
-   **名前空間:** Microsoft.ReportingServices.ReportProcessing.ReportObjectModel  
  
-   **アセンブリ (ローカル レポート):** Microsoft.ReportingServices.ProcessingObjectModel.dll  
  
-   **アセンブリ (サーバー レポート):** Microsoft.ReportViewer.ProcessingObjectModel.dll  
  
 *Fields* コレクションおよび *ReportItems* コレクションの内容は実行時に動的に変更されるので、カスタム アセンブリ内への呼び出し間でそれらを保持することは避けてください (たとえば、メンバー変数内など)。 この推奨事項は、すべての組み込みコレクションについて共通に該当します。  
  
## <a name="see-also"></a>参照  
 [レポートにコードを追加する &#40;SSRS&#41;](add-code-to-a-report-ssrs.md)   
 [レポートでのカスタム アセンブリの使用](../custom-assemblies/using-custom-assemblies-with-reports.md)   
 [レポートにアセンブリへの参照を追加する &#40;SSRS&#41;](add-an-assembly-reference-to-a-report-ssrs.md)   
 [Reporting Services チュートリアル &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [レポート サンプル (レポート ビルダーおよび SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
  
