---
title: F# を使用した Azure File Storage の概要
description: Azure File storage を使用してクラウドにファイルデータを格納し、Azure 仮想マシン (VM) または Windows を実行するオンプレミスアプリケーションからクラウドファイル共有をマウントします。
author: sylvanc
ms.date: 09/20/2016
ms.openlocfilehash: 9c25ab930abcbe7b358ae63c709aba4e97aed3be
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/01/2019
ms.locfileid: "73423863"
---
# <a name="get-started-with-azure-file-storage-using-f"></a>F\# を使用した Azure File storage の概要

Azure File storage は、標準の[サーバーメッセージブロック (SMB) プロトコル](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx)を使用してクラウドでファイル共有を提供するサービスです。 SMB 2.1 と SMB 3.0 の両方がサポートされています。 Azure File storage を使用すると、ファイル共有に依存するレガシアプリケーションを、コストのかかる書き換えなしに迅速に Azure に移行できます。 Azure virtual machines または cloud services またはオンプレミスのクライアントから実行されているアプリケーションは、デスクトップアプリケーションが一般的な SMB 共有をマウントするのと同じように、クラウドにファイル共有をマウントできます。 その後、任意の数のアプリケーションコンポーネントがマウントし、ファイルストレージ共有に同時にアクセスできます。

File storage の概念の概要については、「 [.net ガイド](/azure/storage/storage-dotnet-how-to-use-files)」を参照してください。

## <a name="prerequisites"></a>必要条件

このガイドを使用するには、最初に[Azure ストレージアカウントを作成](/azure/storage/storage-create-storage-account)する必要があります。
また、このアカウントのストレージアクセスキーも必要になります。

## <a name="create-an-f-script-and-start-f-interactive"></a>F#スクリプトを作成してF#対話形式で起動する

この記事のサンプルは、 F#アプリケーションまたはF#スクリプトで使用できます。 F#スクリプトを作成するには、 F#開発環境で `files.fsx`などの `.fsx` 拡張機能を使用してファイルを作成します。

次に、[パケット](https://fsprojects.github.io/Paket/)や[NuGet](https://www.nuget.org/)などの[パッケージマネージャー](package-management.md)を使用して、`#r` ディレクティブを使用してスクリプトに `WindowsAzure.Storage` パッケージと参照 `WindowsAzure.Storage.dll` をインストールします。

### <a name="add-namespace-declarations"></a>名前空間宣言の追加

`files.fsx` ファイルの先頭に、次の `open` ステートメントを追加します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L1-L5)]

### <a name="get-your-connection-string"></a>接続文字列を取得する

このチュートリアルでは、Azure Storage 接続文字列が必要です。 接続文字列の詳細については、「[ストレージ接続文字列の構成](/azure/storage/storage-configure-connection-string)」を参照してください。

このチュートリアルでは、次のように、スクリプトに接続文字列を入力します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L11-L11)]

ただし、実際のプロジェクトではこの方法は**お勧めできません**。 ストレージアカウントキーは、ストレージアカウントのルートパスワードに似ています。 ストレージアカウントキーは常に慎重に保護してください。 他のユーザーに配布したり、ハードコーディングしたり、他のユーザーがアクセスできるプレーンテキストファイルに保存したりしないでください。 侵害された可能性があると思われる場合は、Azure ポータルを使用してキーを再生成することができます。

実際のアプリケーションでは、ストレージ接続文字列を維持する最善の方法は構成ファイルにあります。 構成ファイルから接続文字列を取得するには、次の手順を実行します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L13-L15)]

Azure Configuration Manager の使用は省略可能です。 .NET Framework の `ConfigurationManager` の種類などの API を使用することもできます。

### <a name="parse-the-connection-string"></a>接続文字列を解析する

接続文字列を解析するには、次のように指定します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L21-L22)]

これにより、`CloudStorageAccount`が返されます。

### <a name="create-the-file-service-client"></a>ファイルサービスクライアントを作成する

`CloudFileClient` の種類を使用すると、ファイルストレージに格納されているファイルをプログラムで使用できます。 サービスクライアントを作成する方法の1つを次に示します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L28-L28)]

これで、からデータを読み取り、ファイルストレージにデータを書き込むコードを記述する準備ができました。

## <a name="create-a-file-share"></a>ファイル共有を作成する

この例では、ファイル共有がまだ存在しない場合に作成する方法を示します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L34-L35)]

## <a name="create-a-root-directory-and-a-subdirectory"></a>ルートディレクトリとサブディレクトリを作成する

ここでは、ルートディレクトリを取得し、ルートのサブディレクトリを取得します。 まだ存在しない場合は、両方を作成します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L41-L43)]

## <a name="upload-text-as-a-file"></a>テキストをファイルとしてアップロードする

この例では、テキストをファイルとしてアップロードする方法を示します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L49-L50)]

