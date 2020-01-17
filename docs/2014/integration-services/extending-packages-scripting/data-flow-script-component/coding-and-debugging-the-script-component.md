---
title: スクリプト コンポーネントのコーディングおよびデバッグ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, development environment
- Script component [Integration Services], debugging
- Script component [Integration Services], coding
- SSIS Script component, debugging
- Script component [Integration Services], development environment
- debugging [Integration Services], scripts
- SSIS Script component, coding
- VSTA
ms.assetid: c3913c15-66aa-4b61-89b5-68488fa5f0a4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fd4153aaaf0fdffe32ce48db872a43cb5dbb84c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62894796"
---
# <a name="coding-and-debugging-the-script-component"></a>スクリプト コンポーネントのコーディングおよびデバッグ
  [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでは、スクリプト コンポーネントにメタデータ デザイン モードとコード デザイン モードの 2 つのモードがあります。 **[スクリプト変換エディター]** を開くと、スクリプト コンポーネントはメタデータ デザイン モードになります。このモードでは、メタデータを構成し、コンポーネントのプロパティを設定します。 メタデータ デザイン モードで、スクリプト コンポーネントのプロパティを設定して、入力と出力を構成したら、コード デザイン モードに切り替えてカスタム スクリプトを記述できます。 メタデータ デザイン モードとコード デザイン モードについて詳しくは、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](configuring-the-script-component-in-the-script-component-editor.md)」をご覧ください。  
  
## <a name="writing-the-script-in-code-design-mode"></a>コード デザイン モードでのスクリプトの記述  
  
### <a name="script-component-development-environment"></a>スクリプト コンポーネント開発環境  
 スクリプトを記述するには、**[スクリプト変換エディター]** の **[スクリプト]** ページで **[スクリプトの編集]** をクリックし、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE を開きます。 VSTA IDE には、色分け表示が可能な [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] エディター、IntelliSense、オブジェクト ブラウザーなど、[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] .NET 環境での標準機能がすべて含まれています。  
  
 スクリプト コードは、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# で記述されます。 スクリプト言語を指定するには、**[スクリプト変換エディター]** で **[ScriptLanguage]** プロパティを設定します。 その他のプログラミング言語を使用する場合は、選択した言語でカスタム アセンブリを作成し、スクリプト コンポーネント内のコードからその機能を呼び出すことができます。  
  
 スクリプト コンポーネントで作成したスクリプトは、パッケージ定義に格納されます。 スクリプト ファイルが別途存在するわけではありません。 したがって、スクリプト コンポーネントを使用してもパッケージの配置には影響しません。  
  
> [!NOTE]  
>  パッケージをデザインする際、スクリプト コードは一時的にプロジェクト ファイルに書き込まれます。 機密情報をファイルに保存することはセキュリティ上危険であるため、パスワードなどの重要な情報はスクリプト コードに書き込まないことをお勧めします。  
  
 既定では、`Option Strict` が IDE で無効になっています。  
  
### <a name="script-component-project-structure"></a>スクリプト コンポーネント プロジェクトの構造  
 スクリプト コンポーネントの威力は、インフラストラクチャ コードを生成して、記述する必要のあるコード量を減らす機能にあります。 この機能を実現するには、入力と出力、およびその列とプロパティが固定され、既知である必要があります。 したがって、コンポーネントのメタデータに後で変更を加えた場合、記述したコードが無効になり、 パッケージの実行中にコンパイル エラーが発生する可能性があります。  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>スクリプト コンポーネント プロジェクトのプロジェクト アイテムおよびクラス  
 コード デザイン モードに切り替えると、VSTA IDE が開き、`ScriptMain` プロジェクト アイテムが表示されます。 `ScriptMain` プロジェクト アイテムには、編集可能な `ScriptMain` クラスが含まれています。このクラスは、スクリプトのエントリ ポイントとしての役割を果たし、ここにコードを記述します。 このクラスのコード要素は、スクリプト タスクに対して選択したプログラミング言語に応じて異なります。  
  
 スクリプト プロジェクトには、次の 2 つの読み取り専用のプロジェクト アイテムが自動生成され、追加されます。  
  
-   次の 3 つのクラスを含む `ComponentWrapper` プロジェクト アイテム。  
  
    -   `UserComponent` クラス。<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> から継承され、データの処理およびパッケージとのやり取りに使用するメソッドおよびプロパティが含まれています。 `ScriptMain` クラスは `UserComponent` クラスから継承されます。  
  
    -   `Connections` コレクション クラス。[スクリプト変換エディター] の [接続マネージャー] ページで選択された、接続への参照が含まれています。  
  
    -   A`Variables`で入力された変数への参照を格納するコレクション クラス、`ReadOnlyVariable`と`ReadWriteVariables`プロパティを**スクリプト**のページ、**スクリプト変換エディター**.  
  
