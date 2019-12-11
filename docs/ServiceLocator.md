# Uso de extensiones

Reemplazando componentes en tiempo de ejecución a través de ServiceLocator.

- Instance
- EpochGenerator => RegisterEpochGenerator
- HeadersManager => RegisterHeadersManager
- JwtJsonSerializer => RegisterJwtJsonSerializer
- LoggingProvider => RegisterLoggingProvider
- NonceGenerator => RegisterNonceGenerator
- PayloadClaimNames => RegisterPayloadClaimNames
- PayloadClaimsManager => RegisterPayloadClaimsManager
- RequestHeaderNames => RegisterRequestHeaderNames
- WebProxy => RegisterWebProxy
- Runtime
- Reset()