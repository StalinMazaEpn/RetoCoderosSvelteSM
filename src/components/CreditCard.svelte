<script>
    let tarjetas = [
        {tipo: 'MasterCard', validacion: ['51','52','53','54','55']},
        {tipo: 'Visa', validacion: ['4']},
        {tipo: 'Discovery', validacion: ['6']},
        {tipo: 'Diners Club', validacion: ['36','38']},
        {tipo: 'American Express', validacion: ['34','37']}
    ];
    let numberCreditCard = '';
    let ccvCard = '';
    let monthCard = '';
    let yearCard = '';
    let tipoTarjeta = '';

    export let name2;
    function getNumbersCard(array){    
        let newArray = [];
        let stringCard = '';
        for(let i = 0; i < array.length; i++){
            const valorActual = array[i];
            stringCard = stringCard + valorActual; 
            console.log(numberCardArr[i]);
            if((i+1) % 4 === 0){
                console.log('Valor: ' , stringCard);
                newArray.push(stringCard);
                stringCard = '';
            }
        }
        return newArray;
    }
    let name = '';
    let numberCard = '4697720585000063';
    let numberCard2 = '4';
    let numberCardArr = numberCard.split("");
    let numberCardArr2 = numberCard2.split("");
    // console.log({arr: numberCardArr});
    // console.log({numberCards: getNumbersCard(numberCardArr)});
    //  console.log({numberCards: getNumbersCard(numberCardArr2)});

     function manejarNumeroTarjeta(e){
        //  console.log(e);
        const digitosValidar = 2;
        const valorInput = e.target.value;
        const valorComparar = valorInput.substr(0,digitosValidar);
        console.log({valorCompar: valorComparar});
        if(valorInput.length >= 16 ){
            return;
        }
        if(valorComparar == ''){
            tipoTarjeta = '';
            return;
        }
        // console.log(e.target.value);
        // let tipoTarjeta = null;
        tarjetas.forEach((tarjeta) => {
            // console.log(tarjeta.tipo);
            const tarjetaActual = tarjeta;
            tarjetaActual.validacion.forEach(validacion=>{
                if(validacion.indexOf(valorComparar) > -1){
                    // console.log("La tarjeta es: ", tarjetaActual.tipo);
                    tipoTarjeta = tarjetaActual.tipo;
                    return;
                }else{
                    //  console.log("La tarjeta no es: ", tarjetaActual.tipo);
                }
            });
        });
        (tipoTarjeta) ? console.log('TARJETA ES: ', tipoTarjeta) : console.log('no coincide con ninguna');
     }
</script>

<style>
    .font-card-main{
        font-family: 'Cutive Mono', monospace !important;       
    }
    .card-owner{
        font-weight: bold;
        letter-spacing: 2px;
        text-shadow: 2px 2px 1px rgba(0, 0, 0, 0.3);
        font-size: 1.3em;
    }
    .card-number{
        font-size: 1.3em;
    }
    .card-date{
        font-size: .72rem;
    }
    .form-group input{
        width: 100%;
    }
	.payment-method-container{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }
    .payment-form{
        width: 30%;
    }
    .container-credit-card{
        background: black;
        color: white;
        min-width: 450px;
        max-width: 500px;
        border-radius: 12px;
        /* height: 100%; */
    }
    .two{
        display: flex;
    }
    .flex-sm{
        display: flex;
    }
    .flex-between{
        justify-content: space-between;
    }
    .w100{
        width: 100%;
    }
    .d-block{
        display: block;
    }
    .ss{margin-left: 30px;margin-right: 30px;}
    .card-icon,
    .icon-chip{

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
</style>

<div class="payment-method-container">
    <div class="container-credit-card">
        <div class="front-card">
            <div class="ss">
                <div class="flex-sm" style="justify-content: space-between;align-items:center;">
                    <h1 class="card-title" style="">Bank Name</h1>
                    <img alt="" src="assets/img/visa_icon.png" class="card-icon" />
                </div>
                <div class="flex">
                    <span class="icon-chip"></span>
                </div>
               
                 <p class="font-card-main card-number"> {numberCreditCard || '**** **** **** ****'} </p>
                <p class="card-date">
                    <span> {monthCard || 'MM'} / </span>
                    <span> {yearCard || 'YYYY'} </span>
                </p>
                <p>{ccvCard || '***'}</p>
                <p>{tipoTarjeta || 'none'}</p>
                <p class="font-card-main card-owner credit-card-footer">
                   Juan Antonio
                </p>
            </div>
        </div>
    </div>
    <div class="payment-form" style="margin-left: 30px;margin-right: 30px;">
        <div class="form-group">
            <label for="credit_number">Número de Tarjeta</label>
            <input type="text" id="credit" on:keyup={manejarNumeroTarjeta} bind:value={numberCreditCard} maxlength="16">
        </div>
        <div class="form-group">
            <label for="credit_card_owner">Nombre del Tarjeta Habiente</label>
            <input type="text" id="credit_card_owner">
        </div>
        <div class="xx">
            <label for="credit_card_owner">Vencimiento</label>
           
            <div class="flex-sm d">
                
                    <input type="text" placeholder="MM" style="width: 100px" id="credit_card_owner" bind:value={monthCard} maxlength="2">
                    <input type="text" placeholder="AAAA" style="margin-left: 20px;width: 100px" id="credit_card_owner" bind:value={yearCard} maxlength="4">
              
            </div>
        </div>
         <div class="form-group">
            <label for="credit_card_owner">CCV</label>
            <input type="text" bind:value={ccvCard} maxlength="3" id="credit_card_owner">
        </div>
            <input type="submit" value="Agregar método de pago">

    
    </div>
</div>