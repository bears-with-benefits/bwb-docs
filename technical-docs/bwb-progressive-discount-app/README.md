← [Back to Technical Documentation](/technical-docs/)

# BwB Progressive Discount App

These pages document the Progressive Discount app as implemented in the current codebase. 

## Sections

- [Overview](overview.md)
- [Setup](setup.md)
- [Configuration](configuration.md)
- [Discounts](discounts.md)
- [Checkout Extension](checkout-extension.md)
- [Rebuy Cart Behaviour](rebuy-cart.md)
- [Ops and Deployment](ops-deploy.md)
- [Troubleshooting](troubleshooting.md)

## Scope Notes

- Porting steps live in Ops and Deployment.
- Single active progressive code per store (one `trigger_code`).
- URL/Automatic codes apply at checkout; manual code entry in cart does not apply a progressive discount. A guard-rail message is shown to users.
- Store-specific variants (snippets/callbacks) should be localized per market.
