---
title: OLE オートメーションのリターン コードとエラー情報 | Microsoft Docs
ms.custom: ''
ms.date: 07/05/2017
ms.prod: sql
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 12bfbfa82768efe361f9b067764c7b5a4c408931
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68136762"
---
# <a name="ole-automation-return-codes-and-error-information"></a>OLE オートメーションのリターン コードとエラー情報
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  OLE オートメーション システム ストアド プロシージャでは、 **int** のリターン コードが返されます。これは、基になる OLE オートメーション操作から返される HRESULT です。 HRESULT 0 は成功を示しています。 0 以外の HRESULT は、0x800*nnnnn*という 16 進数形式の OLE エラー コードですが、ストアド プロシージャのリターン コードで **int** 値として返された場合、HRESULT の形式は 214*nnnnnnn*になります。  
  
 たとえば、sp_OACreate に SQLDMO.Xyzzy などの無効なオブジェクト名を渡すと、このプロシージャでは HRESULT が **int** 値 2147221005 として返されます。これは、16 進数形式では 0x800401f3 です。  
  
 `CONVERT(binary(4), @hresult)` を使用すると、 **int** 値の HRESULT を **binary** 値に変換できます。 ただし、 `CONVERT(char(10), CONVERT(binary(4), @hresult))` を使用すると HRESULT の各バイトが 1 文字の ASCII 文字に変換されるので、読みにくい文字列になります。 次のサンプル ストアド プロシージャ HexToChar を使用すると、 **int** 値の HRESULT を、文字として読み取れる 16 進数文字列を保持する **char** 値に変換できます。  
  
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
  
 次のサンプル ストアド プロシージャ **sp_displayoaerrorinfo** を使用すると、いずれかの OLE オートメーション プロシージャから 0 以外の HRESULT リターン コードが返された場合に OLE オートメーション エラー情報を表示できます。 このサンプル ストアド プロシージャでは **HexToChar**を使用しています。  
  
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
    EXEC sp_HexToChar @HResult, @HRHex OUT;  
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
 [sp_OAGetErrorInfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql.md)  
  
  
