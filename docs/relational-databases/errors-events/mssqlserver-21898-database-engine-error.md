---
title: MSSQLSERVER_21898 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21898 (Database Engine error)
ms.assetid: 02405b21-3d4e-4c2d-b4b3-d7b1ec05edb4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 79b6637bcfa0c3484de5d4438c48abbec35e40d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056644"
---
# <a name="mssqlserver21898"></a>MSSQLSERVER_21898
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|21898|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum21898|  
|メッセージ テキスト|パブリッシャー '%s' は、ディストリビューション データベース '%s' を使用しますが、パブリッシング データベース '%s' をホストするために必要な '%s' を使用していません。 ディストリビューター '%s' で **sp_changedistpublisher** を実行して、パブリッシャーで使用されるディストリビューション データベースを '%s' に変更してください。|  
  
## <a name="explanation"></a>説明  
**sp_validate_redirected_publisher** は、ローカル ディストリビューターで msdb.dbo.MSdistpublishers にクエリを実行し、新しいパブリッシャーによって使用されるディストリビューション データベースが元のパブリッシャーによって使用されるディストリビューション データベースと同じであることを確認します。 このエラーは、これらのデータベースが異なり、パブリッシャーがパブリッシャー データベースに不適切なホストになる場合に発生します。  
  
## <a name="user-action"></a>ユーザーの操作  
ストアド プロシージャ **sp_changedistpublisher** を実行し、新しいパブリッシャーのディストリビューション データベースを元のパブリッシャーによって使用されるデータベースに変更します。  
  
> [!NOTE]  
> **sp_changedistpublisher** を実行すると、パブリッシャーのディストリビューターで **sp_adddistpublisher** を実行したときに間違ったディストリビューション データベースを入力した場合の問題が解決されます。 ただし、識別されたディストリビューション データベースを使用する別のパブリッシング データベースからの既存のパブリケーションがリモート パブリッシャーにある場合、この変更は適切ではありません。 指定されたディストリビューション データベースを使用するレプリケーションは、新しいパブリッシャーが適切なホストとして機能するために、体系的に削除してから元のパブリッシャーのディストリビューション データベースを使用して再確立する必要があります。  
  
