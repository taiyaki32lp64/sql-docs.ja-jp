---
title: RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- configuration options [Reporting Services]
- DeviceInfo settings
- rendering extensions [Reporting Services], overriding behaviors
- parameters [Reporting Services], report rendering
- overriding report rendering behavior
- extensions [Reporting Services], rendering
ms.assetid: 3bf7ab2b-70bb-41c8-acda-227994d15aed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: efdea595034f91497befdc7f7b12adacef8d73ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109551"
---
# <a name="customize-rendering-extension-parameters-in-rsreportserverconfig"></a>RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする
  RSReportServer 構成ファイルで表示拡張機能パラメーターを設定すると、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーで実行されるレポートについて、既定のレポート表示動作をオーバーライドできます。 表示拡張機能パラメーターは、次のように目的に応じて変更できます。  
  
-   レポート ツール バーのエクスポートの一覧での表示拡張機能の名前の表示方法を変更します (たとえば、"Web アーカイブ" を "MHTML" に変更する処理など)。または、別の言語に名前をローカライズします。  
  
-   異なる複数のレポート表示オプションをサポートするには、同じ表示拡張機能の複数のインスタンスを作成します (画像表示拡張機能の横モードと縦モードなど)。  
  
-   既定の表示拡張機能パラメーターを変更して、別の値を使用します (たとえば、画像表示拡張機能で既定の出力形式として TIFF を使用している場合、拡張機能パラメーターを変更して EMF を使用できます)。  
  
 表示拡張機能パラメーターへの変更は、レポート サーバーの表示操作にのみ影響します。 レポート デザイナーのレポート プレビューで表示拡張機能の設定はオーバーライドできません。  
  
 構成ファイルでの表示拡張機能パラメーターの設定は、表示拡張機能全体に影響を与えます。 構成ファイルの設定は、特定の表示拡張機能が使用されるたびに既定値に代わって使用されます。 特定のレポートまたは表示操作の表示拡張機能パラメーターを設定する場合は、 <xref:ReportExecution2005.ReportExecutionService.Render%2A> メソッドを使用するか、レポート URL にデバイス情報設定を指定することにより、デバイス情報をプログラムで指定する必要があります。 表示操作のデバイス情報設定の詳細について、およびデバイス情報設定の一覧表示については、 [「表示拡張機能にデバイス情報設定を渡す」](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)を参照してください。  
  
## <a name="finding-and-modifying-rsreportserverconfig"></a>RSReportServer.config の検索および変更  
 レポート出力形式の構成設定は、RSReportServer.config ファイルで表示拡張機能パラメーターとして指定します。 構成ファイルの表示拡張機能パラメーターを指定するには、表示パラメーターを設定する XML 構造の定義方法を理解しておく必要があります。 変更できる XML 構造は次の 2 つです。  
  
-   `OverrideNames` 要素は、表示拡張機能の表示名と言語を定義しています。  
  
