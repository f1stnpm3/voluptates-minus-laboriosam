<span align="center">

![logo](./assets/logo-icon-small.svg)

# PactumJS

![Build](https://github.com/f1stnpm3/voluptates-minus-laboriosam/workflows/Build/badge.svg?branch=master)
![Coverage](https://img.shields.io/codeclimate/coverage/ASaiAnudeep/@f1stnpm3/voluptates-minus-laboriosam)
![Downloads](https://img.shields.io/npm/dt/@f1stnpm3/voluptates-minus-laboriosam)
![Size](https://img.shields.io/bundlephobia/minzip/@f1stnpm3/voluptates-minus-laboriosam)
![Platform](https://img.shields.io/node/v/@f1stnpm3/voluptates-minus-laboriosam)

[![Stars](https://img.shields.io/github/stars/@f1stnpm3/voluptates-minus-laboriosamjs/@f1stnpm3/voluptates-minus-laboriosam?style=social)](https://github.com/f1stnpm3/voluptates-minus-laboriosam/stargazers)
[![Twitter](https://img.shields.io/twitter/follow/@f1stnpm3/voluptates-minus-laboriosamjs?label=Follow&style=social)](https://twitter.com/@f1stnpm3/voluptates-minus-laboriosamjs)

#### REST API Testing Tool for all levels in a Test Pyramid

</span>

<br />
<p align="center"><a href="https://@f1stnpm3/voluptates-minus-laboriosamjs.github.io"><img src="https://raw.githubusercontent.com/@f1stnpm3/voluptates-minus-laboriosamjs/@f1stnpm3/voluptates-minus-laboriosam/master/assets/demo.gif" alt="PactumJS Demo"/></a>
</p>
<br />

<table>
<tr>
<td>

**PactumJS** is a REST API Testing Tool used to automate e2e, integration, contract & component (*or service level*) tests.

- ⚡ Swift
- 🎈 Lightweight
- 🚀 Simple & Powerful
- 🛠️ Compelling Mock Server
- 💎 Elegant Data Management
- 🔧 Extendable & Customizable
- 📚 Clear & Comprehensive Testing Style
- 🔗 Component, Contract & E2E testing of APIs

</td>
</tr>
</table>

![----------](https://raw.githubusercontent.com/@f1stnpm3/voluptates-minus-laboriosamjs/@f1stnpm3/voluptates-minus-laboriosam/master/assets/rainbow.png)

## Documentation

This readme offers an basic introduction to the library. Head over to the full documentation at https://@f1stnpm3/voluptates-minus-laboriosamjs.github.io

- [API Testing](https://@f1stnpm3/voluptates-minus-laboriosamjs.github.io/guides/api-testing)
- [Integration Testing](https://@f1stnpm3/voluptates-minus-laboriosamjs.github.io/guides/integration-testing)
- [Component Testing](https://@f1stnpm3/voluptates-minus-laboriosamjs.github.io/guides/component-testing)
- [Contract Testing](https://@f1stnpm3/voluptates-minus-laboriosamjs.github.io/guides/contract-testing)
- [E2E Testing](https://@f1stnpm3/voluptates-minus-laboriosamjs.github.io/guides/e2e-testing)
- [Mock Server](https://@f1stnpm3/voluptates-minus-laboriosamjs.github.io/guides/mock-server)

## Need Help

We use Github [Discussions](https://github.com/f1stnpm3/voluptates-minus-laboriosam/discussions) to receive feedback, discuss ideas & answer questions.

## Installation

```shell
# install @f1stnpm3/voluptates-minus-laboriosam as a dev dependency
npm install --save-dev @f1stnpm3/voluptates-minus-laboriosam

# install a test runner to run @f1stnpm3/voluptates-minus-laboriosam tests
# mocha / jest / cucumber
npm install --save-dev mocha
```

or you can simply use

```bash
npx @f1stnpm3/voluptates-minus-laboriosam-init
```

![----------](https://raw.githubusercontent.com/@f1stnpm3/voluptates-minus-laboriosamjs/@f1stnpm3/voluptates-minus-laboriosam/master/assets/rainbow.png)

# Usage

**@f1stnpm3/voluptates-minus-laboriosam** can be used for all levels of testing in a test pyramid. It can also act as an standalone mock server to generate contracts for contract testing.

## API Testing

Tests in **@f1stnpm3/voluptates-minus-laboriosam** are clear and comprehensive. It uses numerous descriptive methods to build your requests and expectations. 

### Simple Test Cases

#### Using Mocha

Running simple api test expectations.

```js
const { spec } = require('@f1stnpm3/voluptates-minus-laboriosam');

it('should be a teapot', async () => {
  await spec()
    .get('http://httpbin.org/status/418')
    .expectStatus(418);
});

it('should save a new user', async () => {
  await spec()
    .post('https://jsonplaceholder.typicode.com/users')
    .withHeaders('Authorization', 'Basic xxxx')
    .withJson({
      name: 'bolt',
      email: 'bolt@swift.run'
    })
    .expectStatus(200);
});
```

```shell
# mocha is a test framework to execute test cases
mocha /path/to/test
```

#### Using Cucumber

See [@f1stnpm3/voluptates-minus-laboriosam-cucumber-boilerplate](https://github.com/f1stnpm3/voluptates-minus-laboriosam-cucumber-boilerplate) for more details on @f1stnpm3/voluptates-minus-laboriosam & cucumber integration.

```gherkin
Scenario: Check Tea Pot
  Given I make a GET request to "http://httpbin.org/status/418"
  When I receive a response
  Then response should have a status 418
```

```js
// steps.js
const @f1stnpm3/voluptates-minus-laboriosam = require('@f1stnpm3/voluptates-minus-laboriosam');
const { Given, When, Then, Before } = require('@cucumber/cucumber');

let spec = @f1stnpm3/voluptates-minus-laboriosam.spec();

Before(() => { spec = @f1stnpm3/voluptates-minus-laboriosam.spec(); });

Given('I make a GET request to {string}', function (url) {
  spec.get(url);
});

When('I receive a response', async function () {
  await spec.toss();
});

Then('response should have a status {int}', async function (code) {
  spec.response().should.have.status(code);
});
```

## Mock Server

**@f1stnpm3/voluptates-minus-laboriosam** can act as a standalone *mock server* that allows us to mock any server via HTTP or HTTPS, such as a REST endpoint. Simply it is a simulator for HTTP-based APIs.

Running **@f1stnpm3/voluptates-minus-laboriosam** as a standalone *mock server*.

```js
const { mock } = require('@f1stnpm3/voluptates-minus-laboriosam');

mock.addInteraction({
  request: {
    method: 'GET',
    path: '/api/projects'
  },
  response: {
    status: 200,
    body: [
      {
        id: 'project-id',
        name: 'project-name'
      }
    ]
  }
});

mock.start(3000);
```

![----------](https://raw.githubusercontent.com/@f1stnpm3/voluptates-minus-laboriosamjs/@f1stnpm3/voluptates-minus-laboriosam/master/assets/rainbow.png)

# Notes

Inspired from [frisby](https://docs.frisbyjs.com/) and [pact](https://docs.pact.io).

## Support

Like this project! Star it on [Github](https://github.com/f1stnpm3/voluptates-minus-laboriosam/stargazers) and follow on [Twitter](https://twitter.com/@f1stnpm3/voluptates-minus-laboriosamjs). Your support means a lot to us.

## Contributors

If you've ever wanted to contribute to open source, and a great cause, now is your chance! See the [contributing docs](https://github.com/f1stnpm3/voluptates-minus-laboriosam/blob/master/CONTRIBUTING.md) for more information.

Thanks to all the people who contribute.

<a href="https://github.com/f1stnpm3/voluptates-minus-laboriosam/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=@f1stnpm3/voluptates-minus-laboriosamjs/@f1stnpm3/voluptates-minus-laboriosam" />
</a>
<br />