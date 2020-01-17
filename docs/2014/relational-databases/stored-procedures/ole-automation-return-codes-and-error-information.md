---
title: OLE オートメーションのリターン コードとエラー情報 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- return codes [SQL Server]
- OLE Automation [SQL Server], return codes
- OLE Automation [SQL Server], errors
ms.assetid: 9696fb05-e9e8-4836-b359-d4de0be0eeb2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34744bedb701155d2695f6efc5aab3c493e6cf48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011269"
---
# <a name="ole-automation-return-codes-and-error-information"></a>OLE オートメーションのリターン コードとエラー情報
  OLE オートメーション システム ストアド プロシージャでは、`int` のリターン コードが返されます。これは、基になる OLE オートメーション操作から返される HRESULT です。 HRESULT 0 は成功を示しています。 0 以外の HRESULT は、0x800 という 16 進数形式の OLE エラー コード*nnnnn*、として返された場合は、 `int` HRESULT ストアド プロシージャのリターン コードの値が、形式は 214*nnnnnnn*します。  
  
 たとえば、無効なオブジェクト名を渡す (SQLDMO です。Xyzzy) sp_OACreate ににより、プロシージャから返される、 `int` 16 進数では 0x800401f3 ですと HRESULT。  
  
 `CONVERT(binary(4), @hresult)` を使用すると、`int` 値の HRESULT を `binary` 値に変換できます。 ただし、 `CONVERT(char(10), CONVERT(binary(4), @hresult))` を使用すると HRESULT の各バイトが 1 文字の ASCII 文字に変換されるので、読みにくい文字列になります。 次のサンプル HexToChar ストアド プロシージャを使用して変換することができます、 `int` HRESULT を`char`を読み取れる 16 進数文字列を含む値です。  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT name FROM sys.objects  
          WHERE name = N'dbo.sp_HexToChar')  
    DROP PROCEDURE HexToChar;  
GO  
CREATE PROCEDURE dbo.sp_HexToChar  
    @BinValue varbinary(255),  
    @HexCharValue nvarchar(255) OUTPUT  
AS  
    DECLARE @CharValue nvarchar(255);  
    DECLARE @Position int;  
    DECLARE @Length int;  
    DECLARE @HexString nchar(16);  
    SELECT @CharValue = N'0x';  
    SELECT @Position = 1;  
    SELECT @Length = DATALENGTH(@BinValue);  
    SELECT @HexString = N'0123456789ABCDEF';  
    WHILE (@Position <= @Length)  
    BEGIN  
        DECLARE @TempInt int;  
        DECLARE @FirstInt int;  
        DECLARE @SecondInt int;  
        SELECT @TempInt = CONVERT(int, SUBSTRING(@BinValue,@Position,1));  
        SELECT @FirstInt = FLOOR(@TempInt/16);  
        SELECT @SecondInt = @TempInt - (@FirstInt*16);  
        SELECT @CharValue = @CharValue +  
            SUBSTRING(@HexString, @FirstInt+1, 1) +  
            SUBSTRING(@HexString, @SecondInt+1, 1);  
        SELECT @Position = @Position + 1;  
    END  
    SELECT @HexCharValue = @CharValue;  
GO  
DECLARE @BinVariable varbinary(35);  
DECLARE @CharValue nvarchar(35);  
  
SET @BinVariable = 123456;  
  
EXECUTE dbo.sp_HexToChar  
    @binvalue = @BinVariable,  
    @HexCharValue = @CharValue OUTPUT;  
  
SELECT @BinVariable AS BinaryValue,  
    @CharValue AS CharacterRep;  
GO  
```  
  
 次のサンプル ストアド プロシージャ **sp_displayoaerrorinfo** を使用すると、いずれかの OLE オートメーション プロシージャから 0 以外の HRESULT リターン コードが返された場合に OLE オートメーション エラー情報を表示できます。 このサンプル ストアド プロシージャは`HexToChar`します。  
  
```  
CREATE PROCEDURE dbo.sp_DisplayOAErrorInfo  
    @Object int,  
    @HResult int  
AS  
    DECLARE @Output nvarchar(255);  
    DECLARE @HRHex nchar(10);  
    DECLARE @HR int;  
    DECLARE @Source nvarchar(255);  
    DECLARE @Description nvarchar(255);  
    PRINT N'OLE Automation Error Information';  
    EXEC HexToChar @HResult, @HRHex OUT;  
    SELECT @Output = N'  HRESULT: ' + @HRHex;  
    PRINT @Output;  
    EXEC @HR = sp_OAGetErrorInfo  
        @Object,  
        @Source OUT,  
        @Description OUT;  
    IF @HR = 0  
    BEGIN  
        SELECT @Output = N'  Source: ' + @Source;  
        PRINT @Output;  
        SELECT @Output = N'  Description: '  
               + @Description;  
        PRINT @Output;  
    END  
    ELSE  
    BEGIN  
       PRINT N' sp_OAGetErrorInfo failed.';  
       RETURN;  
    END  
GO  
```  
  
## <a name="related-content"></a>関連コンテンツ  
 [sp_OAGetErrorInfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql)  
  
  
