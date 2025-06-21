---
title: Authentication
weight: 100
url: /nginx-management-suite/admin-guide/authentication/

---

# Authentication Methods in NGINX Instance Manager

NGINX Instance Manager (NIM) supports two authentication methods for accessing the web interface and API:

- **Basic Authentication** (default)
- **OpenID Connect (OIDC) Bearer Token Authentication**

By default, new ("vanilla") NIM deployments use Basic Authentication. OIDC authentication must be explicitly configured. When OIDC is enabled, Basic Authentication is disabled for all users, including the default `admin` user.

## Choosing the Right Authentication Method

- **Basic Authentication**: Used in default/vanilla deployments. Authenticate API requests with the `-u username:password` option in `curl`, or by setting the `Authorization: Basic ...` header.
- **OIDC Bearer Token Authentication**: Used when OIDC is configured. Authenticate API requests by setting the `Authorization: Bearer <access token>` header.

**Note:** When OIDC is enabled, Basic Authentication is no longer available.

## Example API Requests

**Basic Authentication (default):**
```bash
curl -X POST 'https://{{NMS_FQDN}}/api/platform/v1/certs' \
    -u "{{USERNAME}}:{{PASSWORD}}" \
    --header "Content-Type: application/json" \
    -d@nginx-repo-certs.json
```

**OIDC Bearer Token Authentication:**
```bash
curl -X POST 'https://{{NMS_FQDN}}/api/platform/v1/certs' \
    --header "Authorization: Bearer <access token>" \
    --header "Content-Type: application/json" \
    -d@nginx-repo-certs.json
```

For more information, see:
- [Set up basic authentication](https://docs.nginx.com/nginx-instance-manager/admin-guide/authentication/basic-auth/set-up-basic-authentication/)
- [Get started with OIDC](https://docs.nginx.com/nginx-instance-manager/admin-guide/authentication/oidc/getting-started/)

> **Security Recommendation:** For production environments, we recommend configuring OIDC authentication for enhanced security and integration with your identity provider.
