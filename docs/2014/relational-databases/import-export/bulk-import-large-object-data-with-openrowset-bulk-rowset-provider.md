---
title: OPENROWSET 一括行セット プロバイダー (SQL Server) を使用してインポート ラージ オブジェクト データを一括 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: f6fe945ea90a150397abecfd83f0ce1c945f217c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012107"
---
# <a name="bulk-import-large-object-data-by-using-the-openrowset-bulk-rowset-provider-sql-server"></a>OPENROWSET 一括行セット プロバイダーを使用したラージ オブジェクト データの一括インポート (SQL Server)
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
  
## <a name="see-also"></a>関連項目  
 [BULK INSERT または OPENROWSET&#40;BULK...&#41; を使用した一括データのインポート &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)  
  
  
