---
title: SSMA for Oracle コンポーネント (OracleToSQL) の削除 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 0434f88c46d14672c84f5f7939488a827b229e27
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266560"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>SSMA for Oracle コンポーネントの削除 (OracleToSQL)
終了したらを Oracle からのデータベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA コンポーネントをアンインストールしたい場合があります。 クライアント コンポーネントは、いつでもアンインストールできます。 ただしから拡張機能パックをアンインストールする必要がありますいない[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、移行されたデータベースが不要になった内の関数を使用しない限り、 **ssma_oracle**のスキーマ、 **sysdb**データベース。  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>SSMA の Oracle クライアントのアンインストール  
SSMA をアンインストールするにを使用して**プログラム追加と削除**します。  
  
**SSMA をアンインストールするには**  
  
1.  コントロール パネルで、開く**プログラム追加と削除**します。  
  
2.  選択 **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Oracle**、] をクリックし、**削除**します。  
  
3.  SSMA をアンインストールすることを確認するには、次のようにクリックします。**はい**します。  
  
## <a name="uninstalling-the-extension-pack"></a>拡張機能パックをアンインストールします。  
データベースを移行は、内のオブジェクトを使用しない場合は、確認、 **sysdb.ssma_oracle**スキーマ、拡張機能パックを削除するを使用**プログラム追加と削除**します。  
  
**拡張機能パックをアンインストールするには**  
  
1.  コントロール パネルで、開く**プログラム追加と削除**します。  
  
2.  選択**Microsoft SQL Server Migration Assistant for Oracle の拡張機能パック**、 をクリックし、**削除**します。  
  
3.  拡張機能パックをアンインストールすることを確認するには、次のようにクリックします。**はい**します。  
  
4.  ユーティリティのデータベースのスクリプト ページを使用して、インスタンス、インスタンスを選択し、順にクリックします**次**します。  
  
5.  接続パラメーター ページで、認証方式を選択し、クリックして**次**します。  
  
    Windows 認証は、Windows 資格情報を使用してのインスタンスにログオンしようとする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 選択した場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を入力する必要があります、認証、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログイン名とパスワード。  
  
6.  操作の完了 ページで、 **OK**します。  
  
7.  [完了] ページで、次のようにクリックします。**終了**します。  
  
アンインストール後にオブジェクトを確認できます、 **sysdb.ssma_oracle**スキーマ、および場合によっては、全体**sysdb**データベースを使用して削除されました[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。 ただし、他の SSMA 製品を使用する場合も使用、 **sysdb**データベース。 場合は、データベースが存在し、他のデータベースにこのデータベース内のオブジェクトが参照されていないことを確認したら、データベースをデタッチすることができます。  
  
## <a name="see-also"></a>関連項目  
[SSMA for Oracle クライアントのインストール&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[SQL Server での SSMA コンポーネントのインストール&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
