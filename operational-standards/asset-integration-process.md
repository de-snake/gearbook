# Asset integration process

{% hint style="info" %}
WIP: this page is to provide exhaustive guidelines for integrating a new asset class to gearbox. \
It covers development and resting of adapters, price feeds and resulting market configurations.
{% endhint %}

Inputs: \
\- asset class\
\- are reputable external feeds available?

1. SC devs
   1. receive request for asset\
      come up with a scope of required contacts: adapter, phantom token, gateway, price feed, router, withdrawal subcompressor
   2. codes v0 of required contracts; run unit tests
   3. run complex tests in the test environment&#x20;
2. Analyst
   1. Prepare market config for testing based on template
3. PI & infra devs
   1. Create testnet with a functional market to test a new integration based on config from 2.
4. SC dev
   1. Run router tests and compressor tests on that testnet until it's fully ready for audit

{% columns %}
{% column %}
5) DAO\
   Vote to add auditor if it's not already whitelisted in BCR
{% endcolumn %}

{% column %}
5. Auditors\
   Prepare audit report\
   Sign bytecode in BCR
{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
6. PI & infra devs\
   Add adapters to adapters sdk\
   Add adapters to PI\
   Add feed deployment constructor to PI (pfs)
{% endcolumn %}

{% column %}
6. Anvil tests dev\
   Prepare correct faucet for testnet&#x20;
{% endcolumn %}
{% endcolumns %}

7. Instance owner
   1. Add tokens and price feeds to price feed store
   2. Configure router and compressor for the instance
8. Analyst
   1. Prepare new bundles for the target asset class
9. PI devs
   1. Add bundles to PI
10. Analyst & PI devs
    1. Create markets using bundles and test on Staging
    2. Release bundles in production