-   `DeviceInfo` XML 構造は、表示拡張機能で使用するデバイス情報設定を定義しています。 ほとんどの表示拡張機能パラメーターは、デバイス情報設定として指定されます。  
  
 テキスト エディターでファイルを変更できます。 RSReportServer.config ファイルは、\Reporting Services\Report Server\Bin フォルダーにあります。 構成ファイルの変更方法の詳細については、「[Reporting Services の構成ファイルの変更 &#40;RSreportserver.config&#41;](report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  
  
## <a name="changing-the-display-name"></a>表示名の変更  
 表示拡張機能の表示名は、レポート ツール バーのエクスポート一覧に表示されます。 既定の表示名の例として、Web アーカイブ、TIFF ファイル、Acrobat (PDF) ファイルなどがあります。 構成ファイルで `OverrideNames` 要素を指定すると、既定の表示名をカスタム値に置き換えることができます。 また、単一の表示拡張機能の 2 つのインスタンスを定義する場合は、`OverrideNames` 要素を使用して、エクスポート一覧の各インスタンスを区別できます。  
  
 表示名はローカライズされるので、既定の表示名をカスタム値に置き換える場合は `Language` 属性を設定する必要があります。 この設定を行わないと、指定した名前が無視されます。 このとき、レポート サーバーのコンピューターに対して有効な言語値を設定する必要があります。 たとえば、フランス語のオペレーティング システムでレポート サーバーを実行している場合は、属性値に "fr-FR" を指定する必要があります。  
  
 次の例は、英語のレポート サーバーにカスタム名を設定する方法を示しています。  
  
```  
<Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering">  
   <OverrideNames>  
     <Name Language="en-US">My Custom Display Name for XML Rendering</Name>  
   </OverrideNames>  
</Extension>  
```  
  
## <a name="changing-device-information-settings"></a>デバイス情報設定の変更  
 レポート サーバーに既に配置されている表示拡張機能で使用される既定のデバイス情報設定を変更するには、`DeviceInfo` XML 構造を構成ファイルに入力する必要があります。 各表示拡張機能は、その拡張機能に一意のデバイス情報設定をサポートします。 デバイス情報設定の完全な一覧については、 [「表示拡張機能にデバイス情報設定を渡す」](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)をご覧ください。  
  
 次の例は、画像表示拡張機能の既定の設定を変更する XML 構造および構文を示しています。  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">Image (EMF)</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <ColorDepth>32</ColorDepth>  
                <DpiX>300</DpiX>  
                <DpiY>300</DpiY>  
                <OutputFormat>EMF</OutputFormat>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="configuring-multiple-entries-for-a-rendering-extension"></a>表示拡張機能に対する複数のエントリの構成  
 異なる複数のレポート表示オプションをサポートするために、同じ表示拡張機能の複数のインスタンスを作成することができます。 定義する各インスタンスには、さまざまな組み合わせのパラメーター値を設定できます。 既存の表示拡張機能の新しいインスタンスを定義する場合は、次の手順を実行します。  
  
-   拡張機能の一意な名前を指定します。  
  
     各インスタンスは、`Name` 属性に一意な値を使用する必要があります。 次の例では、"IMAGE (EMF Landscape)" と "IMAGE (EMF Portrait)" を使用して、2 つのインスタンスを区別しています。  
  
     既に配置されている表示拡張機能の名前を変更する場合は、注意が必要です。 表示拡張機能がプログラム内で指定されている場合は、特定の表示操作に使用するインスタンスの識別に、拡張名が使用されています。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のカスタム アプリケーションをレポート サーバーで実行する場合、既存の拡張機能名を変更したり、新しい拡張機能名を追加した際には、必ず開発者に知らせてください。  
  
-   各出力形式の違いをユーザーが理解できるように、一意な表示名を指定します。  
  
     同じ拡張機能の複数のバージョンを構成している場合、`OverrideNames` に値を設定して、各バージョンに一意な名前を指定できます。 このように指定しなかった場合は、すべてのバージョンの拡張機能が、レポート ツール バーのエクスポート オプションの一覧に同じ名前で表示されます。  
  
 次の例では、既定の画像表示拡張機能 (TIFF 出力を生成) を使用して縦モードの EMF を出力する方法と共に、横モードの EMF にレポートを出力する 2 番目のインスタンスを示します。 各拡張機能名が一意であることに注意してください。 この例をテストする際には、表示/非表示オプション、マトリックス、ドリルスルー リンクなどの対話機能が含まれないレポートを選択してください (対話機能は、画像表示拡張機能で動作しません)。  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF Landscape)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Landscape Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>8.5in</PageHeight>  
                <PageWidth>11in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
    <Extension Name="IMAGE (EMF Portrait)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Portait Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>11in</PageHeight>  
                <PageWidth>8.5in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="see-also"></a>関連項目  
 [RSReportServer 構成ファイル](report-server/rsreportserver-config-configuration-file.md)   
 [RSReportDesigner 構成ファイル](report-server/rsreportdesigner-configuration-file.md)   
 [CSV デバイス情報設定](csv-device-information-settings.md)   
 [Excel デバイス情報設定](excel-device-information-settings.md)   
 [HTML デバイス情報設定](html-device-information-settings.md)   
 [画像デバイス情報設定](image-device-information-settings.md)   
 [MHTML デバイス情報設定](mhtml-device-information-settings.md)   
 [PDF デバイス情報の設定](pdf-device-information-settings.md)   
 [XML デバイス情報設定](xml-device-information-settings.md)  
  
  
