# Steps

VAULT_ADDR='http://127.0.0.1:8200' vault secrets disable nats-secrets

vault plugin register -sha256 `sha256sum ./build/vault/plugins/vault-plugin-secrets-nats-darwin-amd64 | cut -d' ' -f1` secret vault-plugin-secrets-nats-darwin-amd64

VAULT_ADDR='http://127.0.0.1:8200' vault secrets enable -path=nats-secrets vault-plugin-secrets-nats-darwin-amd64


vault write nats-secrets/issue/operator/myop @example/operator/operator.json

vault write nats-secrets/issue/operator/myop/account/sys @example/sysaccount/sysaccount.json

vault list nats-secrets/issue/operator/myop/account

vault read -field=jwt --format=table nats-secrets/jwt/operator/myop/account/sys