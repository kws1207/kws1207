#Uniswap/web3-react (v6)

<aside>
๐ก A simple, maximally extensible, dependency minimized framework for building modernย Ethereum dApps
</aside>

## General Info

- Maintainer : Noah Zinsmeister(Uniswap Engineering Lead)
- ํจํค์ง ํฌ๊ธฐ : core 20KB, store 60KB, ๊ธฐํ ํจํค์ง 1~10KB
- Projects usingย `web3-react` : [Uniswap.exchange](https://github.com/Uniswap/uniswap-frontend), [useWallet](https://github.com/aragon/use-wallet), [AAVE](https://github.com/aave/interface), [Eth2 Launchpad](https://github.com/ethereum/staking-launchpad)
- `web3-react`๋ dApp์ **์ด์นด์ดํธ ๋ฑ์ ๋ฐ์ดํฐ๊ฐ ํญ์ ์ต์ ์ธ ๊ฒ์ ๋ณด์ฅ**ํด์ฃผ๋ ์ํ ๋จธ์ 

  - ์ฌ๊ธฐ์ ๋ฐ์ดํฐ๋ผ ํจ์ ๋ค์์ ์ ๋ณด๋ค์ ๋งํจ

  ```tsx
  interface Web3ReactContextInterface<T = any> {
    activate: (
      connector: AbstractConnectorInterface,
      onError?: (error: Error) => void,
      throwErrors?: boolean
    ) => Promise<void>;
    setError: (error: Error) => void;
    deactivate: () => void;

    connector?: AbstractConnectorInterface;
    library?: T;
    chainId?: number;
    account?: null | string;

    active: boolean;
    error?: Error;
  }
  ```

## API

### `Web3ReactProvider`

web3 ๊ธฐ๋ฅ์ ์ฌ์ฉํ๊ณ  ์ถ์ ์์ญ์ ์ต์๋จ์ ๊ฐ์ธ๋ ์ปดํฌ๋ํธ (root)

```tsx
import { Web3ReactProvider } from "@web3-react/core";
// import your favorite web3 convenience library here

function getLibrary(provider, connector) {
  return new Web3Provider(provider); // this will vary according to whether you use e.g. ethers or web3.js
}

function App() {
  return (
    <Web3ReactProvider getLibrary={getLibrary}>{/* <...> */}</Web3ReactProvider>
  );
}
```

### `useWeb3React`

```tsx
const web3React = useWeb3React();
```

- web3React์ type์ [์์ ์๋](https://www.notion.so/web3-react-v6-dd18249b0dbb42fa9487d944fd83d5f2) `Web3ReactContextInterface`

### `getWeb3ReactContext`

`useWeb3React` ๋ฅผ ์ฌ์ฉํ์ง ์๊ณ ๋(hooks๊ฐ ์๋ ๊ณณ์์๋) ์ง๊ฐ ๋ฐ์ดํฐ๋ฅผ ์ฌ์ฉํ  ์ ์๊ฒ ํด์ฃผ๋ ํจ์

```tsx
import { getWeb3ReactContext } from "@web3-react/core";

const web3ReactContext = getWeb3ReactContext();

// ...
```

### `createWeb3ReactRoot`

๋์์ ์ฌ๋ฌ ์ง๊ฐ๊ณผ ์ฐ๊ฒฐํ๊ณ  ์ถ์ ๊ฒฝ์ฐ ์ฌ๋ฌ๊ฐ์ root๋ฅผ ๋ง๋ค์ด์ผ ํ๋๋ฐ ์ด ๋ ์ฌ์ฉํ๋ ํจ์

```tsx
import { Web3ReactProvider, createWeb3ReactRoot } from "@web3-react/core";
// import your favorite web3 convenience library here

function getLibrary(provider) {
  return new Web3Provider(provider); // this will vary according to whether you use e.g. ethers or web3.js
}

const Web3ReactProviderReloaded = createWeb3ReactRoot("anotherOne");

function App() {
  return (
    <Web3ReactProvider getLibrary={getLibrary}>
      <Web3ReactProviderReloaded getLibrary={getLibrary}>
        {/* <...> */}
      </Web3ReactProviderReloaded>
    </Web3ReactProvider>
  );
}
```

- ์ด๋ ๋ฃ์ด์ฃผ๋ key๊ฐ(์ ์ฝ๋์์ `'anotherOne'`) ์ `useWeb3React` ๋ `getWeb3ReactContext` **\*\*\*\***์ ์ธ์๋ก ๋ฃ์ด์ฃผ๋ฉด ํด๋น provider์ ๋ฐ์ดํฐ๋ฅผ ์ฌ์ฉํ  ์ ์์

---

## Reference

- [GitHub - Uniswap/web3-react at v6](https://github.com/Uniswap/web3-react/tree/v6)

- [web3-react/docs at v6 ยท Uniswap/web3-react](https://github.com/Uniswap/web3-react/tree/v6/docs)
