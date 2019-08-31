 <script>
    export let src;
 </script>

 <style>
 .card-icon{
        display: block;
        height: 70px;
        width: 70px;
    }
 
 </style>
 
 <img alt="Card Icon" src='{src || 'assets/img/unknown-card.png'}' class="card-icon" />