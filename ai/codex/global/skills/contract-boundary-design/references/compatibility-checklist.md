# Contract compatibility checklist

Use only applicable items.

## Shape and value semantics
- Required vs optional fields
- Defaults and omitted values
- Null vs absent
- Enum/value additions and removals
- Numeric/string/date/identifier representation
- Ordering, pagination, filtering, and sorting semantics

## Compatibility matrix
- Old consumer with new producer
- New consumer with old producer
- Old persisted/event payload read by new code
- New payload observed by old code

## Errors
- Stable error identifiers/codes
- Public message safety
- Retryable vs terminal outcomes
- Partial success semantics

## Lifecycle
- Deprecation window
- Dual-read/write or dual-format period
- Schema/proto/OpenAPI/codegen impact
- Consumer rollout order
