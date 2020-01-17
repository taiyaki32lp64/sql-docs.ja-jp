---
title: XML システム ストアド プロシージャ | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b07b7f782c534c7d98e6e20047f58787fe32e8e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902870"
---
# <a name="xml-system-stored-procedures"></a>XML システム ストアド プロシージャ
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  SQL Server には、OPENXML と共に使用する、次のシステム ストアド プロシージャが用意されています。  
  
-   [sp_xml_preparedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)  
  
-   [sp_xml_removedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)  
  
 OPENXML を使用してクエリを作成するには、最初に **sp_xml_preparedocument**を呼び出して XML ドキュメントの内部表現を作成する必要があります。 このストアド プロシージャは、XML ドキュメントの内部表現へのハンドルを返します。 その後、このハンドルは OPENXML に渡されます。 OPENXML は、XPath を基にドキュメントの行セット ビューを提供します。 具体的には、これは 1 つの行パターンと 1 つ以上の列パターンで構成されます。  
  
> [!NOTE]  
>  **sp_xml_preparedocument** から返されたドキュメント ハンドルは、セッションが確立されている間のみ有効です。  
  
 XML ドキュメントの内部表現は、 **sp_xml_removedocument** システム ストアド プロシージャを呼び出すことによってメモリから削除できます。  
  
## <a name="see-also"></a>参照  
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
