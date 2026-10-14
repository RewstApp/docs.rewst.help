# Encryption and key management

Rewst protects your data and the credentials you connect with layered encryption, both at rest and in transit.

## Data at rest

All customer data stored in AWS is encrypted at rest with AWS Key Management Service (KMS), which protects its keys in hardware security modules validated under FIPS 140-3. This covers our databases, backups, file storage, caches, and secrets store, with customer-managed KMS keys and automatic rotation on production stores.

## Integration credentials

Credentials you connect to Rewst (API keys, passwords, OAuth tokens) get an additional layer of application-level encryption on top of storage encryption:

* Each credential version is encrypted with its own unique AES-256-GCM key (envelope encryption).
* Those keys are protected by a regional master key, stored encrypted in AWS Secrets Manager.
* Credentials are decrypted only at the moment a workflow or integration uses them.

## Data in transit

All traffic is encrypted with TLS.
