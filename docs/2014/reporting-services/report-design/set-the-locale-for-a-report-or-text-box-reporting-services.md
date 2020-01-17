---
title: レポートまたはテキスト ボックスのロケールの設定 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- locales [Reporting Services]
ms.assetid: df115b01-184b-47f0-b5ec-0ad965ff9bee
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d65c02df74cb89fca3d861f01c01da87ff589e3a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104989"
---
# <a name="set-the-locale-for-a-report-or-text-box-reporting-services"></a>レポートまたはテキスト ボックスのロケールの設定 (Reporting Services)
  レポートまたはテキスト ボックスの **Language** プロパティでは、ローカル設定を指定します。ローカル設定は、言語や地域ごとに異なるレポート データ (日付、通貨、数値など) を表示するための既定の形式を指定します。 テキスト ボックスの **Language** プロパティは、レポートの **Language** プロパティをオーバーライドします。 **Language**プロパティに値が指定されてない場合、Reporting Services は、パブリッシュされたレポートのレポート サーバーの OS のロケールか、またはレポート プレビューを行うレポート作成コンピューターのロケールを使用します。  
  
 HTML レポートの場合、既定の **Language** 値をオーバーライドし、ブラウザー クライアントの HTTP ヘッダーで指定している言語を使用できます。この操作を行うには、レポートまたはテキスト ボックスの **Language** プロパティの式で組み込みフィールド User!Language を使用します。  
  
 レポートの **Language** プロパティを URL で指定することもできます。 詳細については、「 [URL でレポート パラメーターの言語を設定する](../set-the-language-for-report-parameters-in-a-url.md)」を参照してください。  
  
### <a name="to-set-the-locale-for-a-report"></a>レポートのロケールを設定するには  
  
1.  デザイン ビューで、レポートのデザイン画面の外側をクリックして、レポートを選択します。  
  
2.  プロパティ ペインの **[Language]** プロパティで、レポートに使用する言語を入力または選択します。  
  
### <a name="to-set-the-locale-for-a-text-box"></a>テキスト ボックスのロケールを設定するには  
  
1.  デザイン ビューで、ロケール設定を適用するテキスト ボックスを選択します。  
  
2.  プロパティ ペインで、次の操作を行います。  
  
    -   **[Calendar]** プロパティで、日付に使用するカレンダーを入力または選択します。  
  
    -   **[Direction]** プロパティで、テキストを記述する方向を入力または選択します。  
  
    -   **[Language]** プロパティで、テキスト ボックスに使用する言語を入力または選択します。 この値は、レポートの **Language** プロパティをオーバーライドします。  
  
    -   **[NumeralLanguage]** プロパティで、テキスト ボックスの数字に使用する形式を入力または選択します。  
  
    -   **[NumeralVariant]** プロパティで、テキスト ボックスの数字に使用する形式の変化形を入力または選択します。  
  
    -   **[UnicodeBiDi]** プロパティで、テキスト ボックスで使用する双方向の埋め込みレベルを選択します。  
  
## <a name="see-also"></a>参照  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  
