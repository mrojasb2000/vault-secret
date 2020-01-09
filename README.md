# vault-secret
Hashicorp Vault Secret


Vault commands:

Usage: vault <command> [args]

Common commands:
    read        Read data and retrieves secrets
    write       Write data, configuration, and secrets
    delete      Delete secrets and configuration
    list        List data or secrets
    login       Authenticate locally
    agent       Start a Vault agent
    server      Start a Vault server
    status      Print seal and HA status
    unwrap      Unwrap a wrapped secret

Other commands:
    audit          Interact with audit devices
    auth           Interact with auth methods
    debug          Runs the debug command
    kv             Interact with Vault's Key-Value storage
    lease          Interact with leases
    namespace      Interact with namespaces
    operator       Perform operator-specific tasks
    path-help      Retrieve API help for paths
    plugin         Interact with Vault plugins and catalog
    policy         Interact with policies
    print          Prints runtime configurations
    secrets        Interact with secrets engines
    ssh            Initiate an SSH session
    token          Interact with tokens
    

1.- Launch DEV server:
$ vault server -dev

2.- Set VAULT ADDRESS environment:
$ export VAULT_ADDR='http://127.0.0.1:8200'

3.- Set VAULT DEV ROOT TOKEN ID
$ export VAULT_DEV_ROOT_TOKEN_ID='<TOKEN>'
  
4.- Check status server
$ vault status

Key             Value
---             -----
Seal Type       shamir
Initialized     true
Sealed          false
Total Shares    1
Threshold       1
Version         1.3.1
Cluster Name    vault-cluster-805ef6af
Cluster ID      1b6e1b08-5316-ac6e-0fb5-b251e404ac84
HA Enabled      false

5.- Secret engine list
$ vault secrets list

Path          Type         Accessor              Description
----          ----         --------              -----------
cubbyhole/    cubbyhole    cubbyhole_58aec4a7    per-token private secret storage
identity/     identity     identity_87f704b4     identity store
secret/       kv           kv_70fe2b65           key/value secret storage
sys/          system       system_7500283d       system endpoints used for control, policy and debugging

6.- Put new secret in path
$ vault kv put secret/hello foo=world excited=yes

Key              Value
---              -----
created_time     2020-01-09T13:16:54.700547Z
deletion_time    n/a
destroyed        false
version          1

7.- Get secret from vault
$ vault kv get secret/hello

====== Metadata ======
Key              Value
---              -----
created_time     2020-01-09T13:16:54.700547Z
deletion_time    n/a
destroyed        false
version          1

===== Data =====
Key        Value
---        -----
excited    yes
foo        world

8.- Enable new secret engine
$ vault secret enabler -path=kv kv

Success! Enabled the kv secrets engine at: kv/

9.- Write secret on new path
$ vault write kv/airplane type=boeing class=787

Success! Data written to: kv/airplane

10.- Read secret from path
$ vault read kv/airplane

Key                 Value
---                 -----
refresh_interval    768h
class               787
type                boeing
