<template>
    <div class="hello">
        <div class="form">
            <p><input type="text" placeholder="Título" class="entrada" v-model="artigo.title"></p>
            <p><textarea class="entrada" placeholder="Descrição" v-model="artigo.description"></textarea></p>
            <p><input type="text" placeholder="Pôster" class="entrada" v-model="artigo.image_url"></p>
            <p><input type="text" placeholder="Trailer" class="entrada" v-model="artigo.trailer_url"></p>
            <p>
                <button v-if="editar" @click="cadastrarArtigos">Editar</button>
                <button v-else @click="cadastrarArtigos">Cadastrar</button>
            </p>
        </div>

        <div class="card">
            <div class="post" v-for="artigo in artigos" v-bind:key="artigo.id">
                <div class="text-post">
                    <h3>Título: {{ artigo.title }}</h3>
                    <p>Descrição: {{ artigo.description }}</p>
                    <p>Trailer: <a v-bind:href="artigo.trailer_url" target="_blank">{{ artigo.trailer_url }}</a></p>
                    <div class="button-container">
                        <p><button class="edit-button" @click="editarArtigo(artigo)">Editar</button></p>
                        <p><button class="del-button" @click="deletarArtigo(artigo._id)">Deletar</button></p>
                    </div>
                </div>
                <img v-bind:src="artigo.image_url" alt="Poster do filme">

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'VueArtigos',
    data() {
        return {
            artigos: [],
            artigo: {
                id: '',
                title: '',
                description: '',
                image_url: '',
                trailer_url: ''
            },
            editar: false
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
        cadastrarArtigos() {
            if (this.editar === false) {
                //verificação
                if (this.artigo.title == '' || this.artigo.description == '') {
                    alert('Preencha os campos vazios!!')
                    return
                }
                fetch(`http://localhost:3000/`, {
                    method: 'post',
                    body: JSON.stringify(this.artigo),
                    headers: {
                        'content-type': 'application/json'
                    }
                })
                    .then(res => res.json())
                    .catch(err => console.log(err))
                alert('Dados cadastrados com sucesso!!')
                this.fetchArtigos()
                this.artigo.title = '',
                this.artigo.description = '',
                this.artigo.image_url = '',
                this.artigo.trailer_url = ''
            } else {
                fetch(`http://localhost:3000/${this.artigo._id}`, {
                    method: 'PUT',
                    body: JSON.stringify(this.artigo),
                    headers: {
                        'content-type': 'application/json'
                    }
                })
                    .then(res => res.json())
                    .catch(err => console.log(err))
                alert('Dados atualizados com sucesso!!')
                this.fetchArtigos()
                this.artigo.title = '',
                this.artigo.description = '',
                this.artigo.image_url = '',
                this.artigo.trailer_url = ''
            }
        },

        //metodo para deletar (DELETE)
        deletarArtigo(id) {
            if (confirm('Deseja deletar o filme selecionado?')) {
                // Chamada para deletar o artigo com o ID fornecido
                fetch(`http://localhost:3000/${id}`, {
                    method: 'DELETE' // Deve ser 'DELETE'
                })
                    .then(res => res.json())
                    .then(() => {
                        // Alerta de sucesso após a exclusão
                        alert('O Filme selecionado foi deletado com sucesso!!');
                        // Recarrega os artigos após a exclusão
                        this.fetchArtigos();
                    })
                    .catch(err => console.log(err));
            }
        },

        editarArtigo(artigo) {
            this.editar = true
            this.artigo._id = artigo._id
            this.artigo.title = artigo.title
            this.artigo.description = artigo.description
            this.artigo.image_url = artigo.image_url
            this.artigo.trailer_url = artigo.trailer_url
        }

    },

    created() {
        this.fetchArtigos()
    }
}
</script>

<style scoped>
.entrada {
    width: 70%;
    padding: 10px;
    border: none;
    border-radius: 8px;
    margin: 5px;
}

.hello {
    background: #7c7b7b;
    color: #333;
    padding: 20px;
    max-width: 1200px;
    margin: 30px auto;
    border-radius: 10px;
}

.card {
    display: flex;
    flex-direction: column;
    gap: 30px;
    color: #333;
}

.post {
    background: #7c7b7b;
    display: flex;
    flex-direction: row;
    align-items: center;
}

.post a {
    color: #000000;
}

.post img {
    max-width: 200px;
}

.button-container {
    display: flex;
    flex-direction: row;
    margin-left: 400px;
    margin-top: 20px;
}

.button-container button {
    margin: 0 10px;
    padding: 10px;
    border: none;
    border-radius: 5px;
}

.form {
    padding: 10px;
}

.form button {
    padding: 10px;
    border-radius: 5px;
}

.form button:hover {
    background: #7c7b7b;
    color: #fff;
}

.edit-button:hover {
    background: #2e63e9;
}

.del-button:hover {
    background: #e92e2e;
}
</style>