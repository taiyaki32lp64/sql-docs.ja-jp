---
title: FILESTREAM データを格納するテーブルを作成する方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], table storage
ms.assetid: 029c3059-5c83-43e2-a859-9027031b7de1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 54c3acef29036c8178b9103e31c7e01e7a02595b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085410"
---
# <a name="create-a-table-for-storing-filestream-data"></a>FILESTREAM データを格納するテーブルを作成する方法
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、FILESTREAM データを格納するテーブルを作成する方法について説明します。  
  
 データベースに FILESTREAM ファイル グループが含まれているときは、FILESTREAM データを格納するテーブルを作成または変更できます。 列に FILESTREAM データが含まれていることを指定するために、 **varbinary(max)** 列を作成し、FILESTREAM 属性を追加します。  
  
### <a name="to-create-a-table-to-store-filestream-data"></a>FILESTREAM データを格納するテーブルを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[新しいクエリ]** をクリックしてクエリ エディターを表示します。  
  
2.  次の例からクエリ エディターに [!INCLUDE[tsql](../../includes/tsql-md.md)] コードをコピーします。 この [!INCLUDE[tsql](../../includes/tsql-md.md)] コードによって、Records という FILESTREAM が有効なテーブルが作成されます。  
  
3.  テーブルを作成するには、 **[実行]** をクリックします。  
  
## <a name="example"></a>例  
 次のコード例では、 `Records`という名前のテーブルを作成します。 `Id` 列は `ROWGUIDCOL` 列で、Win32 API で FILESTREAM を使用する場合に必要となります。 `SerialNumber` 列は `UNIQUE INTEGER`です。 `Chart` 列は `FILESTREAM` 列で、 `Chart` をファイル システムに格納するために使用されます。  
  
> [!NOTE]  
>  この例では、「 [FILESTREAM が有効なデータベースを作成する方法](../../relational-databases/blob/create-a-filestream-enabled-database.md)」で作成した Archive データベースが必要です。  
  
 [!code-sql[FILESTREAM#FS_CreateTable](../../relational-databases/blob/codesnippet/tsql/create-a-table-for-stori_1.sql)]  
  
## <a name="see-also"></a>参照  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
