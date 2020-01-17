---
title: カスタム タスクの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom tasks [Integration Services], creating
ms.assetid: 42965c09-1782-4cdb-9ce1-216af4c23e0a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9123834f1c07a61fa0e1c48d29667d4d71ada359
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896118"
---
# <a name="creating-a-custom-task"></a>カスタム タスクの作成
  カスタム タスクの作成手順は、[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] の他のカスタム オブジェクトの作成手順と同様です。  
  
-   基本クラスを継承する新しいクラスを作成します。 タスク用の基本クラスは <xref:Microsoft.SqlServer.Dts.Runtime.Task> です。  
  
-   クラスに、オブジェクトの種類を識別する属性を適用します。 タスクの属性は <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> です。  
  
-   基本クラスのメソッドとプロパティの実装をオーバーライドします。 タスクでは、<xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> メソッドおよび <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> メソッドが対象です。  
  
-   必要に応じて、カスタム ユーザー インターフェイスを開発します。 タスクでは、<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> インターフェイスを実装するクラスが必要です。  
  
## <a name="getting-started-with-a-custom-task"></a>カスタム タスクの概要  
  
### <a name="creating-projects-and-classes"></a>プロジェクトおよびクラスの作成  
 すべてのマネージド タスクは <xref:Microsoft.SqlServer.Dts.Runtime.Task> 基本クラスから派生するため、カスタム タスクを作成するには、最初に任意のマネージド プログラミング言語でクラス ライブラリ プロジェクトを作成し、基本クラスを継承するクラスを作成します。 この派生クラスで、基本クラスのメソッドとプロパティをオーバーライドして、カスタム機能を実装します。  
  
 同じソリューション内に、もう 1 つのクラス ライブラリ プロジェクトをカスタム ユーザー インターフェイス用に作成します。 配置を容易にするため、ユーザー インターフェイス用に別個のアセンブリを使用することをお勧めします。そうすれば、接続マネージャーやそのユーザー インターフェイスの更新や再配置を個別に行うことができます。  
  
 どちらのプロジェクトも、アセンブリに署名するよう構成します。アセンブリは、厳密な名前のキー ファイルを使用して、ビルド時に生成されます。  
  
### <a name="applying-the-dtstask-attribute"></a>DtsTask 属性の適用  
 作成したクラスに <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 属性を適用して、そのクラスがタスクとして識別されるようにします。 この属性には、名前、説明、およびタスクの種類など、デザイン時の情報を指定します。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A> プロパティを使用して、タスクをそのカスタム ユーザー インターフェイスにリンクします。 このプロパティに必要な公開キー トークンを取得するには、**sn.exe -t** を使用して、ユーザー インターフェイス アセンブリへの署名に使用するキー ペア (.snk) ファイルから公開キー トークンを表示します。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.SSIS.Samples  
{  
  [DtsTask  
  (  
   DisplayName = "MyTask",  
   IconResource = "MyTask.MyTaskIcon.ico",  
   UITypeName = "My Custom Task," +  
   "Version=1.0.0.0," +  
   "Culture = Neutral," +  
   "PublicKeyToken = 12345abc6789de01",  
   TaskType = "PackageMaintenance",  
   TaskContact = "MyTask; company name; any other information",  
   RequiredProductLevel = DTSProductLevel.None  
   )]  
  public class MyTask : Task  
  {  
    // Your code here.  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsTask(DisplayName:="MyTask", _  
 IconResource:="MyTask.MyTaskIcon.ico", _  
 UITypeName:="My Custom Task," & _  
 "Version=1.0.0.0,Culture=Neutral," & _  
 "PublicKeyToken=12345abc6789de01", _  
 TaskType:="PackageMaintenance", _  
 TaskContact:="MyTask; company name; any other information", _  
 RequiredProductLevel:=DTSProductLevel.None)> _  
Public Class MyTask  
  Inherits Task  
  
  ' Your code here.  
  
End Class 'MyTask  
```  
  
## <a name="building-deploying-and-debugging-a-custom-task"></a>カスタム タスクの作成、配置、およびデバッグ  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] でカスタム タスクを作成、配置、およびデバッグする手順は、その他の種類のカスタム オブジェクトで必要な手順とほとんど同様です。 詳細については、「[カスタム オブジェクトのビルド、配置、デバッグ](../building-deploying-and-debugging-custom-objects.md)」を参照してください。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [カスタム タスクの作成](creating-a-custom-task.md)   
 [カスタム タスクのコーディング](coding-a-custom-task.md)   
 [カスタム タスク用ユーザー インターフェイスの開発](developing-a-user-interface-for-a-custom-task.md)  
  
  
