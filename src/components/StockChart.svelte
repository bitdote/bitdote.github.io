<script lang="ts">
  import SymbolOverviewWidget from './base/SymbolOverviewWidget.svelte';
  import Tabs from './base/Tabs.svelte';
  var activeTabId = 0;

  const tabs = [
    {
      name: 'Dollar',
      id: 0,
      hasSignal: false,
    },
    {
      name: 'Gold',
      id: 1,
      hasSignal: true,
    },
    {
      name: 'Bitcoin',
      id: 2,
      hasSignal: true,
    },
  ];

  export let text: string;

  function onChangeTab(event: CustomEvent<number>) {
    activeTabId = event.detail;
  }

  const assets = [
    {
      name: 'Apple',
      symbol: 'AAPL',
    },
    {
      name: 'Tesla',
      symbol: 'TSLA',
    },
    {
      name: 'Google',
      symbol: 'GOOG',
    },
    {
      name: 'Amazon',
      symbol: 'AMZN',
    },
    {
      name: 'CocaCola',
      symbol: 'KO',
    },
    {
      name: 'MSCI World ETF',
      symbol: 'IRRRF',
    },
    {
      name: 'S&P 500 ETF',
      symbol: 'SPY',
    },
    {
      name: 'Johnson & Johnson',
      symbol: 'JNJ',
    },
    {
      name: 'Bayer AG',
      symbol: 'BAYRY',
    },
    {
      name: 'RWE',
      symbol: 'RWEOY',
    },
    {
      name: 'Tesla',
      symbol: 'TSLA',
    },
    {
      name: 'Adidas',
      symbol: 'ADDYY',
    },
    {
      name: 'Meta',
      symbol: 'FB',
    },
    {
      name: 'Alphabet',
      symbol: 'GOOGL',
    },
  ];

  const assetsInDollar = assets.map((asset) => {
    return {
      name: asset.name,
      symbol: `${asset.symbol}|ALL`,
    };
  });

  const assetsInGold = assets.map((asset) => {
    return {
      name: asset.name,
      symbol: `${asset.symbol}/XAUUSD|ALL`,
    };
  });

  const assetsInBtc = assets.map((asset) => {
    return {
      name: asset.name,
      symbol: `${asset.symbol}/BTCUSD|ALL`,
    };
  });
</script>

<Tabs {text} {tabs} on:tabChanged={onChangeTab}>
  <div class="h-72 relative lg:h-96">
    <div class="h-full top-0 left-0 absolute w-full slide" class:show={activeTabId == 0}>
      <SymbolOverviewWidget assets={assetsInDollar} chartOnly={true} copyright={false} />
    </div>
    <div class="h-full top-0 left-0 absolute w-full slide" class:show={activeTabId == 1}>
      <SymbolOverviewWidget assets={assetsInGold} chartOnly={true} copyright={false} />
    </div>
    <div class="h-full top-0 left-0 absolute w-full slide" class:show={activeTabId == 2}>
      <SymbolOverviewWidget assets={assetsInBtc} chartOnly={true} copyright={false} scaleMode="Logarithmic" />
    </div>
  </div>
</Tabs>

<style>
  .slide {
    transition: transform 0.3s ease-in-out;
    transform: translateX(-100%);
  }

  .slide.show {
    transform: translateX(0%);
  }
</style>
