# EKS-Vault
In this YAML file, we first create a Kubernetes secret called vault-creds in the default namespace, which contains the base64-encoded Vault address, role ID, and secret ID.

Next, we create a Kubernetes deployment for the Vault agent, which runs the hashicorp/vault-k8s:0.13.0 Docker image. We mount the vault-agent-config ConfigMap as a volume, and specify the VAULT_ADDR, VAULT_ROLE_ID, and VAULT_SECRET_ID environment variables using the envFrom field and the vault-creds secret.

Finally, we create a Kubernetes ConfigMap called vault-agent-config in the default namespace, which contains the Vault agent configuration. In this example, we configure the agent to authenticate with Vault using the Kubernetes authentication method, and write the resulting token to a file at /var/run/secrets/vaultproject.io/eks-vault-agent/token. We also configure the agent to use the token from the cache if it is still valid.

Note that this YAML file assumes that you have already created the necessary Vault roles and policies for your EKS cluster. You will need to modify the role field in the config.hcl file to match the name of your Vault role.
