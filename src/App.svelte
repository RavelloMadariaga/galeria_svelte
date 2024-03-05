<script>

import { onMount } from 'svelte';

let lightbox ;
let imagenActiva ;
let imagenes ;

onMount(() => {
		
    lightbox = document.getElementById('contenedor-principal');
    imagenActiva = document.getElementById('img-activa');
    imagenes = document.querySelectorAll('#galeria img');
	});

let indiceImagen = 0;

function abreLightbox(event){
  imagenActiva.src = event.target.src;
  lightbox.style.display = 'flex';
  indiceImagen = Array.from(imagenes).indexOf(event.target);

};

function btnCierra() {
  lightbox.style.display = 'none';
};

function adelantaImagen(){
  if (indiceImagen === imagenes.length - 1) {
    indiceImagen = -1;
  }
  imagenActiva.src = imagenes[indiceImagen + 1].src;
  indiceImagen++;
};

function retrocederImagen() {
  if (indiceImagen === 0) {
    indiceImagen = imagenes.length;
  }
  imagenActiva.src = imagenes[indiceImagen - 1].src;
  indiceImagen--;
};

const images = [
		{
			url: "https://imagenes.20minutos.es/files/image_1920_1080/uploads/imagenes/2023/07/12/6-florencia-italia.jpeg",
			alt: 'Atributo ALT de ejemplo para la imagen #1',
		},
		{
			url: 'https://a.cdn-hotels.com/gdcs/production40/d811/5e89ad90-8f10-11e8-b6b0-0242ac110007.jpg?impolicy=fcrop&w=800&h=533&q=medium',
			alt: 'Atributo ALT de ejemplo para la imagen #2',
		},
		{
			url: 'https://www.turismoenvenecia.com/wp-content/uploads/2021/05/plaza-de-san-marcos.jpg',
			alt: 'Atributo ALT de ejemplo para la imagen #1',
		},
    {
			url: 'https://norte-verde.cl/wp-content/uploads/2021/09/ver.jpg',
			alt: 'Atributo ALT de ejemplo para la imagen #1',
		},
    {
			url: 'https://http2.mlstatic.com/D_NQ_NP_946246-MLC51509928986_092022-O.webp',
			alt: 'Atributo ALT de ejemplo para la imagen #1',
		},
    {
			url: 'https://notaboutthemiles.com/wp-content/uploads/2022/05/Ravello-Italy-2.jpg',
			alt: 'Atributo ALT de ejemplo para la imagen #1',
		},
    {
			url: 'https://images.adsttc.com/media/images/5a09/a5a0/b22e/3824/ce00/0478/large_jpg/LAMINA_5L3.jpg?1510581656',
			alt: 'Atributo ALT de ejemplo para la imagen #1',
		},
    {
			url:"https://media.istockphoto.com/id/1495736175/es/foto/vista-a%C3%A9rea-de-winnipeg-manitoba-durante-el-verano.jpg?s=1024x1024&w=is&k=20&c=luS_ZxoRs8kkHjl0ehEPNFX8yNX_eS2lRm1_6RxYjPQ=",
			alt: 'Atributo ALT de ejemplo para la imagen #1',
		},
    {
			url: 'https://www.cdt.cl/wp-content/uploads/2021/12/Edificio-de-Providencia-utilizara%CC%81-madera-nativa-para-revestir-su-estructura-4-1024x651.jpeg',
			alt: 'Atributo ALT de ejemplo para la imagen #1',
		},
    {
			url: 'https://www.premioaporteurbano.cl/uploads/proyectos/_principal_2022/Edificio_21.jpg',
			alt: 'Atributo ALT de ejemplo para la imagen #1',
		},
	];

</script>

<main>
  <div><h1><span>Galeria de imagenes</span></h1></div>
  <section id="galeria">
    
    {#each images as i}   
            <img src={i.url} alt={i.alt} on:click={abreLightbox} width="200px" height="200px" style="flex-grow: 1;"/>     
    {/each}

  </section>

  <section id="contenedor-principal">
      <div id="contenedor-interno">
          <img id="img-activa" src="" alt="galeria de imagenes">
          <button id="btn-cierra" type="button" on:click={btnCierra}>x</button>
          <button id="btn-retrocede" type="button" on:click={retrocederImagen}>&lt;</button>
          <button id="btn-adelanta" type="button" on:click={adelantaImagen}>&gt;</button>
      </div>
  </section>
</main>

<style>

*,
*::after,
*::before {
  box-sizing: inherit;
}

#galeria {
  width: 80%;
    margin: 50px auto 50px;
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(240px,1fr));
    gap: 30px;
}

#galeria img {
  
  border-radius: 5px;
  cursor: pointer;
}

#img-activa {
  width: 100%;
  height: auto;
}

#contenedor-principal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 10;
  background-color: rgba(0, 0, 0, 0.55);
  display: none;
  justify-content: center;
  align-items: center;
  padding: 50px;
}

#contenedor-interno {
  border: 2px #f3f3f3 solid;
  padding: 0%;
  background: #504f4f;
  position: relative;
  display: flex;
  justify-content: center;
  width: 600px;
  height: 550px;
  flex-grow: 1;
}

button {
  cursor: pointer;
  background: transparent;
  border: none;
  color: #f3f3f3;
}

#btn-cierra {
  position: absolute;
  right: 1.5%;
  font-size: 3rem;
}

#btn-retrocede {
  position: absolute;
  top: 50%;
  left: 0;
  font-size: 3rem;
}

#btn-adelanta {
  position: absolute;
  top: 50%;
  right: 0;
  font-size: 3rem;
}

h1{
    text-align: center;
    position: relative;
    width: 80%;
    margin: 50px auto;
}

</style>