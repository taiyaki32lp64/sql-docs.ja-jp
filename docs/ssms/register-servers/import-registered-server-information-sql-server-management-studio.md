---
title: 登録済みサーバー情報のインポート (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.importregisteredservers.f1
helpviewer_keywords:
- transferring registered server information
- Registered Servers [SQL Server], importing
- importing registered server information
ms.assetid: cc497a14-1360-4887-b70c-002f042823b6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9ccbcc8465f713d23922fc10dfe483bb3cfbb774
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267111"
---
# <a name="import-registered-server-information-sql-server-management-studio"></a>登録済みサーバー情報のインポート (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]で保存されている登録済みサーバー情報をインポートする方法について説明します。 登録済みサーバー ファイルをエクスポートした後にインポートすることで、[登録済みサーバー] の同じサーバーを使用して、複数のコンピューターを簡単に構成できます。 この方法は、複数の場所に配置されているコンピューターから多数のサーバーを管理する場合や、経験の浅いユーザーのために基本的な接続設定を構成する場合に便利です。  
  
> [!NOTE]  
>  登録済みサーバーの情報を、以前のバージョンの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にインポートすることはできません。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-import-registered-server-information"></a>登録済みサーバーの情報をインポートするには  
  
1.  [登録済みサーバー] で、[登録済みサーバー] ツール バーのサーバーの種類をクリックします。 クリックするサーバーの種類は、登録済みサーバーのエクスポート ファイルの種類と同じである必要があります。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の登録済みサーバーの情報をエクスポートした場合、[登録済みサーバー] ツール バーで **[データベース エンジン]** をクリックする必要があります。  
  
2.  サーバー グループを右クリックし、 **[インポート]** をクリックします。  
  
3.  **[登録済みサーバーのインポート]** ダイアログ ボックスで、インポートする登録済みサーバーのファイルをクリックし、 **[OK]** をクリックします。  
  
     **[インポート ファイル]**  
     インポート ファイルの名前をテキスト ボックスに入力します。または、参照ボタン ( **[...]** ) をクリックし、クライアント コンピューター上のインポート ファイルを指定します。 既存のファイルを選択した場合は、登録済みサーバー情報がファイルに追加されます。 あらかじめエクスポートされた登録済みサーバー ファイルだけを、インポート ファイルとして使用できます。 登録済みサーバー ファイルは、拡張子 .regsrvr を持ちます。  
  
     **[インポート先のサーバー グループを選択]**  
     ファイル内の登録済みサーバーのエントリのインポート先のルート ノード、または特定のサーバー グループを選択します。 エクスポート ファイルには、すべての登録済みサーバー、特定のサーバー グループ内の登録済みサーバー、または単独の登録済みサーバーをインポートできます。 インポート機能は再帰的です。たとえば、サーバー グループ A にサーバー グループ B が含まれており、サーバー グループ B にサーバー グループ C および D が含まれている場合、サーバー グループ A をインポートすると、A、B、C、および D 内のすべてのエントリがエクスポートされます。  
  
     サーバー グループには、現在の登録済みサーバー ツリーのサーバー グループだけが表示されます。  
  
     既存のサーバー グループまたはサーバーをインポートする場合、既存のサーバーまたはサーバー グループを上書きするかどうかを確認するメッセージが表示されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用するサーバー登録は、パスワードをユーザーごとに格納します。 ユーザーは、サーバー登録をインポートした後、それぞれのサーバーに初めて接続するときにパスワードを入力して、登録済みサーバーの一覧にパスワードを保存する必要があります。 Windows 認証を使用して登録されるサーバーの場合は、この操作は必要ありません。  
  
## <a name="see-also"></a>参照  
 [サーバーの登録の変更 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)   
 [登録済みサーバー情報のエクスポート &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/export-registered-server-information-sql-server-management-studio.md)   
 [新しい登録済みサーバーの作成 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)  
  
  
