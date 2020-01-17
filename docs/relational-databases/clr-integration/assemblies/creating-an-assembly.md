---
title: アセンブリを作成する |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 9493567f33cf07dbfa9ae4f19d037a7db6157eda
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907395"
---
# <a name="creating-an-assembly"></a>アセンブリの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ストアド プロシージャやトリガーなどのマネージド データベース オブジェクトは、コンパイルされた後、アセンブリと呼ばれる単位で配置されます。 マネージ DLL アセンブリは、アセンブリによって提供される機能を使用する前に [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に登録する必要があります。 アセンブリを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに登録するには、CREATE ASSEMBLY ステートメントを使用します。 ここでは、CREATE ASSEMBLY ステートメントを使用してアセンブリをデータベースに登録する方法と、アセンブリのセキュリティ設定を指定する方法について説明します。  
  
## <a name="the-create-assembly-statement"></a>CREATE ASSEMBLY ステートメント  
 データベースにアセンブリを作成するには、CREATE ASSEMBLY ステートメントを使用します。 以下に例を示します。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 FROM 句では、作成するアセンブリのパス名を指定します。 このパスには、UNC (汎用名前付け規則) パスか、コンピューターにローカルの物理ファイル パスを指定できます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、名前、カルチャ、および公開キーが同じでありバージョンが異なるアセンブリの登録を許可していません。  
  
 他のアセンブリを参照するアセンブリを作成することもできます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にアセンブリを作成するときに、ルートレベルのアセンブリによって参照されるアセンブリがデータベースにまだ作成されていない場合は、そのアセンブリが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって作成されます。  
  
 データベース ユーザーまたはユーザー ロールには、データベースにアセンブリを作成して所有する権限が与えられます。 アセンブリを作成するには、データベース ユーザーまたはロールに CREATE ASSEMBLY 権限が許可されている必要があります。  
  
 アセンブリから他のアセンブリを参照できる条件を次に示します。  
  
-   呼び出し先または参照先のアセンブリが同じユーザーまたはロールによって所有されている。  
  
-   呼び出し先または参照先のアセンブリが同じデータベースに作成されている。  
  
## <a name="specifying-security-when-creating-assemblies"></a>アセンブリ作成時のセキュリティの指定  
 アセンブリを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに作成する場合は、コードを実行できる3種類のセキュリティレベル ( **SAFE**、 **EXTERNAL_ACCESS**、 **UNSAFE**) のいずれかを指定できます。 **CREATE ASSEMBLY**ステートメントを実行すると、コードアセンブリに対して特定のチェックが実行され、アセンブリがサーバーに登録できなくなる可能性があります。 詳細については、 [CodePlex](https://msftengprodsamples.codeplex.com/)の Impersonation サンプルを参照してください。  
  
 **SAFE**は既定のアクセス許可セットであり、ほとんどのシナリオで機能します。 特定のセキュリティ レベルを指定するには、CREATE ASSEMBLY ステートメントの構文を次のように変更します。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 上記のコードの3行目を省略するだけで、**安全**なアクセス許可セットを持つアセンブリを作成することもできます。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 アセンブリ内のコードが**安全**なアクセス許可セットで実行されている場合は、インプロセスマネージプロバイダーを使用して、サーバー内での計算とデータアクセスのみを実行できます。  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>EXTERNAL_ACCESS および UNSAFE アセンブリの作成  
 **EXTERNAL_ACCESS**は、ファイル、ネットワーク、レジストリ、環境変数など、コードがサーバー外部のリソースにアクセスする必要があるシナリオに対処します。 サーバーから外部リソースにアクセスする場合、常にマネージド コードの呼び出し元のユーザーのセキュリティ コンテキストが借用されます。  
  
 **UNSAFE** code アクセス許可は、アセンブリが安全であることが保証されていない場合、または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 API などの制限されたリソースへの追加アクセスが必要な場合に適しています。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]で**EXTERNAL_ACCESS**または**安全でない**アセンブリを作成するには、次の2つの条件のいずれかが満たされている必要があります。  
  
1.  アセンブリが、厳密な名前で署名されているか、または証明書を使用して Authenticode で署名されている。 この厳密な名前 (または証明書) は、非対称キー (または証明書) として [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内に作成されます。また、対応するログイン **(外部アクセス**アセンブリの場合) または**unsafe アセンブリ**のアクセス許可 (unsafe アセンブリの場合) が含まれています。  
  
2.  データベース所有者 (DBO) に**外部アクセスアセンブリ**(**外部アクセス**アセンブリの場合) または**安全でないアセンブリ**( **unsafe**アセンブリの場合) アクセス許可があり、データベースの信頼可能な[データベースプロパティ](../../../relational-databases/security/trustworthy-database-property.md)が**ON**に設定されている。  

 上に示した 2 つの条件は、アセンブリの読み込み時 (実行も含む) にもチェックされます。 アセンブリを読み込むには、これらの条件の少なくとも 1 つが満たされている必要があります。  
  
 サーバープロセスで共通言語ランタイム (CLR) コードを実行する場合にのみ、データベースの[信頼可能データベースプロパティ](../../../relational-databases/security/trustworthy-database-property.md)を**on**に設定しないことをお勧めします。 代わりに、master データベースのアセンブリ ファイルから非対称キーを作成してください。 その後、この非対称キーにマップされたログインを作成する必要があります。また、このログインには、 **EXTERNAL ACCESS assembly**権限または**UNSAFE assembly**権限が許可されている必要があります。  
  
 次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントでは、非対称キーを作成し、ログインをこのキーにマップした後、ログインに**EXTERNAL_ACCESS**権限を付与するために必要な手順を実行します。 次に示す [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントは、CREATE ASSEMBLY ステートメントを実行する前に実行する必要があります。  
  
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
  
 **外部アクセス**アセンブリを作成するには、作成者が**外部アクセス**許可を持っている必要があります。 この権限は、アセンブリの作成時に次のように指定します。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントでは、非対称キーを作成し、ログインをこのキーにマップしてから、 **UNSAFE**権限をログインに付与するために必要な手順を実行します。 次に示す [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントは、CREATE ASSEMBLY ステートメントを実行する前に実行する必要があります。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 アセンブリが**unsafe**権限で読み込まれるように指定するには、アセンブリをサーバーに読み込むときに、 **unsafe**権限セットを指定します。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 各設定のアクセス許可の詳細については、「 [CLR 統合のセキュリティ](../../../relational-databases/clr-integration/security/clr-integration-security.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CLR 統合アセンブリの管理](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [アセンブリ](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  の変更  
 [アセンブリ](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  の削除  
 [CLR 統合のコードアクセスセキュリティ](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [TRUSTWORTHY データベース プロパティ](../../../relational-databases/security/trustworthy-database-property.md)   
 [部分的に信頼される呼び出し元の許容](https://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
  
  
