---
title: 図形の APPEND 句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e09113b42f655a3b94ab3877ff81f2553a363931
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924180"
---
# <a name="shape-append-clause"></a>Shape の APPEND 句
Shape コマンドの APPEND 句を追加、列または列を**Recordset**します。 これらの列が子を参照しているチャプター列には多くの場合、 **Recordset**します。  
  
## <a name="syntax"></a>構文  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>説明  
 この句の部分は次のとおりです。  
  
 *parent-command*  
 次のいずれかです (省略することができます、*親コマンド*完全に)。  
  
-   中かっこで囲まれているプロバイダー コマンド ("{}") を返す、 **Recordset**オブジェクト。 基になるデータ プロバイダーに、コマンドが発行され、その構文は、そのプロバイダーの要件によって異なります。 通常これは、SQL 言語では、ADO では、特定のクエリ言語は必要ありません。  
  
-   別の図形のコマンドは、かっこ内に埋め込まれます。  
  
-   テーブル キーワードは、後に、データ プロバイダーでのテーブルの名前。  
  
 *parent-alias*  
 省略可能な親を参照する別名**Recordset**します。  
  
 *column-list*  
 1 つ、または、次の詳細:  
  
-   集計列。  
  
-   計算列です。  
  
-   新しい句を使用して作成された新しい列。  
  
-   チャプター列。 チャプター列の定義は、かっこ (「()」) で囲まれます。 次の構文を参照してください。  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>コメント  
 *child-recordset*  
 -   中かっこで囲まれているプロバイダー コマンド ("{}") を返す、 **Recordset**オブジェクト。 基になるデータ プロバイダーに、コマンドが発行され、その構文は、そのプロバイダーの要件によって異なります。 通常これは、SQL 言語では、ADO では、特定のクエリ言語は必要ありません。  
  
-   別の図形のコマンドは、かっこ内に埋め込まれます。  
  
-   既存の型の名前**Recordset**します。  
  
-   テーブル キーワードは、後に、データ プロバイダーでのテーブルの名前。  
  
 *child-alias*  
 子を参照する別名**Recordset**します。  
  
 *parent-column*  
 内の列、 **Recordset**によって返される、*親コマンド。*  
  
 *child-column*  
 内の列、 **Recordset**によって返される、*子コマンド*します。  
  
 *param-number*  
 参照してください[パラメーター化コマンドの操作](../../../ado/guide/data/operation-of-parameterized-commands.md)します。  
  
 *チャプター エイリアス*  
 親に追加されたチャプター列を参照する別名です。  
  
> [!NOTE]
>  *"親列*TO*子列"* 句がリストでは実際には、各リレーションシップが定義されてがコンマで区切られています。  
  
> [!NOTE]
>  追加のキーワードの後に、句一覧を示します実際には、それぞれの句はコンマで区切られます、親に追加する別の列を定義します。  
  
## <a name="remarks"></a>コメント  
 SHAPE コマンドの一部としてユーザー入力からプロバイダーのコマンドを構築する際に図形はユーザーが指定した不透明な文字列としてプロバイダー コマンドを処理します。 およびにプロバイダーに渡します。 次の図形コマンドでなど  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 図形は 2 つのコマンドを実行します。`select * from t1`と (`select * from t2 RELATE k1 TO k2)`します。 場合はセミコロンで区切られた複数のプロバイダー コマンドで構成される複合コマンドを指定すると、図形は、違いを区別することはありません。 次の図形のコマンドのようになります  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 図形を実行します`select * from t1; drop table t1`と (`select * from t2 RELATE k1 TO k2),`を認識しないまま`drop table t1`独立した、この場合、危険な場合は、プロバイダー コマンドでします。 アプリケーションでは、ユーザーをこのような潜在的なハッカーの攻撃が発生していることを防ぐために入力を常に検証する必要があります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [非パラメーター化コマンドの操作](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [パラメーター化コマンドの操作](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [ハイブリッド コマンド](../../../ado/guide/data/hybrid-commands.md)  
  
-   [介在する Shape COMPUTE 句](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>関連項目  
 [データ シェイプの例](../../../ado/guide/data/data-shaping-example.md)   
 [Shape の正式文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般的な Shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)
