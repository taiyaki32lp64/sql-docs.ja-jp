---
title: アセンブリを作成する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- creating assemblies
- UNSAFE assemblies
- CREATE ASSEMBLY statement
- SAFE assemblies
- EXTERNAL_ACCESS assemblies
- assemblies [CLR integration], creating
ms.assetid: a2bc503d-b6b2-4963-8beb-c11c323f18e0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1883e88b03b205a2fb272a7cb890c79c607b29fc
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75232303"
---
# <a name="creating-an-assembly"></a>アセンブリの作成
  ストアド プロシージャやトリガーなどのマネージド データベース オブジェクトは、コンパイルされた後、アセンブリと呼ばれる単位で配置されます。 マネージ DLL アセンブリは、アセンブリに[!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]よって提供される機能を使用する前に、に登録する必要があります。 アセンブリを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに登録するには、CREATE ASSEMBLY ステートメントを使用します。 ここでは、CREATE ASSEMBLY ステートメントを使用してアセンブリをデータベースに登録する方法と、アセンブリのセキュリティ設定を指定する方法について説明します。  
  
## <a name="the-create-assembly-statement"></a>CREATE ASSEMBLY ステートメント  
 データベースにアセンブリを作成するには、CREATE ASSEMBLY ステートメントを使用します。 たとえば次のようになります。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 FROM 句では、作成するアセンブリのパス名を指定します。 このパスには、UNC (汎用名前付け規則) パスか、コンピューターにローカルの物理ファイル パスを指定できます。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、名前、カルチャ、および公開キーが同じでありバージョンが異なるアセンブリの登録を許可していません。  
  
 他のアセンブリを参照するアセンブリを作成することもできます。 で[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]アセンブリが作成されると、参照先のアセンブリがデータベースにまだ作成されていない場合は、ルートレベルのアセンブリによって参照されるアセンブリも作成されます。  
  
 データベース ユーザーまたはユーザー ロールには、データベースにアセンブリを作成して所有する権限が与えられます。 アセンブリを作成するには、データベース ユーザーまたはロールに CREATE ASSEMBLY 権限が許可されている必要があります。  
  
 アセンブリから他のアセンブリを参照できる条件を次に示します。  
  
-   呼び出し先または参照先のアセンブリが同じユーザーまたはロールによって所有されている。  
  
-   呼び出し先または参照先のアセンブリが同じデータベースに作成されている。  
  
## <a name="specifying-security-when-creating-assemblies"></a>アセンブリ作成時のセキュリティの指定  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースにアセンブリを作成する際には、コードの実行時に適用する異なる 3 つのセキュリティ レベル (`SAFE`、`EXTERNAL_ACCESS`、`UNSAFE`) のうちの 1 つを指定できます。 
  `CREATE ASSEMBLY` ステートメントを実行する際には、アセンブリによる登録を失敗させる可能性があるコード アセンブリに対し、特定のチェックがサーバー上で実行されます。 詳細については、 [CodePlex](https://msftengprodsamples.codeplex.com/)の Impersonation サンプルを参照してください。  
  
 
  `SAFE` は、ほとんどのシナリオに使用できる既定の権限セットです。 特定のセキュリティ レベルを指定するには、CREATE ASSEMBLY ステートメントの構文を次のように変更します。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 上記のコードの 3 行目を省略しても、`SAFE` 権限セットを持つアセンブリを作成できます。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 
  `SAFE` 権限セットで実行されるアセンブリ内のコードでは、インプロセス マネージド プロバイダーを経由して、計算とサーバーのデータへのアクセスのみを実行できます。  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>EXTERNAL_ACCESS および UNSAFE アセンブリの作成  
 
  `EXTERNAL_ACCESS` は、ファイル、ネットワーク、レジストリ、環境変数など、サーバー外部のリソースにコードからアクセスする必要がある場合に使用します。 サーバーから外部リソースにアクセスする場合、常にマネージド コードの呼び出し元のユーザーのセキュリティ コンテキストが借用されます。  
  
 
  `UNSAFE` コード権限は、アセンブリが安全であると検証できない場合や、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 API などの制限付きのリソースへの追加アクセスが必要な場合に使用します。  
  
 
  `EXTERNAL_ACCESS` で `UNSAFE` または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アセンブリを作成するには、次の 2 つの条件のいずれかが満たされている必要があります。  
  
1.  アセンブリが、厳密な名前で署名されているか、または証明書を使用して Authenticode で署名されている。 この厳密な名前 (または証明書) は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部で非対称キー (または証明書) として作成され、それに対応する、`EXTERNAL ACCESS ASSEMBLY` 権限 (外部アクセス アセンブリの場合) または `UNSAFE ASSEMBLY` 権限 (安全でないアセンブリの場合) を持つログインが存在します。  
  
2.  データベース所有者 (DBO) に`EXTERNAL ACCESS ASSEMBLY` (アセンブリ`EXTERNAL ACCESS`の場合) `UNSAFE ASSEMBLY`または`UNSAFE` (アセンブリの場合) アクセス許可があり、データベースの "[信頼できるデータベース" プロパティ](../../security/trustworthy-database-property.md)がに`ON`設定されている。  
  
 上に示した 2 つの条件は、アセンブリの読み込み時 (実行も含む) にもチェックされます。 アセンブリを読み込むには、これらの条件の少なくとも 1 つが満たされている必要があります。  
  
 データベースの["信頼できるデータベース" プロパティ](../../security/trustworthy-database-property.md)は、サーバープロセスで共通`ON`言語ランタイム (CLR) コードを実行するためだけに設定されないようにすることをお勧めします。 代わりに、master データベースのアセンブリ ファイルから非対称キーを作成してください。 その場合、この非対称キーにマップされるログインを作成する必要があります。また、このログインには、`EXTERNAL ACCESS ASSEMBLY` または `UNSAFE ASSEMBLY` 権限を与える必要があります。  
  
 CREATE ASSEMBLY [!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメントを実行する前の次のステートメント。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll'     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey     
GRANT EXTERNAL ACCESS ASSEMBLY TO SQLCLRTestLogin;   
GO   
```  
  
> [!NOTE]  
>  非対称キーに関連付ける新しいログインを作成する必要があります。 このログインは、権限を許可するためにのみ使用します。このログインをユーザーに関連付けたり、アプリケーション内で使用したりする必要はありません。  
  
 
  `EXTERNAL ACCESS` アセンブリを作成するには、作成者に `EXTERNAL ACCESS` 権限が許可されている必要があります。 この権限は、アセンブリの作成時に次のように指定します。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 CREATE ASSEMBLY [!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメントを実行する前の次のステートメント。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 アセンブリを `UNSAFE` 権限で読み込むには、そのアセンブリをサーバーに読み込むときに、次のように `UNSAFE` 権限セットを指定します。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 各設定のアクセス許可の詳細については、「 [CLR 統合のセキュリティ](../security/clr-integration-security.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CLR 統合アセンブリの管理](managing-clr-integration-assemblies.md)   
 [アセンブリを変更する](altering-an-assembly.md)   
 [アセンブリの削除](dropping-an-assembly.md)   
 [CLR 統合のコードアクセスセキュリティ](../security/clr-integration-code-access-security.md)   
 [信頼可能データベースのプロパティ](../../security/trustworthy-database-property.md)   
 [部分的に信頼される呼び出し元の許容](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
  
