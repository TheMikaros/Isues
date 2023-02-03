              Okay! Here I have come to the solution with following three steps:

## 1. IIS content length limit
The default request limit (maxAllowedContentLength) is **30,000,000** bytes, which is approximately **28.6MB**. Customize the limit in the web.config file:

```
<system.webServer>
  <security>
    <requestFiltering>
      <!-- Handle requests up to 1 GB -->
      <requestLimits maxAllowedContentLength="1073741824" />
    </requestFiltering>
  </security>
</system.webServer>
```

**Note: Without this application running on IIS would not work.**

## 2. ASP.NET Core Request length limit:
### For application running on IIS:
```
 services.Configure<IISServerOptions>(options =>
 {
      options.MaxRequestBodySize = int.MaxValue;
 });
```

### For application running on Kestrel:

```
services.Configure<KestrelServerOptions>(options =>
{
     options.Limits.MaxRequestBodySize = int.MaxValue; // if don't set default value is: 30 MB
});
```
## 3. Form's MultipartBodyLengthLimit

```
services.Configure<FormOptions>(x =>
{
     x.ValueLengthLimit = int.MaxValue;
     x.MultipartBodyLengthLimit = int.MaxValue; // if don't set default value is: 128 MB
     x.MultipartHeadersLengthLimit = int.MaxValue;
});
```

**Adding all the above options will solve the problem related to the file upload with size more than 30.0 MB.**

            
