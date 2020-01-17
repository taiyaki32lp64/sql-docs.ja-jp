---
title: '[式ビルダー] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.expressionbuilder.f1
helpviewer_keywords:
- Expression Builder dialog box
ms.assetid: 4717ce33-bd4e-44bc-81e0-002de075b4d1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c2aa59b0806cc0ede01fa728636ab9d90479f14b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62898850"
---
# <a name="expression-builder"></a>[式ビルダー]
  **[式ビルダー]** ダイアログ ボックスには、変数を一覧表示したり、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 式の言語に含まれる関数、型キャスト、および演算子への組み込み参照を提供するグラフィカル ユーザー インターフェイスが用意されています。このグラフィカル ユーザー インターフェイスを使用して、プロパティ式の作成および編集や、変数の値を設定する式の作成を行えます。  
  
 プロパティ式とは、プロパティに割り当てられる式です。 式が評価されると、式の評価結果を使用してプロパティが動的に更新されます。 同様に、変数内で式を使用することにより、式の評価結果で変数値を更新することができます。  
  
 式を使用するには次のように多くの方法があります。  
  
-   **タスク:** 変数内に格納されている電子メール アドレスを挿入することにより、メール送信タスクで使用される [宛先] 行を更新します。または、"売上:" などの文字列と GETDATE 関数から返される現在の日付を連結することにより、[件名] 行を更新します。  
  
-   **変数:** `DATEPART("mm",GETDATE())`などの式を使用して、変数の値を現在の月に設定します。または、式 `"Today's date is " + (DT_WSTR,30)(GETDATE())`を使用して文字列リテラルと現在の日付を連結することにより、文字列の値を設定します。  
  
-   **接続マネージャー :** 異なるコード ページ識別子が格納されている変数を使用することにより、フラット ファイル接続マネージャーのコード ページを設定します。または、式に 3 などの正の整数を入力してデータ ファイル内のスキップする行数を指定します。  
  
 プロパティ式と式の作成の詳細については、「[パッケージでプロパティ式を使用する](use-property-expressions-in-packages.md)」と「[Integration Services (SSIS) の式](integration-services-ssis-expressions.md)」を参照してください。  
  
## <a name="options"></a>および  
  
|項目|定義|  
|----------|----------------|  
|**変数:**|**[変数]** フォルダーを展開し、変数を **[式]** ボックスにドラッグします。|  
|**数学関数**<br /><br /> **文字列関数**<br /><br /> **日付/時刻関数**<br /><br /> **NULL 関数**<br /><br /> **[型キャスト]**<br /><br /> **演算子**|フォルダーを展開し、関数、型キャスト、および演算子を **[式]** ボックスにドラッグします。|  
|**[式]**|式を編集または入力します。|  
|**[評価結果]**|式の評価結果を一覧表示します。|  
|**[式の評価]**|**[式の評価]** をクリックすると、式の評価結果が表示されます。|  
  
## <a name="see-also"></a>参照  
 [[式] ページ](expressions-page.md)   
 [[プロパティ式エディター]](property-expressions-editor.md)   
 [Integration Services (SSIS) の変数](../integration-services-ssis-variables.md)   
 [システム変数](../system-variables.md)  
  
  
