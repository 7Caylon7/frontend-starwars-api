<template>
    <div class="footer">
        <div class="left-footer">
            <h2>Contato:</h2>
            <div class="links">
                <a href="https://www.linkedin.com/in/caylon-solon-monte-costa-10624823b" target="_blank"><span class="pi pi-linkedin"><strong> Linkedin</strong></span></a>
                <a href="https://github.com/7Caylon7" target="_blank"><span class="pi pi-github"><strong> Github</strong></span></a>
                <a href="https://www.instagram.com/ca_ylon" target="_blank"><span class="pi pi-instagram"><strong> Instagram</strong></span></a>
            </div>
        </div>

        <div class="right-footer">
            <h2>₢ 2024 - Caylon Solon</h2>
            <p>Todos os direitos reservados</p>
        </div>
    </div>
</template>

<script>
export default {
    name:'VueFooter'
}
</script>

<style>
.footer{
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    gap: 400px;
    background: #000000;
    color: #abb2bf;
    padding: 50px;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}


.footer a {
    color: #abb2bf;
    display: flex;
    flex-direction: column;
    margin-top: 10px;
}

@media screen and (min-width: 300px) and (max-width: 840px){
    .footer{
    display: flex;
    flex-direction: column;
    gap: 30px;
}
}

</style>