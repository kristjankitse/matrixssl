# MatrixSSL 3.9 changelog

## Changes between 3.9.0 and 3.9.1

- Disabled support for SHA-1 signed certificates by default. SHA-1 can
  no longer be considered secure for this purpose (see
  https://shattered.it/static/shattered.pdf). We decided to disable
  SHA-1 signed certificates by default to ensure that MatrixSSL
  customers consider the security implications before enabling them.
  Support for SHA-1 signed certificates can be restored by defining
  ENABLE_SHA1_SIGNED_CERTS in cryptoConfig.h.

- Regenerated all test certificates. Many of the old ones had exceeded
  their validity period. The new test certificates have some minor
  changes, such as the addition of some missing basicConstraints and
  authorityKeyIdentifier extensions. Note that the test certificates
  should never be used in production, but only for initial testing
  during development.

- Fixed bug that caused a segfault when
  ALLOW_VERSION_1_ROOT_CERT_PARSE was enabled and the peer sent a
  version 1 certificate. Correct behaviour is to just produce an
  internal certificate validation failure in this case, as the above
  define only allows parsing of locally stored trusted root
  certificates. This bug is minor as ALLOW_VERSION_1_ROOT_CERT_PARSE
  is disabled by default, and rarely used by MatrixSSL customers.

- Introduced new function setSocketTlsCertAuthCb for setting certificate
  authentication callback when using MatrixSSL via psSocket_t interface.
  Previously constant function name ssl_cert_auth was used for authentication
  callback.
