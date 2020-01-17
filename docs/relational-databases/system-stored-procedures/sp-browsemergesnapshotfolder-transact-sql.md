---
title: sp_browsemergesnapshotfolder (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsemergesnapshotfolder
- sp_browsemergesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsemergesnapshotfolder
ms.assetid: e248642f-5fea-4ed7-be1a-36ff75abcfde
author: stevestein
ms.author: sstein
ms.openlocfilehash: 92df93d1c14b10aa6587d0eaf13f4de81bc4d7f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046012"
---
# <a name="spbrowsemergesnapshotfolder-transact-sql"></a>sp_browsemergesnapshotfolder (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ パブリケーションに対して生成された最新のスナップショットの完全なパスを返します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_browsemergesnapshotfolder [@publication= ] 'publication'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(2000)**|スナップショット ディレクトリの完全パスです。|  
  
## <a name="remarks"></a>コメント  
 **sp_browsemergesnapshotfolder**はマージ レプリケーションで使用します。  
  
 結果セットが 2 つの行を含める場合は、パブリッシャーの作業ディレクトリとパブリッシャー スナップショット フォルダーの両方にスナップショット ファイルを生成するパブリケーションを設定します。 最初の行には、パブリケーションのスナップショット フォルダーが含まれていますし、2 番目の行には、パブリッシャーの作業が含まれています。ディレクトリ。  
  
 **sp_browsemergesnapshotfolder**は、マージ スナップショット ファイルが生成されるディレクトリを決定するために便利です。 このフォルダーおよびパスとその内容をリムーバブル メディアにコピーし、スナップショットを使用してスナップショットの代替位置からサブスクリプションを同期することができます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_browsemergesnapshotfolder**します。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
