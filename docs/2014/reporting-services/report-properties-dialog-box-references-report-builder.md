---
title: レポートのプロパティ ダイアログ ボックス、参照 (レポート ビルダー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10082"
ms.assetid: 3414c857-8ea6-4fc4-a6d5-b4883c039efa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 99fe80a22f380bbe1406d357846c4103eeb0083e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104393"
---
# <a name="report-properties-dialog-box-references-report-builder"></a>[参照] ([レポートのプロパティ] ダイアログ ボックス) (レポート ビルダー)
  **[レポートのプロパティ]** ダイアログ ボックスの **[参照]** を選択すると、レポート定義内の式で使用される、カスタム アセンブリまたは他の外部アセンブリ、およびカスタム クラスのインスタンスへの参照を追加または削除できます。 レポート ビルダーのローカル モードでは、カスタム アセンブリはサポートされません。 レポートを作成するカスタム アセンブリを使用して、レポート デザイナーを使用する[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]します。  
  
## <a name="options"></a>および  
 **追加またはアセンブリを削除します。**  
 レポートで参照されるアセンブリを一覧表示します。 アセンブリは、レポートのデザインに使用するツールがインストールされているコンピューターおよびレポート サーバー上で使用できる必要があります。 参照の名前がの内容と一致する必要があります **\<CodeModule >** 正確にレポート定義言語 (.rdl) ファイルにタグを付けます。  
  
 **[追加]**  
 アセンブリを追加します。 省略記号 (...) ボタンをクリックして、**開く** ダイアログ ボックスとレポートの処理よぶ式の評価を実行するために必要なアセンブリを選択します。  
  
 **[削除]**  
 アセンブリの参照を一覧から削除するには、削除するアセンブリ名を選択し、 **[削除]** ボタンをクリックします。  
  
 **追加または削除クラス**  
 レポートで使用されるクラスのインスタンスを一覧表示します。 クラスの一覧は、静的メンバーではなく、インスタンス ベースのメンバーでのみ使用されます。  
  
 **[追加]**  
 クラスの参照を追加します。 省略記号 (...) ボタンをクリックして、**開く** ダイアログ ボックスをレポートの処理よぶ式の評価を実行するために必要なクラスを選択します。  
  
 **[削除]**  
 クラスのインスタンスを削除するには、削除するインスタンスを選択し、 **[削除]** ボタンをクリックします。  
  
 **[上へ]**  
 依存関係のあるクラスについては、この参照の表示位置を一覧の上方に移動できます。  
  
 **[下へ]**  
 依存関係のあるクラスについては、この参照の表示位置を一覧の下方に移動できます。  
  
## <a name="see-also"></a>関連項目  
 [レポート ビルダーのダイアログ ボックス、ペイン、およびウィザードに関するヘルプ](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
