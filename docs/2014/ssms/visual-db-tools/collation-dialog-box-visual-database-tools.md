---
title: '[照合順序] ダイアログ ボックス (Visual Database Tools) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.definecolumncollation
- vdtsql.chm:65561
ms.assetid: e4020f79-7abf-4839-b9b2-984ef7049817
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 28c32be0bfb42b923041169c542e21b21074cf70
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62936966"
---
# <a name="collation-dialog-box-visual-database-tools"></a>[照合順序] ダイアログ ボックス (Visual Database Tools)
  このダイアログ ボックスを使用すると、列の照合順序を指定できます。 列の照合順序は、列の値を別の列や定数値と比較する演算で使用されます。 また、SUBSTRING や CHARINDEX などの一部の文字列関数の動作にも影響します。 列の照合順序設定による影響の詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のドキュメントを参照してください。  
  
 このダイアログ ボックスは以下の場合に表示されます。  
  
-   **[列のプロパティ]** タブの **[照合順序]** フィールドに無効な照合順序名を入力した場合。  
  
-   **[列のプロパティ]** タブの **[照合順序]** フィールドをクリックし、フィールドの右の省略記号ボタン ( **[...]** ) をクリックした場合。  
  
## <a name="options"></a>および  
 **[SQL 照合順序]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって定義された照合順序をドロップダウン リストから選択します。  
  
 **[Windows 照合順序]**  
 Windows によって定義された照合順序をドロップダウン リストから選択します。  
  
 **[バイナリ並べ替え]**  
 比較用に文字の値のバイナリ コードを使用します。 このオプションを選択すると、特定のアルファベット比較オプションが使用できなくなります。 たとえば、アルファベットの大文字と小文字のバイナリ コードは異なるため、大文字と小文字を区別しない比較はできなくなります。 **[Windows 照合順序]** を選択した場合にだけ適用されます。  
  
 **[辞書並べ替え]**  
 アルファベット比較オプションを使用します。 **[Windows 照合順序]** を選択した場合にだけ適用されます。 次のアルファベット比較オプションを使用できます。  
  
-   **[大文字と小文字を区別する]** : 大文字と小文字を別の文字として扱う場合に選択します。  
  
-   **[アクセントを区別する]** : 文字にアクセント記号が付いている場合と付いていない場合をそれぞれ別の文字として扱うときに選択します。 このオプションを選択すると、別のアクセント記号が付いている場合にも別の文字として扱われます。  
  
-   **[カタカナを区別する]** : 日本語のひらがなとカタカナを区別して扱う場合に選択します。  
  
-   **[文字幅を区別する]** : 半角文字と全角文字を区別して扱う場合に選択します。  
  
 **[既定値に戻す] ボタン**  
 データベースの既定の照合順序を列に適用します。  
  
## <a name="see-also"></a>参照  
 [集計クエリにおける列の使用 (Visual Database Tools)](visual-database-tools.md)  
  
  
