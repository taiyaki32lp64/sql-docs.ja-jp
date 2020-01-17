---
title: sys.database_filestream_options (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_filestream_options
- sys.database_filestream_options_TSQL
- database_filestream_options_TSQL
- sys.database_filestream_options
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_filestream_options catalog view
ms.assetid: 3383c607-0bbc-456a-ab37-7230f4cbf0e9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 95d9c980927d565b907d666af1317e883126087e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915036"
---
# <a name="sysdatabasefilestreamoptions-transact-sql"></a>sys.database_filestream_options (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  FileTable 内の有効化された FILESTREAM データに対する非トランザクション アクセスのレベルに関する情報を表示します。 SQL Server インスタンス内の各データベースの 1 つの行が含まれています。  
  
 FileTables について詳しくは、「[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)」をご覧ください。  
  
  
|[列]|種類|説明|  
|------------|----------|-----------------|  
|**database_id**|**int**|データベースの ID です。 この値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意になっています。|  
|**directory_name**|**nvarchar (255)**|すべての FileTable 名前空間のデータベース レベルのディレクトリ。|  
|**non_transacted_access**|**tinyint**|有効になっている FILESTREAM データに対する非トランザクション アクセスのレベル。 アクセスのレベルの NON_TRANSACTED_ACCESS オプションで設定されます、 **CREATE DATABASE**または**ALTER DATABASE**ステートメント。<br /><br /> この設定では、次の値の 1 つがあります。<br /><br /> 0 - 有効になっていません。 これは既定値です。 このレベルは、値を提供することによって設定**OFF**の**NON_TRANSACTED_ACCESS**オプション。<br /><br /> 1-読み取り専用アクセス。 このレベルは、値を提供することによって設定**READ_ONLY**の**NON_TRANSACTED_ACCESS**オプション。<br /><br /> 3-フル アクセス。 このレベルは、値を提供することによって設定**完全**の**NON_TRANSACTED_ACCESS**オプション。<br /><br /> 5 - READONLY に移行中。<br /><br /> 6 - OFF に移行中|  
|**non_transacted_access_desc**|**nvarchar(60)**|Non_transacted_access で識別される非トランザクション アクセスのレベルの説明です。<br /><br /> この設定では、次の値の 1 つがあります。<br /><br /> NONE - これは既定値です。<br /><br /> READ_ONLY<br /><br /> FULL<br /><br /> IN_TRANSITION_TO_READ_ONLY<br /><br /> IN_TRANSITION_TO_OFF|  
  
## <a name="see-also"></a>関連項目  
 [FileTable の前提条件の有効化](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
  
