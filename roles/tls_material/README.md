# blueprints.common.tls_material

Place caller-supplied TLS material with correct permissions.

## Deployment model

`tls_material` (capability).

## Inputs

All configuration is supplied via caller variables — see `meta/argument_specs.yml`. Required inputs
have no default and fail fast when missing.

## Non-goals

- Does not retrieve secrets — the caller resolves them and passes them in
  (see [secret consumption standard](../../../../docs/standards/BLUEPRINTS_SECRET_CONSUMPTION.md)).
- Does not deploy or configure any other product. Cross-product wiring lives in
  `blueprints.common_integrations` where applicable.
