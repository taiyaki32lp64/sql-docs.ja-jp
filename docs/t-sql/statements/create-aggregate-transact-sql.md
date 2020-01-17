---
title: CREATE AGGREGATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_AGGREGATE_TSQL
- CREATE AGGREGATE
- AGGREGATE_TSQL
- AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE AGGREGATE statement
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: 62eebc19-9f15-4245-94fa-b3fcd64a9d42
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1e796155210017addb6801930903a5aa38df71e8
ms.sourcegitcommit: e9c1527281f2f3c7c68981a1be94fe587ae49ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064627"
---
# <a name="create-aggregate-transact-sql"></a>CREATE AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] のアセンブリのクラスで実装が定義される、ユーザー定義集計関数を作成します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が集計関数を実装にバインドするには、先に CREATE ASSEMBLY ステートメントを使用して、その実装を含む [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] アセンブリを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにアップロードしておく必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE AGGREGATE [ schema_name . ] aggregate_name  
        (@param_name <input_sqltype>   
        [ ,...n ] )  
RETURNS <return_sqltype>  
EXTERNAL NAME assembly_name [ .class_name ]  
  
<input_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
<return_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
```  
  
## <a name="arguments"></a>引数  
 *schema_name*  
 ユーザー定義集計関数が所属しているスキーマの名前です。  
  
 *aggregate_name*  
 作成する集計関数の名前です。  
  
 **@** _param_name_  
 ユーザー定義集計で定義された 1 つまたは複数のパラメーター。 パラメーターの値は、集計関数の実行時にユーザーが指定する必要があります。 パラメーター名は、最初の文字を "アット" マーク ( **@** ) にして指定します。 パラメーター名は[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。 パラメーターは関数に対してローカルです。  
  
 *system_scalar_type*  
 入力パラメーターの値または戻り値を保持する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システムのスカラーのデータ型です。 **text**、**ntext**、**image** 以外のすべてのスカラーのデータ型は、ユーザー定義集計のパラメーターとして使用できます。 **cursor** や **table** など、スカラー型以外のデータ型は指定できません。  
  
 *udt_schema_name*  
 CLR ユーザー定義型が所属しているスキーマの名前です。 指定しない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] は次の順序で *udt_type_name* を参照します。  
  
-   ネイティブ SQL 型の名前空間。  
  
-   現在のデータベースにおける現在のユーザーの既定のスキーマ。  
  
-   現在のデータベースの **dbo** スキーマ。  
  
 *udt_type_name*  
 現在のデータベースに既に作成されている CLR ユーザー定義型の名前です。 *udt_schema_name* を指定しない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、型は現在のユーザーのスキーマに所属すると見なされます。  
  
 *assembly_name* [ **.** _class_name_ ]  
 ユーザー定義集計関数にバインドするアセンブリ、および必要に応じて、アセンブリが所属するスキーマの名前とユーザー定義集計を実装するアセンブリ内のクラス名を指定します。 アセンブリは、CREATE ASSEMBLY ステートメントを使用してデータベース内に作成されている必要があります。 *class_name* は有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子でなければならず、アセンブリに存在するクラスの名前と一致する必要があります。 C# など、クラスを記述するのに使用するプログラミング言語で名前空間を使用する場合、*class_name* には名前空間で修飾された名前を指定できます。 *class_name* を指定しない場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、*aggregate_name* と同じであると見なされます。  
  
## <a name="remarks"></a>Remarks  
 既定では、CLR コードを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能はオフになっています。 マネージド コード モジュールを参照するデータベース オブジェクトを作成、変更、削除できますが、これらのモジュールのコードは、[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用して [clr enabled option](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) を有効にしない限り [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスでは動作しません。  
  
 *assembly_name* とそのメソッドで参照されているアセンブリのクラスは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスでユーザー定義集計関数を実装するためのすべての要件を満たしている必要があります。 詳細については、「[CLR ユーザー定義集計](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 EXTERNAL NAME 句で指定されているアセンブリ上に CREATE AGGREGATE 権限と REFERENCES 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、StringUtilities.csproj サンプル アプリケーションがコンパイルされていることを前提としています。 詳細については、「[文字列ユーティリティ関数サンプル](https://msdn.microsoft.com/library/9623013f-15f1-4614-8dac-1155e57c880c)」を参照してください。  
  
 この例は集計 `Concatenate` を作成します。 集計が作成される前に、アセンブリ `StringUtilities.dll` がローカル データベースに登録されます。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may have to modify the value of the this variable if you have  
--installed the sample some location other than the default location.  
  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
     FROM master.sys.database_files   
     WHERE name = 'master';  
  
CREATE ASSEMBLY StringUtilities FROM @SamplesPath + 'StringUtilities\CS\StringUtilities\bin\debug\StringUtilities.dll'  
WITH PERMISSION_SET=SAFE;  
GO  
  
CREATE AGGREGATE Concatenate(@input nvarchar(4000))  
RETURNS nvarchar(4000)  
EXTERNAL NAME [StringUtilities].[Microsoft.Samples.SqlServer.Concatenate];  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DROP AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-aggregate-transact-sql.md)  
  
  
