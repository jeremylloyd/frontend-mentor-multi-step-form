
<svelte:head>
  <title>Multi-step form</title>
  <link rel="icon" type="image/png" sizes="32x32" href="images/favicon-32x32.png">
</svelte:head>

<script>
  import Paginator from './Paginator.svelte';
  import TextInput from './TextInput.svelte';
  import Button from './Button.svelte';
  import ButtonSubmit from './ButtonSubmit.svelte';
  import CardPlan from './CardPlan.svelte';
  import SwitchLabelled from './SwitchLabelled.svelte'
  import CardAddon from './CardAddon.svelte'

  let switchChecked;
  
  let pages = [
    'Your info',
    'Select plan',
    'Add-ons',
    'Summary',
  ]

  let plans = {
    'arcade': {
      'alias': 'Arcade',
      'rate': {
        'month': 9,
        'year': 90,
      },
      'icon': 'images/icon-arcade.svg',
    },
    'advanced': {
      'alias': 'Advanced',
      'rate': {
        'month': 12,
        'year': 120,
      },
      'icon': 'images/icon-advanced.svg',
    },
    'pro': {
      'alias': 'Pro',
      'rate': {
        'month': 15,
        'year': 150,
      },
      'icon': 'images/icon-pro.svg',
    },
  }

  let addons = [
    {
      'id': 0,
      'name': 'Online service',
      'description': 'Access to multiplayer games',
      'rate': {
        'month': 1,
        'year': 10
      },
      'selected': false,
    },
    {
      'id': 1,
      'name': 'Larger storage',
      'description': 'Extra 1TB of cloud save',
      'rate': {
        'month': 2,
        'year': 20
      },
      'selected': false,
    },
    {
      'id': 2,
      'name': 'Customizable Profile',
      'description': 'Custom theme on your profile',
      'rate': {
        'month': 2,
        'year': 20
      },
      'selected': false,
    },
  ]

  let page = 1;
  let plan = null;
  let addonsSelected;

  $: paymentFrequency = switchChecked ? 'year' : 'month';
  $: addonsSelected = addons.filter(ao => ao.selected)
  $: pageSelected = Math.min(4, page);
  $: console.log(`Plan selected: ${plan}`);
  $: console.log(`Add-ons selected: ${addonsSelected}`);

  const incrementPage = () => {
    page += 1;
  }

  const decrementPage = () => {
    page -= 1;
  }
</script>

