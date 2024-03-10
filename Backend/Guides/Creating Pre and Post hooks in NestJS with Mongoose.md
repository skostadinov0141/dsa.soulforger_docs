#guide #mongoose #nestjs #pre-hooks #post-hooks 

Since I've now struggled multiple times with creating pre and post hooks in NestJS, here is a step by step guide on how to do it, and what should be considered in order for them to actually trigger.

## Guide
1. Remove the export statement from the current Schema definition inside of its schema.ts File
	- This has to be done in order to ensure that the base schema is not used anywhere, the reason for this will be mentioned later
```typescript
// From
export const UserSchema = SchemaFactory.createForClass(User);
// To
const UserSchema = SchemaFactory.createForClass(User);
```
2. Create a Schema Factory for the Model instead of using a plain Schema definition
```typescript
// ...
export const UserSchemaFactory = () => {  
    UserSchema.post('findOneAndDelete', async function () {  
       console.log('findOneAndDelete hook triggered');  
       console.log(this);  
    return UserSchema;  
};
// ...
```
3. **(OPTIONAL)** Inject any needed models or other dependencies into the hook function
	- Most of the time you might need to inject models in order to implement on-delete-cascade-like functionality
```typescript
// ...
export const UserSchemaFactory = (profileModel: Model<Profile>) => {  
    UserSchema.post('findOneAndDelete', async function () {  
       const _id = this.getQuery()['_id'];  
       await profileModel.deleteOne({ owner: _id }).exec();  
    });  
    return UserSchema;  
};
// ...
```
4. Register the Factory inside of **ALL** NestJS Modules that use the Model

> [!Warning] Important
> Make sure to use the Factory instead of the base Schema in all Modules that use the Model, otherwise the hook will never trigger. No errors are thrown during the process so you might never find out that something is wrong, which might lead to DB pollution in the case of on-delete-cascade implementations for example!

> [!WARNING] Important
> If another model is injected inside of the schema factory, it should be done in all Modules where the factory is used! Otherwise the injected model will result in undefined
```typescript
@Module({  
    imports: [  
       CloudinaryModule,  
       // Notice the forFeatureAsync
       // It is the only way to use factories!
       MongooseModule.forFeatureAsync([  
          {  
             name: User.name,  
             // Inject other models if needed
             // Ensure that the injected model exists
             // in the MongooseModule definition!
             inject: [getModelToken(Profile.name)], 
             useFactory: UserSchemaFactory,  
          },  
          {  
             name: 'Profile',  
             useFactory: () => ProfileSchema,  
          },  
       ]),  
    ],  
    exports: [UserService],  
    controllers: [UserController],  
    providers: [UserService],  
})  
export class UserModule {}
```
