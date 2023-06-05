# Register

## API Path
`https://api.soulforger.net/auth/register`

## Endpoint Description
The endpoint is used to create a user account. The model for the `Body` is described in the nect section.

## Definition
| Name | Type | Description |
| ----------- | ----------- | ----------- |
| email | `string` | This is the unique identifier. It's not only needed to contact the user but also find their account whenever they want to log in. |
| display_name | `string` | The name that the user wants to be publically displayed on their account. |
| password | `string` | The password is the value used to confirm that the user owns the profile whenever they log in. The password should **NEVER** be saved without being hashed first! |
| password_confirmation | `string` | Used to make ensure no typos were made in the password. |
| eula | `boolean` | Used to make sure that the user accepted the *Terms and Conditions*. |

## Backend Model
```python title='./models/account_management/account.py'
class Account(BaseModel):
    email: str
    display_name: str
    password_confirmation: str
    password: str
    eula: bool
```

## Frontend Interface
```ts title='./src/interfaces/authentification.ts'
export interface Account{
    email: string,
    display_name: string,
    password: string,
    password_confirmation: string,
    eula: boolean
}
```



