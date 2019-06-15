<script context="module">
    import creditCardType from 'credit-card-type';
    import Cleave from 'cleave.js';
</script>

<script>
    // Variables Necesarias
    let FormValid = false;
    let cardColor = '';
    let numberCreditCard = '';
    let ccvCard = '';
    let monthCard = '';
    let yearCard = '';
    let tipoTarjeta = '';
    let cardUserName = '';
    let imageCard = '';
    let tarjetas = [
        {tipo: 'MasterCard', validacion: ['51','52','53','54','55'], image: 'assets/img/mastercard_icon.png', color: '#d13022'},
        {tipo: 'Visa', validacion: ['4'],image: 'assets/img/visa_icon.png', color: '#57a4d2'},
        {tipo: 'Discover', validacion: ['6'],image: 'assets/img/discover_icon.png',color: '#7d283d'},
        {tipo: 'Diners-Club', validacion: ['36','38'],image: 'assets/img/diners-club_icon.png', color: '#5d3f3c'},
        {tipo: 'American-Express', validacion: ['34','37'],image: 'assets/img/american_express_icon.png', color: '#9a9a9c'}
    ];

    // Funciones Utilizadas
    function cambiarValides(){
        FormValid = !FormValid;
    }

    function manejarNumeroTarjeta(e){
        const digitosValidar = 2;
        const valorInput = e.target.value;
        // console.log({valueActual: valorInput});
        // console.log({value2Actual: valorInput + ''});
        // console.log({objetoEvaluar: creditCardType(valorInput)[0]});
        // console.log({tipoTarjeta: creditCardType(valorInput)[0].type});
        const tarjetaEs = creditCardType(valorInput)[0].type;
        if(tarjetaEs && valorInput !== ''){
            getUrlCard(tarjetaEs);
        }else{
            imageCard = '';
            cardColor = '';
        }
     }

     function getUrlCard(cardname){
        //  console.log(cardname);
         tarjetas.forEach((card) => {
            //  const ll = card.tipo.toLowerCase;
             (card.tipo.toLowerCase() === cardname.toLowerCase()) ? imageCard = card.image: '';
             (card.tipo.toLowerCase() === cardname.toLowerCase()) ? cardColor = card.color: '';
             }
         );     
     }

     function validarForm(){
        cambiarValides();
     }
</script>

<style>
    :root{
        --card-min-width: 600px;
        --card-max-width: 700px;
        --green-color: #4e9a06;
    }
    *,**:after, **::before{
        outline: none;
        box-sizing: border-box;
    }
    /* ESTILOS FORM */
    input{
        height: calc(1.5em + .5rem + 2px);
        font-size: 1rem;
        font-weight: 400;
        line-height: 1.5;
        background-color: #fff;
        background-clip: padding-box;
        border: 1px solid #ced4da;
        border-radius: .25rem;
        padding: .375rem .75rem;
        color: #495057;
    }
    input:focus{       
        color: #495057;
        background-color: #fff;
        border-color: #80bdff;
        outline: 0;
        box-shadow: 0 0 0 0.2rem rgba(0,123,255,.25);
    }
    input.small{
        width: 100px !important;
    }
    input[type="submit"],
    button {
        height: auto;
        border-radius: 10px;
        display: block;
        margin-top: 1rem;
        margin-bottom: 1rem;
        padding: .7rem;
        font-size: 1.25rem;
        line-height: 1.5;        
        cursor:pointer;
        transition: all 1s;
    }
    input[type="submit"]:hover,
    button:hover{
        transform: scale(1.03);
    }
    input[type="submit"].center{
        margin-left: auto;
        margin-right: auto;
    }
    input[type="submit"].full{
        width: 100%;
    }
    input[type="submit"].btn-success{
        color: #fff;
        background-color: var(--green-color);
        border-color: var(--green-color);
    }
    .form-group input{
        width: 100%;
    }
    label{
        display: block;
        margin-top: .8rem;
        margin-bottom: .8rem;
        font-size: 1rem;
    }    
    /*FUENTE TARJETA*/
    .font-card-main{
        font-family: 'Cutive Mono', monospace !important;       
    }
    /* TARJETA CREDITO */
    .card-owner{
        display: block;
        font-weight: bold;
        letter-spacing: 2px;
        text-shadow: 2px 2px 1px rgba(0, 0, 0, 0.3);
        font-size: 1.3em;
        margin-top: 1.8rem;
    }
    .card-number{
        font-size: 1.7em;
        font-weight: bold;
        margin-top: 1rem;
        margin-bottom: .6rem;

    }
    .card-date{
        font-size: .74rem;
        font-weight: bold;
        word-spacing: .4rem;
    }
    
    .expiration-date label{
        display: block;
    }
    .expiration-date .flex-sm input:nth-child(2){
        margin-left: 25px;
    }
    .icon-chip{
        background: url('assets/img/chip_icon.png');
        background-repeat: no-repeat;
        background-size: cover;
        background-position: center;
        display: inline-block;
        height: 50px;
        width: 50px;
    }
    .card-icon{
        display: block;
        height: 70px;
        width: 70px;
    }
	.payment-method-container{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }
    .payment-form{
        background: white;
        box-shadow: 0 0 3px #ccc;
        padding: 1rem 2rem;
        width: 40%;
        border-radius: 10px;
        margin-left: 30px;
        margin-right: 30px;
        min-width: 400px;
    }
    .container-credit-card{
        display: block;
        margin-top: auto;
        margin-bottom: auto;
        padding: 1rem;
        color: white;
        min-width: var(--card-min-width);
        max-width: var(--card-max-width);
        border-radius: 12px;
    }

    /*Utilidades*/
    .flex-sm{
        display: flex;
    }
    .flex-between{
        justify-content: space-between;
    }
    .flex-items-center{
        align-items: center;
    }    
    .success-container-message{
        display:flex;
        flex-direction: column;
        justify-content:center;
        align-items:center;
        width: 100%;
        height: 100%;
    }
    .success-container-message img{
        display: block;
        width: 150px;
    }
    .success-container-message p{
        color: #4e9a06;
        font-weight: bold;
    }
    /* media queries */
    @media (max-width: 1115px) {
        .payment-form {
            margin-top: 1.5rem !important;
        }
    }
