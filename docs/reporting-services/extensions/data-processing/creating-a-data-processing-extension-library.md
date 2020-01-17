---
title: データ処理拡張機能ライブラリの作成 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 82f4b71b-dd39-467d-8d8c-6771eb2b12de
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7e3c3f4a30b828b889ebfe61617460ff58962fdc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194071"
---
# <a name="creating-a-data-processing-extension-library"></a>データ処理拡張機能ライブラリの作成
  作成する各 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能は、一意の名前空間に割り当てられ、ライブラリまたはアセンブリ ファイルに組み込まれている必要があります。 名前空間の正確な名前はあまり重要ではありませんが、名前は他の拡張機能とは共有しない一意のものである必要があります。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] と共に出荷されるデータ処理拡張機能に名前空間 <xref:Microsoft.ReportingServices.DataProcessing> を使用しています。 独自のデータ処理拡張機能を使用する場合は、重複しない一意な名前空間を作成してください。  
  
 次の例は、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能を開始するためのコードを示しています。データ処理インターフェイスとユーティリティ クラスを含む名前空間を使用しています。  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.DataProcessing  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.DataProcessing;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能をコンパイルする場合は、コンパイラに対して Microsoft.ReportingServices.Interfaces.dll への参照を指定する必要があります。データ処理拡張機能のインターフェイスがそこに格納されているためです。 <xref:Microsoft.ReportingServices.DataProcessing> 名前空間は、データ処理拡張機能インターフェイスを実装するために必要です。<xref:Microsoft.ReportingServices.Interfaces> 名前空間は、<xref:Microsoft.ReportingServices.Interfaces.IExtension> インターフェイスを実装するために必要です。 たとえば、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能を実装するための C# コードを含むすべてのファイルが、拡張子が .cs である 1 つのディレクトリに格納されている場合、CompanyName.ExtensionName.dll に格納されたファイルをコンパイルするために、そのディレクトリから次のコマンドが発行されます。  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll /r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 次のコード例は、拡張子 .vb が付く [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] ファイルに使用されるコマンドを示しています。  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll /r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] を使用して、データ処理拡張機能を設計、開発、および構築することもできます。 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] でのアセンブリ開発の詳細については、[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ドキュメントを参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [データ処理拡張機能の実装](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
