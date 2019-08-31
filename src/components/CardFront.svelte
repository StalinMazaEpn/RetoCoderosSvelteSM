<script>
  import IconCard from "./IconCard.svelte";
  export let color;
  export let image;
  export let numberCreditCard;
  export let monthCard;
  export let yearCard;
  export let cardUserName;
</script>

<style>
  
</style>

<div class="container-credit-card" style="background: {color || '#2a2a2a'}">
  <div class="front-card">
    <div class="card-header">
      <div class="flex-sm flex-between flex-items-center">
        <h1 class="card-title" style="">Banco Bolivariano</h1>
        <IconCard src={image} />
      </div>
      <div>
        <span class="icon-chip" />
      </div>
      <p class="font-card-main card-number">
         {numberCreditCard || '**** **** **** ****'}
      </p>
      <p class="card-date">
        <span> {monthCard || 'MM'} /</span>
        <span> {yearCard || 'YY'} </span>
      </p>
      <p class="font-card-main card-owner"> {cardUserName || 'Your Name'} </p>
    </div>
  </div>
</div>
