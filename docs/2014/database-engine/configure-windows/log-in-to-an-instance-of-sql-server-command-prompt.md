---
title: SQL Server インスタンスへのログイン (コマンド プロンプト) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ec0250a6928dc2dd7b2d1881fbede89eb0aa51f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781779"
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>SQL Server インスタンスへのログイン (コマンド プロンプト)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sqlcmd **ユーティリティを使用して** のインスタンスへの接続をテストする方法について説明します。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-log-in-to-the-default-instance-of-sql-server"></a>SQL Server の既定のインスタンスにログインするには  
  
1.  コマンド プロンプトで次のコマンドを入力し、Windows 認証を使用して接続します。  
  
    ```  
    sqlcmd [ /E ] [ /S servername ]  
  
    ```  
  
#### <a name="to-log-in-to-a-named-instance-of-sql-server"></a>SQL Server の名前付きインスタンスにログインするには  
  
1.  コマンド プロンプトで次のコマンドを入力し、Windows 認証を使用して接続します。  
  
    ```  
    sqlcmd [ /E ] /S servername\instancename  
  
    ```  
  
## <a name="see-also"></a>参照  
 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)   
 [osql ユーティリティ](../../tools/osql-utility.md)  
  
  
