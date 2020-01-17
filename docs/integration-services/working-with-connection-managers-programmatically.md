---
title: プログラムによる接続マネージャーの操作 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4dff74cd1e21ba743fa425bb632c736ee1cce158
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295005"
---
# <a name="working-with-connection-managers-programmatically"></a>プログラムによる接続マネージャーの操作

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、関連付けられた接続マネージャー クラスの AcquireConnection メソッドは、マネージド コードで接続マネージャーを操作する場合に呼び出すことの多いメソッドです。 マネージド コードを記述する場合、接続マネージャーの機能を使用するには AcquireConnection メソッドを呼び出す必要があります。 このメソッドは、マネージド コードを記述する場所がスクリプト タスク、スクリプト コンポーネント、カスタム オブジェクト、またはカスタム アプリケーションのいずれであっても、呼び出す必要があります。  
  
 AcquireConnection メソッドを正常に呼び出すには、次の点を理解しておく必要があります。  
  
-   **AcquireConnection メソッドからマネージド オブジェクトを返す接続マネージャーはどれか**  
  
     多くの接続マネージャーはアンマネージド COM オブジェクト (System.__ComObject) を返します。このオブジェクトをマネージド コードから使用するのは簡単ではありません。 このような接続マネージャーには、使用頻度の高い OLE DB 接続マネージャーも含まれます。  
  
-   **マネージド オブジェクトを返す接続マネージャーの AcquireConnection メソッドによって返されるオブジェクトは何か**  
  
     戻り値を適切な型にキャストするには、AcquireConnection メソッドによって返されるオブジェクトの型を把握しておく必要があります。 たとえば、SqlClient プロバイダーを使用する場合、[!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャーの AcquireConnection メソッドは、開かれている SqlConnection オブジェクトを返します。 これに対し、ファイル接続マネージャーの AcquireConnection メソッドは、文字列のみを返します。  
  
 このトピックでは、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] に付属の接続マネージャーについて、上記の点を説明します。  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>マネージド オブジェクトを返さない接続マネージャー  
 次の表に、AcquireConnection メソッドからネイティブ COM オブジェクト (System.__ComObject) を返す接続マネージャーを示します。 これらのアンマネージド オブジェクトは、マネージド コードから簡単には使用できません。  
  
|接続マネージャーの種類|接続マネージャー名|  
|-----------------------------|-----------------------------|  
|ADO (ADO)|ADO 接続マネージャー|  
|MSOLAP90|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 接続マネージャー|  
|EXCEL|Excel 接続マネージャー|  
|FTP|FTP 接続マネージャー|  
|HTTP|HTTP 接続マネージャー|  
|ODBC|ODBC 接続マネージャー|  
|OLEDB|OLE DB 接続マネージャー|  
  
 通常は、マネージド コードから [!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャーを使用すると、ADO、Excel、ODBC、または OLE DB の各データ ソースに接続できます。  
  
## <a name="return-values-from-the-acquireconnection-method"></a>AcquireConnection メソッドからの戻り値  
 次の表に、AcquireConnection メソッドからマネージド オブジェクトを返す接続マネージャーを示します。 これらのマネージド オブジェクトは、マネージド コードから簡単に使用できます。  
  
|接続マネージャーの種類|接続マネージャー名|戻り値の型|追加情報|  
|-----------------------------|-----------------------------|--------------------------|----------------------------|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|[!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャー|**System.Data.SqlClient.SqlConnection**||  
|FILE|ファイル接続マネージャー|**System.String**|ファイルへのパス。|  
|FLATFILE|フラット ファイル接続マネージャー|**System.String**|ファイルへのパス。|  
|MSMQ (MSMQ)|MSMQ 接続マネージャー|**System.Messaging.MessageQueue**||  
|MULTIFILE|複数ファイル接続マネージャー|**System.String**|いずれかのファイルへのパス。|  
|MULTIFLATFILE|複数フラット ファイル接続マネージャー|**System.String**|いずれかのファイルへのパス。|  
|SMOServer|SMO 接続マネージャー|**Microsoft.SqlServer.Management.Smo.Server**||  
|SMTP (SMTP)|SMTP 接続マネージャー|**System.String**|例: `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI (WMI)|WMI 接続マネージャー|**System.Management.ManagementScope**||  
|SQLMOBILE|SQL Server Compact 接続マネージャー|**System.Data.SqlServerCe.SqlCeConnection**||  
  
## <a name="see-also"></a>参照  
 [スクリプト タスクでのデータ ソースへの接続](../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [スクリプト コンポーネントでのデータ ソースへの接続](../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [カスタム タスクでのデータ ソースへの接続](../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  
