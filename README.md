# kubectl-oidc

`kubectl` plugin for login with
[OAuth 2.0 password grant](https://oauth.net/2/grant-types/password/).
Notice that the latest Internet-Draft
[*OAuth 2.0 Security Best Current Practice*](https://tools.ietf.org/html/draft-ietf-oauth-security-topics-13#section-3.4)
recommends against using this grant type; hence the plugin has its use only in confined, headless test environments,
where it may provide convenient authentication for the `kubectl` CLI.

## Installation

### Global

Set `KUBECTL_OIDC_IDP_ISSUER_URL`, `KUBECTL_OIDC_CLIENT_ID`, `KUBECTL_OIDC_CLIENT_SECRET` according to your actual
OIDC environment.

```
curl -o /usr/local/bin/kubectl-oidc \
  https://raw.githubusercontent.com/christian-2/kubectl-oidc/master/kubectl-oidc
chmod a+x /usr/local/bin/kubectl-oidc
pip3 install pyyaml
cat >/etc/profile.d/kubectl-oidc.sh <<EOF
KUBECTL_OIDC_CLIENT_ID=...
KUBECTL_OIDC_CLIENT_SECRET=...
KUBECTL_OIDC_IDP_ISSUER_URL=...
EOF
kubectl oidc -h
```

### Local (per user)

```
kubectl config set-credentials $USER --auth-provider=oidc \
  --auth-provider-arg=idp-issuer-url=$KUBECTL_OIDC_IDP_ISSUER_URL \
  --auth-provider-arg=client-id=$KUBECTL_OIDC_CLIENT_ID \
  --auth-provider-arg=client-secret=$KUBECTL_OIDC_CLIENT_SECRET
```
