---
title: FILESTREAM および FileTable と AlwaysOn 可用性グループ (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], Availability Groups
- FILESTREAM [SQL Server], Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: fdceda9a-a9db-4d1d-8745-345992164a98
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3fa149aa47c99418bd3109829bfffee698ab3f6e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62814143"
---
# <a name="filestream-and-filetable-with-alwayson-availability-groups-sql-server"></a>FILESTREAM および FileTable と AlwaysOn 可用性グループ (SQLServer)
  このトピックでは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]と FILESTREAM 機能および FileTable 機能を使用する方法について説明します。  
  
 すべての FILESTREAM 機能がサポートされています。 フェールオーバー後、FILESTREAM データは読み取り可能なセカンダリ レプリカと新しいプライマリの両方でアクセスできます。  
  
 FileTable 機能は部分的にサポートされています。 フェールオーバー後、FileTable データはプライマリ レプリカ上でアクセスできますが、読み取り可能なセカンダリ レプリカ上ではアクセスできません。  
  
 **このトピックの内容**  
  
-   [前提条件](#Prerequisites)  
  
-   [FILESTREAM および FileTable アクセスでの仮想ネットワーク名 (VNN) の使用](#vnn)  
  
-   [関連タスク](#RelatedTasks)  
  
-   [関連コンテンツ](#RelatedContent)  
  
##  <a name="Prerequisites"></a> 前提条件  
  
-   FileTable を使用するかどうかにかかわらず、FILESTREAM を使用するデータベースを可用性グループに追加する前に、その可用性グループの可用性レプリカをホストするすべてのサーバー インスタンスで FILESTREAM が有効になっていることを確認してください。 詳細については、「 [Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)」をご覧ください。  
  
##  <a name="vnn"></a> FILESTREAM および FileTable アクセスでの仮想ネットワーク名 (VNN) の使用  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスで FILESTREAM を有効にすると、インスタンス レベルでの共有が作成され、FILESTREAM データにアクセスできるようになります。 この共有にアクセスするには、次の形式でコンピューター名を使用します。  
  
 `\\<computer_name>\<filestream_share_name>`  
  
 ただし AlwaysOn 可用性グループでは、コンピューターの名前が仮想ネットワーク名 (VNN) を使用して仮想化されています。 コンピューターが可用性グループのプライマリ レプリカであり、可用性グループ内のデータベースに FILESTREAM データが格納されている場合、VNN スコープの共有も作成され、FILESTREAM データにアクセスできるようになります。 これは、Transact-SQL による FILESTREAM データへのアクセスには影響しません。 ただし、ファイル システム API を使用するアプリケーションは、次の形式のパスを持つ VNN スコープの共有を使用する必要があります。  
  
 `\\<VNN>\<filestream_share_name>`  
  
 この VNN スコープの共有は、次のいずれかのイベントが発生するときに作成されます。  
  
-   プライマリ レプリカ上にある AlwaysOn 可用性グループに FILESTREAM データを格納するデータベースを追加します。 この場合、共有 `\\<computer_name>\<filestream_share_name>` は既に存在します。 共有 `\\<VNN>\<filestream_share_name>` が作成されます。  
  
-   可用性グループが含まれるプライマリ レプリカ上で、ファイル I/O ストリーム アクセスに対して FILESTREAM を有効にします。 次の共有が作成されます。  
  
    1.  `\\<computer_name>\<filestream_share_name>`  
  
    2.  `\\<VNN1>\<filestream_share_name>` (可用性グループ 1 向け)。  
  
    3.  `\\<VNN2>\<filestream_share_name>` (可用性グループ 2 向け)。  
  
 これらの VNN スコープの共有は、すべてのセカンダリ レプリカにも反映されます。  
  
 FILESTREAM データまたは FileTable データを格納するデータベースが AlwaysOn 可用性グループに属する場合、次の処理が行われます。  
  
-   FILESTREAM および FileTable 関数は、コンピューター名ではなく仮想ネットワーク名 (VNN) のやり取りを行います。 関数の詳細については、「[Filestream および FileTable 関数 &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filestream-and-filetable-functions-transact-sql)」を参照してください。  
  
-   ファイル システム API を介した FILESTREAM または FileTable データへのすべてのアクセスでは、コンピューター名ではなく VNN を使用する必要があります。  
  
 データベースが可用性グループの一部である場合、アプリケーションで `\\<computer_name>\<filestream_share_name>` の形式のコンピューター名を使用して共有にアクセスしようとすると、エラーが発生します。  
  
 データベースが可用性グループの一部ではない場合、アプリケーションで VNN スコープのパスを使用して共有にアクセスしようとすると、要求が正常に終了します。 この場合、仮想ネットワーク名は、コンピューター名に解決されます。 ただし、可用性グループが削除されると VNN スコープのパスの動作が停止するため、この使用法はお勧めしません。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)  
  
-   [FileTable の前提条件の有効化](../../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
 [なし] :  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
