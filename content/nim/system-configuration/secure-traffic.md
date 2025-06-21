    --- 
    +++ 
    @@ -475,6 +475,14 @@
     
     The [`ssl_verify`](https://nginx.org/en/docs/ngx_mgmt_module.html#ssl_verify) directive in the [`mgmt`](https://nginx.org/en/docs/ngx_mgmt_module.html) block ensures that NGINX Plus connects only to trusted reporting endpoints by validating the server's SSL certificate. The `ssl_verify` directive is set to `on` by default.
     
    +{{< important >}}
    +**Certificate revocation checking is not enabled by default.**
    +
    +While enabling `ssl_verify` ensures that the certificate is valid and trusted, it does **not** check whether the certificate has been revoked (for example, due to compromise or mis-issuance). Accepting revoked certificates can expose your system to security risks.
    +
    +To enhance security, it is a best practice to enable certificate revocation checking using Certificate Revocation Lists (CRL) or the Online Certificate Status Protocol (OCSP). You can configure this in NGINX using the [`ssl_crl`](https://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl_crl) and [`ssl_ocsp`](https://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl_ocsp) directives. For more information, see the [NGINX SSL module documentation](https://nginx.org/en/docs/http/ngx_http_ssl_module.html).
    +{{< /important >}}
    +
     ### Why `ssl_verify` is important
     
     When `ssl_verify` is enabled: