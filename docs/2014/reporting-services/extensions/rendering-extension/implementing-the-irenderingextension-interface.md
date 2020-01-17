---
title: IRenderingExtension インターフェイスの実装 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- IRenderingExtension interface
- rendering extensions [Reporting Services], IRenderingExtension interface
ms.assetid: 74b2f2b7-6796-42da-ab7d-b05891ad4001
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 68e965a523df8dadd03d77df8d3d522870f70a93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62987145"
---
# <a name="implementing-the-irenderingextension-interface"></a>IRenderingExtension インターフェイスの実装
  表示拡張機能では、実際のデータと組み合わされるレポート定義から出力結果を取得し、その結果データを使用可能な形式で表示します。 組み合わされたデータの変換と書式設定は、<xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> を実装する共通言語ランタイム (CLR) クラスを使用して実行されます。 これにより、オブジェクト モデルは、ビューアーやプリンターなどの出力先で使用できる出力形式に変換されます。  
  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> には、コーディングが必要なメソッドが 3 つあります。  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> : レポートを表示します。  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> : レポートの特定のストリームを表示します。  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> : アイコンなどのレポートに必要な追加情報を取得します。  
  
 ここでは、これらのメソッドについて詳しく説明します。  
  
## <a name="render-method"></a>Render メソッド  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> メソッドには、次のオブジェクトを表す引数が含まれます。  
  
-   *report*: 表示するレポート。 このオブジェクトには、レポートのプロパティ、データ、およびレイアウト情報が含まれます。 レポートは、レポート オブジェクト モデル ツリーのルートです。  
  
-   *ServerParameters*: 文字列辞書オブジェクト、およびレポート サーバーのパラメーター (存在する場合) が含まれます。  
  
-   *deviceInfo*: デバイス設定を含むパラメーター。 詳細については、「[表示拡張機能にデバイス情報設定を渡す](../../report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)」を参照してください。  
  
-   *clientCapabilities* パラメーター: 表示先クライアントに関する情報を格納している <xref:System.Collections.Specialized.NameValueCollection> 辞書オブジェクトが含まれます。  
  
-   *RenderProperties*: 表示結果に関する情報が含まれます。  
  
-   *createAndRegisterStream*: 表示するストリームを取得するために呼び出すデリゲート関数。  
  
### <a name="deviceinfo-parameter"></a>deviceInfo パラメーター  
 *deviceInfo* パラメーターには、レポート パラメーターではなく、表示パラメーターが含まれます。 表示パラメーターは表示拡張機能に渡されます。 *deviceInfo* 値は、レポート サーバーによって <xref:System.Collections.Specialized.NameValueCollection> オブジェクトに変換されます。 *deviceInfo* パラメーターのアイテムは、大文字と小文字を区別しない値として扱われます。 URL アクセスによる表示要求が行われると、形式 `rc:key=value` の URL パラメーターが *deviceInfo* 辞書オブジェクトのキーと値のペアに変換されます。 ブラウザー検出コードは、次のものでも用意されています。、 *clientCapabilities*ディクショナリ。ある EcmaScriptVersion、JavaScript、MajorVersion、MinorVersion、Win32、種類、および AcceptLanguage します。 *deviceInfo* パラメーターに表示拡張機能が認識しない名前と値のペアがある場合は、すべて無視されます。 次のコード サンプルは、アイコンを取得する <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> メソッドを示します。  
  
```csharp  
public void GetRenderingResource (CreateStream createStreamCallback, NameValueCollection deviceInfo)  
{  
    string[] iconTagValues = deviceInfo.GetValues("Icon");  
    if ((iconTagValues != null) && (iconTagValues.Length > 0) )  
    {  
        // Create a stream to output to.  
        Stream outputStream = createStreamCallback(m_iconResourceName, "gif", null, "image/gif", false);  
        // Get the GIF image for one of the buttons on the toolbar  
        Image requiredImage = (Image) m_resourcemanager.GetObject(m_iconResourceName  
        // Write the image to the output stream  
        requiredImage.Save(outputStream, requiredImage.RawFormat);  
    }  
    return;  
}  
```  
  
## <a name="renderstream-method"></a>RenderStream メソッド  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> メソッドは、レポート内の特定のストリームを表示します。 最初の <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> 呼び出しですべてのストリームが作成されますが、ストリームは最初はクライアントに返されません。 このメソッドは、HTML 表示における画像などのセカンダリ ストリームや、画像 (EMF) などの複数ページ表示拡張機能の追加ページに使用します。  
  
## <a name="getrenderingresource-method"></a>GetRenderingResource メソッド  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> メソッドは、レポート全体を表示せずに情報を取得します。 レポートに情報は必要だが、レポート自体を表示する必要がない場合があります。 たとえば、表示拡張機能に関連付けられたアイコンが必要な場合、 **\<Icon>** タグ 1 つを含む *deviceInfo* パラメーターを使用します。 このような場合に、<xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> メソッドを使用できます。  
  
## <a name="see-also"></a>関連項目  
 [表示拡張機能の実装](implementing-a-rendering-extension.md)   
 [表示拡張機能の概要](rendering-extensions-overview.md)  
  
  
