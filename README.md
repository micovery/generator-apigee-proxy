# generator-apigee-proxy
An Apigee Proxy Yeoman generator

## License

This code is Copyright (c) 2017-2020 Google LLC, and is released under the
Apache Source License v2.0. For information see the [LICENSE](LICENSE) file.

## Disclaimer

This example is not an official Google product, nor is it part of an official Google product.

## Pre-requisites

- Node.js (10.x or later)
- Maven (3.x or later)
- Java (8 or later)

## Using the generator

- Install dependencies `sudo npm install -g yo openapi2apigee oatts`
- Clone this repo `git clone https://github.com/ssvaidyanathan/generator-apigee-proxy.git`
- `cd generator-apigee-proxy`
- Execute `npm install`
- Execute `sudo npm install . -g`

This should install a new yo generator called "Apigee Proxy"

- Run `yo apigee-proxy` on your terminal to start the prompt
- Provide the details prompted
- After the generator is executed, the Proxy is created with all configurations, tests and build scripts

The generator does the following:
- Generate proxy from the spec using [openapi2apigee](https://www.npmjs.com/package/openapi2apigee)
- Apply global policies (optional)
	- FC-Security policy to call the Security sharedflow. This is set to false (will be skipped)
	- FC-LogHandling policy to generate log object to push to your logging servers
	- FC-FaultHanding policy to handle errors and exceptions
	- RF-PathNotFound to handle catch-all flows to return a 404 not found
- update Basepath, Description, Virtual host, Target server
- Copy templates for configurations
- Generate tests from the spec using [oatts](https://www.npmjs.com/package/oatts). Please note that these auto-generated tests will need to be modified to pass.

### Configurations

Current configuration structure only contains `test` and `prod` environments. Please update this to your Apigee environments and include the appropriate config files. You can refer to the [plugin samples](https://github.com/apigee/apigee-config-maven-plugin/tree/master/samples/EdgeConfig/resources) for more details on the structure

### Execution

Once the folder is generated, you can run 
>`mvn clean install -P{profile} -Dusername={username} -Dpassword={password} -Dorg={org}` 
	
It executes the following: 
- Static Code Analysis
- Unit test
- Code Coverage
- Push configurations (KVM, Cache, Target Server, etc)
- Package and Deploy Proxy bundle
- Run integration tests

Please update the pom profiles and any other configuration in the template pom.xml to your needs

### Shared Flows

The tool adds flow callout policies for Security, Logging, Error Handling and Catch all. For these existing Flow Callout policies to work, please update the Flow Callout policy templates to point to your corresponding Shared flows or else deploy it from the [sharedflows](./sharedflows) directory.


