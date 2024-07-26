<script>
    export let message = 'Message Sent! ';
    export let type = 'info';
    let additionalText = "Thanks for completing the form. We'll be in touch soon!"
</script>
<main>

</main>
<style>
    .alert {
        height: 70px;
        padding: 15px;
        margin: -20px;
        border-radius: 10px;
        font-size: 16px;
        position: fixed;
        top: 30px;
        left: 51%;
        transform: translateX(-50%);
        z-index: 1000;
        width: 300px;
        text-align: left;
        gap: 20px;
        justify-content: left;
        
        
    }
    .info {
        justify-content: top;
        font-family: Karla;
        color: hsl(0, 0%, 100%);
        background-color: hsl(187, 24%, 22%);
        border: 1px solid #bce8f1;
    }
    .success {
        background-color: #dff0d8;
        color: #3c763d;
        border: 1px solid #d6e9c6;
    }
    .error {
        background-color: #f2dede;
        color: #a94442;
        border: 1px solid #ebccd1;
    }
    .alert img {
        width: 20px;
        height: 20px;
    }
    .alert .additional-text {
        margin-top: 10px;
        font-size: 14px;
        color: hsl(186, 15%, 59%);
    }

</style>

<div class={`alert ${type}`}>
    
    <img src="src\assets\icon-success-check.svg" alt="alert icon"/>
    <span>{message}</span>
    {#if additionalText}
    <div class="additional-text">{additionalText}</div>
    {/if}
</div>
