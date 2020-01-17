---
title: アセンブリの変更 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], modifying
- permissions [CLR integration]
- altering assemblies
- ALTER ASSEMBLY statement
ms.assetid: 9e765fbd-f339-473c-8537-22f478e79696
author: rothja
ms.author: jroth
ms.openlocfilehash: 80ef9d283f90c50406477a7a651fb418694ae445
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027952"
---
# <a name="altering-an-assembly"></a>アセンブリの変更
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に登録されているアセンブリは、ALTER ASSEMBLY ステートメントを使用することで、比較的最近のバージョンから更新できます。 アセンブリを更新するには、ALTER ASSEMBLY ステートメントを次の構文で使用します。  
  
```  
ALTER ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
```  
  
 ALTER ASSEMBLY を使用しても、そのアセンブリを使用している現在実行中のプロセスは中断されません。プロセスの実行は、変更されていないアセンブリを使用して継続されます。 ALTER ASSEMBLY を使用して、共通言語ランタイム (CLR) 関数、集計関数、ストアド プロシージャ、およびトリガーの署名を変更することはできません。 アセンブリに新しいパブリック メソッドを追加したり、プライベート メソッドを任意の方法で変更したりできます。パブリック メソッドは、署名または属性を変更しない限り変更できます。 データ メンバーや基本クラスなどの、ネイティブ シリアル化されたユーザー定義型に含まれているフィールドは、ALTER ASSEMBLY を使用して変更することはできません。 その他すべての変更はサポートされていません。 詳細については、次を参照してください。 [ALTER ASSEMBLY &#40;TRANSACT-SQL&#41;](../../../t-sql/statements/alter-assembly-transact-sql.md)します。  
  
## <a name="changing-the-permission-set-of-an-assembly"></a>アセンブリの権限セットの変更  
 アセンブリの権限セットも、ALTER ASSEMBLY ステートメントを使用して変更できます。 次のステートメントを SQLCLRTest アセンブリの権限のセットを変更する**EXTERNAL_ACCESS**します。  
  
```  
ALTER ASSEMBLY SQLCLRTest  
WITH PERMISSION_SET = EXTERNAL_ACCESS   
```  
  
 アセンブリの権限のセットから変更される場合**セーフ**に**EXTERNAL_ACCESS**または**UNSAFE**、非対称キーと対応するログインを**EXTERNAL ACCESS ASSEMBLY**権限または**UNSAFE ASSEMBLY**アセンブリのアクセス許可を最初に作成する必要があります。 詳細については、「 [アセンブリの作成](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)」を参照してください。  
  
## <a name="adding-the-source-code-of-an-assembly"></a>アセンブリのソース コードの追加  
 ALTER ASSEMBLY 構文の ADD FILE 句は、CREATE ASSEMBLY 構文には存在しません。 ADD FILE 句を使用すると、アセンブリに関連付けられるソース コードやその他のファイルを追加できます。 ファイルは元の場所からコピーされ、データベース内のシステム テーブルに格納されます。 これにより、現在のバージョンの UDT を再作成またはドキュメント化する必要があれば、ソース コードや他のファイルをいつでも使用できます。  
  
 次に示すステートメントでは、Point UDT の Point.cs クラスのソース コードを追加しています。 Point.cs ファイルに含まれているテキストがコピーされ、"PointSource" という名前でデータベースに格納されます。  
  
 `ALTER ASSEMBLY Point`  
  
 `ADD FILE FROM 'C:\Projects\Point\Point.cs' AS PointSource`  
  
## <a name="see-also"></a>参照  
 [CLR 統合アセンブリの管理](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [アセンブリを作成します。](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [アセンブリの削除](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
