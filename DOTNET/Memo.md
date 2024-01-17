# .NET

## ASP.NET Core MVC

### Razorランタイムコンパイルを有効にする

参照: [ASP.NET Core での Razor ファイルのコンパイル | すべての環境でランタイム コンパイルを有効にする](https://docs.microsoft.com/ja-jp/aspnet/core/mvc/views/view-compilation?view=aspnetcore-6.0&tabs=visual-studio#enable-runtime-compilation-for-all-environments)

```cs
public void ConfigureServices(IServiceCollection services)
{
    services.AddRazorPages().AddRazorRuntimeCompilation();
}
```
