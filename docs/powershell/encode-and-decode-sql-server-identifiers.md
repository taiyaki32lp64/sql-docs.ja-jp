---
title: SQL Server 識別子のエンコードとデコード | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 21e642feba6a2726aa4d5615f6ae508fa33c1694
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934650"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>SQL Server 識別子のエンコードとデコード
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SQL Server の区切られた識別子には、Windows PowerShell パスでサポートされない文字が含まれる場合があります。 これらの文字は、16 進数値にエンコードすることによって指定できます。  

> [!NOTE]
> SQL Server PowerShell モジュールには **SqlServer** と **SQLPS** の 2 つがあります。 **SQLPS** モジュールは (後方互換性のため) SQL Server のインストールに含まれていますが、今後更新されることはありません。 最新の PowerShell モジュールは **SqlServer** モジュールです。 **SqlServer** モジュールには **SQLPS** のコマンドレットの更新バージョンだけでなく、最新の SQL 機能をサポートする新しいコマンドレットも含まれています。  
> SQL Server Management Studio (SSMS) には前のバージョンの **SqlServer** が含まれて*いました*が、SSMS の 16.x バージョンのみです。 PowerShell を SSMS 17.0 以降で使用するには、**SqlServer** モジュールを PowerShell ギャラリーからインストールする必要があります。
> **SqlServer** モジュールをインストールする場合は、「[SQL Server PowerShell のインストール](download-sql-server-ps-module.md)」を参照してください。
  
  
Windows PowerShell パス名でサポートされない文字は、" **%** xx" のように、"%" 文字の後に文字を表すビット パターンの 16 進値を付加して表す、つまりエンコードすることができます。 エンコードは、Windows PowerShell パスでサポートされない文字を処理する場合にいつでも使用できます。  
  
 **Encode-SqlName** コマンドレットは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別子を入力として受け取ります。 また、Windows PowerShell 言語ではサポートされないすべての文字が "%xx" でエンコードされた文字列を出力します。 **Decode-SqlName** コマンドレットは、エンコードされた [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別子を入力として受け取り、元の識別子を返します。  
  
##  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 **Encode-Sqlname** コマンドレットと **Decode-Sqlname** コマンドレットでエンコードまたはデコードできるのは、SQL Server の区切られた識別子ではサポートされるものの PowerShell パスではサポートされない文字のみです。 **Encode-SqlName** によってエンコードされ、**Decode-SqlName** によってデコードされる文字を次に示します。  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**文字**|\ |/|:|%|\<|>|*|?|[|]|&#124;|  
|**16 進エンコード**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="EncodeIdent"></a> 識別子のエンコード  
 **PowerShell パス内で SQL Server 識別子をエンコードするには**  
  
-   SQL Server 識別子をエンコードするには、次の 2 つの方法のいずれかを使用します。  
  
    -   サポートされていない文字の 16 進数コードを、%XX という構文 (XX は 16 進数コード) を使用して指定します。  
  
    -   識別子を引用符で囲まれた文字列として **Encode-Sqlname** コマンドレットに渡します。  
  
### <a name="examples-encoding"></a>例 (エンコード)  
 この例では、":" 文字のエンコードされたバージョン (%3A) を指定します。  
  
```  
Set-Location Table%3ATest  
```  
  
 あるいは、 **Encode-SqlName** を使用して Windows PowerShell でサポートされる名前を作成できます。  
  
```  
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="DecodeIdent"></a> 識別子のデコード  
 **PowerShell パスの SQL Server 識別子をデコードするには**  
  
 16 進数エンコードを、そのエンコードが表す文字に置換するには、 **Decode-Sqlname** コマンドレットを使用します。  
  
### <a name="examples-decoding"></a>例 (デコード)  
 次の例では、"Table:Test" を返します。  
  
```  
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>参照  
 [PowerShell での SQL Server 識別子](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell プロバイダー](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
