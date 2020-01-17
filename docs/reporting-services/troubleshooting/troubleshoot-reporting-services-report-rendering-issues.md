---
title: Reporting Services のレポート レンダリングの問題のトラブルシューティング | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: 1e0fb399-4c16-438a-92cb-db3e877896d0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3f8c5029d66a068d43ebc659592697fd2914fd2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574684"
---
# <a name="troubleshoot-reporting-services-report-rendering-issues"></a>Reporting Services のレポート レンダリングの問題のトラブルシューティング
レポートのデータとレイアウトの情報が結合されると、コンパイルされたレポートがレポート レンダラーに送信されます。 たとえば、レポートをローカルでプレビューする場合、HTML レンダラーを使用してコンパイル済みのレポートが表示されます。 このトピックでは、レポートの表示に固有の問題のトラブルシューティングを行います。   
  
## <a name="why-do-i-have-extra-white-space-including-blank-pages-in-my-report"></a>レポートに余分な空白 (空白ページなど) が表示される  
レポート アイテムは、レポートの一部として定義された空白を保持するようレポートの処理中に自動的に調整されます。 レポート デザイン ビュー上の空白は保持されます。 レポート デザイン画面では、白色の背景は、レポートの閲覧、エクスポート、または印刷時に、対象の媒体に応じて保持される空白を表します。  
  
### <a name="white-space-and-page-breaks-interact-during-rendering"></a>表示中に空白と改ページが互いに影響しあう  
レポートを表示する場合、またはレポートをファイル形式にエクスポートする場合は、関連する表示拡張機能によってレポートが処理され、指定されたファイル形式に保存されます。 各表示拡張機能では、特定の規則に従ってレポートの空白が処理されます。 また、空白は、ページ設定プロパティ、レポート アイテムに設定された改ページ、レポート本文に配置されたレポート アイテムの相対位置、特定のレポート アイテムの KeepTogether プロパティ、およびレポート アイテムが親コンテナーに含まれるかどうかの影響も受けます。   
  
レポートの幅が原因で生じる余分なページをなくすには、レポート デザイン画面の端を、最も外側のレポート アイテムに合わせるようにドラッグします。 左から右に読むレポート レイアウトの場合は、右端を最も外側のレポート アイテムと揃えるようにドラッグします。 詳細については、「 [レンダリングの動作](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="white-space-is-not-preserved-at-the-end-of-a-report"></a>レポートの最後にある空白が保持されない  
Reporting Services には、レポートの最後にある空白を保持するか削除するかを制御できるオプションが用意されています。   
  
レポートの最後にある空白を保持するには、レポートを選択してプロパティ ペインで [ConsumeContainerWhitespace] までスクロールし、「False」と入力します。   
  
## <a name="why-do-my-reports-look-different-when-exported-to-different-formats"></a>レポートを別の形式にエクスポートすると、レイアウトが変化する  
レポートを実行した後は、Excel、Word、PDF など、レポートを別の形式にエクスポートできます。 レポートのエクスポート先の形式に応じて特定の規則や制限が適用されることがあるものの、 多くの制限には、レポートの作成時に考慮することにより対処可能です。 場合によっては、レポートで若干異なるレイアウトを使用する、レポート内へのアイテムの配置を工夫する、レポートのフッターを 1 行のテキストに制限するなどの作業が必要になります。 組み込みの RenderFormat グローバルを使用することにより、条件に応じてレンダラーごとに異なるレポート レイアウトを使用することもできます。 このほかに、エクスポート先の形式で改ページを管理したり、Excel のワークシート タブに名前を付けたりするのに役立つ組み込みのグローバルもあります。 詳細については、「 [レポートのエクスポート](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) 」および「 [組み込み Globals および Users 参照の使用](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)」を参照してください。  
  
## <a name="how-can-i-view-all-my-report-data-on-one-page"></a>すべてのレポート データを 1 ページで表示する方法  
データ量が多すぎないレポートで対話型の表示を実現するために、すべてのデータを 1 ページで表示することができます。   
  
ソフト改ページ レンダラーですべてのデータを 1 ページで表示するには、レポート プロパティの InteractiveHeight を 0 に設定します。 ソフト改ページ レンダラーで、既存の改ページが無視されます。   
  
> [!NOTE]  
> 改ページが含まれていないレポートでは、レポート全体が処理されるまで最初のページが表示されません。   
  
レンダラーのカテゴリの詳細については、「 [レンダリングの動作](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="reports-do-not-run-when-your-browser-is-configured-to-prompt-for-credentials"></a>ブラウザーが資格情報を要求するように構成されているときにレポートが実行されない  
ブラウザーが資格情報を要求するように構成されており、データ ソースが統合 Windows 認証を使用するように構成されているときには、レポートの表示に失敗し、エラー メッセージが表示されることがあります。 この問題が生じるのは、Windows 認証を使用するように構成されたデータ ソースがレポート サーバーとは別のコンピューターに配置されており、ブラウザーが資格情報を要求するように設定されている場合です。 表示されるメッセージの例を次に示します。  
  
データ ソースに構成されている接続の種類が Microsoft SQL Server の場合:  
`An error has occurred during report processing.`  
`Cannot create a connection to data source 'localhost'.`  
`Login failed for user '(null)'. Reason: Not associated with a trusted SQL Server connection.`  
  
データ ソースに構成されている接続の種類が Microsoft SharePoint リストの場合:  
`An error occurred during client rendering.`   
`An error has occurred during report processing.`   
`Query execution failed for dataset 'DataSet1'.`   
`The request failed with HTTP status 401: Unauthorized.`  
  
**この問題の回避方法:** Windows 資格情報ではなく保存されている資格情報を使用するようにデータ ソースを変更します。  
  
**この問題の適用対象:** 資格情報を要求するように構成されているブラウザー。  
  
## <a name="see-also"></a>参照  
[エラーとイベント (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Reporting Services レポートのデータ取得に関する問題のトラブルシューティング](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Reporting Services のサブスクリプションと配信に関するトラブルシューティング](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

