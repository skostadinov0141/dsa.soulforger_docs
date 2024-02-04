#erm #backend #auth #model 

![[Backend/Models/User/user_profile_erm.svg]]

# Purpose
The User model is used to save all important information about a Soulforger.net user. The [[Profile|Profile Model]] is separated from the User model and connected to the User model with a one way connection for security reasons.

# Implementation
## User
```typescript
@Schema()  
export class User {  
    _id: string;  
    @ApiProperty()  
    @Prop({ required: true })  
    email: string;  
    @ApiProperty()  
    @Prop({ required: true })  
    passwordHash: string;  
    @ApiProperty()  
    @Prop({ required: true })  
    username: string;  
    @ApiProperty()  
    @Prop([String])  
    roles: string[];  
    @ApiProperty()  
    @Prop()  
    createdAt: Date;  
    @ApiProperty()  
    @Prop()  
    updatedAt: Date;  
    @Prop({ type: mongoose.Schema.Types.ObjectId, ref: 'Profile' })  
    profile: Profile;  
}
```

## Profile
```typescript
@Schema()  
export class Profile {  
    _id: string;  
    @Prop()  
    @ApiProperty()  
    displayName: string;  
    @Prop()  
    @ApiProperty()  
    bio: string;  
    @Prop()  
    @ApiProperty()  
    avatarUrl: string;  
    @Prop()  
    @ApiProperty()  
    preferredLanguage: string;  
    @Prop()  
    @ApiProperty()  
    favoriteRulebook: string;  
    @Prop()  
    @ApiProperty()  
    preferredRole: string;  
    @Prop()  
    @ApiProperty()  
    createdAt: Date;  
    @Prop()  
    @ApiProperty()  
    updatedAt: Date;  
}
```
