---
title: CREATE ASSEMBLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASSEMBLY
- CREATE ASSEMBLY
- CREATE_ASSEMBLY_TSQL
- ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- assemblies [CLR integration], validating
- validating assemblies
- CREATE ASSEMBLY statement
- assemblies [CLR integration], creating
ms.assetid: d8d1d245-c2c3-4325-be52-4fc1122c2079
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 276e7a88d7cd10f6ee98a6dde80d3f86c39b2c08
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981987"
---
# <a name="create-assembly-transact-sql"></a>CREATE ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  クラス メタデータとマネージド コードを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内のオブジェクトとして含む、マネージド アプリケーション モジュールを作成します。 データベース内でこのモジュールを参照することにより、共通言語ランタイム (CLR) 関数、ストアド プロシージャ、トリガー、ユーザー定義集計関数、ユーザー定義型を作成できます。  
  
> [!WARNING]
>  CLR では、セキュリティ境界としてサポートされなくなった、.NET Framework のコード アクセス セキュリティ (CAS) が使用されます。 `PERMISSION_SET = SAFE` で作成された CLR アセンブリが、外部のシステム リソースにアクセスし、非管理対象コードを呼び出し、sysadmin 特権を取得できる場合があります。 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 以降、CLR アセンブリのセキュリティを強化するために `clr strict security` という `sp_configure` オプションが導入されました。 `clr strict security` は既定で有効になり、`SAFE` および `EXTERNAL_ACCESS` アセンブリを `UNSAFE` とマークされている場合と同様に扱います。 `clr strict security` オプションは、旧バージョンとの互換性のために無効にできますが、これは推奨されません。 Microsoft では、master データベースで `UNSAFE ASSEMBLY` アクセス許可が付与されている対応するログインを含む証明書または非対称キーで、すべてのアセンブリに署名することをお勧めします。 詳しくは、「[CLR の厳密なセキュリティ](../../database-engine/configure-windows/clr-strict-security.md)」をご覧ください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE ASSEMBLY assembly_name  
[ AUTHORIZATION owner_name ]  
FROM { <client_assembly_specifier> | <assembly_bits> [ ,...n ] }  
[ WITH PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE } ]  
[ ; ]  
<client_assembly_specifier> :: =  
        '[\\computer_name\]share_name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
{ varbinary_literal | varbinary_expression }  
```  
  
## <a name="arguments"></a>引数  
 *assembly_name*  
 アセンブリの名前を指定します。 名前はデータベース内で一意であり、有効な[識別子](../../relational-databases/databases/database-identifiers.md)であることが必要です。  
  
 AUTHORIZATION *owner_name*  
 アセンブリの所有者となるユーザーまたはロールの名前を指定します。 *owner_name* に現在のユーザーがメンバーとなっているロールの名前を指定するか、現在のユーザーが *owner_name* に対する IMPERSONATE 権限を持っている必要があります。 このオプションを指定しない場合は、所有権は現在のユーザーに与えられます。  
  
 \<client_assembly_specifier>  
アップロードされているアセンブリが置かれるローカル パスまたはネットワーク上の位置と、そのアセンブリに対応するマニフェスト ファイル名を指定します。  \<client_assembly_specifier> は、固定文字列または変数で固定文字列に評価される式で表すことができます。 CREATE ASSEMBLY では、マルチモジュール アセンブリの読み込みはサポートしていません。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこのアセンブリの依存アセンブリが同じ場所にないか検索され、同じ所有者の依存アセンブリがルート レベル アセンブリとしてアップロードされます。 これらの依存アセンブリが検出されず、現在のデータベースに読み込まれていない場合、CREATE ASSEMBLY は失敗します。 依存アセンブリが現在のアセンブリに既に読み込まれている場合、これらのアセンブリの所有者は、新しく作成されたアセンブリの所有者と同じである必要があります。

> [!IMPORTANT]
> Azure SQL Database では、ファイルからのアセンブリの作成はサポートされません。
  
 ログインしたユーザーの権限が借用されている場合、\<client_assembly_specifier> は指定できません。  
  
 \<assembly_bits>  
 アセンブリとその依存アセンブリを構成するバイナリ値のリストを指定します。 リストの最初の値は、ルート レベルのアセンブリとして扱われます。 依存アセンブリに対応する値は、任意の順序で指定できます。 ルート アセンブリの依存関係に対応していない値は無視されます。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 *varbinary_literal*  
 **varbinary** リテラルです。  
  
 *varbinary_expression*  
 **varbinary** 型の式です。  
  
 PERMISSION_SET { **SAFE** | EXTERNAL_ACCESS | UNSAFE }  
> [!IMPORTANT]
>  `PERMISSION_SET` オプションは、開始の警告で説明されるように、`clr strict security` オプションの影響を受けます。 `clr strict security` が有効になっていると、すべてのアセンブリが `UNSAFE` として処理されます。
 
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がアセンブリにアクセスするときに、アセンブリに対して許可されるコード アクセス権のセットを指定します。 指定しない場合、既定値として SAFE が適用されます。  
  
 SAFE を使用することをお勧めします。 SAFE は最も限定的な権限セットです。 SAFE 権限を持つアセンブリによって実行されるコードでは、ファイル、ネットワーク、環境変数、レジストリなどの外部システム リソースにはアクセスできません。  
  
 EXTERNAL_ACCESS を指定した場合、アセンブリでは、ファイル、ネットワーク、環境変数、レジストリなどの特定の外部システム リソースにアクセスできます。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 UNSAFE を指定した場合、アセンブリでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの内外両方のリソースに制限なしでアクセスできます。 UNSAFE アセンブリ内から実行するコードでは、アンマネージ コードを呼び出すことができます。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
> [!IMPORTANT]  
>  アセンブリで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス外のリソースにアクセスせずに計算やデータ管理タスクを実行する場合は、権限設定として SAFE を使用することをお勧めします。  
>   
>  アセンブリで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス外のリソースにアクセスする場合は、EXTERNAL_ACCESS を使用することをお勧めします。 EXTERNAL_ACCESS アセンブリでは SAFE アセンブリの信頼性とスケーラビリティによる保護が提供されますが、セキュリティの観点からは、このアセンブリは UNSAFE アセンブリと類似しています。 EXTERNAL_ACCESS アセンブリ内のコードは、明示的に呼び出し元の権限を借用しない限り、既定により [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントの下で実行され、外部リソースにアクセスします。 したがって、EXTERNAL_ACCESS アセンブリを作成する権限は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントの下でコードを実行しても安全であると考えられる、信頼できるログインに対してのみ許可してください。 権限借用の詳細については、「[CLR 統合のセキュリティ](../../relational-databases/clr-integration/security/clr-integration-security.md)」を参照してください。  
>   
>  UNSAFE を指定した場合、アセンブリのコードでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス領域に対して自由な操作を実行できるので、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の堅牢性が脅かされる可能性があります。 UNSAFE アセンブリでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または共通言語ランタイムのいずれかのセキュリティ システムが妨害されるおそれもあります。 UNSAFE 権限は、信頼性の高いアセンブリに対してのみ許可してください。 UNSAFE アセンブリを作成または変更できるのは、**sysadmin** 固定サーバー ロールのメンバーだけです。  
  
 アセンブリの権限セットの詳細については、「[アセンブリのデザイン](../../relational-databases/clr-integration/assemblies-designing.md)」をご覧ください。  
  
## <a name="remarks"></a>Remarks  
 CREATE ASSEMBLY では、.dll ファイルとしてコンパイル済みのアセンブリがマネージド コードからアップロードされ、SQL Server インスタンス内で使用できるようになります。  
 
有効にすると、`CREATE ASSEMBLY` および `ALTER ASSEMBLY` のステートメントの `PERMISSION_SET` オプションが実行時に無視されますが、`PERMISSION_SET` オプションはメタデータに保持されます。 オプションを無視すると、既存のコード ステートメントの改変が最小限に抑えられます。
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、名前、カルチャ、および公開キーが同じでありバージョンが異なるアセンブリの登録を許可していません。  
  
\<client_assembly_specifier> で指定したアセンブリにアクセスしようとすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では現在の Windows ログインのセキュリティ コンテキストの権限が借用されます。 \<client_assembly_specifier> でネットワーク上の場所 (UNC パス) を指定した場合は、委任制限があり、現在のログインの権限借用範囲はネットワーク上の場所まで拡大されません。 この場合、アクセスは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントのセキュリティ コンテキストを使って行われます。 詳細については、「[資格情報 &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)」を参照してください。
  
 *assembly_name* で指定するルート アセンブリの他に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、アップロードされるルート アセンブリによって参照されているアセンブリのアップロードも試行されます。 参照先のアセンブリが、先に実行された CREATE ASSEMBLY ステートメントにより既にアップロードされている場合、そのアセンブリはアップロードされませんが、ルート アセンブリからは引き続き使用できます。 依存アセンブリがまだアップロードされておらず、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではソース ディレクトリ内にそのアセンブリのマニフェスト ファイルが検出できない場合、CREATE ASSEMBLY ではエラーが返されます。  
  
 ルート アセンブリにより参照される依存アセンブリがデータベースに存在しておらず、ルート アセンブリと一緒に暗黙的に読み込まれる場合、依存アセンブリにはルート レベル アセンブリと同じ権限セットが与えられます。 ルート レベル アセンブリと異なる権限セットを使って依存アセンブリを作成する必要がある場合は、ルート レベル アセンブリより前に、適切な権限セットが与えられた依存アセンブリを明示的にアップロードする必要があります。  
  
## <a name="assembly-validation"></a>アセンブリの検証  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、CREATE ASSEMBLY ステートメントによりアップロードされたアセンブリ バイナリに対して、次の点を確認するためのチェックが実行されます。  
  
-   アセンブリ バイナリが有効なメタデータとコード セグメントに基づく整形式になっており、コード セグメントに有効な MSIL (Microsoft Intermediate language) 命令が含まれていること。  
  
-   参照先の一連のシステム アセンブリが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされている次のいずれかのアセンブリであること。Microsoft.Visualbasic.dll、Mscorlib.dll、System.Data.dll、System.dll、System.Xml.dll、Microsoft.Visualc.dll、Custommarshallers.dll、System.Security.dll、System.Web.Services.dll、System.Data.SqlXml.dll、System.Core.dll、and System.Xml.Linq.dll。 他のシステム アセンブリは参照できますが、データベースに明示的に登録されている必要があります。  
  
-   SAFE または EXTERNAL ACCESS 権限セットを使用して作成されるアセンブリの場合は、次の点がチェックされます。  
  
    -   アセンブリ コードが安全な型であること。 型の安全性は、アセンブリに対して共通言語ランタイム ベリファイアを実行することにより確立されます。  
  
    -   読み取り専用とマークされていない静的データ メンバーが、アセンブリのクラス内に含まれていないこと。  
  
    -   アセンブリのクラスに、ファイナライザー メソッドが含まれていないこと。  
  
    -   アセンブリのクラスまたはメソッドの注釈が、許可されているコード属性に基づいて設定されていること。 詳細については、「[CLR ルーチンのカスタム属性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)」を参照してください。  
  
 これらのチェックは CREATE ASSEMBLY の実行時に行われますが、アセンブリ内のコードの実行時には追加のチェックも行われます。  
  
-   特定のコード アクセス権を必要とする [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] API を呼び出すときに、アセンブリの権限セットにその権限が含まれていない場合、呼び出しは失敗します。  
  
-   SAFE と EXTERNAL_ACCESS アセンブリの場合は、特定の HostProtectionAttributes に基づいて注釈が設定されている [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] API を呼び出そうとすると、呼び出しは失敗します。  
  
 詳細については、「[アセンブリのデザイン](../../relational-databases/clr-integration/assemblies-designing.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 CREATE ASSEMBLY 権限が必要です。  
  
 PERMISSION_SET = EXTERNAL_ACCESS を指定する場合、サーバーに対する **EXTERNAL ACCESS ASSEMBLY** 権限が必要です。 PERMISSION_SET = UNSAFE を指定する場合、サーバーに対する **UNSAFE ASSEMBLY** 権限が必要です。  
  
 アップロードするアセンブリによって参照されているアセンブリがデータベース内に存在する場合、ユーザーは、この参照先となるアセンブリの所有者である必要があります。 ファイル パスを使ってアセンブリをアップロードするには、現在のユーザーは、Windows 認証済みログインであるか、**sysadmin** 固定サーバー ロールのメンバーであることが必要です。 CREATE ASSEMBLY を実行するユーザーの Windows ログインには、共有フォルダーおよびステートメントに読み込まれるファイルに対する読み取り権限が与えられている必要があります。  

### <a name="permissions-with-clr-strict-security"></a>CLR の厳密なセキュリティによるアクセス許可    
`CLR strict security` が有効になっている場合に CLR アセンブリを作成するには、次のアクセス許可が必要です。

- ユーザーには `CREATE ASSEMBLY` アクセス許可が必要です  
- さらに、次の条件のいずれかを満たす必要があります。  
  - サーバーでの `UNSAFE ASSEMBLY` アクセス許可のある対応するログインを含む証明書または非対称キーでアセンブリが署名されている。 アセンブリへの署名は推奨されます。  
  - データベースに `ON` に設定された `TRUSTWORTHY` プロパティが含まれ、そのデータベースがサーバーでの `UNSAFE ASSEMBLY` アクセス許可のあるログインによって所有されている。 このオプションは推奨されません。  
  
 アセンブリの権限セットの詳細については、「[アセンブリのデザイン](../../relational-databases/clr-integration/assemblies-designing.md)」をご覧ください。  
  
## <a name="examples"></a>使用例  
  
### <a name="example-a-creating-an-assembly-from-a-dll"></a>例 A:dll からアセンブリを作成する  
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 次の例では、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サンプルがローカル コンピューターの既定の場所にインストールされており、HelloWorld.csproj サンプル アプリケーションがコンパイルされていることを前提としています。 詳細については、「[Hello World サンプル](https://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7)」を参照してください。  
  
```sql  
CREATE ASSEMBLY HelloWorld   
FROM <system_drive>:\Program Files\Microsoft SQL Server\100\Samples\HelloWorld\CS\HelloWorld\bin\debug\HelloWorld.dll  
WITH PERMISSION_SET = SAFE;  
```  

> [!IMPORTANT]
> Azure SQL Database では、ファイルからのアセンブリの作成はサポートされません。
  
### <a name="example-b-creating-an-assembly-from-assembly-bits"></a>例 B:アセンブリのビットからアセンブリを作成する  
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 アセンブリ ビットを (完全性または有効ではない) サンプル ビットに置き換えます。  
  
```sql  
CREATE ASSEMBLY HelloWorld  
    FROM 0x4D5A900000000000  
WITH PERMISSION_SET = SAFE;  
```  
  
## <a name="see-also"></a>参照  
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [CLR &#40;共通言語ランタイム&#41; 統合の使用シナリオと例](https://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
  
  
