---
title: SQL Server (OracleToSQL) への接続 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ef384ea-5f3e-4f70-ad7c-b62d7b0da628
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e6e06585ca99305d6825898a98a7dbab31b5b39b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266173"
---
# <a name="connect-to-sql-server--oracletosql"></a>SQL Server への接続 (OracleToSQL)
使用して、 **SQL サーバーへの接続** ダイアログ ボックスのインスタンスに接続する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に移行したいです。 アクセスする、 **SQL サーバーへの接続** ダイアログ ボックスで、**ファイル** メニューのをクリックして**SQL サーバーへの接続**します。  
  
## <a name="options"></a>および  
**サーバー名**  
入力するかに接続する SQL Server のインスタンスを選択します。 既定では、最後に接続されているインスタンスが表示されます。  
  
-   ローカル コンピューターの既定のインスタンスに接続する場合、いずれかを入力する**localhost**またはドット ( **.** )。  
  
-   別のコンピューターで既定のインスタンスに接続する場合は、コンピューターの名前を入力します。  
  
-   別のコンピューター上の名前付きインスタンスに接続する場合などを入力、コンピューター名、円記号、およびインスタンス名を*MyServer*\\*MyInstance*します。  
  
**[サーバー ポート]**  
場合、インスタンスの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が既定の接続ポート (1433)、ポート番号を入力を受け入れるように構成されていません。 それ以外の場合、この値を空白のままにします。  
  
**[データベース]**  
オブジェクトとデータを移行するデータベースを指定します。 このオプションに再接続する場合は使用できません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
**\[認証]**  
接続に使用される認証方法を選択[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 現在の Windows アカウントを使用するには、Windows 認証を選択します。 指定する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインとパスワードで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。  
  
**ユーザー名**  
使用する場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証では、そのインスタンスのログイン名を入力[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 Windows 認証を使用している場合はこのオプションは利用できません。  
  
**Password**  
使用する場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証では、そのインスタンスのログインのパスワードを入力[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 Windows 認証を使用している場合はこのオプションは利用できません。  
  
**[暗号化接続]**  
SQL Server に安全に接続する場合は、調べることにより、暗号化接続の使用、**接続を暗号化**チェック ボックスをオンします。  
  
**[Trust Server Certificate]**  
このオプションを使用する場合は、選択、 **Trust Server Certificate**チェック ボックスをオンします。  
  
> [!NOTE]  
> 有効にする**Trust Server Certificate**に設定する必要があります「暗号化」 **True**します。  
  
