---
title: MSSQLSERVER_4104 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4104 (Database Engine error)
ms.assetid: 52dc32d8-97ad-4ef0-834d-2e68f215d007
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 27f6dfb6a41bab31fb716671f431115468d8bd86
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120587"
---
# <a name="mssqlserver4104"></a>MSSQLSERVER_4104
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|4104|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|ALG_MULTI_ID_BAD|  
|メッセージ テキスト|マルチパート識別子 "%.*ls" をバインドできませんでした。|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのエンティティの名前は、そのエンティティの "*識別子*" と呼ばれます。 識別子は、クエリ内で列やテーブルの名前を指定する場合など、エンティティを参照するときは必ず使用します。 マルチパート識別子には、1 つ以上の修飾子が識別子のプレフィックスとして含まれます。 たとえば、テーブル識別子は、そのテーブルが含まれるデータベースの名前やスキーマの名前などの修飾子をプレフィックスとして持つことができます。また列識別子は、テーブル名やテーブル別名などの修飾子をプレフィックスとして持つことができます。  
  
エラー 4104 は、指定されたマルチパート識別子を既存のエンティティにマップできなかったことを示します。 このエラーは、次のような状況で返される可能性があります。  
  
-   列名のプレフィックスとして指定された修飾子と、クエリで使用されているテーブル名または別名が一致しない。  
  
    たとえば、次のステートメントでは、テーブル別名 (`Dept`) を列プレフィックスとして使用していますが、このテーブル別名は FROM 句で参照されていません。  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department;  
    ```  
  
    次のステートメントでは、WHERE 句で 2 つのテーブル間の JOIN 条件の一部としてマルチパート列識別子 `TableB.KeyCol` を指定していますが、`TableB` はクエリで明示的に参照されていません。  
  
    ```  
    DELETE FROM TableA WHERE TableA.KeyCol = TableB.KeyCol;  
    ```  
  
    ```  
    SELECT 'X' FROM TableA WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   FROM 句でテーブルの別名を指定しているが、列のプレフィックスとして指定しているのはテーブル名である。 たとえば、次のステートメントでは、FROM 句でテーブルの別名 (`Department`) を参照しているにもかかわらず、テーブル名 `Dept` を列プレフィックスとして使用しています。  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department AS Dept;  
    ```  
  
    別名を使用する場合、テーブル名をステートメントの他の部分で使用することはできません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、マルチパート識別子がテーブルをプレフィックスとする列を参照しているか、または列をプレフィックスとする CLR ユーザー定義データ型 (UDT) のプロパティを参照しているかを判断できない。 このような状況が発生するのは、UDT 列のプロパティを参照するとき、列名にテーブル名をプレフィックスとして加える場合と同じように、列名とプロパティ名の間に区切り文字としてピリオド (.) を使用するためです。 次の例では、`a` と `b` という 2 つのテーブルを作成します。 テーブル `b` は列 `a` を含み、この列は CLR UDT の `dbo.myudt2` をデータ型として使用します。 SELECT ステートメントはマルチパート識別子 `a.c2` を含みます。  
  
    ```  
    CREATE TABLE a (c2 int);   
    GO  
    ```  
  
    ```  
    CREATE TABLE b (a dbo.myudt2);   
    GO  
    ```  
  
    ```  
    SELECT a.c2 FROM a, b;   
    ```  
  
    UDT `myudt2` が `c2` という名前のプロパティを持たないと仮定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、識別子 `a.c2` がテーブル `a` の列 `c2` を参照するのか、テーブル `b` の列 `a` のプロパティ `c2` を参照するのかを判断できません。  
  
## <a name="user-action"></a>ユーザーの操作  
  
-   列プレフィックスとクエリの FROM 句で指定したテーブル名または別名を一致させます。 FROM 句でテーブルの別名を定義した場合、テーブルに関連する列の修飾子として使用できるのはその別名だけです。  
  
    `HumanResources.Department` テーブルを参照する上記のステートメントは、次のように修正できます。  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department AS Dept;  
    GO  
    ```  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department;  
    GO  
    ```  
  
-   すべてのテーブルがクエリで指定されていること、およびテーブル間の JOIN 条件が正しく指定されていることを確認します。 上記の DELETE ステートメントは次のように修正できます。  
  
    ```  
    DELETE FROM dbo.TableA  
    WHERE TableA.KeyCol = (SELECT TableB.KeyCol   
                            FROM TableB   
                            WHERE TableA.KeyCol = TableB.KeyCol);  
    GO  
    ```  
  
    `TableA` に対する上記の SELECT ステートメントは次のように修正できます。  
  
    ```  
    SELECT 'X' FROM TableA, TableB WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
    内の複数の  
  
    ```  
    SELECT 'X' FROM TableA INNER JOIN TableB ON TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   明確に定義された一意の名前を識別子に使用します。 こうすることにより、コードの読みやすさと管理性が向上し、複数のエンティティをあいまいに参照する危険性も最小限に抑えられます。  
  
## <a name="see-also"></a>参照  
[MSSQLSERVER_107](~/relational-databases/errors-events/mssqlserver-107-database-engine-error.md)  
[データベース識別子](~/relational-databases/databases/database-identifiers.md)  
  
