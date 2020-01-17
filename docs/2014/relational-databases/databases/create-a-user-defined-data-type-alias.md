---
title: ユーザー定義データ型の別名の作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.userdefineddatatype.general.f1
- sql12.swb.new.datatype.properties.general.f1
helpviewer_keywords:
- alias data types [SQL Server], creating
ms.assetid: b1dd8413-0cd0-411b-a79b-1bb043ccc62d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b073e6025bc1483db2482a03d525b758d39efea4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917446"
---
# <a name="create-a-user-defined-data-type-alias"></a>ユーザー定義データ型の別名の作成
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]にユーザー定義データ型の別名を新しく作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してユーザー定義データ型の別名を作成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   ユーザー定義データ型の別名は、識別子のルールに準拠した名前である必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 現在のデータベース内の CREATE TYPE 権限、および *schema_name*に対する ALTER 権限が必要です。 *schema_name* を指定しなかった場合は、現在のユーザーのスキーマを判断するための既定の名前解決ルールが適用されます。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-user-defined-data-type"></a>ユーザー定義データ型を作成するには  
  
1.  オブジェクト エクスプローラーで、 **[データベース]** を展開し、データベースを展開します。次に、 **[プログラミング]** 、 **[種類]** を順に展開し、 **[ユーザー定義データ型]** を右クリックして、 **[新しいユーザー定義データ型]** をクリックします。  
  
     **[NULL を許容]**  
     ユーザー定義データ型が NULL 値を受け入れるかどうかを指定します。 既存のユーザー定義データ型に対する NULL 値の許容/非許容は編集できません。  
  
     **データ型**  
     基本データ型をリスト ボックスから選択します。 リスト ボックスには、`geography`、`geometry`、`hierarchyid`、`sysname`、`timestamp`、`xml` の各データ型を除くすべてのデータ型が表示されます。 既存のユーザー定義データ型のデータ型は編集できません。  
  
     **既定値**  
     必要に応じて、ユーザー定義データ型の別名にバインドするルールまたは既定値を選択します。  
  
     **[長さ]/[有効桁数]**  
     データ型の長さまたは有効桁数を表示します (適用可能な場合)。 **[長さ]** は、文字ベースのユーザー定義データ型に適用されます。 **[有効桁数]** は、数値に基づくユーザー定義データ型にのみ適用されます。 ラベルは、先に選択されたデータ型によって変わります。 選択されているデータ型の長さまたは有効桁数が固定されている場合、このボックスは変更できません。  
  
     長さは、`nvarchar(max)`、`varchar(max)`、`varbinary(max)` の各データ型に対しては表示されません。  
  
     **名前**  
     ユーザー定義データ型の別名を新規に作成する場合、ユーザー定義データ型を表すためにデータベース全体で使用する一意の名前を入力します。 最大文字数は、システムと一致する必要があります`sysname`データ型。 既存のユーザー定義データ型の別名は編集できません。  
  
     **Rule**  
     必要に応じて、ユーザー定義データ型の別名にバインドするルールを選択します。  
  
     **Scale**  
     小数点の右側にとることのできる 10 進数の最大桁数を指定します。  
  
     **スキーマ**  
     現在のユーザーが使用できるすべてのスキーマの一覧からスキーマを選択します。 既定の選択は、現在のユーザーの既定のスキーマです。  
  
     **ストレージ**  
     ユーザー定義データ型の別名に対応するストレージの最大サイズを表示します。 ストレージの最大サイズは、有効桁数によって異なります。  
  
    |||  
    |-|-|  
    |1 - 9|5|  
    |10 - 19|9|  
    |20 - 28|13|  
    |29 - 38|17|  
  
     `nchar`と`nvarchar`データ型の場合は、ストレージ値は 2 倍の値では常に**長さ**します。  
  
     ストレージは、`nvarchar(max)`、`varchar(max)`、`varbinary(max)` の各データ型に対しては表示されません。  
  
2.  **[新しいユーザー定義データ型]** ダイアログ ボックスで、 **[スキーマ]** ボックスに、このデータ型の別名を所有するスキーマを入力するか、参照ボタン [...] を使用してスキーマを選択します。  
  
3.  **[名前]** ボックスに新しいデータ型の別名を入力します。  
  
4.  **[データ型]** ボックスで、新しいデータ型の別名の基になるデータ型を選択します。  
  
5.  選択したデータ型に該当する場合は、 **[長さ]** 、 **[有効桁数]** 、および **[小数点以下桁数]** ボックスへの設定を完了します。  
  
6.  新しいデータ型の別名で NULL 値を許可する場合は、 **[NULL を許容]** チェック ボックスをオンにします。  
  
7.  新しいデータ型の別名に既定値またはルールをバインドする場合は、 **[バインド]** で、 **[既定値]** または **[ルール]** ボックスへの設定を完了します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では、既定値やルールを作成できません。 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用します。 既定値やルールを作成するためのサンプル コードは、テンプレート エクスプローラーで使用できます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-user-defined-data-type-alias"></a>ユーザー定義データ型の別名を作成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、システムから提供されている `varchar` データ型に基づいて、データ型の別名を作成します。 データ型の別名 `ssn` 型は、11 桁の社会保障番号 (999-99-9999) を格納する列で使用されます。 この列で NULL 値は許容されません。  
  
```sql  
CREATE TYPE ssn  
FROM varchar(11) NOT NULL ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース識別子](database-identifiers.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql)  
  
  
