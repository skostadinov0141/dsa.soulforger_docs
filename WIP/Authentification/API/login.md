# Login

## API Path
`https://api.soulforger.net/auth/login`

## Endpoint Description
The endpoint is used to log into an existing account and retrieve a session. The model for the `Body` is described in the nect section.

## Model Definition
| Name | Type | Description |
| ----------- | ----------- | ----------- |
| email | `string` | Unique identifier used to search for the user's account |
| password | `string` | The password is the value used to confirm that the user owns the profile. |
| keep_logged_in | `boolean` | If true the created session should not be deleted, if not the session is ended by the server after 6 hours. |

## Backend Model
```python title='./models/account_management/account.py'
class Login(BaseModel):
    email: str
    password: str
    keep_logged_in: bool
```

## Frontend Interface
```ts title='./src/interfaces/authentification.ts'
export interface Login{
    email: string,
    password: string,
    keep_logged_in: boolean
}
```