-   `BufferWrapper`プロジェクト アイテムにはから継承するクラスが含まれています<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>各入力と出力で構成されている、**入力と出力**のページ、**スクリプト変換エディター**します。 これらの各クラスには、構成された入力列と出力列、およびそれらの列が含まれるデータ フロー バッファーに対応する、型指定されたアクセサー プロパティが含まれています。  
  
 これらのオブジェクト、メソッド、およびプロパティの使用方法については、「[スクリプト コンポーネントのオブジェクト モデルについて](understanding-the-script-component-object-model.md)」をご覧ください。 特定の種類のスクリプト コンポーネントで、これらのクラスのメソッドおよびプロパティを使用する方法については、セクション「[その他のスクリプト コンポーネントの例](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)」をご覧ください。 サンプルについてのトピックでは、完全なコード例も示します。  
  
 スクリプト コンポーネントを変換として構成するときに、`ScriptMain`プロジェクト項目には、次の自動生成されたコードが含まれています。 コード テンプレートでも、スクリプト コンポーネントの概要、および、変数、イベント、接続など、SSIS オブジェクトを取得および操作する方法に関する追加情報を提供します。  
  
```vb  
' Microsoft SQL Server Integration Services Script Component  
' Write scripts using Microsoft Visual Basic 2008.  
' ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
<Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute> _  
<CLSCompliant(False)> _  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub PreExecute()  
        MyBase.PreExecute()  
        '  
        ' Add your code here for preprocessing or remove if not needed  
        '  
    End Sub  
  
    Public Overrides Sub PostExecute()  
        MyBase.PostExecute()  
        '  
        ' Add your code here for postprocessing or remove if not needed  
        ' You can set read/write variables here, for example:  
        ' Me.Variables.MyIntVar = 100  
        '  
    End Sub  
  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
        '  
        ' Add your code here  
        '  
    End Sub  
  
End Class  
```  
  
```csharp  
/* Microsoft SQL Server Integration Services user script component  
*  Write scripts using Microsoft Visual C# 2008.  
*  ScriptMain is the entry point class of the script.*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
[Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute]  
public class ScriptMain : UserComponent  
{  
  
    public override void PreExecute()  
    {  
        base.PreExecute();  
        /*  
          Add your code here for preprocessing or remove if not needed  
        */  
    }  
  
    public override void PostExecute()  
    {  
        base.PostExecute();  
        /*  
          Add your code here for postprocessing or remove if not needed  
          You can set read/write variables here, for example:  
          Variables.MyIntVar = 100  
        */  
    }  
  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
        /*  
          Add your code here  
        */  
    }  
  
}  
```  
  
#### <a name="additional-project-items-in-the-script-component-project"></a>スクリプト コンポーネント プロジェクトのその他のプロジェクト アイテム  
 スクリプト コンポーネント プロジェクトには、既定の `ScriptMain` アイテム以外のアイテムを格納できます。 プロジェクトには、クラス、モジュール、コード ファイル、およびフォルダーを追加できます。また、フォルダーを使用してアイテムのグループを整理できます。  
  
 追加したすべてのアイテムは、パッケージ内部に保存されます。  
  
#### <a name="references-in-the-script-component-project"></a>スクリプト コンポーネント プロジェクトの参照  
 参照をマネージド アセンブリに追加するには、**[プロジェクト エクスプローラー]** でスクリプト タスク プロジェクトを右クリックし、**[参照の追加]** をクリックします。 詳しくは、「[スクリプティング ソリューションでの他のアセンブリの参照](../referencing-other-assemblies-in-scripting-solutions.md)」をご覧ください。  
  
> [!NOTE]  
>  プロジェクト参照は、VSTA IDE の **[クラス ビュー]** または**プロジェクト エクスプローラー**で表示できます。 どちらのウィンドウも **[表示]** メニューから開きます。 新しい参照は、**[プロジェクト]** メニュー、**プロジェクト エクスプローラー**、または **[クラス ビュー]** から追加できます。  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>スクリプト コンポーネント内でのパッケージとの対話  
 スクリプト コンポーネント内で記述するカスタム スクリプトは、自動生成された基本クラス内の、厳密に型指定されたアクセサーを使用して、コンポーネントに含まれているパッケージの変数や接続マネージャーにアクセスし、それらを使用できます。 ただし、変数および接続マネージャーをスクリプトで使用できるようにするには、コード デザイン モードに切り替える前に、その両方を設定する必要があります。 また、スクリプト コンポーネントのコードから、イベントを発生させたり、ログ記録を実行することもできます。  
  
 スクリプト コンポーネント プロジェクト内に自動生成されるプロジェクト アイテムには、パッケージと情報をやり取りするために、以下のオブジェクト、メソッド、およびプロパティが用意されています。  
  
