---
title: レッスン 1:Azure Storage オブジェクトを作成する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 74edd1fd-ab00-46f7-9e29-7ba3f1a446c5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 53fcba3401a6798fb865613470ba78aa05e9b6dd
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176111"
---
# <a name="lesson-1-create-azure-storage-objects"></a>レッスン 1:Azure Storage オブジェクトの作成
  クラウド記憶域に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] バックアップを作成する前に、まず、ストレージ アカウントを作成してから BLOB コンテナーを作成する必要があります。 レッスン1では、Azure 管理ポータルにログインし、ストレージアカウントと blob コンテナーを作成する手順について説明します。  
  
## <a name="create-a-storage-account"></a>ストレージアカウントを作成する  
 Azure 管理ポータルからストレージアカウントを作成するには、次の手順に従います。  
  
1.  アカウントを使用して Azure 管理ポータルにログインします。 Azure アカウントをお持ちでない場合は、 [azure の3か月間の無料試用版](https://go.microsoft.com/fwlink/?LinkId=271927)に関するページを参照してください。  
  
     ![Azure ログイン画面](../../2014/tutorials/media/windowazurelogin-backuptocloud.gif "Azure ログイン画面")  
  
2.  ストレージアカウントを作成する詳細な手順については、[こちら](https://go.microsoft.com/fwlink/?LinkId=271926)を参照してください。  
  
3.  前の手順で作成したストレージ アカウントを参照します。 Web ページの下部中央にある [キーの**管理**] をクリックします。 アカウント情報が表示されます。 ストレージ アカウント名とアクセス キーをコピーします。 この情報は、SQL の保存された資格情報を作成するために必要です。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、この情報を使用し、ストレージ アカウントにアクセスしてバックアップを作成します。  
  
     ![Azure Storage アカウントキーのスクリーンショット](../../2014/tutorials/media/manageaccesskeys-backuptocloud.gif "Azure Storage アカウントキーのスクリーンショット")  
  
    > [!NOTE]  
    >  ストレージ アカウントは、REST API を使用してプログラムで作成することもできます。 詳細については、「[ストレージアカウントの作成](https://go.microsoft.com/fwlink/?LinkId=271928)」を参照してください。  
  
### <a name="create-a-blob-container"></a>BLOB コンテナーの作成  
 コンテナーには、一連の BLOB をグループ化するコンテナーが用意されています。 すべての BLOB は 1 つのコンテナーに存在する必要があります。 アカウントには、コンテナーを無制限に含めることができますが、少なくとも 1 つのコンテナーが必要です。 コンテナーには、BLOB を無制限に格納できます。  
  
 コンテナーを作成するには、次の手順を実行します。  
  
1.  ストレージアカウントを選択し、 **[コンテナー]** タブをクリックし、画面の下部にある **[コンテナーの追加]** をクリックして、新しいダイアログボックスを開きます。  
  
     ![管理ポータルでのコンテナーの作成](../../2014/tutorials/media/backuptocloud.gif "管理ポータルでのコンテナーの作成")  
  
2.  コンテナーの名前を入力します。 指定したコンテナー名をメモします。 この情報は、レッスン 3 と 4 の T-SQL ステートメントの URL (バックアップ ファイルのパス) で使用されます。  
  
3.  [アクセスの**種類**] で [プライベート] を選択します。 バックアップ ファイルをセキュリティで保護するためのプライベート コンテナーを作成することをお勧めします。  
  
     ![新しい blob コンテナーの作成](../../2014/tutorials/media/backuptocloud-newblobcontainer.gif "新しい blob コンテナーの作成")  
  
    > [!NOTE]  
    >  ストレージ アカウントへの認証は、パブリック コンテナーの作成を選択した場合でも、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のバックアップと復元に必要です。  
    >   
    >  コンテナーは、REST API を使用してプログラムで作成することもできます。 詳細については、[コンテナーの作成](https://go.microsoft.com/fwlink/?LinkId=271946)に関する説明を参照してください。  
  
### <a name="next-lesson"></a>次のレッスン  
 [レッスン 2:SQL Server 資格情報](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md)を作成します。  
  
  
