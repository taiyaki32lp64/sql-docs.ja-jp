---
title: 配信拡張機能での RenderedOutputFile クラスの使用 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 152a60911157b261ed95f7a68364e59470110637
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193668"
---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>配信拡張機能での RenderedOutputFile クラスの使用
  <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> クラスは、データ ストリームおよびデータ ストリームの関連付けられたプロパティに関する情報を表します。 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> クラスの **Data** プロパティは、表示レポートまたはレポート リソースを **Stream** オブジェクトとして表すために使用します。  
  
 **Report** オブジェクトの <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> メソッドは、1 つの表示レポートを一緒に構成する 1 つ以上の <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> オブジェクトの配列を返します。 1 番目の <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> オブジェクトが表示レポートです。 その他の <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> オブジェクトは、レポート データと一緒に配信される必要があるリソースです (HTML ファイルや関連付けられた画像など)。 表示拡張機能がシングル ストリーム表示拡張機能である場合は (IMAGE、PDF、MHTML、および EXCEL)、配列の <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> オブジェクトを 1 つだけ返します。  
  
 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> クラスの使用例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」 (SQL Server Reporting Services 製品サンプル) を参照してください。  
  
## <a name="see-also"></a>参照  
 [配信拡張機能の実装](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
