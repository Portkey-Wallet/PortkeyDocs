Sign In
===================

### Sign-In Flow

```javascript
import { SignIn, PortkeyProvider } from "@portkey/did-ui-react";
import { useRef, useCallback } from "react";
import "@portkey/did-ui-react/dist/assets/index.css"; // import portkey css 

const App = () => {
  const ref = useRef();

  const onFinish = useCallback((didWallet) => {
    console.log("didWallet:", didWallet);
  }, []);

  return (
    <PortkeyProvider networkType={"TESTNET"}>
      <button
        onClick={() => {
          ref.current?.setOpen(true);
        }}
      >
        Sign In
      </button>
      <SignIn ref={ref} onFinish={onFinish} />
    </PortkeyProvider>
  );
};

export default App;

``` 

### Setting up the proxy to connect to testnet for testing 
As during Sign In process, there are number of api calls that are used to retrieve holder info or guardians info from chain to verify user. Thus you can setup your proxy in your project

```javascript
// adding this in package.json file
"proxy": "https://did-portkey-test.portkey.finance" //testnet

```
