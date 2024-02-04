#backend #erm #model 

![[nirve_tag_erm.svg]]
# Purpose
The Nirve Tag is used to organize one or Multiple [[Nirve Phase 1 Common]] Models. It is functionally similar to a [[Nirve Group]] but does not contain a description field.

# Implementation
```typescript
@Schema()  
export class NirveTag {  
    _id: string;  
    @Prop()  
    @ApiProperty()  
    tag: string;  
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