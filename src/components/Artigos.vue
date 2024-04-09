<template>
    <div class="hello">

        <div class="form">
            <p><input type="text" placeholder="Insira o titulo do filme" class="entrada" v-model="artigo.title"></p>
            <p><textarea class="entrada" placeholder="Insira a descrição do filme" v-model="artigo.description"></textarea></p>
            <p><button class="sucess" @click="cadastrarArtigos">Cadastrar</button></p>
        </div>

        <div class="card">
            <div class="post"  v-for="artigo in artigos" v-bind:key="artigo.id">
                <h3>Título: {{ artigo.title }}</h3>
                <p>Descrição: {{ artigo.description }}</p>
                <!-- <img src="{{ artigo.image_url }}" alt="poster do filme">
                <a href="{{ artigo.trailer_url }}">Trailer</a> -->
                <p><button class="del-button" @click="deletarArtigo(artigo.id)">Deletar</button></p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'VueArtigos',
    data(){
        return {
            artigos: [],
            artigo: {
                id: '',
                title: '',
                description: ''
            }
        }
    },

    methods: {
        //metodo para acessar a lista de filmes (GET)
    fetchArtigos() {
        fetch(`http://localhost:3000/`)
            .then(res => res.json())
            .then(data => {
                this.artigos = data; // Atribuir diretamente os dados ao array artigos
            })
            .catch(err => console.error('Erro ao buscar artigos:', err));
    },

    //metodo para cadastrar na lista de filmes (POST)
    cadastrarArtigos(){
        //verificação
        if( this.artigo.title == '' || this.artigo.description == ''){
            alert('Preencha os campos de título e descrição!!')
            return
        }
        fetch(`http://localhost:3000/`,{
            method:'post',
            body: JSON.stringify( this.artigo ),
            headers: {
                'content-type':'application/json'
            }
        })
        .then( res => res.json())
        .catch( err => console.log( err ))
        alert('Dados cadastrados com sucesso!!')
        this.fetchArtigos()
        this.artigo.title = '',
        this.artigo.description = ''
    }

    //metodo para deletar (DELETE)
    // deletarArtigo( id ){
    //     if(confirm('Deseja deletar o filme selecionado?')){
    //         alert('Agora sim!')
    //         fetch(`http://localhost:3000/${id}`, {
    //             method: 'delete'
    //         })
    //         .then( res => res.json())
    //         .catch( err => console.log( err ))
    //         alert('O Filme selecionado foi deletado com sucesso!!')
    //         this.fetchArtigos()
    //     }
    // }
    },

    created(){
        this.fetchArtigos()
    }
}
</script>

<style scoped>
.entrada{
    width: 70%;
    padding: 10px;
    border-radius: 8px;
    margin: 5px;
}

.hello{
    color: #333;
    padding: 20px;
    max-width: 1200px;
    margin: auto;
}

.card{
    background-color: #fff;
    color: #333;
}

.post{
    border: 1px solid silver;
    padding: 10px;
}

.post a{
    color: #333;
}
</style>