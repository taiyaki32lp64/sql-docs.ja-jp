---
title: SQL Server の単体テストでの Transact-SQL アサーションの使用 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 55d8be9c-9282-47d3-be7f-e2c26f00c95e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b4ff76e7d980081208f310dcae2a498f857151df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140964"
---
# <a name="using-transact-sql-assertions-in-sql-server-unit-tests"></a>SQL Server の単体テストでの Transact-SQL アサーションの使用
SQL Server の単体テストでは、Transact\-SQL テスト スクリプトが実行され、結果が返されます。 結果が結果セットとして返される場合もあります。 テスト条件を使用して結果を検証できます。 たとえば、テスト条件を使用すると、特定の結果セットで返された行数を確認したり、特定のテストの実行にかかった時間を調べたりできます。 テスト条件について詳しくは、「[SQL Server の単体テストでのテスト条件の使用](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)」をご覧ください。  
  
テスト条件を使用する代わりに、Transact\-SQL アサーション (Transact\-SQL スクリプト内で THROW ステートメントまたは RAISERROR ステートメント) を使用することもできます。 状況によっては、テスト条件ではなく Transact\-SQL アサーションを使用することをお勧めします。  
  
## <a name="using-transact-sql-assertions"></a>Transact-SQL アサーションの使用  
データの検証に Transact\-SQL アサーションとテスト条件のどちらを使用するかを決定する前に、次の点を考慮してください。  
  
-   **パフォーマンス**。 サーバーで Transact\-SQL アサーションを実行すると、データをクライアント コンピューターに移動してローカルで操作する場合よりも処理速度が向上します。  
  
-   **使い慣れた言語**。 現在の使用経験に応じて特定の言語を選択することにより、Transact\-SQL アサーションか、Visual C\# または Visual Basic のテスト条件を選択できます。  
  
-   **複雑な検証**。 場合によっては、より複雑なテストを Visual C\# または Visual Basic でビルドし、クライアントでテストを検証できます。  
  
-   **簡潔さ**。 定義済みのテスト条件を使用する方が、Transact\-SQL で同じスクリプトを記述するよりも簡単になることがよくあります。  
  
-   **従来の検証ライブラリ**。 検証を実行するコードが既にある場合は、テスト条件の代わりに、既存のコードを SQL Server の単体テストで使用できます。  
  
## <a name="mark-unit-test-methods-with-the-expected-exception"></a>予期される例外が指定された単体テスト メソッドのマーク  
SQL Server の単体テスト メソッドに予期される例外を指定するには、次の属性を追加します。  
  
```vb  
<ExpectedSqlException(MessageNumber=nnnnn, Severity=x, MatchFirstError=false, State=y)> _  
```  
  
```csharp  
[ExpectedSqlException(MessageNumber=nnnnn, Severity=x, MatchFirstError=false, State=y)]  
```  
  
各要素の説明は次のとおりです。  
  
-   *nnnnn* は、予期されるメッセージの番号 (たとえば 14025) です。  
  
-   *x* は、予期される例外の重大度です。  
  
-   *y* は、予期される例外の状態です。  
  
指定されていないパラメーターは無視されます。 これらのパラメーターは、データベース コードの RAISERROR ステートメントに渡します。 MatchFirstError = true を指定すると、この属性は例外のいずれの SqlErrors にも一致します。 既定の動作 (MatchFirstError = true) は、最初に発生するエラーにしか一致しません。  
  
予期される例外と SQL Server のネガティブ単体テストの使用方法の例については、「[チュートリアル: SQL Server の単体テストの作成と実行](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)」を参照してください。  
  
## <a name="the-raiserror-statement"></a>RAISERROR ステートメント  
  
> [!NOTE]  
> RAISERROR の代わりに THROW を使用します。 RAISERROR は非推奨とされます。  
  
Transact\-SQL スクリプトで RAISERROR ステートメントを使用すると、サーバーで Transact\-SQL アサーションを直接使用できます。 構文は次のとおりです。  
  
**RAISERROR (@ErrorMessage, @ErrorSeverity, @ErrorState)**  
  
それぞれの文字の説明は次のとおりです。  
  
@ErrorMessage は、ユーザー定義のエラー メッセージです。 このメッセージ文字列は、printf_s 関数に似た形式で書式設定できます。  
  
@ErrorSeverity は、ユーザー定義の重大度レベル (0 から 18) です。  
  
> [!NOTE]  
> 重大度レベルの値が "0" および "10" の場合、SQL Server の単体テストは失敗しません。 0 ～ 18 の範囲でその他の値を使用すると、テストが失敗します。  
  
@ErrorState は、1 から 127 の任意の整数です。 この整数を使用すると、コード内の別の場所で発生した 1 つのエラーの複数の出現を区別できます。  
  
詳しくは、「[RAISERROR (Transact-SQL)](https://msdn.microsoft.com/library/ms178592.aspx)」をご覧ください。 SQL Server の単体テストでの RAISERROR の使用例については、トピック「[単一のトランザクションのスコープ内で実行する SQL Server の単体テストを作成する方法](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md)」を参照してください  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server の単体テストでのテスト条件の使用](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
[SQL Server の単体テストを使用したデータベース コードの検証](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[方法: SQL Server の単体テストを開いて編集する](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md)  
  
