---
title: 'ICommand:: Execute | を使用した行セットの作成Microsoft Docs'
description: ICommand::Execute を使用した行セットの作成
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
- Execute method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: f89db69fba4e4a661d4128122181dae9fb9d3ece
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994319"
---
# <a name="creating-rowsets-with-icommandexecute"></a>ICommand::Execute を使用した行セットの作成
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ICommand::Execute** メソッドを使用して作成された行セットの場合、結果の行セットに設定するプロパティで、コマンドのテキストを制約できます。 これは、動的コマンド テキストをサポートするコンシューマーにとって特に重要です。  
  
 OLE DB Driver for SQL Server は、多数のコマンドで生成される複数の行セット結果をサポートする場合に、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] カーソルを使用できません。 コンシューマーが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] カーソル サポートを必要とする行セットを要求した場合に、コマンド テキストが結果として複数行を生成すると、エラーが発生します。 詳細については、「[複数行セットの結果を生成するコマンド](../../oledb/ole-db-commands/commands-generating-multiple-rowset-results.md)」を参照してください。  
  
 SQL Server 行セットのスクロール可能な OLE DB ドライバー [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]は、カーソルによってサポートされています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、他のデータベース ユーザーの変更によって影響を受けるカーソルに制限が設けらます。 たとえば、一部のカーソル内の行は順序付けできません。この場合に、SQL ORDER BY 句を含むコマンドを使用して行セットを作成しようとすると、エラーが発生します。 詳細については、「[行セットと SQL Server カーソル](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [行セット](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
