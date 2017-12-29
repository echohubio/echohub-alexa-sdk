# EchoHub Alexa Lambda SDK

This library is intended to be used when writing an Alexa Skill targeted at
EchoHub users.

## Installation

```
yarn add echohub-alexa-sdk
```

## Usage

The SDK currently assumes you are using [Alexa Skills Kit for NodeJS](https://github.com/alexa/alexa-skills-kit-sdk-for-nodejs)
``` javascript
import EchoHubAlexaSDK from 'echohub-alexa-sdk';

const echohub = new EchoHubAlexaSDK();

const languageStrings = {
  'en-US': {
    translation: {
      HELLO: 'Hi! Welcome to my cool skill using EchoHub'
      TIME: 'The time is {{time}}'
    },
  },
};

const handlers = {
  TimeIntent() {
    args = {
      a: 1.
    }

    echohub.execute('mycommand', args).then((response) => {
      if (response.errorType) {
        EchoHubApi.handleError(alexa, response);
        return;
      }

      this.emit(:tell, this.t('RESPONSE', { time: response.time });
    }
  },
};

export default (event, context) => {
  const alexa = Alexa.handler(event, context);
  alexa.appId = process.env.ALEXA_SKILL_ID;
  // If you don't localise your own module just don't pass anything below
  alexa.resources = EchoHubApi.languageStrings(languageStrings);

  echohub.handler(event, context);

  alexa.registerHandlers(handlers);
  alexa.execute();
};
```

## Development

After checking out the repo, run `yarn test` to run the tests.

To release a new version:

* yarn test
* yarn publish

This will run the tests, update the version, create a git tag for the version, push git commits and tags. Publish the module file to [npmjs.com](https://npmjs.com).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/echohubio/echohub-alexa-sdk. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [ISC License](http://opensource.org/licenses/ISC).
