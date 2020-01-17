---
title: スクリプト タスクでのデータ ソースへの接続 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- connections [Integration Services], scripts
- Integration Services packages, connections
- connection managers [Integration Services], scripts
- scripts [Integration Services], connections
- SSIS packages, connections
- packages [Integration Services], connections
- Script task [Integration Services], connections
- Connections property
- SQL Server Integration Services packages, connections
- SSIS Script task, connections
ms.assetid: 9c008380-715b-455b-9da7-22572d67c388
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bda11bd7e4a3cdb90dde0cba5992c91f6fffd7f9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296908"
---
# <a name="connecting-to-data-sources-in-the-script-task"></a>スクリプト タスクでのデータ ソースへの接続

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  接続マネージャーは、パッケージ内に構成されたデータ ソースへのアクセスを提供します。 詳細については、「[Integration Services (SSIS) の接続](../../../integration-services/connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
 スクリプト タスクは、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> プロパティを介して、これらの接続マネージャーにアクセスできます。 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> コレクション内の各接続マネージャーは、基になるデータ ソースへの接続方法に関する情報を格納しています。  
  
 接続マネージャーの <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> メソッドを呼び出すと、その接続マネージャーがまだ接続されていない場合、データ ソースに接続され、ユーザーのスクリプト タスク コードで使用する適切な接続または接続情報が返されます。  
  
> [!NOTE]  
>  **AcquireConnection** を呼び出す前に、接続マネージャーによって返される接続の種類を知っておく必要があります。 スクリプト タスクでは **Option Strict** が有効なので、**Object** 型として返される接続は、使用する前に適切な種類の接続にキャストする必要があります。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> プロパティによって返される <xref:Microsoft.SqlServer.Dts.Runtime.Connections> コレクションの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> メソッドを使用すると、既存の接続をコードで使用する前に検索できます。  
  
> [!IMPORTANT]  
>  スクリプト タスクのマネージド コードでは、OLE DB 接続マネージャーや Excel 接続マネージャーなど、アンマネージド オブジェクトを返す接続マネージャーの AcquireConnection メソッドを呼び出すことはできません。 ただし、これらの接続マネージャーの ConnectionString プロパティを読み取り、**System.Data.OleDb** 名前空間の **OledbConnection** と共に接続文字列を使用することにより、コード内でデータ ソースに直接接続することができます。  
>   
>  アンマネージ オブジェクトを返す接続マネージャーの AcquireConnection メソッドを呼び出す必要がある場合は、[!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 接続マネージャーを使用してください。 OLE DB プロバイダーを使用するように [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 接続マネージャーを構成すると、接続には [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Data Provider for OLE DB が使用されます。 この場合、AcquireConnection メソッドは、アンマネージ オブジェクトではなく **System.Data.OleDb.OleDbConnection** を返します。 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 接続マネージャーで Excel データ ソースを使用するように構成するには、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider for Jet を選択して Excel ファイルを指定し、 **[接続マネージャー]** ダイアログ ボックスの **[すべて]** ページにある **[拡張プロパティ]** の値に「`Excel 8.0`」(Excel 97 以降の場合) と入力します。  
  
## <a name="connections-example"></a>接続の例  
 次の例では、スクリプト タスク内での接続マネージャーへのアクセス方法を示します。 このサンプルでは、**Test ADO.NET Connection** という名前の [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 接続マネージャーと **Test Flat File Connection** という名前のフラット ファイル接続マネージャーが作成および構成済みであることを前提にしています。 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 接続マネージャーは、データ ソースに接続するときにすぐに使用できる **SqlConnection** オブジェクトを返します。 これに対し、フラット ファイル接続マネージャーは、パスとファイル名が含まれる文字列のみを返します。 フラット ファイルを開いて作業するには、**System.IO** 名前空間のメソッドを使用する必要があります。  
  
```vb  
    Public Sub Main()

        Dim myADONETConnection As SqlClient.SqlConnection =
            DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction),
                SqlClient.SqlConnection)
        MsgBox(myADONETConnection.ConnectionString,
            MsgBoxStyle.Information, "ADO.NET Connection")

        Dim myFlatFileConnection As String =
            DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction),
                String)
        MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")

        Dts.TaskResult = ScriptResults.Success

    End Sub
```  
  
```csharp  
        public void Main()
        {
            SqlConnection myADONETConnection = 
                Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)
                as SqlConnection;
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");

            string myFlatFileConnection = 
                Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) 
                as string;
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");

            Dts.TaskResult = (int)ScriptResults.Success;
        }
```  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の接続](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [接続マネージャーを作成する](https://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
