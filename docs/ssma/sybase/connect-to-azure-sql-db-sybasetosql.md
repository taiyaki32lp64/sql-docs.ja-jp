---
title: Azure SQL DB (SybaseToSQL) への接続 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 68fbac69959d423477750a69bb6e5b06ab62af2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083471"
---
# <a name="connect-to-azure-sql-db--sybasetosql"></a>Azure SQL DB への接続 (SybaseToSQL)
Azure SQL DB ダイアログ ボックスに、Connect を使用して、移行する Azure SQL DB データベースに接続します。  
  
このダイアログ ボックスにアクセスする、**ファイル**メニューの  **Azure SQL DB への接続**します。 以前接続した場合、コマンドは**Azure SQL DB に再接続します。**  
  
## <a name="options"></a>および  
**[サーバー名]**  
  
選択するか、Azure SQL DB に接続するためのサーバー名を入力します。  
  
**[データベース]**  
  
選択、入力または**参照**データベース名。  
  
> [!IMPORTANT]  
> SSMA for Sybase では、Azure SQL DB で master データベースに接続をできません。  
  
**ユーザー名**  
  
SSMA が Azure SQL DB データベースへの接続に使用するユーザー名を入力します。  
  
**Password**  
  
ユーザー名に対応するパスワードを入力します。  
  
**Encrypt**  
  
SSMA では、Azure SQL DB に暗号化された接続をお勧めします。  
  
## <a name="create-azure-database"></a>Azure のデータベースを作成します。  
Azure SQL DB のアカウントには、データベースがない場合、は、最初のデータベースを作成できます。  
  
非常に最初に新しいデータベースを作成するには、次の手順に従います  
  
1.  Azure SQL DB ダイアログ ボックスに、Connect に表示される参照ボタンをクリックします。  
  
2.  データベースがない場合は、次の 2 つのメニュー項目が表示されます。  
  
    1.  **(データベースが見つかりません)** は無効であるすべての時間が淡色表示になりますが  
  
    2.  **新しいデータベースの作成**Azure SQL DB のアカウントにデータベースがない場合にのみ有効になっています。 このメニュー項目をクリックするとは、Azure データベースの作成 ダイアログ ボックスはデータベース名とサイズで存在します。  
  
3.  データベースの作成時に、次の 2 つのパラメーターは入力として指定します。  
  
    1.  **データベース名:** データベース名を入力します。  
  
    2.  **データベースのサイズ:** Azure SQL DB のアカウントを作成する必要があるデータベースのサイズを選択します。  
  
