---
title: ALTER ASSEMBLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_ASSEMBLY_TSQL
- ALTER ASSEMBLY
dev_langs:
- TSQL
helpviewer_keywords:
- assemblies [CLR integration], modifying
- refreshing assemblies
- assemblies [CLR integration], versioning
- assemblies [CLR integration], adding files
- modifying assemblies
- adding files
- ALTER ASSEMBLY statement
ms.assetid: 87bca678-4e79-40e1-bb8b-bd5ed8f34853
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2881c4ee5145506158585611f61219983b764936
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066111"
---
# <a name="alter-assembly-transact-sql"></a>ALTER ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  アセンブリの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カタログ プロパティを変更することにより、アセンブリを変更します。 ALTER ASSEMBLY では、アセンブリの実装を保持する [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] モジュールの最新コピーが反映されるようにアセンブリを更新し、アセンブリに関連付けられているファイルを追加または削除します。 アセンブリは、[CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md) を使用して作成されます。  

> [!WARNING]
>  CLR では、セキュリティ境界としてサポートされなくなった、.NET Framework のコード アクセス セキュリティ (CAS) が使用されます。 `PERMISSION_SET = SAFE` で作成された CLR アセンブリが、外部のシステム リソースにアクセスし、非管理対象コードを呼び出し、sysadmin 特権を取得できる場合があります。 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 以降、CLR アセンブリのセキュリティを強化するために `clr strict security` という `sp_configure` オプションが導入されました。 `clr strict security` は既定で有効になり、`SAFE` および `EXTERNAL_ACCESS` アセンブリを `UNSAFE` とマークされている場合と同様に扱います。 `clr strict security` オプションは、旧バージョンとの互換性のために無効にできますが、これは推奨されません。 Microsoft では、master データベースで `UNSAFE ASSEMBLY` アクセス許可が付与されている対応するログインを含む証明書または非対称キーで、すべてのアセンブリに署名することをお勧めします。 詳しくは、「[CLR の厳密なセキュリティ](../../database-engine/configure-windows/clr-strict-security.md)」をご覧ください。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ALTER ASSEMBLY assembly_name  
    [ FROM <client_assembly_specifier> | <assembly_bits> ]  
    [ WITH <assembly_option> [ ,...n ] ]  
    [ DROP FILE { file_name [ ,...n ] | ALL } ]  
    [ ADD FILE FROM   
    {   
        client_file_specifier [ AS file_name ]   
      | file_bits AS file_name   
    } [,...n ]   
    ] [ ; ]  
<client_assembly_specifier> :: =  
    '\\computer_name\share-name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
    { varbinary_literal | varbinary_expression }  
  
<assembly_option> :: =  
    PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
  | VISIBILITY = { ON | OFF }  
  | UNCHECKED DATA  
  
