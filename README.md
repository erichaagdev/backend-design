# Backend Design

- About
- Layers
  - Domain (Models & Interactions)
  - Application (Coordinators & Ports)
  - Infrastructure (Frameworks & Adapters)

<!--- RANDOM WIP NOTES BELOW

## Layers

### Domain

Models are like the pieces in a board game.
Interactions are like the rule book. 





## Access Restrictions (Authorization)

### Multi-tenancy

- Multi-tenancy access restrictions always apply across all sub-domains within the domain. This type of access restriction is an inherent property of multi-tenancy and should not be included within the domain logic. Multi-tenancy access restrictions could be coded within a component and distributed for re-use across all multi-tenant applications within the organization.
- When a resource is requested over HTTP that violates multi-tenancy restrictions, 404 should be returned.
- (Should this actually be included as part of the infrastructure layer?? This logic could (should?) be implemented as part of a service mesh and enforced as a domain-wide policy. Or it could be implemented as part of a generic IAM supporting sub-domain) Multi-tenancy access restrictions should be included in repositories. Repository ports should include access restrictions as part of their API contract, either in their documentation or as part of their method signature. Repository adapters must enforce these access restrictions. 

#### Examples

- TenantUser may only access resources within their Tenant.
- ApplicationAdmin may access resources across all Tenants.

### Domain (Use Case)

- Restrictions may be applied to initiating use cases. These restrictions should be enforced within the core domain and only apply to resources or operations within a particular bounded context.
- Over HTTP, violations of domain access restriction should result in a 403.
- Domain restrictions should be enforced in the domain layer / within use cases themselves.

#### Examples

- TenantUser may only create a domain resource if they have sufficient permission.
- TenantUser may only create a resource if the FeatureX switch is enabled. 
