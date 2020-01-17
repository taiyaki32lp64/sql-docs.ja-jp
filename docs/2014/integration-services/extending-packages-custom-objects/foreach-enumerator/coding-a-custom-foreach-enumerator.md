---
title: カスタム Foreach 列挙子のコーディング | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom foreach enumerators [Integration Services], coding
ms.assetid: 279cf6de-d06f-40e7-b8ca-569310449f36
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 84e1b606c9eedaf4ae1d4b8394b8bf8d2bdcb140
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768628"
---
# <a name="coding-a-custom-foreach-enumerator"></a>カスタム Foreach 列挙子のコーディング
  <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> 基本クラスを継承するクラスを作成し、<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 属性をそのクラスに適用したら、基本クラスのプロパティとメソッドの実装をオーバーライドして、カスタム機能を提供する必要があります。  
  
 カスタム列挙子の実際のサンプルについては、「[カスタム ForEach 列挙子用ユーザー インターフェイスの開発](developing-a-user-interface-for-a-custom-foreach-enumerator.md)」を参照してください。  
  
## <a name="initializing-the-enumerator"></a>列挙子の初期化  
 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.InitializeForEachEnumerator%2A> メソッドをオーバーライドして、パッケージで定義されている接続マネージャーへの参照と、エラー、警告、および情報メッセージを発生させるために使用できるイベント インターフェイスへの参照をキャッシュすることができます。  
  
## <a name="validating-the-enumerator"></a>列挙子の検証  
 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> メソッドをオーバーライドして、列挙子が正しく構成されているかどうかを検証します。 メソッドの `Failure` を返す場合、列挙子および列挙子を含むパッケージは実行されません。 このメソッドの実装方法は列挙子ごとに異なりますが、列挙子が <xref:Microsoft.SqlServer.Dts.Runtime.Variable> オブジェクトまたは <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> オブジェクトに依存する場合は、メソッドに渡されたコレクション内に、これらのオブジェクトが存在することを検証するためのコードを追加する必要があります。  
  
 次のコード例では、列挙子のプロパティで指定された変数を確認するために <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> を実装する方法を示します。  
  
```csharp  
private string variableNameValue;  
  
public string VariableName  
{  
    get{ return this.variableNameValue; }  
    set{ this.variableNameValue = value; }  
}  
  
public override DTSExecResult Validate(Connections connections, VariableDispenser variableDispenser, IDTSInfoEvents infoEvents, IDTSLogging log)  
{  
    if (!variableDispenser.Contains(this.variableNameValue))  
    {  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + this.variableNameValue + " does not exist in the collection.", "", 0);  
            return DTSExecResult.Failure;  
    }  
    return DTSExecResult.Success;  
}  
```  
  
```vb  
Private variableNameValue As String  
  
Public Property VariableName() As String  
    Get   
         Return Me.variableNameValue  
    End Get  
    Set (ByVal Value As String)   
         Me.variableNameValue = value  
    End Set  
End Property  
  
Public Overrides Function Validate(ByVal connections As Connections, ByVal variableDispenser As VariableDispenser, ByVal infoEvents As IDTSInfoEvents, ByVal log As IDTSLogging) As DTSExecResult  
    If Not variableDispenser.Contains(Me.variableNameValue) Then  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + Me.variableNameValue + " does not exist in the collection.", "", 0)  
            Return DTSExecResult.Failure  
    End If  
    Return DTSExecResult.Success  
End Function  
```  
  
## <a name="returning-the-collection"></a>コレクションを返す処理  
 実行中は、<xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> コンテナーが、カスタム列挙子の <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> メソッドを呼び出します。 このメソッドでは、列挙子はアイテムのコレクションを作成し、値を設定して返します。 次に、<xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> はコレクション内のアイテムを繰り返し、各アイテムの制御フローを実行します。  
  
 次に、ランダムな整数の配列を返す <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> の実装例を示します。  
  
```csharp  
public override object GetEnumerator()  
{  
    ArrayList numbers = new ArrayList();  
  
    Random randomNumber = new Random(DateTime.Now);  
  
    for( int x=0; x < 100; x++ )  
        numbers.Add( randomNumber.Next());  
  
    return numbers;  
}  
```  
  
```vb  
Public Overrides Function GetEnumerator() As Object  
    Dim numbers As ArrayList =  New ArrayList()   
  
    Dim randomNumber As Random =  New Random(DateTime.Now)   
  
        Dim x As Integer  
        For  x = 0 To  100- 1  Step  x + 1  
        numbers.Add(randomNumber.Next())  
        Next  
  
    Return numbers  
End Function  
```  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [カスタム Foreach 列挙子の作成](creating-a-custom-foreach-enumerator.md)   
 [カスタム ForEach 列挙子用ユーザー インターフェイスの開発](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  
