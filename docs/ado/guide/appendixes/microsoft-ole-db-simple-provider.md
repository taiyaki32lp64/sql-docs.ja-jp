---
title: Microsoft OLE DB の単純なプロバイダー |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3acdfc7e03115b415e7641047e7621d5ab463e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926604"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Microsoft OLE DB プロバイダーの簡単な概要
Microsoft OLE DB 単純なプロバイダー (OSP) により、対象のプロバイダーが書き込まれたを使用して任意のデータにアクセスする ADO、 [OLE DB 単純なプロバイダー (OSP) Toolkit](https://msdn.microsoft.com/6e7b7931-9e4a-4151-ae51-672abd3f84a6)します。 単純なプロバイダーはインメモリ配列、または XML ドキュメントなどの OLE DB の基本的なサポートを必要とするデータ ソースにアクセスするためのものです。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 OLE DB 単純なプロバイダーの DLL に接続するには、設定、*プロバイダー*への引数、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティ。

```vb
MSDAOSP
```

 この値も設定またはを使用して読み取る、[プロバイダー](../../../ado/reference/ado-api/provider-property-ado.md)プロパティ。

 プロバイダーの作成者によって決定されます、登録済みのプロバイダー名を使用して完全な OLE DB プロバイダーとして登録されている単純なプロバイダーに接続することができます。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=MSDAOSP;Data Source=serverName"
```

 文字列は、これらのキーワードで構成されます。

|Keyword|説明|
|-------------|-----------------|
|**Provider**|SQL Server の OLE DB プロバイダーを指定します。|
|**Data Source**|サーバーの名前を指定します。|

## <a name="xml-document-example"></a>XML ドキュメントの例
 OLE DB 単純なプロバイダー (OSP) MDAC 2.7 以降と Windows Data Access Components (Windows DAC) は階層の ADO のオープンをサポートする強化されています**レコード セット**を任意の XML ファイル。 これらの XML ファイルは、ADO の XML 永続性スキーマを含めることができますが、必須ではありません。 これは、OSP に接続することによって実装されて、 **MSXML2.DLL**。 したがって**MSXML2.DLL**以降が必要です。

 **Portfolio.xml**次の例で使用されるファイルには、次のようなツリーが含まれています。

```console
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 XML の DSO が組み込みのヒューリスティックを使用して XML ツリー内のノードを階層構造の各章に変換する**Recordset**します。

 これらの組み込みのヒューリスティックを使用して、XML ツリーが 2 つのレベル階層に変換されます**Recordset**次の形式。

```console
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 ポートフォリオおよび情報のタグは、階層で表されないことに注意してください。 **Recordset**します。 XML の DSO に階層を XML ツリーを変換する方法の詳細については**レコード セット**、次の規則を参照してください。 $Text 列は、次のセクションについて説明します。

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>XML 要素の割り当てと属性を行と列のルール
 XML DSO では、要素を割り当てるための手順し、データ主体のアプリケーションの列と行に属性します。 XML は、階層全体を含む 1 つのタグを持つツリーとしてモデル化されます。 たとえば、本の XML の説明には」の章のタグには、図タグ、セクション タグが含まれます。 最上位レベルは、サブ要素」の章、図、およびセクションを含む、書籍のタグになります。 XML の DSO では、XML 要素を行と列にマップ、最上位レベル要素ではなく、サブ要素が変換されます。

 XML DSO は、サブ要素を変換するため、この手順を使用します。

-   各サブ要素と属性がいくつかの列に対応**レコード セット**階層にします。

-   列の名前がサブ要素または属性の名前と同じ親要素、属性と同じ名前のサブ要素を後者があるない限り、"!"サブ要素の列名に付加されます。

-   各列は、いずれかを*単純*スカラー値 (通常は文字列) を含む列または**レコード セット**子を含む列**レコード セット**します。

-   属性に対応する列は、常に単純です。

-   サブ要素に対応する列は**Recordset**場合は、サブ要素が、独自のサブ要素または属性 (または両方)、またはサブ要素の親が子としてのサブ要素の 1 つ以上のインスタンスのいずれかの列。 それ以外の場合、列は簡単です。

-   (別の親) の下のサブ要素の複数のインスタンスが存在する場合、その列を**レコード セット**列場合*任意*インスタンスの意味を**レコード セット**列、列が単純な場合にのみ*すべて*インスタンスが単純な列を意味します。

-   すべて**レコード セット**ある $Text という名前の列を追加します。

 構築するために必要なコードを**レコード セット**のとおりです。

```vb
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "https://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  4 つの異なる名前付け規則を使用して、データ ファイルのパスを指定できます。

```vb
'HTTP://
adoRS.Open "https://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 すぐに、**レコード セット**が開かれた、通常、ADO **Recordset**ナビゲーション コマンドを使用できます。

 **レコード セット**OSP によって生成されるいくつかの制限があります。

-   クライアント カーソル (**adUseClient**) はサポートされていません。

-   階層**レコード セット**任意に作成された XML で保存できません**Recordset.Save**します。

-   **レコード セット**OSP で作成された読み取り専用です。

-   XMLDSO を各 $Text のデータの追加の列を追加します**Recordset**階層にします。

 OLE DB 単純なプロバイダーの詳細については、次を参照してください。[単純なプロバイダーを構築](https://msdn.microsoft.com/b31a6cba-58ae-4ee8-9039-700973d354d6)します。

## <a name="code-example"></a>コード例
 Visual Basic コードを次に示します、階層を構築する任意の XML ファイルを開く**レコード セット**、およびそれぞれの各レコードの書き込みを再帰的に**レコード セット**デバッグ ウィンドウにします。

 株価情報を含む単純な XML ファイルを次に示します。 次のコードはこのファイルを使用して 2 つのレベル階層を構築する**Recordset**します。

```xml
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>https://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>https://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>https://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>https://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 Visual Basic の 2 つのサブ プロシージャを次に示します。 最初の作成、 **Recordset**に渡されます、 *WalkHier* sub プロシージャ、再帰的には、それぞれの書き込み、階層の下位でについて説明します**フィールド**で各レコードごとに**Recordset**デバッグ ウィンドウにします。

```vb
Private Sub BrowseHierRecordset()
' Add ADO 2.7 or later to Project/References
' No need to add MSXML2, ADO just passes the ProgID through to the OSP.

    Dim adoConn As ADODB.Connection
    Dim adoRS As ADODB.Recordset
    Dim adoChildRS As ADODB.Recordset

    Set adoConn = New ADODB.Connection
    Set adoRS = New ADODB.Recordset
    Set adoChildRS = ADODB.Recordset

    adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
    adoRS.Open "https://bwillett3/Kowalski/portfolio.xml", adoConn

    Dim iLevel As Integer
    iLevel = 0
    WalkHier iLevel, adoRS

End Sub

Sub WalkHier(ByVal iLevel As Integer, ByVal adoRS As ADODB.Recordset)
    iLevel = iLevel + 1
    PriorLevel = iLevel
    While Not adoRS.EOF
        For ndx = 0 To adoRS.Fields.Count - 1
            If adoRS.Fields(ndx).Name <> "$Text" Then
                If adoRS.Fields(ndx).Type = adChapter Then
                    Set adoChildRS = adoRS.Fields(ndx).Value
                    WalkHier iLevel, adoChildRS
                Else
                    Debug.Print iLevel & ": adoRS.Fields(" & ndx & _
                       ") = " & adoRS.Fields(ndx).Name & " = " & _
                       adoRS.Fields(ndx).Value
                End If
            End If
        Next ndx
        adoRS.MoveNext
    Wend
    iLevel = PriorLevel
End Sub
```
