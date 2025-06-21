    --- 
    +++ 
    @@ -475,6 +475,10 @@
     
     The [`ssl_verify`](https://nginx.org/en/docs/ngx_mgmt_module.html#ssl_verify) directive in the [`mgmt`](https://nginx.org/en/docs/ngx_mgmt_module.html) block ensures that NGINX Plus connects only to trusted reporting endpoints by validating the server's SSL certificate. The `ssl_verify` directive is set to `on` by default.
     
    +{{< call-out "note" "Best practice: check for revoked certificates" "fa-solid fa-shield-halved" >}}
    +Enabling `ssl_verify` ensures that the server's certificate is valid and trusted, but it does **not** check whether the certificate has been revoked (for example, due to compromise or mis-issuance). To further enhance security, it is a recommended best practice to enable certificate revocation checking using Certificate Revocation Lists (CRL) or the Online Certificate Status Protocol (OCSP). This helps prevent the acceptance of revoked certificates and reduces the risk of unauthorized access. Revocation checking is not enabled by default and requires additional configuration. For details, see the [NGINX documentation on OCSP and CRL](https://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl_ocsp).
    +{{< /call-out >}}
    +
     ### Why `ssl_verify` is important
     
     When `ssl_verify` is enabled: