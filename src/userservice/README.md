# User Service

The user service manages user accounts and authentication. 
It creates and signs JWTs that are used by other services to authenticate users.

Implemented in Python with Flask.

### Endpoints

| Enndpoint      | Type  | JWT Required | Description                                                |
| -------------- | ----- | ------------ | ---------------------------------------------------------- |
| `/version`     | GET   |              |  Returns the contents of `$VERSION`                        |
| `/ready`       | GET   |              |  Readiness probe endpoint.                                 |
| `/create_user` | POST  |              |  Validates and creates a new user record.                  |
| `/login`       | GET   |              |  Returns a JWT if authentication is successful.            |
| `/get_user`    | GET   | 🔒           |  Returns metadata for the authenticated user.              |

### Environment Variables

- `VERSION`
  - a version string for the service
- `PORT`
  - the port for the webserver
- `ACCOUNTS_DB_ADDR`
  - the address and port of the `accounts-db` service
- `TOKEN_EXPIRY_SECONDS`
  - how long JWTs are valid before forcing user logout
- `PRIV_KEY_PATH`
  - the path to the private key for JWT signing, mounted as a secret
- `PUB_KEY_PATH`
  - the path to the public key for JWT signing, mounted as a secret

### Kubernetes Resources

- [deployments/userservice](/kubernetes-manifests/userservice.yaml)
- [service/userservice](/kubernetes-manifests/userservice.yaml)