<script context="module">
    //import { flip } from 'svelte/animate';
    import creditCardType from 'credit-card-type';
    import IconCard from './IconCard.svelte';
    import { fade } from 'svelte/transition';
</script>

<script>
    // Variables Necesarias
    let FormValid = false;    
    let cardCredit = {
        color: '',
        image: '',
        type: ''
    };
    let cardForm = {
        numberCreditCard: '',
        ccvCard: '',
        cardUserName : '',
        monthCard: '',
        yearCard: ''
    };
    let tarjetas = [
        {tipo: 'MasterCard', image: 'assets/img/mastercard_icon.png', color: '#d13022'},
        {tipo: 'Visa',image: 'assets/img/visa_icon.png', color: '#57a4d2'},
        {tipo: 'Discover',image: 'assets/img/discover_icon.png',color: '#bf6078'},
        {tipo: 'Diners-Club',image: 'assets/img/diners-club_icon.png', color: '#9ee4c7'},
        {tipo: 'American-Express',image: 'assets/img/american_express_icon.png', color: '#c8b1f5'}
    ];
    // Funciones Utilizadas
    function cambiarValides(){
        FormValid = !FormValid;
    }

    function cc_format(value) {
        var v = value.replace(/\s+/g, '').replace(/[^0-9]/gi, '')
        var matches = v.match(/\d{4,16}/g);
        var match = matches && matches[0] || ''
        var parts = []

        for (let i=0, len=match.length; i<len; i+=4) {
            parts.push(match.substring(i, i+4))
        }

        if (parts.length) {
            return parts.join(' ')
        } else {
            return value
        }
    }

    function manejarNumeroTarjeta(e){
        console.log("---------------");
        const valorInput = e.target.value;
        console.log("Valor", valorInput);
        console.log(e.target);
        console.log(valorInput.length);
        let valueFormatted = cc_format(valorInput);
        const valueCheckCard = valueFormatted.replace(/ /g, "");

        if(valorInput){
           // console.log({typeCard: creditCardType(valorInput)});
            const validarTipoCard = creditCardType(valueCheckCard);
            
            if(validarTipoCard.length > 0){
                const tarjetaEs = creditCardType(valorInput)[0].type;
                if(tarjetaEs && valorInput !== ''){
                    getUrlCard(tarjetaEs);
                }else{
                    cardCredit.image = '';
                    cardCredit.color = '';
                }
            }else{
                    cardCredit.image = '';
                    cardCredit.color = '';
                }
        }

        console.log(valueFormatted);
        console.log("---------------");
        e.target.value = valueFormatted;
     }
     function getUrlCard(cardname){
         tarjetas.forEach((card) => {
             (card.tipo.toLowerCase() === cardname.toLowerCase()) ? cardCredit.image = card.image: '';
             (card.tipo.toLowerCase() === cardname.toLowerCase()) ? cardCredit.color = card.color: '';
             }
         );     
     }
     function validarForm(e){
         if(cardForm.numberCreditCard !== '' && cardForm.ccvCard !== ''
         && cardForm.cardUserName !== ''
         && cardForm.monthCard!== ''
         && cardForm.yearCard !== ''){
             FormValid = true;
         }else{
             alert("Formulario No Valido");
         }
       
     }
</script>

<style>
:root{
    --card-min-width: 600px;
    --card-max-width: 700px;
    --green-color: #4e9a06;
    --red-color: #dc3545;
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
.form-group input.error{
    border-color: var(--red-color);
}
 .form-group input.success{
    border-color: var(--green-color);
}
small.error{
    display: block;
    color: var(--red-color);
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
.expiration-date .flex-sm div:nth-child(2){
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
.payment-form .grid-form{
    display:grid;
    grid-template-columns: 1fr;
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
    height: 300px;
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

.container-credit-card {
    display: block;
    margin-top: auto;
    margin-bottom: auto;
    padding: 1rem;
    color: white;
    min-width: var(--card-min-width);
    max-width: var(--card-max-width);
    border-radius: 12px;
    height: 300px;
  }
  .icon-chip {
    background: url("assets/img/chip_icon.png");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    display: inline-block;
    height: 50px;
    width: 50px;
  }
  .card-number {
    font-size: 1.7em;
    font-weight: bold;
    margin-top: 1rem;
    margin-bottom: 0.6rem;
  }
  .card-date {
    font-size: 0.74rem;
    font-weight: bold;
    word-spacing: 0.4rem;
  }
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
         width: auto !important;
    }
    .payment-form .grid-form{
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
       
    }
}    
</style>
<!--<button on:click={cambiarValides}>Cambiar</button>-->
<div class="payment-method-container">
    <div class="container-credit-card" style="background: {cardCredit.color || '#2a2a2a'}">
        <div class="front-card">
            <div class="card-header">
                <div class="flex-sm flex-between flex-items-center">
                    <h1 class="card-title" style="">Banco Bolivariano</h1>
                    <IconCard src={cardCredit.image}/>
                </div>
                <div>
                    <span class="icon-chip"></span>
                </div>               
                <p class="font-card-main card-number"> {cardForm.numberCreditCard || '**** **** **** ****'} </p>
                <p class="card-date">
                    <span> {cardForm.monthCard || 'MM'} / </span><span> {cardForm.yearCard || 'YY'} </span>
                </p>
                <p class="font-card-main card-owner">
                   {cardForm.cardUserName || 'Your Name'}
                </p>
            </div>
        </div>
    </div>
    <!-- <CardFront color={cardCredit.color} image={cardCredit.image} numberCreditCard={cardForm.numberCreditCard}
    monthCard={cardForm.monthCard} yearCard={cardForm.yearCard} cardUserName={cardForm.cardUserName}/> -->
    <div class="payment-form">    
        {#if !FormValid }
        <div>
            <h2>Agregar un método de Pago</h2>
            <div class="grid-form">
                <div class="form-group">
                    <label for="credit_card_owner">Nombre del Dueño de la Tarjeta</label>
                    <input bind:value={cardForm.cardUserName} placeholder="John Doe" type="text" id="credit_card_owner">
                </div>
                <div class="form-group">
                    <label for="credit_number">Número de Tarjeta</label>
                    <input class="creditCardNumber" autocomplete="cc-number" type="text" placeholder="Card Number" on:keyup={manejarNumeroTarjeta} bind:value={cardForm.numberCreditCard}>
                </div>
                <div class="expiration-date">
                    <label for="credit_card_owner">Vencimiento</label>            
                    <div class="flex-sm">                    
                        <div>
                            <input class="small" type="text" placeholder="MM" bind:value={cardForm.monthCard} maxlength="2">
                        </div>
                        <div>
                            <input type="text" class="small" placeholder="AA" bind:value={cardForm.yearCard} maxlength="2">
                        </div>
                          
                    </div>
                </div>
                <div class="form-group">
                    <label for="credit_card_owner">CCV</label>
                    <input type="text" class="small success" placeholder="CCV" bind:value={cardForm.ccvCard} maxlength="3" id="credit_card_owner">
                </div>
            </div>
            <input type="submit" on:click="{validarForm}" class="btn-success center full" value="Agregar método de pago">
        </div>
            
        {/if}
        {#if FormValid }
            <div class="success-container-message" transition:fade="{{ duration: 2000 }}">
                <img src="assets/img/success_icon.png" alt="Success Method Payment Icon">
                <p>El Método de Pago fue agregado correctamente</p>
            </div>
        {/if}

    
    </div>
</div>