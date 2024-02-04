#backend #erm #model 

![[nirve_pase_1_common_erm.svg]]
# Purpose
The Nirve Phase 1 Common is the primary component for creating Nirve Elements. It describes an early blueprint of a certain Nirve Element (spell, skill, item etc.). The blueprint is later expanded on by transforming the basic blueprint into different models.

# Related Models
- [[Nirve Group]]
- [[Nirve Tag]]
- [[User]]
# Implementation
```typescript
@Schema()  
export class NirvePhase1Common {  
    _id: string;  
    @Prop()  
    @ApiProperty()  
    name: string;  
    @Prop()  
    @ApiProperty()  
    description: string;  
    @Prop()  
    @ApiProperty()  
    location: string;  
    @Prop({ type: mongoose.Schema.Types.ObjectId, ref: 'User' })  
    @ApiProperty()  
    createdBy: User;  
    @Prop()  
    @ApiProperty()  
    createdAt: Date;  
    @Prop()  
    @ApiProperty()  
    updatedAt: Date;  
    @Prop()  
    @ApiProperty()  
    creationPhase: number;  
    @Prop()  
    @ApiProperty()  
    creatorNotes: string;  
    @Prop()  
    @ApiProperty()  
    type: string;  
    @Prop({ type: [mongoose.Schema.Types.ObjectId], ref: 'NirveTag' })  
    @ApiProperty()  
    tags: NirveTag[];  
    @Prop({ type: [mongoose.Schema.Types.ObjectId], ref: 'NirveGroup' })  
    @ApiProperty()  
    groups: NirveGroup[];  
}
```