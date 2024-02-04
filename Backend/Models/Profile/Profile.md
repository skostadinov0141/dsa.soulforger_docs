#erm #backend #auth #model

![[Backend/Models/Profile/user_profile_erm.svg]]

# Purpose
Any interaction with a User in Soulforger.net is done through the profile. This means that the Profile contains partially public data, the [[User|User Model]] contains only private data. The 

# Implementation
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
