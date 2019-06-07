# RESTful架构

## 请求方法

* 如果请求头中存在 X-HTTP-Method-Override 或参数中存在 _method（拥有更高权重），且值为 GET, POST, PUT, DELETE, PATCH, OPTION, HEAD 之一，则视作相应的请求方式进行处理
* GET, DELETE, HEAD 方法，参数风格为标准的 GET 风格的参数，如 url?a=1&b=2
* POST, PUT, PATCH, OPTION 方法
    默认情况下请求实体会被视作标准 json 字符串进行处理，当然，依旧推荐设置头信息的 Content-Type 为 application/json
    在一些特殊接口中（会在文档中说明），可能允许 Content-Type 为 application/x-www-form-urlencoded 或者 multipart/form-data ，此时请求实体会被视作标准 POST 风格的参数进行处理
