---
title: スクリプト コンポーネントでのデータ ソースへの接続 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96041fa9b632be0162259d72cd4001e9d7defdd5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768458"
---
# <a name="connecting-to-data-sources-in-the-script-component"></a>スクリプト コンポーネントでのデータ ソースへの接続
  接続マネージャーは、便宜上、特定の種類のデータ ソースに接続するために必要な情報をカプセル化して格納するユニットです。 詳細については、「[Integration Services (SSIS) の接続](../../connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
 既存の接続マネージャーを、変換元または変換先コンポーネントのカスタム スクリプトでアクセスできるようにするには、 **[スクリプト変換エディター]** の **[接続マネージャー]**  ページで、 **[追加]** および **[削除]**  ボタンをクリックします。 ただし、データの読み込みや保存、場合によってはデータ ソースとの接続や切断を行うためには、独自のカスタム コードを記述する必要があります。 **[スクリプト変換エディター]** の **[接続マネージャー]** ページの詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](configuring-the-script-component-in-the-script-component-editor.md)」および「[スクリプト変換エディター &#40;[接続マネージャー] ページ&#41;](../../script-transformation-editor-connection-managers-page.md)」を参照してください。  
  
 スクリプト コンポーネントは、`Connections` プロジェクト アイテム内に `ComponentWrapper` コレクション クラスを作成します。ここには、各接続マネージャーに対して、接続マネージャー自体と同じ名前を持つ、厳密に型指定されたアクセサー プロパティが含まれています。 このコレクションは、`Connections` クラスの `ScriptMain` プロパティを介して公開されます。 アクセサー プロパティは、接続マネージャーへの参照を <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> のインスタンスとして返します。 たとえば、ダイアログ ボックスの [接続マネージャー] ページで `MyADONETConnection` という名前の接続マネージャーを追加した場合、次のコードを追加することで、スクリプト内のその接続マネージャーへの参照を取得できます。  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  `AcquireConnection` を呼び出す前に、接続マネージャーによって返される接続のデータ型を知っておく必要があります。 スクリプト タスクでは `Option Strict` が有効なので、`Object` 型として返される接続は、使用する前に適切な種類の接続にキャストする必要があります。  
  
 次に、特定の接続マネージャーの `AcquireConnection` メソッドを呼び出して、基になる接続、またはデータ ソースへの接続に必要な情報を取得します。 たとえば、次のコードを使用すると、ADO.NET 接続マネージャーによってラップされた **System.Data.SqlConnection** への参照を取得できます。  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 これに対し、同じ呼び出しをフラット ファイル接続マネージャーに対して行った場合、ファイル データ ソースのパスとファイル名のみが返されます。  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 フラット ファイルからデータを読み取る、またはそのファイルにデータを書き込むためには、このパスとファイル名を、`System.IO.StreamReader` または `Streamwriter` に渡す必要があります。  
  
> [!IMPORTANT]  
>  スクリプト コンポーネントでマネージド コードを記述する場合、OLE DB 接続マネージャーや Excel 接続マネージャーなど、アンマネージド オブジェクトを返す接続マネージャーの AcquireConnection メソッドを呼び出すことはできません。 ただし、これらの接続マネージャーの ConnectionString プロパティを読み取り、**System.Data.OleDb** 名前空間の OLEDB **接続**の接続文字列を使用することにより、コード内でデータ ソースに直接接続することができます。  
>   
>  アンマネージ オブジェクトを返す接続マネージャーの AcquireConnection メソッドを呼び出す必要がある場合は、ADO.NET 接続マネージャーを使用してください。 OLE DB プロバイダーを使用するように ADO.NET 接続マネージャーを設定すると、接続には .NET Framework Data Provider for OLE DB が使用されます。 この場合、AcquireConnection メソッドを返します、`System.Data.OleDb.OleDbConnection`非管理対象のオブジェクトの代わりにします。 ADO.NET 接続マネージャーで Excel データ ソースを使用するように設定するには、Microsoft OLE DB Provider for Jet を選択して Excel ワークブックを指定し、 **[接続マネージャー]** ダイアログ ボックスの **[すべて]** ページにある **[拡張プロパティ]** の値に「`Excel 8.0`」(Excel 97 以降の場合) と入力します。  
  
 スクリプト コンポーネントを使用して接続マネージャーを使用する方法の詳細については、「[スクリプト コンポーネントによる変換元の作成](../../extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)」および「[スクリプト コンポーネントによる変換先の作成](../../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)」を参照してください。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services &#40;SSIS&#41; の接続](../../connection-manager/integration-services-ssis-connections.md)   
 [接続マネージャーを作成する](../../create-connection-managers.md)  
  
  
