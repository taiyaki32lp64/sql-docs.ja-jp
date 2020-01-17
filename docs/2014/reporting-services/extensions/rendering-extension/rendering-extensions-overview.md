---
title: 表示拡張機能の概要 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- formats [Reporting Services], rendering extensions
- rendering extensions [Reporting Services], about extensions
ms.assetid: 909356a0-4709-43e5-b597-33bd9bb22882
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5386c8db5c3d240533b21311794779905039e70a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62985812"
---
# <a name="rendering-extensions-overview"></a>表示拡張機能の概要
  表示拡張機能は、レポート サーバーのコンポーネントまたはモジュールで、レポートのデータとレイアウト情報をデバイス固有の形式に変換します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 7 つの表示拡張機能が含まれています。HTML、Excel、Word、CSV またはテキスト、XML、イメージ、および PDF です。 追加の表示拡張機能を作成して、他の形式でレポートを生成できます。  
  
> [!NOTE]  
>  どの表示拡張機能を利用できるかは、RSReportServer.config ファイルのインストール済み拡張機能の一覧で確認できます。  
  
 次の表は、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] が備えている表示拡張機能の説明です。  
  
|Extension Name|説明|  
|--------------------|-----------------|  
|`XML`|XML 形式でレポートを表示します。 レポートは任意のブラウザーで開きます。 この XML 出力にさらに手を加えれば、新しい表示拡張機能を開発しなくても、必要な表示拡張機能を効率的に追加することができます。|  
|`CSV`|コンマ区切り形式でレポートを表示します。 レポートは、CSV ファイル形式に関連付けられている表示ツールで開きます。|  
|`IMAGE`|ページ指向形式でレポートを表示します。 この形式は、レポート ツール バーの [エクスポート] ボックスに **[TIFF]** と表示されます。|  
|`PDF`|Adobe Acrobat Reader 形式でレポートを表示します。 この形式は、レポート ツール バーの [エクスポート] ボックスに **[Acrobat (PDF) ファイル]** と表示されます。|  
|`EXCEL`|[!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)] 形式でレポートを表示します。|  
|`WORD`|レポートを [!INCLUDE[ofprword](../../../includes/ofprword-md.md)] で表示します。|  
|`HTML 4.0` (HTML 表示拡張機能の一部)|HTML は、初期状態でレポートを表示するのに使用される形式です。 ブラウザーが HTML4.0 をサポートしている場合は、HTML4.0 形式が使用されます。 それ以外の場合は、HTML 3.2 が使用されます。|  
|`MHTML` (HTML 表示拡張機能の一部)|MHTML 形式でレポートを表示します。 レポートは、Internet Explorer で開きます。 この形式は、レポート ツール バーの [エクスポート] ボックスに **[Web アーカイブ]** として表示されます。|  
|`NULL`|レポートを特定の形式で表示しません。 この表示拡張機能はレポートをキャッシュするのに有用です。 Null 表示形式は、スケジュールされた実行または配信と連動して使用する必要があります。|  
  
 推奨形式とその使い方の詳細については、「[レポートのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../../report-builder/export-reports-report-builder-and-ssrs.md)」を参照してください。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] によって [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] に実装された表示拡張機能は、すべて共通のインターフェイスを使用します。 これにより、すべての拡張機能で同じレベルの機能性が実装され、レポート サーバーのコア部分での表示処理用コードがより単純になります。  
  
## <a name="rendering-object-model"></a>表示オブジェクト モデル  
 レポートが処理されると、その処理結果は、表示オブジェクト モデル (ROM) として知られる、公開オブジェクト モデルになります。 この表示オブジェクト モデルは、処理されたレポートの内容、レイアウト、およびデータを定義するクラスのコレクションです。 開発者は、ROM を使用して、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のカスタム表示拡張機能を設計、開発、展開できます。 ROM は、レポートの XML 定義とユーザーにより定義されたレポート データが、レポート サーバーにより処理される際に作成されます。 処理が完了すると、表示拡張機能によりこの公開オブジェクト モデルが使用され、レポートの出力が定義されます。 ROM の利用可能なパブリック クラスは `Microsoft.ReportingServices.OnDemandReportRendering` 名前空間で定義されています。  
  
## <a name="writing-custom-rendering-extensions"></a>カスタム表示拡張機能の記述  
 カスタム表示拡張機能の作成を決める前に、より簡単な代替手段を評価する必要があります。 可能な代替手段としては以下の方法があります。  
  
-   既存の拡張機能のデバイス情報の設定を詳細に指定して、表示される出力をカスタマイズする。  
  
-   XML 表現形式の出力に XSL 変換 (XSLT) を組み合わせることで、カスタムの形式と表現機能を追加する。  
  
 カスタム表示拡張機能の記述は難しい作業です。 表示拡張機能は、一般的には、レポートの要素のあらゆる組み合わせをサポートする必要があり、多くのクラス、インターフェイス、メソッド、およびプロパティを実装しなければなりません。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] によりサポートされていない形式でレポートを表示する必要があり、独自に表示拡張機能のコードを記述して実装する場合、開発する表示拡張機能のコードは `Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension` インターフェイスを実装する必要があります。このインターフェイスはレポート サーバーにより必要とされます。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] に関する補足資料とホワイト ペーパーについては、[Reporting Services Web サイト](https://go.microsoft.com/fwlink/?LinkId=19951)の最新の技術文書を参照してください。  
  
## <a name="see-also"></a>参照  
 [表示拡張機能の実装](implementing-a-rendering-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../reporting-services-extension-library.md)  
  
  