### <a name="download-a-file-to-a-local-copy-of-the-file"></a>ファイルのローカルコピーにファイルをダウンロードする

ここでは、作成したばかりのファイルをダウンロードし、ローカルファイルに内容を追加します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L56-L56)]

### <a name="set-the-maximum-size-for-a-file-share"></a>ファイル共有の最大サイズを設定する

次の例では、共有の現在の使用状況を確認する方法と、共有のクォータを設定する方法を示しています。 共有の `Properties`を設定 `SetProperties` し、ローカルの変更を Azure File storage に反映するために `FetchAttributes` を呼び出す必要があります。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L62-L72)]

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>ファイルまたはファイル共有の共有アクセス署名を生成する

ファイル共有または個々のファイルの共有アクセス署名 (SAS) を生成できます。 また、共有アクセスポリシーをファイル共有に作成して、共有アクセス署名を管理することもできます。 共有アクセスポリシーを作成することをお勧めします。これにより、セキュリティが侵害された場合に SAS を取り消すことができます。

ここでは、共有に対して共有アクセスポリシーを作成し、そのポリシーを使用して、共有内のファイルの SAS に対する制約を指定します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L78-L94)]

Shared access signature の作成と使用の詳細については、「 [Shared Access signature (sas) の使用](/azure/storage/storage-dotnet-shared-access-signature-part-1)」および「 [Blob ストレージでの sas の作成と使用](/azure/storage/storage-dotnet-shared-access-signature-part-2)」を参照してください。

### <a name="copy-files"></a>ファイルのコピー

ファイルを別のファイルまたは blob にコピーしたり、blob をファイルにコピーしたりできます。 Blob をファイルにコピーする場合、またはファイルを blob にコピーする場合は、同じストレージアカウント内でコピーする場合でも、共有アクセス署名 (SAS) を使用してソースオブジェクトを認証する*必要があり*ます。

### <a name="copy-a-file-to-another-file"></a>ファイルを別のファイルにコピーする

ここでは、同じ共有内の別のファイルにファイルをコピーします。 このコピー操作では同じストレージアカウント内のファイルがコピーされるため、共有キー認証を使用してコピーを実行できます。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L100-L101)]

### <a name="copy-a-file-to-a-blob"></a>Blob へのファイルのコピー

ここでは、ファイルを作成し、同じストレージアカウント内の blob にコピーします。 コピー操作中にソースファイルへのアクセスを認証するためにサービスが使用するソースファイルの SAS を作成します。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L107-L120)]

Blob は、同じ方法でファイルにコピーできます。 ソースオブジェクトが blob の場合は、コピー操作中にその blob へのアクセスを認証するための SAS を作成します。

## <a name="troubleshooting-file-storage-using-metrics"></a>メトリックを使用したファイルストレージのトラブルシューティング

Azure Storage Analytics は、ファイルストレージのメトリックをサポートしています。 メトリックデータを使用して、要求をトレースし、問題を診断することができます。

[Azure Portal](https://portal.azure.com)から File storage のメトリックを有効にすることも、次のF#ようにすることもできます。

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L126-L140)]

## <a name="next-steps"></a>次のステップ

Azure File storage の詳細については、次のリンクを参照してください。

### <a name="conceptual-articles-and-videos"></a>概念に関する記事とビデオ

- [Azure Files Storage: Windows および Linux 用の、競合のないクラウド SMB ファイルシステム](https://azure.microsoft.com/resources/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
- [Linux で Azure File Storage を使用する方法](/azure/storage/storage-how-to-use-files-linux)

### <a name="tooling-support-for-file-storage"></a>ファイルストレージのツールのサポート

- [Azure Storage での Azure PowerShell の使用](/azure/storage/storage-powershell-guide-full)
- [Microsoft Azure Storage で AzCopy を使用する方法](/azure/storage/storage-use-azcopy)
- [Azure Storage での Azure CLI の使用](/azure/storage/storage-azure-cli#create-and-manage-file-shares)

### <a name="reference"></a>辞書／辞典／その他

- [.NET 用ストレージクライアントライブラリのリファレンス](https://msdn.microsoft.com/library/azure/mt347887.aspx)
- [ファイルサービス REST API リファレンス](/rest/api/storageservices/fileservices/File-Service-REST-API)

### <a name="blog-posts"></a>ブログ投稿

- [Azure File storage の一般提供が開始されました](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
- [Azure File Storage 内](https://azure.microsoft.com/blog/inside-azure-file-storage/)
- [Microsoft Azure ファイルサービスの概要](https://blogs.msdn.microsoft.com/windowsazurestorage/2014/05/12/introducing-microsoft-azure-file-service/)
- [Microsoft Azure ファイルへの接続の保持](https://blogs.msdn.microsoft.com/windowsazurestorage/2014/05/26/persisting-connections-to-microsoft-azure-files/)
