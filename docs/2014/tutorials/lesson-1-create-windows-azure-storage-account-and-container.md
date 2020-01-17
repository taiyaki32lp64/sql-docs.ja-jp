---
title: 'レッスン 1: Azure Storage アカウントとコンテナーを作成する |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: efdbd930-cde5-41b0-90ad-58a6cc68dddc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fbe773b8b8115cafc20bb60e962bfb42c9821636
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253503"
---
# <a name="lesson-1-create-azure-storage-account-and-container"></a>レッスン 1: Azure Storage アカウントとコンテナーを作成する
  Azure Storage で SQL Server データファイルの格納を開始するには、まず Azure Storage アカウントと blob コンテナー、および shared access signature を作成する必要があります。 レッスン1では、Azure 管理ポータルにログインし、ストレージアカウント、blob コンテナー、および共有アクセス署名を作成する手順について説明します。  
  
 既定では、ストレージ アカウントの所有者のみがそのアカウントを使って BLOB、テーブル、キューなどにアクセスできます。 この新しい SQL Server の機能強化を使用して、ストレージ アカウント アクセス キーを共有しないで、これらのリソースにアクセスするには、次の操作をする必要があります。  
  
-   コンテナーの権限をプライベートに設定します。  
  
-   Shared Access Signature を作成します。 これにより、リソースを利用可能な期間とクライアントに必要な権限を指定して、コンテナー、BLOB、テーブル、またはキュー リソースに対する制限付きアクセスをデリゲートすることができます。  
  
-   保存されたアクセス ポリシーを使用して、コンテナーまたは BLOB の Shared Access Signature を管理します。 保存されたアクセス ポリシーは、Shared Access Signatures をコントロールするもう 1 つの手段となり、それを取り消す直接的な手段にもなります。  
  
 詳細については、 [Azure Storage リソースへのアクセスの管理](https://msdn.microsoft.com/library/windowsazure/ee393343.aspx)に関するページを参照してください。  
  
## <a name="create-storage-account"></a>[ストレージ アカウントを作成]  
 Azure 管理ポータルでストレージアカウントを作成するには、次の手順を実行します。  
  
1.  アカウントを使用して[Azure 管理ポータル](https://manage.windowsazure.com)にログインします。 Azure アカウントを持っていない場合は、 [Azure の無料試用版サイト](https://www.windowsazure.com/pricing/free-trial/)にアクセスしてください。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  詳細な手順に従って、[ストレージアカウントを作成](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)します。 Azure 機能でのデータファイルの SQL Server に使用するストレージアカウントを作成する場合は、geo レプリケーションの選択を解除するか無効にする必要があることに注意してください。 これは、地理的レプリケーションに参加している複数の BLOB では、書き込みの順序が保証されていないためです。 ストレージ アカウントで地理的レプリケーションが実行されていて、復旧が必要になった場合、データが破損します。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>BLOB コンテナーを作成する  
 Azure では、コンテナーは一連の blob をグループ化します。 すべての BLOB はコンテナーに格納されている必要があります。 ストレージ アカウントには、コンテナーを無制限に含めることができますが、少なくとも 1 つのコンテナーが必要です。 また、1 つのコンテナーに保存できる BLOB の数も無制限です。 ストレージサイズの制限に関する最新情報については、「 [.net での Azure Blob Storage サービスの使用方法](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)」を参照してください。  
  
 Azure でコンテナーを作成するには、次の手順を実行します。  
  
1.  
  [Azure 管理ポータル](https://manage.windowsazure.com)にログインします。  
  
2.  ストレージアカウントを選択し、[**コンテナー** ] タブをクリックし、画面の下部にある [**コンテナーの追加**] をクリックすると、新しいダイアログボックスが開きます。  
  
3.  コンテナーの名前を入力します。  
  
4.  [アクセスの**種類**] で [**プライベート**] を選択します。 アクセスをプライベートに設定すると、コンテナーと blob のデータは、Azure アカウントの所有者のみが読み取ることができます。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  コンテナーをプログラムで作成するために、REST API を使用することもできます。 詳細については、「 [Create Container](https://msdn.microsoft.com/library/windowsazure/dd179468.aspx) 」と「 [Azure Storage Services REST API リファレンス](https://msdn.microsoft.com/library/windowsazure/dd179355.aspx)」を参照してください。  
  
 **次のレッスン:**  
  
 [レッスン2。コンテナーでポリシーを作成し、SAS&#41; キー &#40;Shared Access Signature を生成する](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
