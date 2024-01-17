# AWS

## API Reference

[AWS SDK for .NET Version 3 API Reference](https://docs.aws.amazon.com/sdkfornet/v3/apidocs/index.html)

## AmazonS3

### AmazonS3クライアントの作成

```CS
// サンプル // AmazonS3クライアントを作成する。
private static AmazonS3Client CreateAmazonS3Client()
{
    // 端末に保存されている共通認証情報ファイルからプロファイル名を指定してプロファイルを取得する。
    var credential = new SharedCredentialsFile();
    if (!credential.TryGetProfile(PROFILE_NAME, out var profile))
    {
        throw new Exception();
    }
    // プロファイルから認証情報を作成する。
    if (!AWSCredentialsFactory.TryGetAWSCredentials(profile, credential, out var awsCredentials))
    {
        throw new Exception();
    }
    // AmazonS3コンフィグを生成する。
    var config = new AmazonS3Config()
    {
        RegionEndpoint = RegionEndpoint.APNortheast1
    };
    // 認証情報とAmazonS3コンフィグからAmazonS3Clientを生成する。
    var client = new AmazonS3Client(awsCredentials, config);
    return client;
}
```

### オブジェクト格納

```CS
// サンプル バケットにオブジェクトを格納する。
private static async Task PutObjectSample(AmazonS3Client client)
{
    // バケットに文字列をオブジェクトとして格納する。
    var putObjectRequest = new PutObjectRequest()
    {
        BucketName = BUCKET_NAME,
        Key = "Sample-String",
        ContentBody = "Sample-String-Body uploaded by .NET App"
    };
    var putObjectResponse = await client.PutObjectAsync(putObjectRequest);
}
```

### オブジェクト取得

```CS
// サンプル バケットからオブジェクトを取得する。
private static async Task GetObjectSample(AmazonS3Client client)
{
    // バケットからオブジェクトを取得する。
    var getObjectRequest = new GetObjectRequest()
    {
        BucketName = BUCKET_NAME,
        Key = "Sample-String"
    };
    var getObjectResponse = await client.GetObjectAsync(getObjectRequest);
    // オブジェクトの内容をResponseStreamから取得する。
    using var reader = new StreamReader(getObjectResponse.ResponseStream, new UTF8Encoding(false), leaveOpen: true);
    var getContentString = reader.ReadToEnd();
    Console.WriteLine($"GET: {getContentString}");
}
```
