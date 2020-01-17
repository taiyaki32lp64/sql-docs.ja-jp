---
title: 外部メタデータの実装 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disconnected validation [Integration Services]
- connected validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- metadata [Integration Services]
- data flow components [Integration Services], validating
- data flow components [Integration Services], external metadata
- custom data flow components [Integration Services], external metadata
- external metadata [Integration Services]
ms.assetid: 8f5bd3ed-3e79-43a4-b6c1-435e4c2cc8cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 70e99073f07e7e285d1fcbfad51cf9a275dd9441
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896153"
---
# <a name="implementing-external-metadata"></a>外部メタデータの実装
  コンポーネントがそのデータ ソースから切断されると、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100> インターフェイスを使用することによって、入力および出力列のコレクション内の列を、その外部データ ソースの列に対して検証できます。 このインターフェイスを使用すると、外部データ ソースの列のスナップショットを保持し、これらの列をコンポーネントの入力および出力列コレクションの列にマップできます。  
  
 外部メタデータ列を実装することで、追加した列のコレクションに対する管理と検証の必要が生じるため、コンポーネントの開発にオーバーヘッドと複雑性が加わりますが、検証のためのサーバーへのラウンド トリップに余計な費用をかけなくても済むので、開発作業は行う価値のあるものになるでしょう。  
  
## <a name="populating-external-metadata-columns"></a>外部メタデータ列の設定  
 外部メタデータ列は、通常、対応する入力または出力列を作成するときにコレクションに追加されます。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.New%2A> メソッドを呼び出して、新しい列を作成します。 次に、外部データ ソースに一致するように列のプロパティを設定します。  
  
 外部メタデータ列を対応する入力または出力列にマップするには、外部メタデータ列の ID を入力または出力列の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> プロパティに割り当てます。 これにより、コレクションの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.GetObjectByID%2A> メソッドを使用して、特定の入力列または出力列に対する外部メタデータ列を簡単に探すことができます。  
  
 次の例では、外部メタデータ列を作成し、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> プロパティを設定することによって出力列にマップする方法を示します。  
  
```csharp  
public void CreateExternalMetaDataColumn(IDTSOutput100 output, int outputColumnID )  
{  
    IDTSOutputColumn100 oColumn = output.OutputColumnCollection.GetObjectByID(outputColumnID);  
    IDTSExternalMetadataColumn100 eColumn = output.ExternalMetadataColumnCollection.New();  
  
    eColumn.DataType = oColumn.DataType;  
    eColumn.Precision = oColumn.Precision;  
    eColumn.Scale = oColumn.Scale;  
    eColumn.Length = oColumn.Length;  
    eColumn.CodePage = oColumn.CodePage;  
  
    oColumn.ExternalMetadataColumnID = eColumn.ID;  
}  
```  
  
```vb  
Public Sub CreateExternalMetaDataColumn(ByVal output As IDTSOutput100, ByVal outputColumnID As Integer)   
 Dim oColumn As IDTSOutputColumn100 = output.OutputColumnCollection.GetObjectByID(outputColumnID)   
 Dim eColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New   
 eColumn.DataType = oColumn.DataType   
 eColumn.Precision = oColumn.Precision   
 eColumn.Scale = oColumn.Scale   
 eColumn.Length = oColumn.Length   
 eColumn.CodePage = oColumn.CodePage   
 oColumn.ExternalMetadataColumnID = eColumn.ID   
End Sub  
```  
  
## <a name="validating-with-external-metadata-columns"></a>外部メタデータ列での検証  
 検証を行うには、外部メタデータ列のコレクションを保持するための手順をコンポーネントに追加する必要があります。追加された列のコレクションに対して検証を行う必要があるためです。 検証は、接続された状態での検証と切断された状態での検証に分けられます。  
  
### <a name="connected-validation"></a>接続された状態での検証  
 コンポーネントが外部データ ソースに接続されると、入力または出力コレクション内の列は、外部データ ソースに対して直接検証されます。 また、外部メタデータのコレクション内の列を検証する必要があります。 外部メタデータのコレクションは [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] の **[詳細エディター]** による変更が可能なうえに、それによってコレクションに行われた変更は検出できないため、この検証が必要となります。 したがって、接続された状態のコンポーネントでは、外部メタデータ列のコレクション内の列が外部データ ソースの列を継続して反映していることを確認する必要があります。  
  
 内の外部メタデータ コレクションを非表示にすることができます、**高度なエディター**を設定して、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.IsUsed%2A>にコレクションのプロパティ`false`します。 ただし、この設定を行うと、入力または出力コレクションの列を外部メタデータ列のコレクションの列にマップするために使用する、エディターの **[列マッピング]** タブも非表示になります。 このプロパティを `false` に設定すると、開発者のプログラムによるコレクションの変更を妨げることなく、[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] でのみ使用されるコンポーネントの、外部メタデータ列のコレクションをある程度保護できます。  
  
### <a name="disconnected-validation"></a>切断された状態での検証  
 コンポーネントが外部データ ソースから切断されている場合、検証は簡略化されます。これは、外部ソースに対してではなく、外部メタデータのコレクション内の列に対して、入力または出力コレクション内の列が直接検証されるためです。 コンポーネントの外部データ ソースへの接続が確立されていない場合、または <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> プロパティが `false` の場合は、コンポーネントは切断された状態での検証を行う必要があります。  
  
 次のコード例は、コンポーネントの外部メタデータ列のコレクションに対し、検証を実行するコンポーネントの実装です。  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    if( this.isConnected && ComponentMetaData.ValidateExternalMetaData )  
    {  
        // TODO: Perform connected validation.  
    }  
    else  
    {  
        // TODO: Perform disconnected validation.  
    }  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
 If Me.isConnected AndAlso ComponentMetaData.ValidateExternalMetaData Then   
  ' TODO: Perform connected validation.  
 Else   
  ' TODO: Perform disconnected validation.  
 End If   
End Function  
```  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [データ フロー](../../data-flow/data-flow.md)  
  
  
