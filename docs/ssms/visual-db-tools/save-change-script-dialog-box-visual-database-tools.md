---
title: '[変更スクリプトの保存] ダイアログ ボックス (Visual Database Tools) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.generatechangescript
- vdtsql.chm:65544
ms.assetid: fc9d1639-5efa-44fe-a04f-4d4d0def2833
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d258f93f5b6ada2199e7375d73ae870244268815
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267800"
---
# <a name="save-change-script-dialog-box-visual-database-tools"></a>[変更スクリプトの保存] ダイアログ ボックス (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
このダイアログ ボックスには、最後にテーブルを保存してから、変更を行った [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトが表示されます。 選択した場所に、テキスト ファイル形式でスクリプトを保存することもできます。  
  
テーブル デザイナーのテーブルへの変更を保存しなかった場合に、このダイアログ ボックスにアクセスできます。 **[テーブル デザイナー]** メニューの **[変更スクリプトの生成]** をクリックします。  
  
> [!NOTE]  
> Visual Database Tools によって提供される変更スクリプトにはエラー処理は含まれていません。 ツールが開いた後でデータベース オブジェクトが変更されていないことを前提としているため、変換関連の問題が発生することを想定していません。 変更スクリプトを実行する前に、適切なエラー処理ステートメントを含める必要があります。  
  
## <a name="options"></a>オプション  
**[保存時に変更スクリプトを自動作成する]**  
オンにすると、テーブルへの変更を保存するときに毎回 **[変更スクリプトの保存]** ダイアログ ボックスが表示されるようになります。  
  
**はい**  
テキスト ファイルの場所を選択できる **[上書き保存]** ダイアログ ボックスを呼び出します。  
  
**いいえ**  
変更スクリプトの作成を取り消します。  
  
