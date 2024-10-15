AWS CDK is installed using node: `sudo npm i -g aws-cdk`

by default the CDK library initializes a project inside its current folder.

to initialize a project: `cdk init`

The bin folder just contains the code to initialize our application and the lib folder contains contains our actual cloudformation stacks.

The dependencies `aws-cdk-lib` and `constructs` are required in a project, because both have types and the functionality that generate cloudformation templates.

`devDependencies` for typescript:
- `@types/jest` --> for tests
- `ts-jest` --> required by jest to run typescript files.
- `aws-cdk`, `ts-node` and `typescript` --> It will help us to directly execute TypeScript code so we won't need to first of all call this build step before executed.

The `cdk.json` file is what makes a typescript project, it configures `cdk` inside the project. 

`"app:"` --> the most important entry, has the command `npx ts-node --prefer-ts-exys bin/cdk-starter.ts`, that will be called when we will call different CDK commands.
Npx stands for Node Execute
ts-node library --> directly executes TypeScript

`const app = new cdk.App();` --> application which is required to run others stacks in a CDK project 

`new CdkStarterStack(app, 'CdkStarterStack');` --> initialization of a new Stacks
Stacks are defined in the `lib` folder 

`cdk boostrap` --> command to 
`cdk deploy` --> deploy the stack
`cdk synth` --> only generates a template

the `cdk.out` folder contains the cloud formation template that is deployed 