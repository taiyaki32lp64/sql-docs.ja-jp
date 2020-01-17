---
title: Shape の正式文法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91bdf0cfbfe87075d2c9484bca7edd835a950ee6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925346"
---
# <a name="formal-shape-grammar"></a>Shape の正式文法
これは、任意図形のコマンドを作成するための正式な文法です。  
  
-   必要な文法的な用語では、山かっこ ("<>") で区切られたテキスト文字列を示します。  
  
-   省略可能な条件は、角かっこ ("") で区切られます。  
  
-   代替手段は、縦棒で示されます ("&#124;") です。  
  
-   繰り返しの代替手段は、省略記号 (「...」) によって示されます。  
  
-   *アルファ*英文字の文字列を示します。  
  
-   *数字*の数値の文字列を示します。  
  
-   *Unicode の数字*unicode の数字の文字列を示します。  
  
 その他のすべての用語は、リテラルです。  
  
|項目|定義|  
|----------|----------------|  
|\<shape-command>|SHAPE [\<table-exp> [[AS] \<alias>]][\<shape-action>]|  
|\<table-exp>|{\<プロバイダー コマンド テキスト >} &#124; です。<br /><br /> (\<shape コマンド >) &#124;<br /><br /> テーブル\<引用符で囲まれた名 > &#124; です。<br /><br /> \<quoted-name>|  
|\<shape-action>|APPEND\<エイリアス フィールド リスト > &#124; です。<br /><br /> コンピューティング\<エイリアス > [BY\<フィールド リスト >]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<関係 exp >) &#124;<br /><br /> \<計算 exp > &#124; です。<br /><br /> \<集計 exp > &#124; です。<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias>]<br /><br /> RELATE \<relation-cond-list>|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<フィールド名 > に\<子 ref >|  
|\<child-ref>|\<フィールド名 > &#124; です。<br /><br /> PARAMETER \<param-ref>|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM (\<修飾されたフィールド名 >) &#124;<br /><br /> AVG (\<修飾されたフィールド名 >) &#124;<br /><br /> MIN (\<修飾されたフィールド名 >) &#124;<br /><br /> MAX (\<修飾されたフィールド名 >) &#124;<br /><br /> カウント (\<修飾されたエイリアス > &#124; です。\<修飾名 >) &#124;<br /><br /> STDEV (\<修飾されたフィールド名 >) &#124;<br /><br /> ANY(\<qualified-field-name>)|  
|\<calculated-exp>|CALC(\<expression>)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<エイリアス >|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias>]|  
|\<quoted-name>|"\<文字列 >"&#124; です。<br /><br /> '\<文字列 >' &#124;<br /><br /> [\<文字列 >] &#124; です。<br /><br /> \<name>|  
|\<qualified-name>|エイリアス [.alias...]|  
|\<name>|アルファ [alpha &#124; 数字 &#124; 以外の場合は _ &#124; # &#124; : &#124;...]|  
|\<number>|[数字] の数字|  
|\<new-exp>|NEW \<field-type> [(\<number> [, \<number>])]|  
|\<field-type>|OLE DB または ADO データ型。|  
|\<string>|unicode char [unicode 文字...]|  
|\<expression>|アプリケーションの式オペランドが同じ行の場合は、他の非計算列用の Visual Basic の場合。|  
  
## <a name="see-also"></a>関連項目  
 [階層レコード セット内の行へのアクセス](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [データ シェイプの概要](../../../ado/guide/data/data-shaping-overview.md)   
 [データ シェイプに必要なプロバイダー](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape の APPEND 句](../../../ado/guide/data/shape-append-clause.md)   
 [一般的な shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape COMPUTE 句](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications の関数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
