```CS
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;

namespace WebApplication1.Web
{
    public class Startup
    {
        // This method gets called by the runtime. Use this method to add services to the container.
        // For more information on how to configure your application, visit https://go.microsoft.com/fwlink/?LinkID=398940
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddControllersWithViews();
        }
        //Bu kısımda gönderdiğimiz service parametresiyle kullanacağımız servis havuzunu projeye ekleriz.
        //Projeye NVS dahil etmek için

        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.UseRouting();
            //Bu HTTP pipelinedır yani bir istek geldiğinde neler olacağıdır.

            app.UseEndpoints(endpoints =>
            {
                endpoints.MapGet("/", async context =>
                {
                    await context.Response.WriteAsync("Hello World!");
                });
					//Sayfa hiyerarşisini oluşturan controllerla birlikte çalışan kısım. 
                endpoints.MapGet("NewPage", async context =>
                {
                    await context.Response.WriteAsync("Yeni sayfaya hosgeldiniz");
                });

            });
        }
    }
}
```

Start kısmı bizim mainimize benzer temel kısımlar controller dosyalarıyla haberlleşerek buradan yürütülür. 


### JSON DOSYALARI
- Bu dosyaya properties json  altından erişebilirsiniz
```json
  {
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:43801",
      //Uygulamanın çalışacağı kısmın bilgileri ve port ayarları
      "sslPort": 0
    }
  },
  "profiles": {
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "WebApplication1.Web": {
      "commandName": "Project",
      "dotnetRunMessages": "true",
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
        //bu sayfada iki farklı çalıştırma yöntemi var IIE Express vsin kendi sunucusuyla çalışır 
        //WebApp kısmı ise .Netin kendi suınucusunu kullanır.
      }
    }
  }
}
```
