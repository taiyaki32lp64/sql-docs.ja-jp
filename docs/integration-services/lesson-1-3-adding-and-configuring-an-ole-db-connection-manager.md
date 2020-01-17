---
title: 手順 3:OLE DB 接続マネージャーを追加し、構成する | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4bf9a4a922c8aeed7ca344b423193e8b01c19037
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296142"
---
# <a name="lesson-1-3-add-and-configure-an-ole-db-connection-manager"></a>レッスン 1-3:OLE DB 接続マネージャーを追加し、構成する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



データ ソースに接続するためのフラット ファイル接続マネージャーを追加したら、データの変換先に接続するための OLE DB 接続マネージャーを追加します。 パッケージに OLE DB 接続マネージャーを追加すれば、OLE DB 対応のデータ ソースからデータを抽出したり、OLE DB 対応のデータ ソースへデータを読み込んだりできるようになります。 OLE DB 接続マネージャーでは、接続に必要なサーバー、認証方法、既定のデータベースを指定できます。  
  
この実習では、Windows 認証を使用して **AdventureWorksDW2012** のローカル インスタンスに接続する OLE DB 接続マネージャーを作成します。 参照変換や OLE DB 変換先など、このチュートリアルで後ほど作成するその他のコンポーネントも、この OLE DB 接続マネージャーを参照します。  
  
## <a name="add-and-configure-an-ole-db-connection-manager"></a>OLE DB 接続マネージャーを追加し、構成する

1. **[ソリューション エクスプローラー]** ウィンドウで **[接続マネージャー]** を右クリックし、 **[新しい接続マネージャー]** を選択します。

1. **[SSIS 接続マネージャーの追加]** ダイアログで **[OLEDB]** 、 **[追加]** の順に選択します。
    
2. **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスで、 **[新規作成]** を選択します。  
  
3. **[サーバー名]** に「 **localhost**」と入力します。  
  
    サーバー名に localhost という名前を使用すると、接続マネージャーは、ローカル コンピューター上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既定のインスタンスに接続します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のリモート インスタンスを使用するには、localhost ではなく、接続先のサーバー名を指定します。  
  
4. **[サーバーにログオンする]** で、 **[Windows 認証を使用する]** が選択されていることを確認します。  
  
5. **[データベースへの接続]** で、 **[データベース名の選択または入力]** ボックスに「 **AdventureWorksDW2012**」と入力するか、またはこのデータベースを一覧から選択します。  
  
6. **[接続テスト]** を選択し、指定した接続設定が有効であることを確認します。  
  
7. **[OK]** を選択します。  
  
8. **[OK]** を選択します。  
  
9. **[接続マネージャー]** ウィンドウで、**localhost.AdventureWorksDW2012** が選択されていることを確認します。  
  

## <a name="go-to-next-task"></a>次の実習に進む
[手順 4:データ フロー タスクをパッケージに追加する](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>参照  
[[キャッシュなし]](../integration-services/connection-manager/ole-db-connection-manager.md)  
  
