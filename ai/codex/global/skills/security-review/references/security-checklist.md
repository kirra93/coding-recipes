# Security review deep checklist

Use only sections that match the changed surface.

## Identity and authorization
- Authentication enforced where required
- Ownership/tenant boundary checked server-side
- Role/permission/admin boundary checked at the authoritative layer
- Session/token validation, expiry, revocation/logout behavior
- Privilege changes and confused-deputy risks

## Input and injection
- SQL/query construction
- Shell/process execution
- Template/script/HTML rendering
- Path traversal and archive extraction
- Unsafe deserialization/evaluation/dynamic loading

## External calls / SSRF
- User-controlled schemes/hosts/ports
- DNS/rebinding/private-network restrictions if needed
- Redirect behavior
- Sensitive header forwarding
- Timeout and response-size limits

## Secrets and sensitive data
- Secret/token/client exposure
- Logs/errors/telemetry
- Storage/access controls
- Retention and accidental over-collection

## Webhooks/payments
- Signature/authenticity verification
- Replay/duplicate handling
- Idempotency
- Client-trusted payment state
- Auditability of sensitive state transitions

## Files/uploads/downloads
- Size/type/path limits
- Storage isolation and generated names
- Ownership/authorization on download
- Active content/malware handling where relevant

## Network/deployment
- Publicly exposed admin/internal ports
- Default credentials
- Privileged containers/capabilities
- Secret-bearing mounts
- Internal-service exposure