```  
  
## <a name="arguments"></a>引数  
 *assembly_name*  
 変更するアセンブリの名前です。 *assembly_name* がデータベースに既に存在する必要があります。  
  
 FROM \<client_assembly_specifier> | \<assembly_bits>  
 アセンブリを更新して、アセンブリの実装を保持する [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] モジュールの最新コピーを反映させます。 このオプションを使用できるのは、指定したアセンブリに関連付けられているファイルが存在しない場合だけです。  
  
 \<client_assembly_specifier> には、更新するアセンブリが配置されているネットワーク上の場所またはローカルの場所を指定します。 ネットワーク上の場所を指定する場合は、コンピューター名、共有名、および共有内のパスを指定します *manifest_file_name* には、アセンブリのマニフェストを含むファイルの名前を指定します。  

> [!IMPORTANT]
> Azure SQL Database では、ファイルの参照はサポートされません。
  
 \<assembly_bits> は、アセンブリのバイナリ値です。  
  
 更新も必要な依存アセンブリに対して、個別の ALTER ASSEMBLY ステートメントを実行する必要があります。  
  
 PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
> [!IMPORTANT]
>  `PERMISSION_SET` オプションは、開始の警告で説明されるように、`clr strict security` オプションの影響を受けます。 `clr strict security` が有効になっていると、すべてのアセンブリが `UNSAFE` として処理されます。  
>  アセンブリの [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] コード アクセス権セットのプロパティを指定します。 このプロパティの詳細については、「[CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)」を参照してください。  
> 
> [!NOTE]
>  EXTERNAL_ACCESS および UNSAFE オプションは、包含データベースでは使用できません。  
  
 VISIBILITY = { ON | OFF }  
 アセンブリに対する共通言語ランタイム (CLR) 関数、ストアド プロシージャ、トリガー、ユーザー定義型、およびユーザー定義集計関数の作成時に、そのアセンブリが表示されるかどうかを指定します。 OFF に設定した場合、アセンブリは、他のアセンブリによってのみ呼び出されることが想定されます。 アセンブリに対して既に作成された CLR データベース オブジェクトが存在する場合、そのアセンブリの表示は変更できません。 *assembly_name* によって参照されるアセンブリは、既定では非表示としてアップロードされます。  
  
 UNCHECKED DATA  
 既定では、個々のテーブル行の一貫性を検証する必要がある場合、ALTER ASSEMBLY は失敗します。 このオプションを指定すると、DBCC CHECKTABLE を使用して、この検証を後に延期することができます。 これを指定した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データベースのテーブルに次のデータが含まれていても、ALTER ASSEMBLY ステートメントが実行されます。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数やメソッドから直接または間接的にアセンブリ内のメソッドを参照する、保存される計算列。  
  
-   直接または間接的にアセンブリ内のメソッドを参照する CHECK 制約。  
  
-   アセンブリに依存する CLR ユーザー定義型の列と、**UserDefined** (非**ネイティブ**) シリアル化形式を実装する型の列。  
  
-   WITH SCHEMABINDING を使用して作成されたビューを参照する、CLR ユーザー定義型の列。  
  
 CHECK 制約がある場合、これらのデータは無効になり、信頼されていないことを示すマークが付きます。 アセンブリに依存する列が含まれるテーブルは、明示的に検証されるまで、未検証のデータが含まれていることを示すマークが付きます。  
  
 このオプションを指定できるのは、**db_owner** 固定データベース ロールと **db_ddlowner** 固定データベース ロールのメンバーだけです。  
  
 このオプションを指定するには、**ALTER ANY SCHEMA** 権限が必要です。  
  
 詳細については、「[アセンブリの実装](../../relational-databases/clr-integration/assemblies-implementing.md)」を参照してください。  
  
 [ DROP FILE { *file_name*[ **,** _...n_] | ALL } ]  
 アセンブリに関連付けられているファイル名、またはアセンブリに関連付けられているすべてのファイルを、データベースから削除します。 続けて ADD FILE を指定する場合は、最初に DROP FILE が実行されます。 このため、同じファイル名でファイルを置き換えることができます。  
  
> [!NOTE]  
>  このオプションは、包含データベースまたは Azure SQL Database では使用できません。  
  
 [ ADD FILE FROM { *client_file_specifier* [ AS *file_name*] | *file_bits*AS *file_name*}  
 ソース コード、デバッグ ファイル、その他の関連情報など、アセンブリに関連付けられるファイルをサーバーにアップロードし、**sys.assembly_files** カタログ ビューに表示できるようにします。 *client_file_specifier* には、ファイルのアップロード元となる場所を指定します。 *file_bits* を代わりに使用し、ファイルを構成するバイナリ値の一覧を指定できます。 *file_name* には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに格納する必要があるファイルの名前を指定します。 *file_name* は、*file_bits* が指定されている場合は指定する必要があり、*client_file_specifier* が指定されている場合はオプションになります。 *file_name* が指定されていない場合、*client_file_specifier* の file_name の部分が *file_name* として使用されます。  
  
> [!NOTE]  
>  このオプションは、包含データベースまたは Azure SQL Database では使用できません。  
  
## <a name="remarks"></a>Remarks  
 変更するアセンブリ内のコードが、現在実行中のセッションで実行されている場合、ALTER ASSEMBLY でセッションは中断されません。 現在のセッションは、アセンブリの変更されていないビット列を使用して最後まで実行されます。  
  
 FROM 句を指定した場合、ALTER ASSEMBLY では、指定したモジュールの最新コピーが反映されるようにアセンブリが更新されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内に CLR 関数、ストアド プロシージャ、トリガー、データ型、ユーザー定義集計関数が存在し、それらがアセンブリに対して既に定義されている可能性があるため、ALTER ASSEMBLY ステートメントでは、これらがアセンブリの最新の実装に再バインドされます。 この再バインドを適切に行うには、CLR 関数、ストアド プロシージャ、およびトリガーにマップされるメソッドが、同じ署名を持つ変更済みのアセンブリ内に存在している必要があります。 CLR ユーザー定義型とユーザー定義集計関数が実装されているクラスは、ユーザー定義型または集計の要件を満たしている必要があります。  
  
> [!CAUTION]  
>  WITH UNCHECKED DATA を指定せず、新しいバージョンのアセンブリによってテーブルの既存のデータ、インデックス、または他の固有サイトに影響が生じる場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では ALTER ASSEMBLY の実行回避が試みられます。 ただし、CLR アセンブリが更新された場合、計算列、インデックス、インデックス付きビュー、式と、基になるルーチンとデータ型との一貫性は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では保証されません。 式の結果と、アセンブリに格納されている式に基づく値に不一致がないかどうかを ALTER ASSEMBLY で確認する場合は注意してください。  
  
 ALTER ASSEMBLY ではアセンブリのバージョンが変更されます。 アセンブリのカルチャおよび公開キー トークンは変更されません。  
  
 ALTER ASSEMBLY ステートメントを使用しても、次の情報は変更できません。  
  
-   アセンブリを参照する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内の CLR 関数、集計関数、ストアド プロシージャ、およびトリガーの署名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内の [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データベース オブジェクトを新しいバージョンのアセンブリに再バインドできない場合、ALTER ASSEMBLY は失敗します。  
  
-   別のアセンブリから呼び出されるアセンブリ内のメソッドの署名。  
  
-   アセンブリに依存するアセンブリの一覧。この一覧はアセンブリの **DependentList** プロパティ内で参照されます。  
  
-   メソッドのインデックス機能。ただし、直接または間接的にそのメソッドに依存するインデックスや保存される計算列が存在する場合に限ります。  
  
-   CLR テーブル値関数の **FillRow** メソッド名の属性。  
  
-   ユーザー定義集計のメソッド署名、**Accumulate** と **Terminate**。  
  
-   システム アセンブリ。  
  
-   アセンブリの所有権。 代わりに [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md) を使用します。  
  
 さらに、ユーザー定義型を実装するアセンブリに対しては、ALTER ASSEMBLY を使用して次の変更だけを行えます。  
  
-   ユーザー定義型クラスのパブリック メソッドの変更 (署名または属性が変更されない場合のみ)。  
  
-   新しいパブリック メソッドの追加。  
  
-   任意の方法でのプライベート メソッドの変更。  
  
 データ メンバーやベース クラスなど、ネイティブでシリアル化されたユーザー定義型に含まれるフィールドは、ALTER ASSEMBLY では変更できません。 その他の変更はいずれもサポートされていません。  
  
 ADD FILE FROM を指定しない場合、ALTER ASSEMBLY ではそのアセンブリに関連付けられているファイルがいずれも削除されます。  
  
 UNCHECKED データ句を指定せずに ALTER ASSEMBLY を実行した場合は、新しいバージョンのアセンブリがテーブル内の既存のデータに影響しないかどうかを検証するためのチェックが行われます。 チェックの対象となるデータ量によっては、パフォーマンスが影響を受ける場合があります。  
  
## <a name="permissions"></a>アクセス許可  
 アセンブリに対する ALTER 権限が必要です。 その他に次の要件があります。  
  
-   既存の権限セットが EXTERNAL_ACCESS になっているアセンブリを変更するには、サーバーに対する **EXTERNAL ACCESS ASSEMBLY** 権限が必要です。  
  
-   既存の権限セットが UNSAFE のアセンブリを変更するには、サーバーに対する **UNSAFE ASSEMBLY** 権限が必要です。  
  
-   アセンブリの権限セットを EXTERNAL_ACCESS に変更するには、サーバーに対する **EXTERNAL ACCESS ASSEMBLY** 権限が必要です。  
  
-   アセンブリの権限セットを UNSAFE に変更するには、サーバーに対する **UNSAFE ASSEMBLY** 権限が必要です。  
  
-   WITH UNCHECKED DATA を指定するには、**ALTER ANY SCHEMA** 権限が必要です。  


### <a name="permissions-with-clr-strict-security"></a>CLR の厳密なセキュリティによるアクセス許可    
`CLR strict security` が有効になっている場合に CLR アセンブリを変更するには、次のアクセス許可が必要です。

- ユーザーには `ALTER ASSEMBLY` アクセス許可が必要です  
- さらに、次の条件のいずれかを満たす必要があります。  
  - サーバーでの `UNSAFE ASSEMBLY` アクセス許可のある対応するログインを含む証明書または非対称キーでアセンブリが署名されている。 アセンブリへの署名は推奨されます。  
  - データベースに `ON` に設定された `TRUSTWORTHY` プロパティが含まれ、そのデータベースがサーバーでの `UNSAFE ASSEMBLY` アクセス許可のあるログインによって所有されている。 このオプションは推奨されません。  
  
  
 アセンブリの権限セットの詳細については、「[アセンブリのデザイン](../../relational-databases/clr-integration/assemblies-designing.md)」をご覧ください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-refreshing-an-assembly"></a>A. アセンブリを更新する  
 次の例では、`ComplexNumber` アセンブリを更新して、その実装を保持する [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] モジュールの最新コピーを反映させます。  
  
> [!NOTE]  
>  アセンブリ `ComplexNumber` は、サンプル スクリプト UserDefinedDataType を実行することによって作成できます。 詳細については、「[ユーザー定義型](https://msdn.microsoft.com/library/a9b75f36-d7f5-47f7-94d6-b4448c6a2191)」を参照してください。  
  
 ```
 ALTER ASSEMBLY ComplexNumber 
 FROM 'C:\Program Files\Microsoft SQL Server\130\Tools\Samples\1033\Engine\Programmability\CLR\UserDefinedDataType\CS\ComplexNumber\obj\Debug\ComplexNumber.dll' 
  ```

> [!IMPORTANT]
> Azure SQL Database では、ファイルの参照はサポートされません。

### <a name="b-adding-a-file-to-associate-with-an-assembly"></a>B. ファイルを追加してアセンブリに関連付ける  
 次の例では、ソース コード ファイル `Class1.cs` をアップロードして、アセンブリ `MyClass` に関連付けます。 この例では、アセンブリ `MyClass` がデータベースに既に作成されていることを前提としています。  
  
```  
ALTER ASSEMBLY MyClass   
ADD FILE FROM 'C:\MyClassProject\Class1.cs';  
```  

> [!IMPORTANT]
> Azure SQL Database では、ファイルの参照はサポートされません。

### <a name="c-changing-the-permissions-of-an-assembly"></a>C. アセンブリの権限を変更する  
 次の例では、アセンブリ `ComplexNumber` の権限セットを、SAFE から `EXTERNAL ACCESS` に変更します。  
  
```  
ALTER ASSEMBLY ComplexNumber WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
