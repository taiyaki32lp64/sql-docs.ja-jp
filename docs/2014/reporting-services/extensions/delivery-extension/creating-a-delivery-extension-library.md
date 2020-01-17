---
title: 配信拡張機能ライブラリの作成 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 63b32f93-4bab-4b07-bd72-39a47aca1cda
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 133d97cc2d4c04e147d5f4a88c13674429f5c784
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63164900"
---
# <a name="creating-a-delivery-extension-library"></a>配信拡張機能ライブラリの作成
  作成する [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配信拡張機能は、それぞれ一意の名前空間に割り当てられ、ライブラリまたはアセンブリ ファイルに組み込まれている必要があります。 名前空間の正確な名前はあまり重要ではありませんが、名前は他の拡張機能とは共有しない一意のものである必要があります。 会社の配信拡張機能には、独自に一意の名前空間を作成してください。  
  
 次の例は、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配信拡張機能を開始するためのコードを示しています。配信インターフェイスとユーティリティ クラスを含む名前空間を使用しています。  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配信拡張機能をコンパイルする場合は、コンパイラに対して Microsoft.ReportingServices.Interfaces.dll への参照を指定する必要があります。配信拡張機能のインターフェイスとクラスがそこに格納されているためです。 <xref:Microsoft.ReportingServices.Interfaces> 名前空間は、<xref:Microsoft.ReportingServices.Interfaces.IExtension> インターフェイス、<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> インターフェイスなどを実装するために必要です。 たとえば、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配信拡張機能を実装するために C# で書き込まれたコードを含むすべてのファイルが、拡張子 .cs が付いた 1 つのディレクトリに格納されている場合は、CompanyName.ExtensionName.dll に格納されたファイルをコンパイルするために、そのディレクトリから次のコマンドが発行されます。  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 次のコード例は、拡張子 .vb が付く [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] ファイルに使用されるコマンドを示しています。  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] を使用して、配信拡張機能を設計、開発、および構築することもできます。 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] でのアセンブリ開発の詳細については、[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ドキュメントを参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../reporting-services-extensions.md)   
 [配信拡張機能の実装](implementing-a-delivery-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../reporting-services-extension-library.md)  
  
  
