<template>
  <div>
    <button @click="modal.open()">Open Connect Modal</button>
    <button @click="modal.open({ view: 'Networks' })">Open Network Modal</button>
  </div>
</template>

<script>
import { createWeb3Modal, defaultConfig } from '@web3modal/ethers/vue';

export default {
  data() {
    return {
      modal: null,
    };
  },
  mounted() {
    // 1. Get projectId from https://cloud.walletconnect.com
    const projectId = '4f88dfdcec8f22c4e7ea1368c35eba3b';

    // 2. Set chains
    const mainnet = {
      chainId: 1,
      name: 'Ethereum',
      currency: 'ETH',
      explorerUrl: 'https://etherscan.io',
      rpcUrl: 'https://cloudflare-eth.com',
    };

    // 3. Create your application's metadata object
    const metadata = {
      name: 'My Website',
      description: 'My Website description',
      url: 'http://localhost:5174/', // url must match your domain & subdomain
      icons: ['https://avatars.mywebsite.com/'],
    };

    // 4. Create Ethers config
    const ethersConfig = defaultConfig({
      metadata,
      enableEIP6963: true, // true by default
      enableInjected: true, // true by default
      enableCoinbase: true, // true by default
      rpcUrl: '3f76c4ffb3b346059fa8b97cfb8b49b2', // used for the Coinbase SDK
      defaultChainId: 1, // used for the Coinbase SDK
    });

    // 5. Create a Web3Modal instance
    this.modal = createWeb3Modal({
      ethersConfig,
      chains: [mainnet],
      projectId,
      enableAnalytics: true, // Optional - defaults to your Cloud configuration
      enableOnramp: true, // Optional - false as default
    });

    console.log('Web3Modal initialized');
  },
};
</script>
