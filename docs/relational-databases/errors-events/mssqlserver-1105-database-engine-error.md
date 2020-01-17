---
title: MSSQLSERVER_1105 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1105 (Database Engine error)
ms.assetid: e7f4ad02-8c7f-4bb9-9781-2c86253f2138
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 270308b2129e5bf34fe5f334d86b2f650846dafc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116197"
---
# <a name="mssqlserver1105"></a>MSSQLSERVER_1105
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1105|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|NO_MORE_SPACE_IN_FG|  
|メッセージ テキスト|データベース '%.\*ls' にオブジェクト '%.*ls'%.\*ls の領域を割り当てられませんでした。'%.\*ls' ファイル グループがいっぱいです。 不要なファイルの削除、ファイル グループ内のオブジェクトの削除、ファイル グループへの新しいファイルの追加、またはファイル グループの既存のファイルの自動拡張の設定のいずれかを行ってディスク領域を作成してください。|  
  
## <a name="explanation"></a>説明  
ファイル グループでディスク領域が不足しています。  
  
## <a name="user-action"></a>ユーザーの操作  
次の操作により、ファイル グループで領域を使用できるようになることがあります。  
  
-   AUTOGROW をオンにする。  
  
-   ファイル グループにファイルをさらに追加する。  
  
-   不要になったインデックスやテーブルを削除することにより、ディスク領域を解放する。  
  
-   詳細については、SQL Server オンライン ブックの「データ ディスク領域の不足に関するトラブルシューティング」を参照してください。  
  
> [!NOTE]  
> 1 つのインデックスが複数のファイルに存在している場合に、いずれかのファイルがいっぱいになると、**ALTER INDEX REORGANIZE** からエラー 1105 が返される可能性があります。 いっぱいになったファイルに行を移動しようとしたときに、再構成プロセスはブロックされます。 この制限を回避するには、**ALTER INDEX REORGANIZE** ではなく **ALTER INDEX REBUILD** を実行するか、いっぱいになったファイルの拡張制限を大きくしてください。  
  
