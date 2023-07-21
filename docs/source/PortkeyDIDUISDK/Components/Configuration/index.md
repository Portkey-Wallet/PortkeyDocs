Configuration
===================

### Configuration

Global configuration is required for network API calls during the Sign-In flow.

```javascript
import {ConfigProvider} from '@portkey/did-ui-react';

ConfigProvider.setGlobalConfig({
    graphQLUrl: 'https://dapp-portkey-test.portkey.finance/Portkey_DID/PortKeyIndexerCASchema/graphql',
    requestDefaults: {
        baseUrl: '/portkey'
    },
    network: {
        defaultNetwork: 'TESTNET',
        networkList:[{
           name: 'aelf Testnet',
           walletType: 'aelf',
           networkType: 'TESTNET',
           isActive: true,
           apiUrl: 'https://did-portkey-test.portkey.finance',
        }]
    },
});
``` 

API

| Props           | Type          | Description  |
| --------------- |:--------------------:| -----:|
| network         | NetworkInfo          | Configure network information. If using QR code login, make sure to configure the default network. If on the web page, you need to configure the proxy service yourself as we have not implemented cross-origin handling. |
| socialLogin     | ISocialLoginConfig (Optional)   | Configure your clientId and other related information when you use Google or Apple third-party login. |
| requestDefaults | IRequestDefaults (Optional)      |  API request configuration, cross-domain issues need to be handled separately. |
| graphQLUrl      | string (Optional)                |  The address for scanning the chain, cross-domain issues need to be handled separately. |
| storageMethod   | IStorageSuit (Optional)          | If you need to customize persistent storage, the default storage is localStorage. |
| reCaptchaConfig | BaseReCaptcha (Optional)         | Configure captcha |


