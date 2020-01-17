---
title: ストアド プロシージャを SQL Server の拡張を追加する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], adding
- adding extended stored procedures
- collations [SQL Server], extended stored procedures
ms.assetid: 10f1bb74-3b43-4efd-b7ab-7a85a8600a50
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3a5e5ab2d0dba0d7d39fcf3223f0aeec5ab6a058
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62512350"
---
# <a name="adding-an-extended-stored-procedure-to-sql-server"></a>SQL Server への拡張ストアド プロシージャの追加
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに CLR Integration を使用してください。  
  
 拡張ストアド プロシージャ関数を含んでいる DLL は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の拡張機能としての役割を果たします。 DLL をインストールするには、標準を含んでいるなどのディレクトリにファイルをコピー [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL ファイル (C:\Program files \microsoft SQL Server\MSSQL12.0 *。x*既定 \MSSQL\Binn)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者は、拡張ストアド プロシージャ DLL をサーバーにコピーした後、DLL 内の各拡張ストアド プロシージャを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に登録する必要があります。 この操作を行うには、sp_addextendedproc システム ストアド プロシージャを使用します。  
  
> [!IMPORTANT]  
>  システム管理者は、拡張ストアド プロシージャをサーバーに追加し、他のユーザーに実行権限を許可する前に、拡張ストアド プロシージャに有害なコードや悪意のあるコードが含まれていないことを十分に確認する必要があります。  すべてのユーザー入力を検証します。 また、ユーザー入力は検証するまで連結しないでください。 検証していないユーザー入力から作成されたコマンドは、絶対に実行しないでください。  
  
 sp_addextendedproc の最初のパラメーターには、関数の名前を指定します。2 番目のパラメーターには、その関数が含まれている DLL の名前を指定します。 DLL の完全なパスを指定することをお勧めします。  
  
> [!IMPORTANT]  
>  完全パスを使用して登録されなかった既存の DLL は、SQL Server 2005 以降へのアップグレード後に機能しなくなります。 この問題を修正するには、sp_dropextendedproc を使用して DLL の登録を解除し、sp_addextendedproc を使用して完全パスと共に登録し直します。  
  
 `sp_addextendedproc` に指定する関数の名前は、大文字と小文字の区別を含め、DLL 内の関数名とまったく同じにする必要があります。 たとえば、次のコマンドは `xp_hello,` という名前の dll に含まれている `xp_hello.dll` 関数を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張ストアド プロシージャとして登録します。  
  
```  
sp_addextendedproc 'xp_hello', 'c:\Program Files\Microsoft SQL Server\MSSQL12.0.MSSQLSERVER\MSSQL\Binn\xp_hello.dll';  
```  
  
 `sp_addextendedproc` に指定した関数の名前が、DLL 内の関数名と正確に一致しない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に新しい名前が登録されますが、その名前は役に立ちません。 たとえばが`xp_Hello`として登録されて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]拡張であるストアド プロシージャ`xp_hello.dll`、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用する場合は、DLL で関数を検索することはできません`xp_Hello`を後で、関数を呼び出します。  
  
```  
--Register the function (xp_hello) with an initial upper case  
sp_addextendedproc 'xp_Hello', 'c:\xp_hello.dll';  
  
--Use the newly registered name to call the function  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
--This is the error message  
Server: Msg 17750, Level 16, State 1, Procedure xp_Hello, Line 1  
Could not load the DLL xp_hello.dll, or one of the DLLs it references. Reason: 127(The specified procedure could not be found.).  
```  
  
 `sp_addextendedproc` に指定した関数の名前が DLL 内の関数名とまったく同じであり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの照合順序で大文字と小文字が区別されない場合、ユーザーは大文字と小文字を任意に組み合わせた名前を使用して、拡張ストアド プロシージャを呼び出すことができます。  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will succeed in calling xp_hello  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HelLO @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
```  
  
 名前と照合順序が DLL 内の関数とまったく同じになるように拡張ストアド プロシージャが登録されていても、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの照合順序で大文字と小文字が区別される場合は、呼び出し時に大文字と小文字を誤ると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はこの拡張ストアド プロシージャを呼び出すことができません。  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will result in an error  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
  
--This is the error  
Server: Msg 2812, Level 16, State 62, Line 1  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を停止して再起動する必要はありません。  
  
## <a name="see-also"></a>参照  
 [sp_addextendedproc &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
