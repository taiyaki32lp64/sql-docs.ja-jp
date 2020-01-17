---
title: レッスン 2:スナップショット フォルダーの準備 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f286cde9-c0d0-43ef-b7ba-53c3cbb8906c
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 5ec45b0a29f9f4c8fb1e6a9b683e47797f194885
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721021"
---
# <a name="lesson-2-preparing-the-snapshot-folder"></a>レッスン 2:スナップショット フォルダーの準備
  このレッスンでは、パブリケーション スナップショットの作成と保存に使用されるスナップショット フォルダーを設定する方法を学習します。  
  
### <a name="to-create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>スナップショット フォルダーの共有を作成し、アクセス許可を与えるには  
  
1.  Windows エクスプローラーで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ フォルダーに移動します。 既定の場所は、C:\Program Files\Microsoft SQL Server\MSSQL.X\MSSQL\Data です。  
  
2.  **repldata**という名前の新しいフォルダーを作成します。  
  
3.  このフォルダーを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[repldata のプロパティ]** ダイアログ ボックスの **[共有]** タブで、 **[共有]** をクリックします。  
  
5.  **[ファイルの共有]** ダイアログ ボックスで、 **[共有]**、 **[完了]** の順にクリックします。  
  
6.  **[セキュリティ]** タブで、 **[編集]** をクリックします。  
  
7.   **[アクセス許可]** ダイアログ ボックスで **[追加]** をクリックします。 **[選択するオブジェクト名を入力してください]** ボックスに、レッスン 1 で作成したスナップショット エージェント アカウントの名前「\<_コンピューター名>_**\repl_snapshot**」を入力します (\<*コンピューター名>* はパブリッシャーの名前)。 **[名前の確認]** をクリックして、 **[OK]** をクリックします。  
  
8.  前の手順を繰り返して、ディストリビューション エージェント (\<_コンピューター名>_**\repl_distribution**) とマージ エージェント (\<_コンピューター名>_**\repl_merge**) のアクセス許可を追加します。  
  
9. 次のアクセス許可が与えられていることを確認します。  
  
    -   repl_snapshot - フル コントロール  
  
    -   repl_distribution - 読み取り  
  
    -   repl_merge - 読み取り  
  
10. **[OK]** をクリックして **[repldata のプロパティ]** ダイアログ ボックスを閉じると、repldata 共有フォルダーが作成されます。  
  
## <a name="next-steps"></a>次の手順  
 ここでは、スナップショット フォルダーの共有を構成しました。 次は、ディストリビューションを構成します。 「[レッスン 3:ディストリビューションの構成](lesson-3-configuring-distribution.md)します。  
  
## <a name="see-also"></a>関連項目  
 [スナップショット フォルダーのセキュリティ保護](security/secure-the-snapshot-folder.md)  
  
  
