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
    return   localStorage.removeItem(key);
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
did.setConfig(
    {requestDefaults: {
        baseURL: 'your did server node',
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
  loginGuardianAccount: 'loginGuardianAccount',
  guardiansApproved: [
    {
      type: 'Email',
      value: 'value',
      verifierId: 'verifierId',
      verificationDoc: 'verificationDoc',
      signature: 'signature',
    },
  ],
  deviceString: 'deviceString',
  context: {
    requestId: 'requestId',
    clientId: 'clientId',
  },
});
```

**type:scan**

Logged in management to add management.

```javascript
login(type: 'scan', params: ScanLoginParams): Promise<true>;
  Example
did.login('scan',{
  chainId: 'chainId',
  caHash: 'caHash',
  management: {
    managementAddress: 'managementAddress',
    deviceString: 'deviceString';
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
register(params: Omit<RegisterParams, 'managementAddress'>): Promise<RegisterResult>;
```

Example

```javascript
did.register({
  type: 'Email',
  loginGuardianAccount: 'loginGuardianAccount',
  deviceString: 'deviceString',
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
getHolderInfo(params: Pick<GetHolderInfoParams, 'managementAddress' | 'chainId'>): Promise<Array<GetCAHolderByManagementResult>>;
```

Example

```javascript
did.getHolderInfo({
  managementAddress: 'managementAddress', // optional
  chainId: 'chainId',
});
```

getHolderInfo by contracts.

```javascript
getHolderInfo(params: Pick<GetHolderInfoParams, 'managementAddress' | 'chainId'>): Promise<Array<GetCAHolderByManagementResult>>;
```

Example

```javascript  
did.getHolderInfo({
  caHash: 'caHash', // loginGuardianAccount and caHash choose one
  loginGuardianAccount: 'loginGuardianAccount', // loginGuardianAccount and caHash choose one
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

```javascript
getVerificationCode(params: SendVerificationCodeParams): Promise<SendVerificationCodeResult>;
```

Example

```javascript
did._services.getVerificationCode({
  chainId: 'chainId',
  guardianAccount: 'guardianAccount',
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
did._services.verifyVerificationCode({
  verifierSessionId: 'verifierSessionId',
  chainId: 'chainId',
  guardianAccount: 'guardianAccount',
  verifierId: 'verifierId',
  verificationCode: 'verificationCode',
});
```