</style>
<button on:click={cambiarValides}>Cambiar</button>
<div class="payment-method-container">
    <div class="container-credit-card" style="background: {cardColor || '#2a2a2a'}">
        <div class="front-card">
            <div class="card-header">
                <div class="flex-sm flex-between flex-items-center">
                    <h1 class="card-title" style="">Banco Bolivariano</h1>
                    <img alt="Card Icon" src='{imageCard || 'assets/img/unknown-card.png'}' class="card-icon" />
                </div>
                <div>
                    <span class="icon-chip"></span>
                </div>               
                <p class="font-card-main card-number"> {numberCreditCard || '**** **** **** ****'} </p>
                <p class="card-date">
                    <span> {monthCard || 'MM'} / </span><span> {yearCard || 'YY'} </span>
                </p>
                <p class="font-card-main card-owner">
                   {cardUserName || 'Your Name'}
                </p>
            </div>
        </div>
    </div>
    <div class="payment-form">    
        {#if !FormValid }
            <h2>Agregar un método de Pago</h2>
            <div class="form-group">
                <label for="credit_card_owner">Nombre del Dueño de la Tarjeta</label>
                <input bind:value={cardUserName} placeholder="John Doe" type="text" id="credit_card_owner">
            </div>
            <div class="form-group">
                <label for="credit_number">Número de Tarjeta</label>
                <input class="creditCardNumber" autocomplete="cc-number" type="text" placeholder="Card Number" on:keyup={manejarNumeroTarjeta} bind:value={numberCreditCard} maxlength="16">
            </div>
            <div class="expiration-date">
                <label for="credit_card_owner">Vencimiento</label>            
                <div class="flex-sm">                    
                    <input class="small" type="text" placeholder="MM" bind:value={monthCard} maxlength="2">
                    <input type="text" class="small" placeholder="AA" bind:value={yearCard} maxlength="2">                
                </div>
            </div>
            <div class="form-group">
                <label for="credit_card_owner">CCV</label>
                <input type="text" class="small" placeholder="CCV" bind:value={ccvCard} maxlength="3" id="credit_card_owner">
            </div>
            <input type="submit" on:click="{validarForm}" class="btn-success center full" value="Agregar método de pago">
        {/if}
        {#if FormValid }
            <div class="success-container-message">
                <img src="assets/img/success_icon.png" alt="Success Method Payment Icon">
                <p>El Método de Pago fue agregado correctamente</p>
            </div>
        {/if}

    
    </div>
</div>