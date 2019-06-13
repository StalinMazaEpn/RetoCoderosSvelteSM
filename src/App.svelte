        <script>
    import CreditCard from './components/CreditCard.svelte';
	// export let name2;
    let name = '';
</script>

<style>
	h1 {
		color: purple;
    }
    .container-sm{
        display: block;
        width: 100%;
        /* margin-left: 20px;
        margin-right: 20px; */
        /* height: 250px; */
        background: lime;
    }
</style>

<div class="container-sm">
    <h1>Nuevo método de Pago</h1>
    <CreditCard/>
</div>