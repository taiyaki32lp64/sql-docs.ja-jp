---
title: MSSQL_ENG003724 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f3ea7c8720d43fdba53821091c0664bfe375a57b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191450"
---
# <a name="mssqleng003724"></a>MSSQL_ENG003724
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|3724|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|%S_MSG '%.*ls' を %S_MSG できません。レプリケーションに使用されています。|  
  
## <a name="explanation"></a>説明  
 データベース内のオブジェクトがレプリケートされると、システム テーブル **sysarticles** (スナップショット パブリケーションまたはトランザクション パブリケーションの場合) または **sysmergearticles** (マージ パブリケーションの場合) に、レプリケート済みのマークが付けられています。 レプリケート済みのオブジェクトを削除しようとした場合に、このエラーが発生します。  
  
## <a name="user-action"></a>ユーザーの操作  
 データベース オブジェクトを削除する前に、そのオブジェクトがレプリケートされていないことを確認します。 例 :  
  
-   パブリケーション データベースでエラーが発生した場合、オブジェクトを削除する前にパブリケーションからアーティクルを削除します。 詳細については、「[Add Articles to and Drop Articles from Existing Publications](publish/add-articles-to-and-drop-articles-from-existing-publications.md)」 (既存のパブリケーションでのアーティクルの追加および削除) を参照してください。  
  
-   サブスクリプション データベースでエラーが発生した場合、オブジェクトを削除する前にそのサブスクリプションを削除します。 詳細については、「[パブリケーションのサブスクライブ](subscribe-to-publications.md)」をご覧ください。 トランザクション パブリケーションに対するサブスクリプションの場合、パブリケーション全体を削除するのではなく、個々のアーティクルに対するサブスクリプションを削除することができます。 詳細については、「[sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql)」を参照してください。  
  
 レプリケートされていないデータベースでこのエラーが発生した場合は、[sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) を実行して、データベース内のオブジェクトにレプリケート済みのマークが付かないようにしてください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
