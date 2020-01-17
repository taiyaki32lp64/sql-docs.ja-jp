---
title: INSERT ステートメントの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1676af6216ac703e9a8976951ec2888b9e940b67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085523"
---
# <a name="insert-statement-limitations"></a>INSERT ステートメントの制限事項
長すぎて、列に収まりきらない場合、警告なしの右側に挿入されたデータは切り捨てられます。  
  
 列のデータ型の範囲外の値を挿入しようと、列に挿入する、NULL が発生します。  
  
 DBASE、Excel、Paradox、または Textdriver を使用すると、長さ 0 の文字列を列に挿入します。 実際に挿入 NULL 代わりにします。  
  
 Microsoft Excel のドライバーを使用すると、空の文字列が列に挿入する場合は、空の文字列が NULL に変換します。実行すると、WHERE 句で空の文字列を検索した SELECT ステートメントは、その列には成功しません。  
  
 テーブルでは、2 つの条件下で Paradox ドライバーによって更新できません。  
  
-   ときに一意のインデックスはテーブルで定義されていません。 空のテーブル、テーブルの一意のインデックスが定義されていない場合でも、1 つの行を更新できる場合は true ではありません。 一意のインデックスがない空のテーブル内 1 つの行が挿入される場合、アプリケーションが一意インデックスを作成または 1 つの行が挿入された後に、追加のデータを挿入できません。  
  
-   Borland データベース エンジンが実装されていない場合のみ読み取りし、追加ステートメントは、テーブルで使用します。  
  
 テキストのドライバーを使用すると、NULL 値には、固定長ファイルで空白が埋め込まれて文字列で表されますが、空白で区切られたファイルで表されます。 たとえば、3 つのフィールドを格納している次の行、2 番目のフィールドでは、NULL 値には。  
  
```  
"Smith:,, 123  
```  
  
 テキストのドライバーを使用する場合、すべての列の値は先頭のスペースが埋め込まれていることができます。 任意の行の長さは 65,543 バイト以下である必要があります。
