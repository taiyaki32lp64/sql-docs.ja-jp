---
title: レポートのプロパティ ダイアログ ボックスを参照 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10530"
- sql12.rtp.rptdesigner.reportproperties.references.f1
ms.assetid: 4639d368-9918-4bb1-9953-7a724ca78dea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e57e0eb15c8c0ae7e326927ab14493f21c52cc14
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104297"
---
# <a name="report-properties-dialog-box-references"></a>[参照] ([レポートのプロパティ] ダイアログ ボックス)
  **[レポートのプロパティ]** ダイアログ ボックスの **[参照]** を選択すると、レポート定義内の式で使用される、カスタム アセンブリまたは他の外部アセンブリ、およびカスタム クラスのインスタンスへの参照を追加または削除できます。  
  
## <a name="options"></a>および  
 **追加またはアセンブリを削除します。**  
 レポートで参照されるアセンブリを一覧表示します。 アセンブリは、レポートのデザインに使用するツールがインストールされているコンピューターおよびレポート サーバー上で使用できる必要があります。 参照の名前がの内容と一致する必要があります **\<CodeModule >** 正確にレポート定義言語 (.rdl) ファイルにタグを付けます。  
  
 **[追加]**  
 アセンブリを追加します。 省略記号 (...) ボタンをクリックして、**開く** ダイアログ ボックスとレポートの処理よぶ式の評価を実行するために必要なアセンブリを選択します。  
  
 **削除**  
 アセンブリの参照を一覧から削除するには、削除するアセンブリ名を選択し、 **[削除]** ボタンをクリックします。  
  
 **追加または削除クラス**  
 レポートで使用されるクラスのインスタンスを一覧表示します。 クラスの一覧は、静的メンバーではなく、インスタンス ベースのメンバーでのみ使用されます。  
  
 **[追加]**  
 クラスの参照を追加します。 省略記号 (...) ボタンをクリックして、**開く** ダイアログ ボックスをレポートの処理よぶ式の評価を実行するために必要なクラスを選択します。  
  
 **削除**  
 クラスのインスタンスを削除するには、削除するインスタンスを選択し、 **[削除]** ボタンをクリックします。  
  
 **[上へ]**  
 依存関係のあるクラスについては、この参照の表示位置を一覧の上方に移動できます。  
  
 **[下へ]**  
 依存関係のあるクラスについては、この参照の表示位置を一覧の下方に移動できます。  
  
## <a name="see-also"></a>参照  
 [レポート デザイナーでカスタム コードやアセンブリを式から参照する (SSRS)](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [レポート変数コレクションとグループ変数コレクションの参照 (レポート ビルダーおよび SSRS)](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)   
 [式の例 &#40;レポート ビルダーおよび SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
