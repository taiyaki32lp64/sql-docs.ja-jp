---
title: SQL Server 識別子のエスケープ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c196b316424c941cba52eb50c61c82ca772ba18c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951704"
---
# <a name="escape-sql-server-identifiers"></a>SQL Server 識別子のエスケープ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の区切られた識別子には使用でき、Windows PowerShell パス名には使用できない文字をエスケープするためによく使用されるのが、バック ティック エスケープ文字 (`) です。 ただし、エスケープできない文字もあります。 たとえば、Windows PowerShell ではコロン文字 (:) をエスケープできません。 この文字を含んだ識別子は、エンコードする必要があります。 エンコードは、すべての文字に有効であるため、エスケープよりも確実です。  

> [!NOTE]
> SQL Server PowerShell モジュールには **SqlServer** と **SQLPS** の 2 つがあります。 **SQLPS** モジュールは (後方互換性のため) SQL Server のインストールに含まれていますが、今後更新されることはありません。 最新の PowerShell モジュールは **SqlServer** モジュールです。 **SqlServer** モジュールには **SQLPS** のコマンドレットの更新バージョンだけでなく、最新の SQL 機能をサポートする新しいコマンドレットも含まれています。
> SQL Server Management Studio (SSMS) には前のバージョンの **SqlServer** が含まれて*いました*が、SSMS の 16.x バージョンのみです。 PowerShell を SSMS 17.0 以降で使用するには、**SqlServer** モジュールを PowerShell ギャラリーからインストールする必要があります。
> **SqlServer** モジュールをインストールする場合は、「[SQL Server PowerShell のインストール](download-sql-server-ps-module.md)」を参照してください。

通常、バック ティック文字 (`) のキーは、キーボード左上の Esc キーの下にあります (英語キーボードの場合)。  
  
## <a name="examples"></a>使用例  
 次に示すのは、# 文字をエスケープする例です。  
  
```  
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```  
  
 次に示すのは、コンピューター名として (local) を指定する際に、かっこをエスケープする例です。  
  
```  
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```  
  
## <a name="see-also"></a>参照  
 [PowerShell での SQL Server 識別子](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell プロバイダー](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
