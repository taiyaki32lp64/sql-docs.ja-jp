---
title: データ フロー コンポーネントのログ エントリの記録と定義 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- logs [Integration Services], custom
- custom log entries [Integration Services]
- custom data flow components [Integration Services], logging
- data flow components [Integration Services], logging
ms.assetid: 2190dba9-59b5-480b-b8e9-21d5a54c5917
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e4b328e1e39646f9b47e66bd313940de768ea73c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768648"
---
# <a name="logging-and-defining-log-entries-in-a-data-flow-component"></a>データ フロー コンポーネントのログ エントリの記録と定義
  カスタム データ フロー コンポーネントは、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.PostLogMessage%2A> インターフェイスの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> メソッドを使用して既存のログ エントリにメッセージを送信できます。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A> メソッドまたは <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> インターフェイスの同様のメソッドを使用して、ユーザーに情報を提供することもできます。 ただし、この方法では追加のイベントの発生と処理によるオーバーヘッドが発生し、ユーザーにとって意味のあるメッセージの詳細情報メッセージをユーザーが取捨選択する必要があります。 次に示す方法でカスタム ログ エントリを使用すると、明確にラベル付けされたカスタム ログ情報をコンポーネントのユーザーに提供できます。  
  
## <a name="registering-and-using-a-custom-log-entry"></a>カスタム ログ エントリの登録と使用  
  
### <a name="registering-a-custom-log-entry"></a>カスタム ログ エントリの登録  
 コンポーネントで使用するためにカスタム ログ エントリを登録するには、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterLogEntries%2A> 基本クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> メソッドをオーバーライドします。 次の例では、カスタム ログ エントリを登録し、名前と説明を入力します。  
  
```csharp  
using Microsoft.SqlServer.Dts.Runtime;  
...  
private const string MyLogEntryName = "My Custom Component Log Entry";  
private const string MyLogEntryDescription = "Log entry from My Custom Component ";  
...  
    public override void RegisterLogEntries()  
    {  
      this.LogEntryInfos.Add(MyLogEntryName,  
        MyLogEntryDescription,  
        Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT);  
    }  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
...  
Private Const MyLogEntryName As String = "My Custom Component Log Entry"   
Private Const MyLogEntryDescription As String = "Log entry from My Custom Component "  
...  
Public  Overrides Sub RegisterLogEntries()   
  Me.LogEntryInfos.Add(MyLogEntryName, _  
    MyLogEntryDescription, _  
    Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT)   
End Sub  
```  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency> 列挙は、イベントのログが記録される頻度に関するヒントをランタイムに提供します。  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_OCCASIONAL>:毎回実行時ではなく、不定期でイベントのログが記録されます。  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT>:毎回実行時に一定の回数でイベントのログが記録されます。  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_PROPORTIONAL>:完了した作業量に比例する回数だけイベントのログが記録されます。  
  
 上の例では、コンポーネントが実行ごとに 1 回エントリのログを記録するため、<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT> を使用します。  
  
 カスタム ログ エントリを登録し、カスタム コンポーネントのインスタンスをデータ フローのデザイナー画面に追加したら、デザイナーの **[ログ記録]** ダイアログ ボックスの使用可能なログ エントリの一覧に、"My Custom Component Log Entry" という名前の新しいログ エントリが表示されます。  
  
### <a name="logging-to-a-custom-log-entry"></a>カスタム ログ エントリへのログ記録  
 カスタム ログ エントリを登録したら、コンポーネントがカスタム メッセージのログを記録できるようになります。 次の例では、コンポーネントによって使用される SQL ステートメントのテキストを含む <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> メソッドの実行時にカスタム ログ エントリを記述します。  
  
```csharp  
public override void PreExecute()  
{  
  DateTime now = DateTime.Now;  
  byte[] additionalData = null;  
  this.ComponentMetaData.PostLogMessage(MyLogEntryName,  
    this.ComponentMetaData.Name,  
    "Command Sent was: " + myCommand.CommandText,  
    now, now, 0, ref additionalData);  
}  
```  
  
```vb  
Public  Overrides Sub PreExecute()   
  Dim now As DateTime = DateTime.Now   
  Dim additionalData As Byte() = Nothing   
  Me.ComponentMetaData.PostLogMessage(MyLogEntryName, _  
    Me.ComponentMetaData.Name, _  
    "Command Sent was: " + myCommand.CommandText, _  
    now, now, 0, additionalData)   
End Sub  
```  
  
 ユーザーがパッケージを実行し、**[ログ記録]** ダイアログ ボックスで [My Custom Component Log Entry] を選択すると、「User::My Custom Component Log Entry」というラベルが付けられたエントリがログに含まれます。 この新しいログ エントリには、SQL ステートメントのテキスト、タイムスタンプ、および開発者によってログが記録された追加のデータが含まれます。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のログ記録](../../performance/integration-services-ssis-logging.md)  
  
  
