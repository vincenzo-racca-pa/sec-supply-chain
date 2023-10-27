# Securing Supply Chain
modifica 2

This repo is based from: https://github.com/ThomasVitale/supply-chain-security-java


## Verifying policies for signatures and provenance

### Verifying the signature on an OCI image

```shell
cosign verify \
   --certificate-identity-regexp https://github.com/vincenzo-racca-pa \
   --certificate-oidc-issuer https://token.actions.githubusercontent.com \
   ghcr.io/vincenzo-racca-pa/sec-supply-chain | jq
```

### Verifying the SLSA provenance for an OCI image

```shell
IMAGE=ghcr.io/vincenzo-racca-pa/sec-supply-chain
IMAGE="${IMAGE}@"$(crane digest "${IMAGE}")
slsa-verifier verify-image "$IMAGE" \
  --source-uri github.com/vincenzo-racca-pa/sec-supply-chain \
  --print-provenance | jq
```
