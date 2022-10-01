#Uniswap/web3-react (v6)

<aside>
💡 A simple, maximally extensible, dependency minimized framework for building modern Ethereum dApps
</aside>

## General Info

- Maintainer : Noah Zinsmeister(Uniswap Engineering Lead)
- 패키지 크기 : core 20KB, store 60KB, 기타 패키지 1~10KB
- Projects using `web3-react` : [Uniswap.exchange](https://github.com/Uniswap/uniswap-frontend), [useWallet](https://github.com/aragon/use-wallet), [AAVE](https://github.com/aave/interface), [Eth2 Launchpad](https://github.com/ethereum/staking-launchpad)
- `web3-react`는 dApp에 **어카운트 등의 데이터가 항상 최신인 것을 보장**해주는 상태 머신

  - 여기서 데이터라 함은 다음의 정보들을 말함

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

web3 기능을 사용하고 싶은 영역의 최상단을 감싸는 컴포넌트 (root)

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

- web3React의 type은 [위에 있는](https://www.notion.so/web3-react-v6-dd18249b0dbb42fa9487d944fd83d5f2) `Web3ReactContextInterface`

### `getWeb3ReactContext`

`useWeb3React` 를 사용하지 않고도(hooks가 아닌 곳에서도) 지갑 데이터를 사용할 수 있게 해주는 함수

```tsx
import { getWeb3ReactContext } from "@web3-react/core";

const web3ReactContext = getWeb3ReactContext();

// ...
```

### `createWeb3ReactRoot`

동시에 여러 지갑과 연결하고 싶을 경우 여러개의 root를 만들어야 하는데 이 때 사용하는 함수

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

- 이때 넣어주는 key값(위 코드에서 `'anotherOne'`) 을 `useWeb3React` 나 `getWeb3ReactContext` **\*\*\*\***의 인자로 넣어주면 해당 provider의 데이터를 사용할 수 있음

---

## Reference

- [GitHub - Uniswap/web3-react at v6](https://github.com/Uniswap/web3-react/tree/v6)

- [web3-react/docs at v6 · Uniswap/web3-react](https://github.com/Uniswap/web3-react/tree/v6/docs)
