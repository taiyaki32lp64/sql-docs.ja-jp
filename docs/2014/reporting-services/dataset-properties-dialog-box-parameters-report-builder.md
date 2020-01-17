---
title: データセットのプロパティ ダイアログ ボックスのパラメーター (レポート ビルダー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10023"
ms.assetid: 3a0672ad-c969-455b-b952-585164ce1dda
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 295a40bc7964e50e5fc0c4a9ea0294b593fdde18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109392"
---
# <a name="dataset-properties-dialog-box-parameters-report-builder"></a>[パラメーター] ([データセットのプロパティ] ダイアログ ボックス) (レポート ビルダー)
  選択**パラメーター**で、**データセットのプロパティ**ダイアログ ボックスを追加、変更、およびクエリ パラメーターを削除します。  
  
 埋め込みデータセットの場合、オプションはレポート定義のデータセットに適用されます。  
  
 共有データセットの場合、オプションはレポート サーバーの共有データセット定義に適用されます。  
  
 詳細については、「[埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[追加]**  
 一覧に新しいパラメーターを追加します。  
  
 **削除**  
 選択したパラメーターを一覧から削除します。  
  
 **上矢印**  
 選択したパラメーターを一覧内で上に移動します。  
  
 **下矢印**  
 選択したパラメーターを一覧内で下に移動します。  
  
 **[パラメーター名]**  
 **[データセットのプロパティ]** ダイアログ ボックスの **[クエリ]** タブでデータセットに追加したクエリ パラメーターの名前を入力します。  
  
 **[パラメーター値]**  
 埋め込みデータセットにのみ適用されます。  
  
 クエリ パラメーターの値を入力します。 この値には、静的な値、またはレポート内のオブジェクトを参照するがレポート アイテムやフィールドは参照できない式を指定できます。 既定では、 **[値]** に、レポート パラメーターを参照する式が設定されています。  
  
 **既定値**  
 共有データセットにのみ適用されます。  
  
 既定値を指定する場合に、このチェック ボックスをオンにします。  
  
 既定値を入力します。 この値には、静的な値か、レポート内のオブジェクトを参照する式を使用できます。 式は、レポート アイテム、レポート パラメーター、またはフィールドを参照できません。  
  
 空白を指定するには、テキスト ボックスを空のままにします。  
  
 NULL を指定するには、NULL 許容オプションを選択します。  
  
 **[読み取り専用]**  
 共有データセットにのみ適用されます。  
  
 共有データセット定義でこのパラメーターを読み取り専用に指定する場合は、このオプションを選択します。 共有データセットがレポートに追加されると、パラメーターはプロパティに表示されなくなります。 レポート サーバー上で共有データセットがキャッシュされると、値は変更できなくなります。  
  
 **NULL 値の使用**  
 共有データセットにのみ適用されます。  
  
 NULL 値を許容する場合は、このオプションを選択します。  
  
 **クエリから省略します。**  
 共有データセットにのみ適用されます。  
  
 レポート パラメーターの参照が共有データセット フィルターの式に含まれ、クエリに含まれていない場合に、このオプションを選択します。 このオプションを選択した場合、クエリの実行時にこのパラメーターの既定値を指定する必要はありません。  
  
## <a name="see-also"></a>参照  
 [レポート ビルダーのダイアログ ボックス、ペイン、およびウィザードに関するヘルプ](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [データセットのプロパティ] ダイアログ ボックスの [クエリ&#40;レポート ビルダー&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [チュートリアル: レポートへのパラメーターの追加 &#40;レポート ビルダー&#41;](tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [クエリ デザイナー &#40;レポート ビルダー&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
  
