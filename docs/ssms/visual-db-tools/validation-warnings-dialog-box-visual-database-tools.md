---
title: '[評価に関する警告] ダイアログ ボックス (Visual Database Tools) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65556
- vdt.dlgbox.validationwarnings
ms.assetid: fc76e234-ec9c-4a19-a65b-cb558ec8268e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eb7dc987ba03dc4d50c12c80519f769d6f5b3261
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267449"
---
# <a name="validation-warnings-dialog-box-visual-database-tools"></a>[評価に関する警告] ダイアログ ボックス (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
このダイアログ ボックスは、データベースに悪影響を及ぼす可能性のある変更を保存しようとした場合、またはデータベースのコミット動作が失敗する可能性がある場合に表示されます。 このダイアログ ボックスには、可能性のある具体的な悪影響またはコミット動作が失敗する理由が示されます。 このまま変更を保存するか取り消すかを選択できます。  
  
> [!NOTE]  
> このダイアログ ボックスは、変更をデータベースに適用しようとしたとき、または変更スクリプトを保存したときに表示されます。  
  
このダイアログ ボックスは、次のような理由によって表示されます。  
  
-   すべての変更をコミットするためのデータベース アクセス許可を持っていない。  
  
-   変更によって、派生された列、既定の制約、または CHECK 制約が不適切に形成される。  
  
-   列のデータ型を変更することでデータの損失が発生する。  
  
-   変更によって 900 バイトを超えるインデックスが生成される。  
  
-   変更によって、スキーマ連結ビューやユーザー定義関数で使用されるテーブルまたは列が変更される。  
  
-   変更によって、1 つ以上の暗号化されたトリガーを含むテーブルが再作成され、トリガーが無効になる。  
  
-   変更によって、1 つのテーブル内の列に対して ANSI_NULLS と ANSI_PADDING のいずれかまたは両方に意味のある設定がされる。  
  
## <a name="options"></a>オプション  
**はい**  
操作を続行し、変更スクリプトを生成するか、変更をデータベースに転送します。 データベースを変更する権限を持っていない場合、変更によってインデックスが 900 バイトを超える場合、または変更の結果として計算される列、既定の制約、CHECK 制約が正しく作成されない場合に、コミット操作は失敗します。  
  
**いいえ**  
保存操作を取り消します。  
  
**[テキスト ファイルを保存]**  
**[名前を付けて保存]** ダイアログ ボックスを表示し、警告リストを含むテキスト ファイルの保存場所を指定できます。  
  
## <a name="see-also"></a>参照  
[テーブルのデザイン (Visual Database Tools)](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
