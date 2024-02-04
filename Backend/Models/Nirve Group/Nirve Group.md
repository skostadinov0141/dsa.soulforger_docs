#backend #erm #model 

![[nirve_group_erm.svg]]

# Purpose
The Nirve Group is used to further specify a [[Nirve Phase 1 Common]], similarly to a [[Nirve Tag]] it applies a more rulebook relevant category to the Model. 

# Implementation
```typescript
@Schema()  
export class NirveGroup {  
    _id: string;  
    @Prop()  
    @ApiProperty()  
    name: string;  
    @Prop()  
    @ApiProperty()  
    description: string;  
    @Prop({ type: mongoose.Schema.Types.ObjectId, ref: 'User' })  
    @ApiProperty()  
    createdBy: User;  
    @Prop()  
    @ApiProperty()  
    createdAt: Date;  
    @Prop()  
    @ApiProperty()  
    updatedAt: Date;  
}
```
