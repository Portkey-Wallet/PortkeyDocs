Portkey DID SDK
===================

## Getting started

### Typescript

The `@portkey/did` library is a collection of modules that contain functionality for the did ecosystem.

- `@portkey/accounts` is for the portkey account.  
- `@portkey/utils` is for the portkey utils.
- `@portkey/contracts` is for the portkey contracts.
- `@portkey/graphql` is for the portkey graphql.
- `@portkey/contracts` is for the portkey request.
- `@portkey/types` is for the portkey types.
- `@portkey/utils` is for the portkey utils.
- `@portkey/validator` is for the portkey validator.

#### Installation

Using NPM

```bash
npm install @portkey/did
```

Using Yarn

```bash
yarn add @portkey/did
```

After that, you need configure did server node、graphQL node、storage suite.

```javascript
class Store implements IStorageSuite {
  async getItem(key: string) {
    return localStorage.getItem(key);
  }
  async setItem(key: string, value: string) {
    return localStorage.setItem(key, value);
  }
  async removeItem(key: string) {
    return localStorage.removeItem(key);
  }
}
did.setConfig({
  requestDefaults: {
    baseURL: 'your did server node',
    timeout: 'timeout', // optional default 8000ms
  },
  graphQLUrl: 'your graphQL node',
  storageMethod: new Store(),
});
```

That’s it! Now you can use the did object.

## API Reference

### Typescript

#### Portkey

##### portkey.did

###### did.setConfig

Where you configure did server node, graphQL node, storage suite.

```javascript
did.setConfig({
  requestDefaults: {
    baseURL: 'you did server node',
    timeout: 'timeout', // optional default 8000ms
  },
  graphQLUrl: 'your graphQL node',
  storageMethod: 'your storage suite',
});
```

###### did.login

**loginAccount**

Email or phone number login.

```javascript
did.login(type: 'loginAccount', params: AccountLoginParams): Promise<LoginResult>;
```

Example

```javascript
did.login('loginAccount', {
  chainId: 'chainId',
  loginGuardianIdentifier: 'loginGuardianIdentifier',
  guardiansApproved: [
    {
      type: 'Email',
      identifier: 'identifier',
      verifierId: 'verifierId',
      verificationDoc: 'verificationDoc',
      signature: 'signature',
    },
  ],
  extraData: 'extraData',
  context: {
    requestId: 'requestId',
    clientId: 'clientId',
  },
});
```

**type:scan**

Logged in management to add management.

```ts
login(type: 'scan', params: ScanLoginParams): Promise<true>;
```

Example

```javascript
did.login('scan',{
  chainId: 'chainId',
  caHash: 'caHash',
  managerInfo: {
    address: 'address',
    extraData: 'extraData'
  };
})
```

**getLoginStatus**

```javascript
getLoginStatus(params: { chainId: ChainId; sessionId: string }): Promise<RecoverStatusResult>;
```

Example

```javascript
did.getLoginStatus({
  chainId: 'chainId',
  sessionId: 'sessionId',
});
```

###### Logout

```javascript
logout(params: EditManagementParams): Promise<boolean>;
```

Example

```javascript
did.logout({ chainId: 'chainId' });
```

###### register

```javascript
register(params: Omit<RegisterParams, 'manager'>): Promise<RegisterResult>;
```

Example

```javascript
did.register({
  type: 'Email',
  loginGuardianIdentifier: 'loginGuardianIdentifier',
  extraData: 'extraData',
  chainId: 'chainId',
  verifierId: 'verifierId',
  verificationDoc: 'verificationDoc',
  signature: 'signature',
  context: {
    requestId: 'requestId',
    clientId: 'clientId',
  },
});
```

**getRegisterStatus**

```javascript
getRegisterStatus(params: { chainId: ChainId; sessionId: string }): Promise<RegisterStatusResult>;
```

Example

```javascript
did.getRegisterStatus({
  chainId: 'chainId',
  sessionId: 'sessionId',
});
```

###### getHolderInfo

getHolderInfo by graphQL.

```javascript
getHolderInfo(params: Pick<GetHolderInfoParams, 'manager' | 'chainId'>): Promise<GetCAHolderByManagerResult>;
```

Example

```javascript
did.getHolderInfo({
  manager: 'manager', // optional
  chainId: 'chainId',
});
```

getHolderInfo by server.

```javascript
getHolderInfo(params: Omit<GetHolderInfoParams, 'manager'>): Promise<IHolderInfo>;
```

Example

```javascript
did.getHolderInfo({
  caHash: 'caHash', // loginGuardianIdentifier and caHash choose one
  loginGuardianIdentifier: 'loginGuardianIdentifier', // loginGuardianIdentifier and caHash choose one
  chainId: 'chainId',
});
```

###### getVerifierServers

Get the VerifierServer information of the corresponding chain.

```javascript
getVerifierServers(chainId: ChainId): Promise<VerifierItem[]>;
```

Example

```javascript  
did.getVerifierServers({
  chainId: 'chainId',
});
```

###### Services

**services.getVerificationCode**

send verification code.

```ts
getVerificationCode(params: SendVerificationCodeParams): Promise<SendVerificationCodeResult>;
```

Example

```javascript
did.services.getVerificationCode({
  chainId: 'chainId',
  guardianIdentifier: 'guardianIdentifier',
  type: 'Email',
  verifierId: 'verifierId',
});
```

**services.verifyVerificationCode**

verify verification code.

```javascript
verifyVerificationCode(params: VerifyVerificationCodeParams): Promise<VerifyVerificationCodeResult>;
```

Example

```javascript
did.services.verifyVerificationCode({
  verifierSessionId: 'verifierSessionId',
  chainId: 'chainId',
  guardianIdentifier: 'guardianIdentifier',
  verifierId: 'verifierId',
  verificationCode: 'verificationCode',
});
```
[npm-image-version](https://img.shields.io/npm/v/@portkey/did)
[npm-image-downloads](https://img.shields.io/npm/dm/@portkey/did.svg)
[npm-url](https://npmjs.org/package/@portkey/did)

