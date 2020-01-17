---
title: SSRS のレポート ビューアー コントロールのリリース ノート
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: d6c7130e45e535ad1849bed5713313bf6f89020f
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923812"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>SSRS の WebForms および WinForms のレポートビューアーコントロールのリリースノート

これらは、[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) に関連する WebForms および WinForms のレポートビューアーコントロールのリリースノートです。

SSRS のリリースノートについては、 [SQL Server Reporting Services (ssrs) 2017 以降のリリースノート](../release-notes-reporting-services.md)を参照してください。

## <a name="15013580"></a>150.1358.0
| 説明の変更 | 詳細 |
| :----------------- | :------ |
| バグの修正 | プロジェクト参照から、Microsoft ReportViewer アセンブリを削除した変更を元に戻しました。 |
|           | 他の変更の一部として、2つのアセンブリが15.0 バージョンから15.3 に変更されました。 これは元に戻されました。 |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| 説明の変更 | 詳細 |
| :----------------- | :------ |
| バグの修正  | 高 DPI モニターの適切な印刷プレビュー |
|            | 印刷ダイアログが表示領域の外側に表示される |
|            | パラメーターの数が多すぎて、パラメーターのスクロールバーとドロップダウンリストが正しく機能しませんでした |
|            | Null および日付と時刻のパラメーターに関する問題を修正した |
|            | JQuery をバージョン3.3.1 に更新しました |
|            | HTML レンダリングで tablix セルとの重複が修正される |
|            | プロジェクトに誤った VS アセンブリが追加されないようにするために、デザイン時のプロジェクト参照を削除しました |
|            | アクティブな項目に対してのみナレーションを行うツールバーのアクセシビリティの修正 |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| 説明の変更 | 詳細 |
| :----------------- | :------ |
| パラメーターのないレポートが **Server.LoadReportDefinition** によって読み込まれないバグが修正されています。 | &nbsp; |
| WebForms レポート ビューアー コントロール。 | RTL ページ (*direction: rtl;* css を使用してテキスト フローをを変更するページ) への埋め込みがサポートされました。<br/><br/>*IReportViewerMessages5* ローカリゼーション インターフェイスを使用した、印刷ダイアログ テキストのカスタマイズがサポートされました。<br/><br/>ユーザー補助のサポートが改善されました。<br/><br/>&bull; &nbsp; &nbsp; [WebForms のレポートビューアーコントロールの NuGet パッケージ](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| WinForms レポート ビューアー コントロール。 | アプリが高 DPI モードで実行されている場合の印刷機能が修正されました。<br/><br/>&bull; &nbsp; &nbsp; [WinForms のレポートビューアーコントロールの NuGet パッケージ](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>次の手順

レポート ビューアー コントロールの[概要](integrating-reporting-services-using-reportviewer-controls-get-started.md)。

その他の質問 [Reporting Services のフォーラムをお試しください](https://go.microsoft.com/fwlink/?LinkId=620231)。
