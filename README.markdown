headers more nginx module for windows, follow compile requirement on http://nginx.org/en/docs/howto_build_on_win32.html newer visual studio should work, tested with visual studio 2012

**Build**

**1. clone or download this repo or edit yours with following:**

in `src/ddebug.h` reorder/replace

```
#include <ngx_config.h>
#include <ngx_core.h>
#include <ngx_http.h>
#include <nginx.h>
```
with
```
#include <ngx_core.h>
#include <ngx_http.h>
#include <nginx.h>
#include <ngx_config.h>
```
and also in 
```
src/ngx_http_headers_more_filter_module.c
src/ngx_http_headers_more_headers_in.c
src/ngx_http_headers_more_headers_out.c
src/ngx_http_headers_more_util.c
```
replace
```
#include "ddebug.h"
```
with
```
#include <ngx_config.h>
#include "ddebug.h"
```
**2. Configure**

    auto/configure --with-cc=cl --builddir=objs --prefix= --conf-path=conf/nginx.conf --pid-path=logs/nginx.pid --http-log-path=logs/access.log --error-log-path=logs/error.log --sbin-path=nginx.exe --http-client-body-temp-path=temp/client_body_temp --http-proxy-temp-path=temp/proxy_temp --http-fastcgi-temp-path=temp/fastcgi_temp --http-scgi-temp-path=temp/scgi_temp --http-uwsgi-temp-path=temp/uwsgi_temp --with-cc-opt=-DFD_SETSIZE=1024 --with-pcre=objs/lib/pcre-8.39 --with-pcre-jit --with-zlib=objs/lib/zlib-1.2.8 --with-select_module --with-http_realip_module --with-http_addition_module --with-http_sub_module --with-http_stub_status_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_auth_request_module --with-http_random_index_module --with-http_secure_link_module --with-http_slice_module --with-stream --with-http_v2_module --add-module=objs/lib/headers-more-nginx-module-0.30

**3. in file `objs/Makefile` delete `-WX` argument**

**4. then**
`nmake -f objs/Makefile`

**5. done, nginx.exe with headers-more module compiled in `objs` directory**


----------


Read more: https://github.com/openresty/headers-more-nginx-module
