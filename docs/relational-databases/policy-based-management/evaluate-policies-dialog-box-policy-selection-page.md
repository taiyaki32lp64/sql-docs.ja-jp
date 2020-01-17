---
title: '[ポリシーの評価] ダイアログ ボックスの [ポリシーの選択] ページ'
description: SQL Server Management Studio (SSMS) のポリシーベース管理のための [ポリシーの評価] ダイアログ ボックスの [ポリシーの選択] ページについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.runnow.f1
ms.assetid: 20075fbe-0b48-42c8-b747-690f1aa23dcf
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 84e9e7577f74aa3ea43d99bc6b3c12cd5637c9ec
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558217"
---
# <a name="evaluate-policies-dialog-box-policy-selection-page"></a>[ポリシーの評価] ダイアログ ボックスの [ポリシーの選択] ページ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このダイアログ ボックスを使用すると、ポリシー ベースの管理ポリシーを評価できます。 **[評価の結果]** ページを選択すると、ポリシーに準拠していない対象セット内の項目にポリシーを適用できます。  
  
## <a name="options"></a>オプション  
 **ソース**  
 ポリシーのソースを指定します。 ソースを変更するには、参照ボタン ( **[...]** ) をクリックして、 **[ソースの選択]** ダイアログ ボックスを開きます。  
  
 **[ファイル]**  
 ポリシー ベースの管理ポリシーを含むファイルのパスを入力するか、参照ボタン ( **[...]** ) を使用してファイルを選択します。  
  
 **[サーバー]**  
 必要なポリシーを含む [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続する場合に選択します。  
  
 **ポリシー: ポリシー**  
 クリックすると、指定したポリシーの [ポリシー] ダイアログ ボックスが開きます。  
  
 **ポリシー: カテゴリ**  
 ポリシーのカテゴリ。 このボックスは読み取り専用です。  
  
 **ポリシー: ファセット**  
 ポリシーによって実装されるファセット。 このボックスは読み取り専用です。  
  
 **[評価]**  
 ポリシーを評価モードで実行します。 これにより対象セットの準拠レポートが生成されますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再構成されたり、今後の準拠が適用されたりすることはありません。  
  
## <a name="possible-errors"></a>発生する可能性のあるエラー  
  
-   **対象が見つかりません**  
  
     対象セットは、次のいずれかの理由により空になっている可能性があります。  
  
    -   ポリシーで指定された型の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対象が存在しない。  
  
    -   サーバーの制限によって対象を含む [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが除外されている。  
  
    -   ポリシーがデータベース内のオブジェクト (テーブル、ビュー、ユーザーなど) を対象としている場合に、データベースがポリシーのカテゴリをサブスクライブしていない。  
  
    -   対象セットのフィルターによって、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのインスタンスのすべての対象が除外されている。  
  
    -   ターゲット サーバーの種類とポリシーが評価されるサーバーの種類が異なっている。 たとえば、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]で、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]用に作成されたポリシーを評価しようとすると、空の対象セットが返されます。  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [[ポリシーの評価] ダイアログ ボックスの [評価の結果] ページ](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)  
  
  
