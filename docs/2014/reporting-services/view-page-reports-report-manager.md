---
title: ページで、表示レポート (レポート マネージャー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4874ba29-429b-4dd4-a8cb-d4f087237dc2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c8731c1d0f79d99919c4a087521565a6ec590278
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098741"
---
# <a name="view-page-reports-report-manager"></a>[表示] ページ、レポート (レポート マネージャー)
  レポートの [表示] ページではレポートを参照できます。 レポートをレポート マネージャーで最初に開くと、HTML で書式設定されます。 HTML レポートの場合、レポートの一番上に [レポート] ツール バーが表示されます。このツール バーを使用すると、レポート ページ間の移動、レポート内の検索、または異なる形式でのレポートの表示が可能になります。 次の図は、[レポート] ツール バーを示しています。  
  
 ![レポート ツールバー](media/htmlviewer-toolbar.gif "レポート ツールバー")  
レポート ツール バー  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]では、レポートを要求時に実行するか、レポート実行スナップショットから実行するかを構成できます。 レポートを要求時に実行する場合、すべてのデータ処理およびレポート処理が、レポートを開くたびに実行されます。 レポートをレポート実行スナップショットとして実行するよう構成している場合、スナップショットの作成時にデータ処理が行われます。  
  
## <a name="exporting-reports"></a>レポートのエクスポート  
 エクスポートの形式によっては、レポートの機能が一部失われる場合があります。 HTML レポートを別の形式にエクスポートすると、レポートの表示形式が一部異なる場合があります。 また、レポートに対話機能 (ハイパーリンク、ブックマーク、またはドキュメント マップ) が含まれている場合、別の形式ではこれらの機能が使用できなかったり、同じように動作しなかったりする場合があります。  
  
## <a name="generating-data-feeds-from-report-data"></a>レポート データからのデータ フィードの生成  
 レポートからは、データ フィードを生成できます。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Atom 表示拡張機能は、2 種類の Atom 準拠のドキュメント (レポートから提供されるデータ フィードとレポート データを含むデータ フィードを一覧表示する Atom サービス ドキュメント) を生成します。 データ フィードは、Atom 準拠のデータ フィードを使用するアプリケーションで読み取りと交換が可能な標準化された Atom 1.0 準拠の形式で、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] によって生成されます。 たとえば、 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] クライアントは、レポートから生成されたデータ フィードを使用できます。  
  
## <a name="running-parameterized-reports"></a>パラメーター化されたレポートの実行  
 入力フィールドおよび **[レポートの表示]** ボタンが含まれているレポートは、パラメーター化されたレポートです。 パラメーター化されたレポートを表示する際、レポートの実行に使用する値を指定する必要がある場合があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のどのエディションでも、レポート実行スナップショットおよび一部のエクスポート形式は使用できません。 詳しくは「 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [レポート マネージャー F1 ヘルプ](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
