<script lang="ts">
  import SymbolOverviewWidget from './../base/SymbolOverviewWidget.svelte';
  import Tabs from './../base/Tabs.svelte';

  var activeTabId = 0;

  const tabs = [
    {
      name: 'Linear',
      id: 0,
      hasSignal: false,
    },
    {
      name: 'Log',
      id: 1,
      hasSignal: true,
    },
  ];

  export let text: string;

  function onChangeTab(event: CustomEvent<number>) {
    activeTabId = event.detail;
  }

  let assets = [
    {
      name: 'Dollar in Gold',
      symbol: 'USD/XAU|ALL',
    },
    {
      name: 'Dollar in Bitcoin',
      symbol: 'USD/BTCUSD|ALL',
    },
    {
      name: 'Gold in Dollar',
      symbol: 'XAU/USD|ALL',
    },
    {
      name: 'Gold in Bitcoin',
      symbol: 'XAU/BTCUSD|ALL',
    },
    {
      name: 'Bitcoin in Dollar',
      symbol: 'BTCUSD|ALL',
    },
    {
      name: 'Bitcoin in Gold',
      symbol: 'BTCUSD/XAU|ALL',
    },
  ];
</script>

<Tabs {text} {tabs} on:tabChanged={onChangeTab}>
  <div class="h-72 relative lg:h-96">
    <div class="h-full top-0 left-0 absolute w-full slide" class:show={activeTabId == 0}>
      <SymbolOverviewWidget dateRanges={['all|1M']} {assets} chartOnly={true} copyright={false} />
    </div>
    <div class="h-full top-0 left-0 absolute w-full slide" class:show={activeTabId == 1}>
      <SymbolOverviewWidget
        dateRanges={['all|1M']}
        {assets}
        chartOnly={true}
        copyright={false}
        scaleMode={'Logarithmic'}
      />
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
