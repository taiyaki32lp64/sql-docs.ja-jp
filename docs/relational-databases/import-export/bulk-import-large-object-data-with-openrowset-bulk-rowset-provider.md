---
title: OPENROWSET 一括行セット プロバイダーを使用したラージ オブジェクト データの一括インポート
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- SINGLE_NCLOB option
- bulk rowset providers [SQL Server]
- bulk importing [SQL Server], data formats
- OPENROWSET function, bulk importing large data
- SINGLE_CLOB option
- data formats [SQL Server], large-object data
- large data, bulk imports
- SINGLE_BLOB option
ms.assetid: 171cdd5c-1e47-4bd7-b99a-4f0fd4e10526
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 845b552762574aa6a75a7ad00a1ce93aabff35c3
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056039"
---
# <a name="bulk-import-large-object-data-with-openrowset-bulk-rowset-provider-sql-server"></a>OPENROWSET 一括行セット プロバイダーを使用したラージ オブジェクト データの一括インポート (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OPENROWSET 一括行セット プロバイダーを使用すると、データ ファイルをラージ オブジェクト データとして一括インポートすることができます。  
  
 OPENROWSET 一括行セット プロバイダーがサポートするラージ オブジェクト データ型は、 **varbinary**(max) (または **image**)、 **varchar**(max) (または **text**)、および **nvarchar**(max) (または **ntext**) です。  
  
> [!NOTE]  
>  **image**、 **text** 、 **ntext** の各データ型は非推奨とされます。  
  
 OPENROWSET BULK 句では、データ ファイルの内容を単一行、単一列の行セットとしてインポートするための 3 つのオプションがサポートされています。 フォーマット ファイルを使用する代わりに、ラージ オブジェクトのいずれかのオプションを指定できます。 これらのオプションを次に示します。  
  
 SINGLE_BLOB  
 *data_file* の内容を単一行として読み取り、 **varbinary(max)** 型の単一列の行セットとして内容を返します。  
  
 SINGLE_CLOB  
 指定したデータ ファイルの内容を文字として読み取り、テキストや **Word 文書などの現在のデータベースの照合順序を使用して、** varchar(max) [!INCLUDE[msCoName](../../includes/msconame-md.md)] 型の単一行および単一列の行セットとして内容を返します。  
  
 SINGLE_NCLOB  
 指定したデータ ファイルの内容を Unicode として読み取り、現在のデータベースの照合順序を使用して、 **nvarchar(max)** 型の単一行および単一列の行セットとして内容を返します。  
  
## <a name="see-also"></a>参照  
 [BULK INSERT または OPENROWSET&#40;BULK...&#41; を使用した一括データのインポート &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [bcp ユーティリティ](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  
