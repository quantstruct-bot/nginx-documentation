    --- 
    +++ 
    @@ -467,6 +467,10 @@
     
     ## Configure SSL verification for usage reporting with self-signed certificates {#configure-ssl-verify}
     
    +{{<call-out "warning" "Certificate revocation checking is recommended" "">}}
    +Enabling `ssl_verify` ensures that certificates are valid and trusted, but it does **not** check if a certificate has been revoked (for example, due to compromise or mis-issuance). To prevent the acceptance of revoked certificates, it is a best practice to enable certificate revocation checking using Certificate Revocation Lists (CRL) or the Online Certificate Status Protocol (OCSP). For instructions on enabling OCSP or CRL checking in NGINX, see the [NGINX SSL Termination guide](https://docs.nginx.com/nginx/admin-guide/security-controls/terminating-ssl-http/#setup_ocsp).
    +{{< /call-out >}}
    +
     {{<call-out "note" "Version requirements" "">}}
     Usage reporting for NGINX Plus R33 or later in disconnected environments requires **NGINX Instance Manager version 2.18 or later**.
     {{</call-out>}}