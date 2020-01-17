---
title: 登録済みサーバーの情報のエクスポート
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.exportregisteredservers.f1
helpviewer_keywords:
- Registered Servers [SQL Server], exporting
- exporting registered server information
- transferring registered server information
ms.assetid: b65e168f-b6bf-489c-b8ad-3b8644acf0b6
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 2d5dcbaf6f478d3cb637c72ada8bee2bb2a088d2
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244597"
---
# <a name="export-registered-server-information-sql-server-management-studio"></a>登録済みサーバー情報のエクスポート (SQL Server Management Studio)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]で登録済みサーバーの情報を保存およびエクスポートして、他の従業員またはサーバーに配布する方法について説明します。 このエクスポート機能を使用すると、複数のコンピューターに一貫性のあるユーザー インターフェイスを提供できます。  
  
 [登録済みサーバー] のファイルのエクスポートとインポートを順に行うことにより、[登録済みサーバー] の同一サーバーを使用して、複数のコンピューターを簡単に構成できます。 これは、複数の場所にあるコンピューターから多数のサーバーを管理する場合、また、経験の少ないユーザーを基本接続設定で構成する場合に便利です。  
  
> [!NOTE]  
>  SQL Server 認証を使用するサーバー登録では、パスワードをユーザーごとに格納します。 サーバー登録のエクスポートとインポートが終了したら、ユーザーは、各サーバーに対して最初の接続時にパスワードを入力する必要があります。これにより、パスワードは登録済みサーバーの一覧に格納されます。 Windows 認証を使用して登録されたサーバーの場合は必要ありません。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-export-registered-server-information"></a>登録済みサーバーの情報をエクスポートするには  
  
1.  [登録済みサーバー] で、サーバー グループを右クリックし、 **[エクスポート]** をクリックします。  
  
    > [!NOTE]  
    >  エクスポートできるのは、個別のサーバー、すべての登録済みサーバー ツリー、登録済みサーバー ツリーのサブセットのいずれかです。  
  
2.  
  **[登録済みサーバーのエクスポート]** ダイアログ ボックスで、次のオプションを設定します。  
  
     **サーバーグループ**  
     エクスポートするサーバー グループを指定します。 すべての登録済みサーバー、特定のサーバー グループ内の登録済みサーバー、または 1 つの登録済みサーバーをエクスポート ファイルにエクスポートします。 エクスポート機能は再帰的です。たとえば、サーバー グループ A にはサーバー グループ B が含まれ、サーバー グループ B にはサーバー グループ C および D が含まれます。サーバー グループ A をエクスポートすると、A、B、C、および D のすべてのエントリがエクスポートされます。  
  
     サーバー グループには、現在の登録済みサーバー ツリーのサーバー グループだけが表示されます。  
  
     **ファイルのエクスポート**  
     テキスト ボックスにエクスポート ファイルの名前を入力するか、参照ボタン (**[...]**) を使用してクライアント コンピューター内のエクスポート ファイルを選択します。 既存のファイルを選択した場合は、登録済みサーバー情報がファイルに追加されます。 .regsrvr 拡張子を使用します。 登録済みサーバーの情報を他のユーザーまたはコンピューターが利用できるようにする場合は、ネットワーク上にファイルを保存できます。 他のユーザーは、そのファイルにアクセスし、一部またはすべての登録済みサーバーの情報をインポートできます。 既存のファイルをエクスポート ファイルとして選択した場合、そのファイルの内容はサーバーの登録情報で上書きされます。  
  
     **エクスポートファイルにユーザー名とパスワードを含めないでください**  
     ファイルをエクスポートするときにユーザー名を除外します。  
  
    > [!IMPORTANT]  
    >  エクスポート ファイルは暗号化されますが、ユーザー名および SQL&#xA0;Server 認証パスワードがファイルに含まれている場合は、ファイルへのアクセスを慎重に管理する必要があります。 したがって、既定では、ユーザー名およびパスワードはエクスポート ファイルから除外されます。  
  
## <a name="see-also"></a>参照  
 [登録済みサーバーの情報をインポート &#40;SQL Server Management Studio&#41;](import-registered-server-information-sql-server-management-studio.md) [新しい登録済みサーバー &#40;SQL Server Management Studio を作成&#41;](create-a-new-registered-server-sql-server-management-studio.md)  
  
  
