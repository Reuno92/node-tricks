# Node JS Trick beginner to Advanced

## Node.JS BEST PRACTISE AND SECURITY

**From:** [Node JS Best Practices And Security](https://www.tatvasoft.com/blog/node-js-best-practices/)
**Author:** Vishal Shah
**Rewrite** Renaud Racinet

### Summary

* [Managing Project Structure](#1-managing-project-structure)
* [Error Handling Of The App](#2-error-handling-of-the-app)
* [Code Style Nodejs Best Practises](#3-code-style-nodejs-best-practices)
* [Nodejs Security Best Practices](#4-nodejs-security-best-practices)
* [Best Practices For Testing And Overall Quality](#5-best-practices-for-testing-and-overall-quality)
* [Conclusion](#6-conclusion)

### 1. Managing Project Structure
#### 1.1 Divide your Solution by Components

One of the hardest things for larger applications is to maintain a huge code base with tons of dependencies. This slows production and down development while adding new features. According to Node.js best practices, we should divide the entire codebase into smaller components so that each module gets its own folder, and certain that each module is kept simple and small.

As a node.js node.js best practices, we should develop modular applications by dividing the whole codebase into modular components. In this way, we don’t have to share code with others (e.g. APIs, services, data access, test cases, etc.) This makes the process easier. So that it’s very easy to reason about it.

[<img src="https://www.tatvasoft.com/blog/wp-content/uploads/2021/02/solution-by-component-1.png">](https://www.tatvasoft.com/blog/wp-content/uploads/2021/02/solution-by-component-1.png)

#### 1.2 Layering Components

Layering is important and thus each component is designed to have ‘layers’. As a node.js best practices, these layers have a dedicated object that can be used on the web, logic, and data access code. By doing this, it can make a clean separation of performance issues and can significantly differentiate processes from mock and test codes.

Many developers mix the layers by passing the layer objects (Express req, res) to the Service layer and data layers. This makes your application tightly coupled. your app performance tightly coupled.

#### 1.3 Use npm in it for a New Project

Npm init will automatically generate a package.json file for your project that shows all the packages/node app of npm install has the information of your project.

```Bash
$ mkdir demo-node app
$ cd demo-node app
$ npm init -y

## Now you need to specify an engine’s key with the currently installed version of node (node -v):

"engines": {
"node": "10.3.16"
}
```

#### 1.4 Wrap Common Utilities as npm Package

Larger app/project process typically has the same code used repeatedly multiple times at different locations. We can combine them into a single private package files and use that package at various places within our app. Npm install eliminates code duplication and makes code more manageable.

#### 1.5 Separate Express ‘app’ and ‘server’

The most common mistake that many developers do in any project is to define the entire express application process on  huge files. Instead of doing that, we should separate the ‘Express’ definition into at least two different files. One for the API declaration (app.js) and another one for the network concerns. We can also locate our API declarations within multiple components.

#### 1.6 Using Environment Aware, Secured and Hierarchical Configuration File

As security best practices, we should keep our app-level keys easily readable from file and environment variables. We should also keep secrets outside the committed code and make a config file hierarchy for easier accessibility. To meet all this, a perfect and flawless configuration setup is required. There are few node.js development project structure that are available that can help to do this like rc, nconf and config.

Also, developers should leverage the power of npmrc file in their projects, which can automatically restarts a few environment production configurations during npm init like setting up production of metadata inside project package.json config file – Author name/email/licensing details/version, setting up production of  npm registry changes, log levels, log messages output level changes, installing global modules and many more.

Developers can set default values can be set through npmrc file with the below commands:

```Bash
npm config set init.author.name "Your Name"
npm config set init.author.email "name.lastname@tatvasoft.com"
npm config set init.author.url "http://www.tatvasoft.com"
npm config set init.license "MIT"
npm config set init.version "1.0.0"
```

#### 1.7 Avoiding Garbage in-app

Node js has a default limit of 1.5 GB Single CPU core  as process manager but still, it uses a greedy and lazy garbage collector. It waits until the memory usage is reached and gets recovered on its own.

If you want to gain more control over the garbage collector then we can set the flags on V8.

```Bash
node --optimize_for_size --max_old_space_size=920 --gc_interval=100 server.js
```

You can also otherwise try to run the application using the Docker image. This is important if the app is running in an environment with less than 1.5 GB of available memory usage. For example, if you’d like to tailor a node.js to a 512 MB container, try:

node --optimize_for_size --max_old_space_size=460 --gc_interval=100 server.js

#### 1.8 Hook Things Up

For automation, we can make use of Npm’s lifecycle scripts to make great hooks. If we want to run something before building our app, we can use preinstall script. You can use a post-install script in JSON package to develop assets with a grunt, gulp and browserify or webpack of production application.

in package.json:

```json
"scripts": {
    "postinstall": "bower install && grunt build",
	  "start": "nf start"
}
```

To take hold of these scripts, you can also otherwise use an environment variable.

```json
"postinstall": "if $BUILD_ASSETS; then npm run build-assets; fi",
"build-assets": "bower install && grunt build"
```

You can convert your scripts into files if they aren’t in control.

```json
"postinstall": "scripts/postinstall.sh"
```

Scripts in package.json automatically have ./node_modules/.bin added to their PATH, so you can execute binaries like bower or webpack directly.

### 2. Error Handling of the App 

#### 2.1 Using Async-Await or Promises

Good development practices say to use javascript ‘synchronous function’ for multiple callbacks inside promises to handle async error this process results in a callback hell problem. We can take a look at the available libraries or async and await of javascript to overcome this performance issue. The process manager will use the promises function to catch code error. It reduces code complexity and makes code more readable.

Code Example - use promises

```Javascript
return A()
  .then((a) => B(a))
  .then((b) => C(b))
  .then((c) => D(c))
  .catch((error) => logger.error(error))
  .then(E())

// Code Example - using async/await to catch errors

async function E() {
  try {
    const a= await A();
    const b= await B(a);
    const c= await C(c);
    return await D(c);
  }
  catch(error) {
    logger.error(error);
  }
}
```

### 2.2 Handling Errors Centrally

Every logic that handles errors like logging performance, sending mails regarding error should be written in such a way so that all APIs, night-jobs, unit testing can debug messages and call this method whenever any error occurs.

### 2.3 Validating Request Body

Developers can use available open-source packages like Joi to ensure the request body is proper and does not contain any malicious content. We can validate all the request parameters and body parameters to meet the expected schema before executing actual logic. By doing so we can throw an error to the user input that the requested body is not valid before executing actual logic.

### 2.4 Using Built-in Error Handling Mechanism

There are many ways otherwise available for developers to raise error and resolve them. They can use strings or even define custom types. The Built-in error object makes a uniform approach to handle errors within our source code and other open-source JSON packages.

It is also recommended to log errors and their  names and other Meta properties of errors so that it can be easily identifiable.

```
 // throwing an Error from typical function, whether sync or async
 if(!productToAdd)
       throw new Error('How can I add new product when no value provided?');

 // 'throwing' an Error from EventEmitter
 const myEmitter = new MyEmitter();
 myEmitter emit('error', new Error('whoops!'));

 // 'throwing' an Error from a Promise
 const addProduct = async (productToAdd) => {
      try {
             const existingProduct = await DAL.getProduct (productToAdd.id);
             if (existingProduct !== null) {
                   throw new Error('Product already exists!');
            }
     } catch (err) {
                  // ...
    }
}
```

#### 2.5 Always Await Promises before Returning to Avoid a Partial Stacktrace

When an error occurs, whether, from a synchronous or asynchronous flow, it’s imperative to have a full stacktrace of the error flow. Surprisingly, if an async function returns a promise (e.g., calls another async function) without awaiting, then an error should occur that makes the caller function disappear in the stacktrace.

This will leave the person to diagnose the problem with partial information – All the more if the error cause lies within that caller function then there is a feature v8, also called “zero-cost async stacktraces” that allow stacktraces not to be cut on the most recent await. But due to non-trivial implementation details, it will not work if the return value of a function (sync or async) is a promise. So, to avoid these loopholes in stacktraces for the cases when the returned promises would get rejected. So, we must always explicitly resolve these promises by waiting before returning them from the functions.

###  3. Code Style Node.js Best Practices 

#### 3.1 Use Linting Packages

There are many linting tools available, ESLint is one the most popular linting package which is used to check possible errors in code otherwise you can also [check code styles](https://www.tatvasoft.com/blog/importance-code-quality/) to meet best practices standards. It identifies spacing issues to any potential code patterns that could lead to any security threats as well as possible app-breaking that could occur in the future.

> Note of Rewriter: You can use [gts](https://www.npmjs.com/package/gts) for your Typescript's project.  

There are also other tools available that automatically format code and put it in a more readable way. Also, it resolves minor syntax errors like adding semicolons at the end of each statement, etc.

#### 3.2 Name Your Functions

You can name all the functions which may include the closures and callbacks. You can restrict the use of anonymous functions. Make sure you use the Naming function. Naming will allow you to simply implement what you want and then Take a snapshot of memory usage.

#### 3.3 Proper Naming Conventions for Constants, Variables, Functions, and Classes

As a standard best practice, we should use all constants, functions, variables, and class names in lowercase when we declare them. Also, we should not use any short forms instead use only full forms that are easily understandable by everyone using it. We should use underscore between two words.

Code example

```Javascript
// for class name we use Uppercase
class MyClassExample {}

// Use the const keyword and lowercase
const conf = {
  key: 'value'
};

// for variables and functions names use lowercase
let variableExample = 'value';

function foo() {}
```

#### 3.4 Use Const Over Let, Do Not Use Var

Const variables assigned cannot be changed, this will help you prevent the use of a single variable multiple times so that way we can keep our code clean. In some scenarios where we need to re-assign variables, we will use the let keyword. For example, in a loop, if we want to re-declare variable value we can use let.

Apart from this, “let variables” have blocked the scope, meaning they are accessible inside of a particular block where they are declared. Variables declared using var can be used anywhere inside the function.

The process manager is a simple command-line interface that keeps the inflow of scripts continuously in all the projects.

#### 3.5 Add Required Modules at the Beginning, Avoid Inside Functions

We should put required modules at the beginning of the and avoid putting them in the middle of the function, By doing this we can easily identify dependencies of the entire file and avoid some of the potential performance issues.

#### 3.6 Add Required Modules by Folders, Instead of Whole Files

We can place the index.js files which exports the module’s members so that we can import it into other files. It behaves as an interface to our module and makes it easy to change in the future without breaking the contract.

Code example

```javascript
// Do
module.exports.ServiceProvider = require('./ServiceProvider');
module.exports.NumberResolver = require('./NumberResolver ');
 
// Avoid
module.exports.ServiceProvider = require('./ServiceProvider/ServiceProvider.js');
module.exports.NumberResolver = require('./NumberResolver /NumberResolver.js');
```

#### 3.7 Use of Strict Equality Operator (===)

Use the strict equality operator === instead of weaker abstract equality operator = ==. == will convert two variables to a common type then compare them while === doesn’t type case variables, and ensures that both variables are of the same type and equal.

Example

```Javascript
null       == undefined   // true
true       == 'true'      // false
false      == undefined   // false
''         == '0'         // false
false      == '0'         // true
0          == '0'         // true
' \t\r\n ' == 0           // true
0          == ''          // true
false      == null        // false
```

All above statements will return false when === is used

#### 3.8 Don’t Use Callbacks, Instead Use Async Await

Async-await is supported in all node.js version above Node 8 LTS. We can minimize the use of ‘callbacks’ and ‘promises’ to better deal with asynchronous code. It makes code look synchronous but in reality, it’s a non-blocking mechanism. The best thing with async-await we can do is to make code compact and make code syntax like try-catch.

#### 3.9 Using Arrow Functions (=>)

The Arrow functions make the code more compact and keep the lexical context of the root function (i.e. this). However, it is a suggestion to use async-await applications to stop the use of functional parameters when they are working with old API’s which can accept promises or callbacks.

### 4. Node.js Security Best Practices

We can implement the below security practices to keep the Node.js application safe from attacks. In this blog, we have ensured to cover all the top OWASP (Open Web Security Project) practices for all the Node js security vulnerabilities you come across. Please find security tips below for your web application.

#### 4.1 Use Lint Plug-ins

We can use linter plugins like eslint-plugin-security to identify security plugins and vulnerabilities when we implement codes in Node.js.

##### Possible Errors

These rules relate to possible syntax or logic errors in JavaScript code:

| Error                          | Explanation                                                                |
| ------------------------------ |:---------------------------------------------------------------------------|
| for-direction                  | enforce `for` loop update clause moving the counter in the right direction.|
| getter-return                  | enforce `return` statements in getters                                     |
| no-async-promise-executor      | disallow using an async function as a Promise executor                     |
| no-await-in-loop               | disallow `await` inside of loops                                           |
| no-compare-neg-zero            | disallow comparing against -0                                              |
| no-cond-assign                 | disallow assignment operators in conditional expressions                   |
| no-console                     | disallow the use of `console`                                              |
| no-constant-condition          | disallow constant expressions in conditions                                |
| no-control-regex               | disallow control characters in regular expressions                         |
| no-debugger                    | disallow the use of `debugger`                                             |
| no-dupe-args                   | disallow duplicate arguments in `function` definitions                     |
| no-dupe-else if                | disallow duplicate conditions in if-else-if chains                         |
| no-dupe-keys                   | disallow duplicate keys in object literals                                 |
| no-duplicate-case              | disallow duplicate case labels                                             |
| no-empty                       | disallow empty block statements                                            |
| no-empty-character-class       | disallow empty character classes in regular expressions                    |
| no-ex-assign                   | disallow reassigning exceptions in `catch` clauses                         |

Linting plug-ins, which ensures we eliminate the vulnerable code during the development process.

#### 4.2 Prevent DOS Attacks by Using Middlewares

In case when the legit users do not receive the desired service or in case they receive degraded services, here we can ensure that our node app is under the threat of a DOS attack.
To prevent this situation from happening, we should implement rare limiting using middleware for apps. For larger apps, there are some plug-ins available like rate-limiter-flexible package, Nginx, cloud firewalls, cloud load balancer.

#### 4.3 Prevent SQL Injections

When you frequently use JS strings or string concatenations, this increases the risk of database manipulation. This practice makes your information invalidated, and the developed app highly vulnerable to SQL injection attacks.

In-built security against certain SQL injection attacks is available for ORMs such as Sequelize and mongoose. The built-in indexed parameterized queries provided by Object-Relational Mapping/Object Document Mapper ORM/ODM or database libraries supporting indexed parameterized queries must always be used to avoid these attacks.

> Beware example below is for `Typescript` only, you must readjust for javascript.

Bad example:

```typescript
class BadExample {
    public async searchDrivers(id: number, name: string): Promise<Array<drivers>> {
        const drivers = await db.sequelize.query(
            `SELECT * FROM "get_drivers"(${id}, ${name})`
        );

        return drivers
    }    
}
```

Good example:

```typescript
class GoodExample {
    public async searchDrivers(id: number, name: string): Promise<Array<drivers>> {
        const drivers = await db.sequelize.query(
            `SELECT * FROM "get_drivers"($id, $name)`,
            bind: {
                $id: id,
                $name: name
            }
        );
        return drivers
    };
}
```

#### 4.4 Secure Transmission of Data

For our application data’s integrity and confidentiality in transit is very important. One of the major reasons that compromise the application security of our data and confidentiality are some encryption misconfiguration in the tested infrastructure.

Protocols like TLS (Transport Layer Security) and SSL (Secure Sockets Layer), are used to establish an encrypted end-to-end connection between client side and server (web server and a browser). SSL makes use of strong ciphers and secure algorithms, for client-server communication the same way TLS ensures sensitive data such as card details and user credentials be transmitted securely.

#### 4.5 Manage HTTP Headers

In order to prevent clickjacking, cross-site scripting (XSS attacks), and other malicious attacks, you can create a new impact on impactful impactful node.js applications with secure HTTP headers. We can use plug-ins like the helmet which is easy to configure and create our own Node.js security rules.

##### Recommendation:

Use HTTP headers as per the project’s requirements as shown below

* **Access-Control-Allow-Origin:** This shows if the response can be shared with requesting client from the given origin.
* **Server:** Describes the server information that generated the response.
* **Strict-Transport-Security:** Ensures website is accessed through HTTPS instead of HTTP.
* **X-Content-Type-Options:** Makes sure that MIME types mentioned in Content-type cannot be changed. In this way, you can restrict the app from MIME type sniffing.
* **X-XSS-Protection:** In the older versions of IE, Chrome and Safari it prevents loading of webpages when they find XSS attacks. Modern web browsers don’t need this kind of production setting when sites implement a strong Content-Security-Policy as it already disables inline javascript.
* **X-frame-options:** This header makes sure if a page is allowed to be rendered in frame/iframe.
* **Content-Security-Policy:** This helps to track and stop threats such as XSS attacks (Cross-Site Scripting) and data injection. These attacks can cause data theft, site defacement, and distribution of malware.
* **Referrer-Policy:** It controls how much referrer information should be included in requests.

#### Remove below HTTP headers,

* **x-powered-by:** It is set by servers to show what kind of servers are being requested. It unveils what technologies being used to develop the application which can be useful to attackers.

### 4.6 Examine for Vulnerable Dependencies

In any Node.js application, we can use any of the open-source packages available in various process management tools. We must always be sure of which dependencies package has and what patches are being made from time to time to keep our application safe. Here we are implementing functions with tools like nsp or snyk, and npm audit, to track, monitor, and patch vulnerabilities.

```log
L../code/vacasb.github.10 node v10.15.1] (update-deps) $ npm 1
npm WARN friendly-errors-webpack-plugin@1.7.0 requires a peer of webpack@^2.0.0 || ^3.0.0
 
audited 28156 packages in 8.916s
found 24 vulnerabilities (10 low, 11 moderate, 2 high, 1 critical)
run ‘npm audit fix’ to fix them, or ‘npm audit’ for details
```

#### 4.7 Control Request Payload Size

When the traffic on our application increases, it is difficult to process other important requests, which lowers app performance and exposes our application to Denial-Of-Service (DOS) attacks. A bigger request body is executed by a single thread.

Because of the bigger payload size, attackers can implement vulnerabilities even without making multiple requests. We can limit the body size by using express body-parser that accepts only small-size payloads.

**Example:**

Express body-parser throws an error if the request payload is greater than the specified limit.

Request entity too large

When the entered body crosses the size mentioned in the “limit” option, express throws the above error. The limit set in the byte limit and the length set to the body’s length. The status is set to 413 and the type is set to ‘entity.too.large’.

#### 4.8 Hide Error Details from Clients

In the node.js application, We should use our own error handler that has the ability to handle server errors. While doing that, we must prevent the entire information to the user because it might expose some of our application’s sensitive data like physical paths of files, connection string, sensitive code, etc.

Bad Example of Error files:

```log
SequelizeForeignKeyConstraintError: update or delete on table drivers violates foreign key constraint "drivers_driver_id_fkey" ontable " drivers_devices"
at Query.format Error (D:\Projects\api-2\api lambda drivers.webpack\service webpack:\node_modules seguelize lib\dialects\postgresquery.js:295:1)
at query.catch.err (D:\Projects\api-2\api lambda drivers\.webpack service webpack:\node_modules sequelize\lib\dialects\postgresqueryjs:72:1)
at tyCatcher (D:\Projects\api-2\api lambda drivers\.webpack\service webpack:\node_modules\bluebird is release\util.js:16:1)
at Promise. settlePromiseFromHandler (D:\Projects\api-2\api lambda drivers\.webpack\service webpack:\node_modules\bluebird is release\promise.js: 547:1)
at Promise. settlePromise (D:\Projects\api-2\api lambda\drivers\.webpack\service\webpack:\node_modules\bluebird is release\promise.js:604:11
at Promise._settlePromised (D:\Projects\api-2\api lambda drivers.webpack\service\webpack:\node_modules\bluebird is release\promise.js:649:1}
at Promise.settlePromises (D:\Projects\api-2\api lambda\drivers\.webpack\service webpack:\node_modules\bluebird is release\promise.js:725:1)
at drainQueueStep (D:\Projects\api-2\api lambda\drivers webpack\service webpack:\node_modules\bluebird is release async.js:93:1)
at_drainQueue (D:\Projects\api-2\api lambda drivers\.webpack service webpack:\node_modules\bluebird is releaselasync.is:86:1)
at Async../node_modules/bluebird/js/release/async.is. Async._drainQueues (D:\Projects\api-2\api lambda\drivers\.webpack\service\webpack:\node_modules\bluebird is release async.js:102:1) 
at Immediate Async.drainQueues (as_onlmmediate) (D:\Projects\api-2\api lambda\drivers\.webpack\service webpack:\node_modules\bluebird is release async.is:15:1) at runCallback (timers.is: 705:18) at tryOnlmmediate (timers.js:676:5)
```

**Good Example**

```json
{ "message": "Requested resource is already in use, you cannot delete it." }
```

#### 4.9 Configure 2FA for NPM or Yarn

The attackers can exploit the user-sensitive information and install malicious software in project libraries, even if we apply multi-factor authentication (MFA). If the attackers insert the malicious malware into the public domain, it is possible to degrade the whole web program and web app. Therefore, with npm/yarn, we must use two-factor authentication 2FA, which leaves little hope for hackers.

###  5. Best Practices for Testing and Overall Quality 

#### 5.1 Implement Automated Testing

You should plan your project deadline in such a way that all your developed functionality by developers can adhere to automated testing. It helps to test APIs without even actually calling them. We can mock database calls, and also it makes sure if the last changes done by someone else are not broken after implementing new features.

#### 5.2 Structuring Test

You can use Arrange, Act & Assert (AAA) to structure your tests with 3 well-separated sections. Arrange contains all the data or parameters or expected output which will be used in subsequent calls or comparing actual and expected results, Act – calls actual implementation with all arranged parameters, Assert – compares the actual result with the expected result.

Code example:

```javascript
describe.skip('Employee classification', () => {
    test('When employee ranks more than 3.5, classify as Good', () => {
        
        //Arrange
        const employee = {rank:3.5, joined: new Date(), id:1}
        const stub = sinon.stub(db, "getEmployee")
            .reply({id:1, class: 'Good'});
        
        //Act
        const actual_result = employeeClassifier.classifyEmployee(employee);
        
        //Assert
        expect(actual_result).toMatch('Good');
    });
});
```

#### 5.3 Detect Code Issues with a Linter

We can use linter plugins like eslint-plugin-security to catch code issues while we are coding our node.js app. Linting plugs-ins, which ensures we eliminate vulnerable code while developing.

#### 5.4 Avoid Global Mock Data

While writing test cases we should use separate mock data for each process case rather than declaring it as global and modifying it every time.

Good code example:

```javascript
it("When name, it should get success message", async () => {
    const site = await service.add({
        name: "oldName"
    });
    
    const result = await service.update(site, "changedName");
    
    expect(result).to.be(true);
});
```

Bad code example :

```javascript
before(() => {
    await dbmock.GetDataFromJson('mock.json');
});

it("When name, it should get success message", async () => {
    const site = await service.add({
        name: "oldName"
    });

    const result = await service.update(site, "changedName");

    expect(result).to.be(true);
});
```

#### 5.5 Inspect Vulnerable Dependencies

We can use tools like NPM audit or snyk.io to check vulnerable dependencies.

#### 5.6 Tag Your Tests

There are multiple scenarios where we have to run tests like smoke testing, before committing changes to a source control system or when the pull request is created. We can do this by using tags on tests with different keywords.

#### 5.7 Check Test Coverage

Each testing environment comes with this feature that shows how much percentage of your code is converted under test cases. Some of the frameworks also show different colored texts to identify whether the code is covered or not, or code is covered but the branch is not covered, etc. We can set a minimum limit of test coverage % before committing code to make sure most of the statements are covered.

#### 5.8 Inspect for Outdated Packages

When we add any open-source package then we must check at regular intervals if it is outdated or not. We can do this using available packages like npm-check-update. We can add it into the CI-CD pipeline so that it checks if all the packages are up to date before deploying code to production, otherwise, the build fails and shows an Notice that a particular package is outdated.

#### 5.9 Use Mock Data that is Similar to Real Data

In end-to-end testing, we should not use live data but we should use data that is identical to real ones so that it won’t affect the real data and proper testing can be performed.

#### 5.10 Use Static Analysis Tools

Tools like [SonarQube](https://www.tatvasoft.com/blog/introduction-to-sonarqube-sonarlint/) and Code Climate can do a static analysis that helps to improve code quality, performance and keeps our code manageable. We can add these tools to the CI-CD pipeline which causes build failure when they detect any areas where we can improve code quality so as to boost performance.

### 6. Conclusion

By enlisting the industry-standard Node.js best practices that are followed by us, we want to ensure all Node.js aspirants adopt them from the beginning of their development journey to produce high-quality production applications. These best practices can also be equally valuable for experienced developers wanting to hone their Node.js skills. With the help of these coding best practices, style guides and techniques, you can easily improve your application performance.

We have presented an info-graphical representation of Node.js Best Practices. Take a look:

> From author and according to his wishes:
>
> if you want copy this picture please use this below code, thank you at him:

```html
<p>
    <strong>
        Please include attribution to TatvaSoft.com with this graphic.
    </strong><br /><br />
    <a href='https://www.tatvasoft.com/blog/node-js-best-practices/'>
        <img class="js-lazy-image" data-src='https://www.tatvasoft.com/blog/wp-content/uploads/2021/02/NodeJS-Infographics.jpg' alt='Node.js Best Practices' width='952' height='3948' border='0' />
    </a>
</p>
```

[<p><strong>Please include attribution to TatvaSoft.com with this graphic.</strong><br /><br /><img src='https://www.tatvasoft.com/blog/wp-content/uploads/2021/02/NodeJS-Infographics.jpg' alt='Node.js Best Practices' /></p>](https://www.tatvasoft.com/blog/node-js-best-practices/)
