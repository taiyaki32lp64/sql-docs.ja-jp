---
title: パラメーター化コマンドの操作 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7d4399a8cf279ed2283061fff9064ffcc1adfba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924735"
---
# <a name="operation-of-parameterized-commands"></a>パラメーター化コマンドの操作
大規模な子を使用する場合**レコード セット**、特に、親のサイズと比較**レコード セット**、いくつかの子章のみにアクセスする必要がある場合がありますを使用する方が効率的、パラメーター化されたコマンド。  
  
 A*コマンドのパラメーター化されていない*全体の親と子の両方を取得します**レコード セット**を親にチャプター列を追加します。 や、親の行ごとに関連する子章への参照を割り当てます.  
  
 A*コマンドをパラメーター化された*全体の親を取得します。**レコード セット**、章のみを取得しますが、**レコード セット**チャプター列にアクセスするとします。 この違い取得方法の大幅なパフォーマンスのメリットが得ことができます。  
  
 たとえば、次のように指定できます。  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 親と子テーブルが共通の列名を含ま*cust_id*します。 *子コマンド*が、"でしょうか"プレース ホルダー、RELATE 句で参照する (つまり、"…。パラメーター 0")。  
  
> [!NOTE]
>  パラメーターの句は、shape コマンドの構文にのみ関連します。 ADO のいずれかに関連付けられてない[パラメーター](../../../ado/reference/ado-api/parameter-object.md)オブジェクトまたは[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)コレクション。  
  
 パラメーター化された図形のコマンドを実行すると、以下の処理が行われます。  
  
1.  *親コマンド*が実行され、親を返します**Recordset** Customers テーブルから。  
  
2.  チャプター列が、親に追加されます**Recordset**します。  
  
3.  親行のチャプター列がアクセスされたとき、*子コマンド*パラメーターの値として、customer.cust_id の値を使用して実行します。  
  
4.  手順 3 で作成したデータ プロバイダーの行セットのすべての行は、子の作成に使用されます**Recordset**します。 この例では、cust_id customer.cust_id の値に等しいを Orders テーブルのすべての行です。 既定では、子**Recordset**s が、親に対するすべての参照まで、クライアントにキャッシュされる**レコード セット**リリースされます。 この動作を変更するには、設定、**レコード セット**[動的プロパティ](../../../ado/reference/ado-api/ado-dynamic-property-index.md)**子行をキャッシュ**に**False**します。  
  
5.  取得した子の行への参照 (子の章では、**レコード セット**) は、親の現在の行のチャプター列に配置されます**レコード セット**します。  
  
6.  別の行のチャプター列にアクセスする場合は、3 ~ 5 の手順が繰り返されます。  
  
 **子行をキャッシュ**動的プロパティに設定されて**True**既定。 キャッシュの動作は、クエリのパラメーターの値によって異なります。 子の 1 つのパラメーターを持つクエリで**Recordset**その値を持つ子に対する要求間で特定のパラメーターの値がキャッシュされます。 次のコードでは、これを示しています。  
  
```  
SCmd = "SHAPE {select * from customer} " & _  
         "APPEND({select * from orders where cust_id = ?} " & _  
         "RELATE cust_id TO PARAMETER 0) AS chpCustOrder"  
Rst1.Open sCmd, Cnn1  
Set RstChild = Rst1("chpCustOrder").Value  
Rst1.MoveNext      ' Next cust_id passed to Param 0, & new rs fetched   
                   ' into RstChild.  
Rst1.MovePrevious  ' RstChild now holds cached rs, saving round trip.  
```  
  
 2 つ以上のパラメーターを持つクエリでは、キャッシュされた子をすべてのパラメーター値がキャッシュされた値と一致する場合にのみ使用します。  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>パラメーター化コマンドと複雑な親子関係  
 パラメーター化コマンドを使用して、等結合型の階層のパフォーマンスを向上させるために、だけでなくより複雑なプロセスの親子関係をサポートするためにパラメーター化コマンドを使用できます。 たとえば、2 つのテーブルでの少年野球リーグ データベース: チーム (team_id、チーム名) と (日付、home_team、visiting_team) ゲームの他から成る 1 つ。  
  
 パラメーター化されていない階層を使用して、方法はありません、このような方法でチームやゲームのテーブルを関連付けるを子**Recordset**に各チームには、完全なスケジュールが含まれています。 ホーム スケジュールまたは道路のスケジュールが、両方が含まれている章を作成することができます。 RELATE 句に、フォームの親子関係を制限します。 これは (pc1 = cc1) AND (pc2 = pc2)。 そのため、コマンドに"関連付け team_id TO home_team、team_id TO visiting_team"が含まれている場合得ゲームのみで、チームが再生されて自体。 必要なの"(team_id=home_team) または (team_id = visiting_team)"、Shape プロバイダーで OR 句がサポートされていません。  
  
 目的の結果を取得するには、パラメーター化されたコマンドを使用することができます。 以下に例を示します。  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 この例では、必要のある結果を取得するには、SQL の WHERE 句の柔軟性を悪用します。  
  
> [!NOTE]
>  WHERE 句を使用して、パラメーターは使用できません、SQL データ型 text、ntext および image またはエラーが発生する場合は、次の説明が含まれています:`Invalid operator for data type`します。  
  
## <a name="see-also"></a>関連項目  
 [データ シェイプの例](../../../ado/guide/data/data-shaping-example.md)   
 [Shape の正式文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般的な Shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)
