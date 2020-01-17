---
title: Lock Pages in Memory オプションの有効化 (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8041f5f057962af79d75f121423233d3d6a3a806
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011775"
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>Lock Pages in Memory オプションの有効化 (Windows)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  この Windows ポリシーにより、プロセスを使用して物理メモリにデータを保持できるアカウントを指定し、ディスク上の仮想メモリへのデータのページングを防止します。  
  
> [!NOTE]  
>  メモリ内のページをロックすると、ディスクへのメモリのページングの際にパフォーマンスが向上する場合があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が使用するアカウントに対してこのポリシーを有効にするには、Windows グループ ポリシー ツール (gpedit.msc) を使用します。 このポリシーを変更できるのは、システム管理者だけです。  
  
### <a name="to-enable-the-lock-pages-in-memory-option"></a>lock pages in memory オプションを有効にするには  
  
1.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。 **[開く]** ボックスに「 **gpedit.msc**」と入力します。  
  
2.  **[ローカル グループ ポリシー エディター]** コンソールで **[コンピューターの構成]** を展開し、次に **[Windows の設定]** を展開します。  
  
3.  **[セキュリティの設定]** を展開し、 **[ローカル ポリシー]** を展開します。  
  
4.  **[ユーザー権利の割り当て]** フォルダーをクリックします。  
  
     ポリシーが詳細ペインに表示されます。  
  
5.  詳細ペインで、 **[メモリ内のページのロック]** をダブルクリックします。  
  
6.  **[ローカル セキュリティの設定 - メモリ内のページのロック]** ダイアログ ボックスで、 **[ユーザーまたはグループの追加]** をクリックします。  
  
7.  **[Select Users, Service Accounts, or Groups]\(ユーザー、サービス アカウント、またはグループの選択\)** ダイアログ ボックスで、SQL Server サービス アカウントを選択します。  
  
8.  SQL Server サービスを再起動して、この設定を反映します。
  
## <a name="see-also"></a>参照  
 [サーバー メモリに関するサーバー構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
