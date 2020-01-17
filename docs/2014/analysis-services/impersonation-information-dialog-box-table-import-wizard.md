---
title: 権限借用情報 ダイアログ ボックス (テーブルのインポート ウィザード) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.impersonationinfo.f1
ms.assetid: bee7eee5-0650-41f1-a372-5076ae97a58c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6592d81e91e0582c79bc1a8bb1264b6ab9a7b733
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080696"
---
# <a name="impersonation-information-dialog-box-table-import-wizard"></a>[権限借用情報] ダイアログ ボックス (テーブル インポート ウィザード)
  **[権限借用情報]** ページを使用して、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] がデータ ソースに接続する際に使用される資格情報を指定します。 権限借用の資格情報の詳細については、次を参照してください。[偽装&#40;SSAS 表形式&#41;](tabular-models/impersonation-ssas-tabular.md)します。  
  
## <a name="options"></a>および  
 **特定の Windows ユーザー名とパスワード**  
 表形式モデルで指定した Windows ユーザー アカウントのセキュリティ資格情報を使用するには、このオプションを使用します。  
  
 **ユーザー名**  
 使用するユーザー アカウントのドメインと名前を入力します。 次の形式を使用します。  
  
 *\<ドメイン名 >* **\\** *\<ユーザー アカウント名 >*  
  
 このオプションは、 **[特定のユーザー名とパスワードを使用する]** がオンになっている場合にのみ有効になります。  
  
 **Password**  
 テーブル モデルで使用するユーザー アカウントのパスワードを入力します。  
  
 このオプションは、 **[特定のユーザー名とパスワードを使用する]** がオンになっている場合にのみ有効になります。  
  
 **サービス アカウント**  
 このオプションを選択すると、モデルを管理する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] サービスに関連付けられているセキュリティ資格情報が使用されます。  
  
## <a name="see-also"></a>参照  
 [権限借用 (SSAS テーブル)](tabular-models/impersonation-ssas-tabular.md)  
  
  
