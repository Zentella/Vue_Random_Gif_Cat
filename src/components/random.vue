<template>
  <div class="pag">
      <h1>Random Gif Cat</h1>
      <div class="main">   
        <ol class="lista">        
            <li><label>Título: </label><input v-model="titulo"/></li>            
            <li class="Filtro"><label>Filtro: </label>
             <select @change="cambioFiltro($event)"> 
                <option v-for="(filtro, index) in filtros" :key="index" :value="filtro" v-text="filtro"></option> 
            </select> 
            <!--<select  v-model="filtro" id="filtro">
                <option value="sepia">sepia</option>
                <option value="blur">blur</option>
                <option value="mono">mono</option>
                <option value="negative">negative</option>
                <option value="paint">paint</option>
                <option value="pixel">pixel</option>            
            </select>-->
            </li>
            <li class="Color"><label>Color: </label>
            <select @change="cambioColor($event)"> 
                <option v-for="(item, index) in colores" :key="index" :value="item.color" v-text="item.texto"></option> 
            </select> 
            <!--<select   v-model="color" id="color">
                <option value="red">rojo</option>
                <option value="green">verde</option>
                <option value="yellow">amarillo</option>
                <option value="blue">azul</option>
                <option value="white">blanco</option>
                <option value="black">negro</option>
                <option value="orange">salmón</option>
                <option value="brown">café</option>
                <option value="pink">rosa</option>
                <option value="gray">gris</option>
            </select>-->
            <div :style="[styleObject, {background: color}]"></div><!--style v-bind o :style-->
            </li>
            <li><label>Tamaño: </label><input type="number" v-model="tamano"/></li><!--input type="number" para solo ingresar numeros y no hacer la expresion regular-->
        </ol>           
      </div>   
      <button @click="buscar">Obtener mi gatito</button>  
        <img class="cat" :src="clip">
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
        filtros: ['blur','mono','sepia','negative','paint','pixel'],
        colores: [// array de objetos
            {color: 'red', texto: 'rojo'},//item (primera pasada) item.texto=rojo item.color=red
            {color: 'green', texto: 'verde'},
            {color: 'blue', texto: 'azul'},
            {color: 'white', texto: 'blanco'},
            {color: 'green', texto: 'verde'},
        ],
        titulo: 'Miau',
        tamano: '30',
        filtro: 'sepia',
        color: 'red',
        clip: '',
        styleObject: {
            height:'30px',
            width:'30px',  
            borderRadius:'50%',//redondea bordes para convertir el cuadrado en circulo
            mozBorderRadius:'50px',
            webkitBorderRadius:'50px',
            margin: '-5% 0 0 105%',
        },
    };
  },
      

  created() {
    fetch(`https://cataas.com`)
      .then((response) => {
          this.clip = `https://cataas.com/cat/gif/says/Miau?filter=sepia&color=red&size=30`
      });
  },
  computed: {
    gif(){
        return this.clip            
    },
        
  },
  methods:{
        buscar(){
            var url = `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamano}`
            this.clip = url

            /*fetch(`https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamano}`)
            .then((response) => {
                this.clip = `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamano}`
            });*/
        },
        cambioFiltro(event){//($event)
            this.filtro = event.target.value
        },
        cambioColor(event){//($event)
            this.color = event.target.value
        },

    }   
};
</script>

<style scoped>
.pag {
    color: black;
    text-align: center;
    padding-top: 30px;
}
.main {
    background: rgb(236, 132, 132);
}
.lista {
    list-style: none;
}
li {
    padding: 8px 0;
    margin: 10px 400px 10px 0;
    text-align: right;
    font-size: 22px;
}
.Filtro {
    padding: 10px 0;
    margin: 0px 515px 0px 0;
    text-align: right;
}
.Color {
    padding: 10px 0;
    margin: 0px 518px 0px 0;
    text-align: right;
}
button {
    position: absolute;
    margin: 0% 0px 0% 4%;
}
img {
    margin: 4% 0px 0px 0px;
}
</style>