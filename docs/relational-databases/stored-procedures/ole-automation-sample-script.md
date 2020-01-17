---
title: OLE オートメーションのサンプル スクリプト | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- OLE Automation [SQL Server], examples
ms.assetid: e59f75a9-ed41-4f12-888e-ffc57f9b3882
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 882c02f863fb27f27d806e6d7c470960d03ff832
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68136719"
---
# <a name="ole-automation-sample-script"></a>OLE オートメーションのサンプル スクリプト
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  このトピックでは、OLE オートメーション ストアド プロシージャを使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のローカル インスタンスに SQL-DMO SQLServer オブジェクトを作成および使用する [!INCLUDE[ssDE](../../includes/ssde-md.md)]ステートメント バッチの例について説明します。 このコードの一部は、OLE オートメーション システム ストアド プロシージャのリファレンス トピックで例として使用されています。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @Object int;  
DECLARE @HR int;  
DECLARE @Property nvarchar(255);  
DECLARE @Return nvarchar(255);  
DECLARE @Source nvarchar(255), @Desc nvarchar(255);  
  
-- Create a SQLServer object.  
SET NOCOUNT ON;  
  
-- First, create the object.  
EXEC @HR = sp_OACreate N'SQLDMO.SQLServer',  
    @Object OUT;  
IF @HR <> 0  
BEGIN  
    -- Report the error.  
    EXEC sp_OAGetErrorInfo @Object,  
        @Source OUT,  
        @Desc OUT;  
    SELECT HR = convert(varbinary(4),@HR),  
        Source=@Source,  
        Description=@Desc;  
    GOTO END_ROUTINE  
END  
ELSE  
-- A DMO.SQLServer object has been successfully created.  
BEGIN  
    -- Specify Windows Authentication for connections.  
    EXEC @HR = sp_OASetProperty @Object,  
        N'LoginSecure',  
        N'TRUE';  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Set a property.  
    EXEC @HR = sp_OASetProperty @Object,  
        N'HostName',  
        N'SampleScript';  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Get a property using an output parameter.  
    EXEC @HR = sp_OAGetProperty @Object, N'HostName', @Property OUT;  
    IF @HR <> 0   
        GOTO CLEANUP  
    ELSE  
        PRINT @Property;  
  
    -- Get a property using a result set.  
    EXEC @HR = sp_OAGetProperty @Object,  
        N'HostName';  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Get a property by calling the method.  
    EXEC @HR = sp_OAMethod @Object,  
        N'HostName',  
        @Property OUT;  
    IF @HR <> 0   
        GOTO CLEANUP  
    ELSE  
        PRINT @Property;  
  
    -- Call the connect method.  
    -- SECURITY NOTE - When possible, use Windows Authentication.  
    EXEC @HR = sp_OAMethod @Object,  
        N'Connect',  
        NULL,  
        N'localhost',  
        NULL,  
        NULL;  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Call a method that returns a value.  
    EXEC @HR = sp_OAMethod @Object,  
        N'VerifyConnection',  
        @Return OUT;  
    IF @HR <> 0  
        GOTO CLEANUP  
    ELSE  
        PRINT @Return;  
END  
  
CLEANUP:  
-- Check whether an error occurred.  
IF @HR <> 0  
BEGIN  
    -- Report the error.  
    EXEC sp_OAGetErrorInfo @Object,  
        @Source OUT,  
        @Desc OUT;  
    SELECT HR = convert(varbinary(4),@HR),  
        Source=@Source,  
        Description=@Desc;  
END  
  
-- Destroy the object.  
BEGIN  
    EXEC @HR = sp_OADestroy @Object;  
    -- Check if an error occurred.  
    IF @HR <> 0   
    BEGIN  
        -- Report the error.  
        EXEC sp_OAGetErrorInfo @Object,  
        @Source OUT,  
        @Desc OUT;  
        SELECT HR = convert(varbinary(4),@HR),  
        Source=@Source,  
        Description=@Desc;  
    END  
END  
  
END_ROUTINE:  
RETURN;  
GO  
```  
  
## <a name="related-content"></a>関連コンテンツ  
 [Transact-SQL での OLE オートメーション オブジェクト](../../relational-databases/stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
 [sp_OACreate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)  
  
 [sp_OAGetProperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oagetproperty-transact-sql.md)  
  
 [sp_OASetProperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oasetproperty-transact-sql.md)  
  
 [sp_OAMethod &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oamethod-transact-sql.md)  
  
 [sp_OADestroy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oadestroy-transact-sql.md)  
  
  
