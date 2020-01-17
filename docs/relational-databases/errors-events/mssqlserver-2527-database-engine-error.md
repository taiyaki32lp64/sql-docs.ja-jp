---
title: MSSQLSERVER_2527 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bc2b1094a4ea7f8f6c2d2d60c804260286c5f237
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085993"
---
# <a name="mssqlserver2527"></a>MSSQLSERVER_2527
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2527|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|メッセージ テキスト|テーブル O_NAME のインデックス I_NAME を処理できません。ファイル グループ F_NAME がオフラインです。|  
  
## <a name="explanation"></a>説明  
この情報メッセージは、インデックスに対応するデータを格納しているファイル グループの 1 つがオフライン状態なので、インデックスをチェックできないことを示しています。 ファイル グループ内のファイルの状態により、ファイル グループ全体の可用性が決まります。 ファイル グループを使用可能にするには、ファイル グループ内のすべてのファイルがオンラインである必要があります。 他に問題がなければ、同じオブジェクトの他のインデックスはすべてチェックされます。  
  
## <a name="user-action"></a>ユーザーの操作  
指定したファイル グループのファイルの状態を表示するには、**sys.database_files** カタログ ビューまたは **sys.master_files** カタログ ビューにクエリを実行します。  
  
オフライン ファイルをバックアップから復元します。  
  
## <a name="see-also"></a>参照  
[sys.database_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[sys.master_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