|パッケージの機能|アクセス方法|  
|---------------------|-------------------|  
|変数:|`Variables` プロジェクト アイテムの `ComponentWrapper` コレクション クラス内の、名前付きで型指定されたアクセサー プロパティを使用します。これは `Variables` クラスの `ScriptMain` プロパティを介して公開されています。<br /><br /> `PreExecute` メソッドでは、読み取り専用変数にのみアクセスできます。 `PostExecute` メソッドでは、読み取り専用変数および読み取り/書き込み変数の両方にアクセスできます。|  
|接続|`Connections` プロジェクト アイテムの `ComponentWrapper` コレクション クラス内の、名前付きで型指定されたアクセサー プロパティを使用します。これは `Connections` クラスの `ScriptMain` プロパティを介して公開されています。|  
|イベント|使用してイベントを発生させる、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>のプロパティ、`ScriptMain`クラスおよび**火災\<X >** のメソッド、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>インターフェイス。|  
|ログの記録|`ScriptMain` クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> メソッドを使用して、ログ記録を実行します。|  
  
## <a name="debugging-the-script-component"></a>スクリプト コンポーネントのデバッグ  
 スクリプト コンポーネントのコードをデバッグするには、コードに少なくとも 1 つのブレークポイントを設定し、VSTA IDE を閉じて [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] でパッケージを実行します。 パッケージが実行されてスクリプト コンポーネントが開始されると、VSTA IDE が再度開き、読み取り専用モードでコードが表示されます。 実行によりブレークポイントに到達したら、変数の値の検証や、残りのコードのステップ スルーができます。  
  
> [!NOTE]  
>  パッケージ実行タスクから実行されている子パッケージの一部としてスクリプト コンポーネントを実行する場合は、スクリプト コンポーネントをデバッグできません。 このような場合は、子パッケージのスクリプト コンポーネント内で設定したブレークポイントは無視されます。 子パッケージを単独で実行することにより、通常どおりパッケージをデバッグできます。  
  
> [!NOTE]  
>  複数のスクリプト コンポーネントが含まれるパッケージをデバッグする場合、デバッガーによってデバッグされるスクリプト コンポーネントは 1 つです。 Foreach ループまたは For ループ コンテナーの場合と同様に、デバッガーが完了した場合、システムは別のスクリプト コンポーネントをデバッグできます。  
  
 ただし、次の方法を使用することにより、スクリプト コンポーネントの実行を監視することもできます。  
  
-   実行を中断しを使用して、モーダル メッセージを表示、`MessageBox.Show`メソッドで、 **System.Windows.Forms**名前空間。 デバッグが完了したら、このコードは削除してください。  
  
-   情報メッセージ、警告、およびエラーを発生させます。 FireInformation、FireWarning、FireError の各メソッドでは、イベントの説明が Visual Studio の **[出力]** ウィンドウに表示されます。 ただし、FireProgress メソッド、Console.Write メソッド、および Console.WriteLine メソッドでは、**[出力]** ウィンドウに情報は表示されません。 FireProgress イベントからのメッセージが [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーの **[進行状況]** タブに表示されます。 詳しくは、「[スクリプト コンポーネントでのイベントの発生](../../data-flow/transformations/script-component.md)」をご覧ください。  
  
-   イベントまたはユーザー定義のメッセージを、有効なログ プロバイダーに記録します。 詳しくは、「[スクリプト コンポーネントでのログ記録](logging-in-the-script-component.md)」をご覧ください。  
  
 データを変換先に保存せずに、変換元または変換として構成されたスクリプト コンポーネントの出力を調べるだけの場合は、[行数変換](../../data-flow/transformations/row-count-transformation.md)を使ってデータ フローを終了し、スクリプト コンポーネントの出力にデータ ビューアーをアタッチできます。 データ ビューアーについて詳しくは、「[データ フローのデバッグ](../../troubleshooting/debugging-data-flow.md)」をご覧ください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 スクリプト コンポーネントのコーディングの詳細については、このセクションの次のトピックを参照してください。  
  
 [スクリプト コンポーネントのオブジェクト モデルについて](understanding-the-script-component-object-model.md)  
 スクリプト コンポーネントで使用できる、オブジェクト、メソッド、およびプロパティの使用方法について説明します。  
  
 [スクリプティング ソリューションでの他のアセンブリの参照](../referencing-other-assemblies-in-scripting-solutions.md)  
 スクリプト コンポーネントで、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] クラス ライブラリのオブジェクトを参照する方法について説明します。  
  
 [スクリプト コンポーネントに対するエラー出力のシミュレート](../../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 スクリプト コンポーネントによる処理中にエラーを発生させる行の、エラー出力のシミュレーション方法について説明します。  
  
## <a name="external-resources"></a>外部リソース  
  
-   blogs.msdn.com のブログ「[VSTA setup and configuration troubles for SSIS 2008 and R2 installations](https://go.microsoft.com/fwlink/?LinkId=215661)」(SSIS 2008 インストールおよび R2 インストールでの VSTA のセットアップと構成に関する問題)。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](configuring-the-script-component-in-the-script-component-editor.md)  
  
  