<div class="container-centred">
  <div class="page">
    <header class="page__header">
      <img class="page__bg page__bg--mobile" src="images/bg-sidebar-mobile.svg" alt="background-mobile">
      <img class="page__bg page__bg--desktop" src="images/bg-sidebar-desktop.svg" alt="background-desktop">
      <Paginator pages={pages} bind:pageSelected/>
    </header>
  
    <div class="page__contents" class:hidden={page != 1}>
      <main class="page__main">
        <h2 class="page__title">Personal info</h2>
        <p class="page__desc">Please provide your name, email address, and phone number.</p>
        <form class="page__form" id="form__info" method=post on:submit|preventDefault={incrementPage}>
          <TextInput name="name" label="Name" placeholder="e.g. Stephen King"/>
          <TextInput name="email" type="email" label="Email Address" placeholder="e.g. stephenking@lorem.com"/>
          <TextInput name="phone" type="tel" label="Phone Number" placeholder="e.g. +1 234 567 890"/>
        </form>
      </main>
    
      <footer class="page__footer">
        <div></div>
        <ButtonSubmit form="form__info">Next Step</ButtonSubmit>
      </footer>
    </div>
    
    <div class="page__contents" class:hidden={page != 2}>
      <main class="page__main">
        <h2 class="page__title">Select your plan</h2>
        <p class="page__desc">You have the option of monthly or yearly billing.</p>
        <form class="page__form" id="form__plan" method=post on:submit|preventDefault={incrementPage}>
          <CardPlan inputId='arcade' plan={plans['arcade']} paymentFrequency={paymentFrequency} bind:selected={plan}></CardPlan>
          <CardPlan inputId='advanced' plan={plans['advanced']} paymentFrequency={paymentFrequency} bind:selected={plan}></CardPlan>
          <CardPlan inputId='pro' plan={plans['pro']} paymentFrequency={paymentFrequency} bind:selected={plan}></CardPlan>
        </form>
        
        <SwitchLabelled bind:checked={switchChecked}/>
      </main>
      
      <footer class="page__footer">
        <Button on:click={decrementPage} variant="light">Go Back</Button>
        <!-- <Button on:click={incrementPage}>Next Step</Button> -->
        <ButtonSubmit form="form__plan">Next Step</ButtonSubmit>
      </footer>
    </div>
  
    <div class="page__contents" class:hidden={page != 3}>
      <main class="page__main">
        <h2 class="page__title">Pick add-ons</h2>
        <p class="page__desc" id="page__desc--addons">Add-ons help enhance your gaming experience.</p>
  
        {#each addons as addon}
          <CardAddon bind:addon={addon} paymentFrequency={paymentFrequency}/>
        {/each}
      </main>
    
      <footer class="page__footer">
        <Button on:click={decrementPage} variant="light">Go Back</Button>
        <Button on:click={incrementPage}>Next Step</Button>
      </footer>
    </div>
  
    <div class="page__contents" class:hidden={page != 4}>
      <main class="page__main">
        <h2 class="page__title">Finishing up</h2>
        <p class="page__desc">Double-check everything looks OK before confirming.</p>
        <div class="summary">
          <div class="summary__items">
            <div class="summary__plan">
              <div class="flex-col">
                <h3 class="summary__title">{plans[plan]?.alias} ({paymentFrequency == "month" ? 'Monthly' : 'Yearly'})</h3>
                <a href="./" class="summary__link" on:click={() => page = 2}>Change</a>
              </div>
              <div class="summary__price summary__price--strong">${plans[plan]?.rate[paymentFrequency]}/{paymentFrequency == 'month' ? 'mo' : 'yr'}</div>
            </div>
            <div class="summary__sep"></div>
            <div class="summary__addons">
              <div class="flex-col">
                {#each addonsSelected as ao}
                  <div class="summary__addon">
                    <p>{ao.name}</p>
                    <div class="summary__price">+${ao.rate[paymentFrequency]}/{paymentFrequency == 'month' ? 'mo' : 'yr'}</div>
                  </div>
                {/each}
                  
                {#if addonsSelected.length == 0}
                  <div class="summary__addon">
                    <p>No add-ons selected</p>
                    <div class="summary__price"></div>
                  </div>
                {/if}
              </div>
            </div>
          </div>
          <div class="summary__total">
            <p>Total (per year)</p>
            <div class="summary__price summary__price--strong summary__price--primary">
              ${plans[plan]?.rate[paymentFrequency] + addonsSelected.reduce((partialSum, ao) => partialSum + ao.rate[paymentFrequency], 0)}/{paymentFrequency == 'month' ? 'mo' : 'yr'}
            </div>
          </div>
        </div>
      </main>
    
      <footer class="page__footer">
        <Button on:click={decrementPage} variant="light">Go Back</Button>
        <Button on:click={incrementPage} variant="primary">Confirm</Button>
      </footer>
    </div>
  
    <div class="page__contents" class:hidden={page != 5}>
      <main class="page__main centred" style="min-height: 400px">
        <img class="page__img" src="images/icon-thank-you.svg" alt="">
        <h2 class="page__title">Thank you!</h2>
        <p class="page__desc">
          Thanks for confirming your subscription! We hope you have fun 
          using our platform. If you ever need support, please feel free 
          to email us at support@loremgaming.com.
        </p>
      </main>
    </div>
  </div>
</div>
