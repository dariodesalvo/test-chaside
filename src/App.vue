<template>
<div id="app">
 <div class="container" v-if="start">
        <div class="row justify-content-center">
          <div class="col-md-8">
          <h5 v-if="a==0">¿Estás pensando en elegir una carrera? <br> Te ofrecemos el siguiente cuestionario de 98 preguntas, gratuito, para que puedas conocer cuáles son las áreas de intereses y aptitudes que se destacan en vos.</h5> 
                <div class="progress">
                  <div ref="progreso" class="progress-bar" role="progressbar"  style="width: 1%" aria-valuenow="20" aria-valuemin="0" aria-valuemax="100"></div>
                </div>
                <div v-for="(question,index) in questions.slice(a,b)" :key="index"  class="card">
                <div class="card-header">
                    <h4 id="question"> {{question.n}}. {{question.text}} </h4>
                    <input type="hidden" :value="question.category" id="category">
                </div>
                    <div class="card-body">
                    <div  class="form-inline justify-content-left">
                    <i @click="backQuestion(1)" v-show="a>0" data-toggle="tooltip" data-placement="top" title="Repensar" class="fas fa-arrow-left ml-1"></i>
                    </div>
                    <div class="form-inline justify-content-center">
                        <button @click="nextQuestion(1)" v-bind:class="{ 'btn btn-outline-success': question.choice==0, 'btn btn-success': question.choice==1 }" type="button" >Sí</button>
                        <button @click="nextQuestion(0)" v-bind:class="{ 'ml-2 btn btn-outline-danger': question.choice==1, 'ml-2 btn btn-danger': question.choice==0 }" type="button" >No</button>
                    </div> 
                  
                </div>
            </div>
        </div>
    </div>
  </div>
<!-- results -->
<div class="mt-5 container" id="results" v-show="end">
 <h5>Este cuestionario es una herramienta que te orienta en tu búsqueda.<br>  Sugerimos sea acompañada por un profesional dentro de un proceso de orientación vocacional- ocupacional.</h5>
<div class="row justify-content-center">
<div class="card p-4 mb-1 col-md-5 border border-primary">
<h3 class="text-primary" >Intereses</h3>
<hr />

<h4 class="text-left">Área Contable y Administrativa {{(i1/10*100)}}%</h4>
<div class="progress mb-4">
  <div ref="i1" class="progress-bar bg-success" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="text-left" >Área Humanística {{(i2/10*100)}}%</h4>
<div class="progress mb-4">
  <div ref="i2" class="progress-bar bg-info" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="text-left">Área de Arte y Diseño {{(i3/10*100)}}%</h4>
<div class="progress mb-4">
  <div ref="i3" class="progress-bar bg-warning" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="text-left">Área de Salud {{(i4/10*100)}}%</h4>
<div class="progress mb-4">
  <div ref="i4" class="progress-bar bg-danger" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="mt-1 text-left">Área de Ingeniería e Informática {{(i5/10*100)}}%</h4>
<div class="progress mb-4">
  <div ref="i5" class="progress-bar bg-primary" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="mt-1 text-left">Área de Defensa y Seguridad {{(i6/10*100)}}%</h4>
<div class="progress mb-4">
  <div ref="i6" class="progress-bar bg-secondary" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="mt-1 text-left">Área de Exactas {{(i7/10*100)}}%</h4>
<div class="progress mb-2">
  <div ref="i7" class="progress-bar bg-dark" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>


</div>

<div class="card p-4 mb-1 ml-1 col-md-5 border border-success">
<h3 class="text-success">Aptitudes</h3>
<hr />
<h4 class="text-left">Área Contable y Administrativa {{(a1/4*100)}}%</h4>
<div class="progress mb-4">
  <div ref="a1" class="progress-bar bg-success" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>


<h4 class="text-left" >Área Humanística {{(a2/4*100)}}%</h4>
<div class="progress mb-4">
  <div ref="a2" class="progress-bar bg-info" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="text-left">Área de Arte y Diseño {{(a3/4*100)}}%</h4>
<div class="progress mb-4">
  <div ref="a3" class="progress-bar bg-warning" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="text-left">Área de Salud {{(a4/4*100)}}%</h4>
<div class="progress mb-4">
  <div ref="a4" class="progress-bar bg-danger" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="mt-1 text-left">Área de Ingeniería e Informática {{(a5/4*100)}}%</h4>
<div class="progress mb-4">
  <div ref="a5" class="progress-bar bg-primary" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="mt-1 text-left">Área de Defensa y Seguridad {{(a6/4*100)}}%</h4>
<div class="progress mb-4">
  <div ref="a6" class="progress-bar bg-secondary" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>

<h4 class="mt-1 text-left">Área de Exactas {{(a7/4*100)}}%</h4>
<div class="progress mb-3">
  <div ref="a7" class="progress-bar bg-dark" role="progressbar" style="width: 0%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>
</div>
</div>
</div>
</div>
  </template>

<script>

export default {
  name: 'App',
  data(){
    return {questions:[
      { n:'1',
        text:'¿Escribirías artículos en la sección económica de un diario?',
        category:'i1',
        choice:0
       },
      { n:'2',
        text:'¿Te ofrecerías para organizar la despedida de soltero de uno de tus amigos?',
        category:'a1',
        choice:0
       },
      { n:'3',
        text:'¿Te gustaría dirigir un proyecto de urbanización en tu ciudad o provincia?',
        category:'i3',
        choice:0
       },
      { n:'4',
        text:'¿A una frustración siempre oponés un pensamiento positivo?',
        category:'a4',
        choice:0
       },
      { n:'5',
        text:'¿Te dedicarías a socorrer a personas accidentadas o atacadas por asaltantes?',
        category:'i6',
        choice:0
       },
      { n:'6',
        text:'¿De chico te interesaba saber sobre cómo estaban construidos tus juguetes?',
        category:'i5',
        choice:0
       },
      { n:'7',
        text:'¿Te interesan más los misterios de la naturaleza que los secretos de la tecnología?',
        category:'a7',
        choice:0
       },
      { n:'8',
        text:'¿Escuchas atentamente los problemas que te plantean tus amigos?',
        category:'i4',
        choice:0
       },
      { n:'9',
        text:'¿Te ofrecerías a explicarles a tus compañeros de clase un tema que no entendieron?',
        category:'i2',
        choice:0
       },
      { n:'10',
        text:'¿Sos exigente y crítico con tu equipo de trabajo?',
        category:'a5',
        choice:0
       },
      { n:'11',
        text:'¿Te atrae armar rompecabezas?',
        category:'i3',
        choice:0
       },
      { n:'12',
        text:'¿Podés establecer la diferencia entre Macroeconomía y Microeconomía?',
        category:'i1',
        choice:0
       },
      { n:'13',
        text:'¿Usar uniforme te hacer sentir distinto, importante?',
        category:'a6',
        choice:0
       },
      { n:'14',
        text:'¿Participarías como profesional de un espectáculo de acrobacia aérea?',
        category:'i6',
        choice:0
       },
      { n:'15',
        text:'¿Organizas tu economía de manera que te alcance hasta el próximo cobro?',
        category:'a1',
        choice:0
       },
      { n:'16',
        text:'¿Sabés convencer a las personas  sobre la validez de tus argumentos?',
        category:'i4',
        choice:0
       },
      { n:'17',
        text:'¿Estás informado sobre los nuevos descubrimientos de la Teoría del Big-Bang?',
        category:'i7',
        choice:0
       },
      { n:'18',
        text:'¿Ante una situación de emergencia, actuás rápidamente?',
        category:'a6',
        choice:0
       },
      { n:'19',
        text:'¿Ante un problema matemático, perseverás hasta encontrar la solución?',
        category:'i5',
        choice:0
       },
      { n:'20',
        text:'¿Si tu organización deportiva favorita te convocara para planificar y dirigir un campo de deportes, aceptarías?',
        category:'i1',
        choice:0
       },
      { n:'21',
        text:'¿Sos vos la persona que pone un toque de alegría en las fiestas?',
        category:'i3',
        choice:0
       },
      { n:'22',
        text:'¿Crees que los detalles son tan importantes como el todo?',
        category:'a3',
        choice:0
       },
      { n:'23',
        text:'¿Te sentirías a gusto trabajando en un ámbito hospitalario?',
        category:'i4',
        choice:0
       },
      { n:'24',
        text:'¿Te gustaría participar para mantener el orden ante grandes desordenes y cataclismos?',
        category:'i6',
        choice:0
       },
      { n:'25',
        text:'¿Pasarías varias horas leyendo algún libro de tu interés?',
        category:'i2',
        choice:0
       },
      { n:'26',
        text:'¿Planificás detalladamente tus trabajos antes de  empezar?',
        category:'a5',
        choice:0
       },
      { n:'27',
        text:'¿Entablás una relación casi personal con tu computadora?',
        category:'i5',
        choice:0
       },
      { n:'28',
        text:'¿Disfrutás modelando arcilla?',
        category:'i3',
        choice:0
       },
      { n:'29',
        text:'¿Ayudás habitualmente a los no videntes a cruzar la calle?',
        category:'a4',
        choice:0
       },
      { n:'30',
        text:'¿Creés importante que la escuela fomente la actitud crítica y participación activa?',
        category:'a2',
        choice:0
       },
      { n:'31',
        text:'¿Aceptarías que las mujeres formen parte de las Fuerzas Armadas al igual que los hombres?',
        category:'i6',
        choice:0
       },
      { n:'32',
        text:'¿Te gustaría crear nuevas técnicas para descubrir enfermedades a través del microscopio?',
        category:'i7',
        choice:0
       },
      { n:'33',
        text:'¿Participarías en una campaña de prevención contra la enfermedad de Chagas?',
        category:'i4',
        choice:0
       },
      { n:'34',
        text:'¿Te interesan los temas relacionados con el pasado y la evolución del hombre?',
        category:'i2',
        choice:0
       },
      { n:'35',
        text:'¿Te incluirías en una investigación de los movimientos sísmicos y sus consecuencias?',
        category:'i7',
        choice:0
       },
      { n:'36',
        text:'¿Fuera del horario escolar o de trabajo, dedicas algún día de la semana a actividades corporales?',
        category:'i3',
        choice:0
       },
      { n:'37',
        text:'¿Te interesa las actividades de mucha acción, en situaciones imprevistas o  de riesgo?',
        category:'i6',
        choice:0
       },
      { n:'38',
        text:'¿Te ofrecerías para  colaborar como voluntario en los gabinetes especiales de la NASA?',
        category:'i5',
        choice:0
       },
      { n:'39',
        text:'¿Te gusta más el trabajo manual que el intelectual?',
        category:'a3',
        choice:0
       },
      { n:'40',
        text:'¿Renunciarías a un momento placentero para ofrecer tus servicios como profesional?',
        category:'a4',
        choice:0
       },
      { n:'41',
        text:'¿Participarías de una investigación sobre la violencia en el fútbol?',
        category:'i2',
        choice:0
       }
       ,
      { n:'42',
        text:'¿Te gustaría trabajar en un laboratorio mientras estudias?',
        category:'i7',
        choice:0
       },
      { n:'43',
        text:'¿Arriesgarías tu vida por salvar la vida de otro que no conocés?',
        category:'a6',
        choice:0
       },
      { n:'44',
        text:'¿Te agradaría hacer un curso de primeros auxilios?',
        category:'i4',
        choice:0
       },
      { n:'45',
        text:'¿Empezarías una actividad tantas veces como fuese necesario hasta obtener el logro deseado?',
        category:'i3',
        choice:0
       },
      { n:'46',
        text:'¿Distribuís tus horarios adecuadamente para poder hacer lo planeado?',
        category:'a1',
        choice:0
       },
      { n:'47',
        text:'¿Harías un curso para aprender a fabricar piezas de las máquinas con las que trabajás?',
        category:'i5',
        choice:0
       },
      { n:'48',
        text:'¿Elegirías una profesión que te aleja de tu familia por meses, por ejemplo marino?',
        category:'i6',
        choice:0
       },
      { n:'49',
        text:'¿Te radicarías en una zona agrícola-ganadera para desarrollarte como profesional?',
        category:'i7',
        choice:0
       },
      { n:'50',
        text:'¿Cuando trabajás en grupo, te entusiasma producir ideas originales y que sean tenidas en cuenta?',
        category:'i3',
        choice:0
       },
      { n:'51',
        text:'¿Te resulta fácil coordinar un grupo de trabajo?',
        category:'a1',
        choice:0
       },
      { n:'52',
        text:'¿Te interesaste alguna vez por el estudio de la biología?',
        category:'i4',
        choice:0
       },
      { n:'53',
        text:'¿Si una empresa solicitara un gerente de comercialización, te gustaría ocupar ese puesto?',
        category:'i1',
        choice:0
       },
      { n:'54',
        text:'¿Te incluirías en un proyecto de desarrollo de la principal fuente de recursos de tu provincia?',
        category:'i5',
        choice:0
       },
      { n:'55',
        text:'¿Te interesan las causas que determinan ciertos fenómenos, aunque saberlo no altere tu vida?',
        category:'a7',
        choice:0
       },
      { n:'56',
        text:'¿Descubriste algún filosofo o escritor que haya expresado tus mismas ideas con antelación?',
        category:'i2',
        choice:0
       },
      { n:'57',
        text:'¿Desearías que te regalen algún instrumento musical para tu cumpleaños?',
        category:'i3',
        choice:0
       },
      { n:'58',
        text:'¿Aceptarías colaborar en el cumplimiento de las normas de lugares públicos?',
        category:'i6',
        choice:0
       },
      { n:'59',
        text:'¿Creés que tus ideas son importantes y haces todo lo posible por ponerlas en práctica?',
        category:'a5',
        choice:0
       },
      { n:'60',
        text:'¿Cuando se descompone un artefacto en tu casa, te dispones rápidamente a repararlo?',
        category:'i5',
        choice:0
       },
      { n:'61',
        text:'¿Integrarías un equipo de trabajo orientado a la preservación de la flora y fauna en extinción?',
        category:'i7',
        choice:0
       },
      { n:'62',
        text:'¿Leés revistas relacionadas con los últimos avances científicos y tecnológicos en el área de la salud?',
        category:'i4',
        choice:0
       },
      { n:'63',
        text:'¿Preservar las raíces culturales de tu país, te parece importante y necesario?',
        category:'a2',
        choice:0
       },
      { n:'64',
        text:'¿Te gustaría investigar para contribuir a hacer más justa la distribución de la riqueza?',
        category:'i1',
        choice:0
       },
      { n:'65',
        text:'¿Realizarías tareas en una nave: arriado de velas, pintura del casco, arreglo de averías, etc.?',
        category:'i6',
        choice:0
       },
      { n:'66',
        text:'¿Creés que un país debe poseer la más alta tecnología armamentista, a cualquier precio?',
        category:'a6',
        choice:0
       },
      { n:'67',
        text:'¿La verdad y la justicia son valores fundamentales en tu vida?',
        category:'i2',
        choice:0
       },
      { n:'68',
        text:'¿Realizarías una práctica rentada en una industria alimenticia en el sector de Control de Calidad?',
        category:'i7',
        choice:0
       },
      { n:'69',
        text:'¿Consideras que la salud pública debe ser prioritaria, gratuita y eficiente para todos?',
        category:'a4',
        choice:0
       },
      { n:'70',
        text:'¿Te interesaría investigar sobre alguna nueva vacuna?',
        category:'i4',
        choice:0
       },
      { n:'71',
        text:'¿En un equipo de trabajo, preferís el rol de coordinador?',
        category:'i1',
        choice:0
       },
      { n:'72',
        text:'¿En una discusión entre amigos, te ofrecés como mediador?',
        category:'a2',
        choice:0
       },
      { n:'73',
        text:'¿Estás de acuerdo con la formación de un Cuerpo de Soldados Profesionales?',
        category:'i6',
        choice:0
       },
      { n:'74',
        text:'¿Lucharías por una causa justa hasta las últimas consecuencias?',
        category:'i2',
        choice:0
       },
      { n:'75',
        text:'¿Te gustaría investigar científicamente sobre cultivos agrícolas?',
        category:'i5',
        choice:0
       },
      { n:'76',
        text:'¿Harías un nuevo diseño de una prenda pasada de moda, ante una reunión imprevista?',
        category:'a3',
        choice:0
       },
      { n:'77',
        text:'¿Visitarías un observatorio astronómico para conocer el funcionamiento de los aparatos?',
        category:'i7',
        choice:0
       },
      { n:'78',
        text:'¿Dirigirías el área Importaciones y Exportaciones de una empresa?',
        category:'i1',
        choice:0
       },
      { n:'79',
        text:'¿Te inhibe entrar en un lugar con gente desconocida?',
        category:'a7',
        choice:0
       },
      { n:'80',
        text:'¿Te gratifica trabajar con niños?',
        category:'i2',
        choice:0
       },
      { n:'81',
        text:'¿Harías el diseño de un afiche para la campaña contra el SIDA?',
        category:'i3',
        choice:0
       },
      { n:'82',
        text:'¿Dirigirías un grupo de teatro independiente?',
        category:'a3',
        choice:0
       },
      { n:'83',
        text:'¿Enviarías tu CV a una empresa automotriz que solicita gente de Producción?',
        category:'i5',
        choice:0
       },
      { n:'84',
        text:'¿Participarías de un grupo de defensa internacional dentro de alguna Fuerza Armada?',
        category:'i6',
        choice:0
       },
      { n:'85',
        text:'¿Te costearías tus estudios trabajando en una Auditoría?',
        category:'i1',
        choice:0
       },
      { n:'86',
        text:'¿Sos vos de los que defienden causas perdidas?',
        category:'a2',
        choice:0
       },
      { n:'87',
        text:'¿Ante una emergencia epidémica, participarías en una campaña brindando tu ayuda?',
        category:'i4',
        choice:0
       },
      { n:'88',
        text:'¿Sabes responder que significa ADN y ARN?',
        category:'i7',
        choice:0
       },
      { n:'89',
        text:'¿Elegirías una carrera donde el instrumento de trabajo fuese un idioma extranjero?',
        category:'i2',
        choice:0
       },
      { n:'90',
        text:'¿Trabajar con objetos te resulta más gratificante que trabajar con personas?',
        category:'a5',
        choice:0
       },
      { n:'91',
        text:'¿Te resultaría agradable ser asesor contable en una empresa reconocida?',
        category:'i1',
        choice:0
       },
      { n:'92',
        text:'¿Ante un llamado solidario, te ofrecerías para cuidar un enfermo?',
        category:'i4',
        choice:0
       },
      { n:'93',
        text:'¿Te atrae investigar sobre los misterios del universo, por ejemplo los agujeros negros?',
        category:'i7',
        choice:0
       },
      { n:'94',
        text:'¿El trabajo individual te resulta más rápido y efectivos que el grupal?',
        category:'a7',
        choice:0
       },
      { n:'95',
        text:'¿Dedicarías parte de tu tiempo para ayudar personas carenciadas?',
        category:'i2',
        choice:0
       },
      { n:'96',
        text:'¿Al elegir tu ropa o decorar un ambiente, te preocupa combinar colores, telas o estilos?',
        category:'i3',
        choice:0
       },
      { n:'97',
        text:'¿Te gustaría como profesional dirigir la construcción de una empresa hidroeléctrica?',
        category:'i5',
        choice:0
       },
      { n:'98',
        text:'¿Sabés qué significa la sigla PBI?',
        category:'i1',
        choice:0
       }


     ],

     a:0,
     b:1,
     progressBar:1,
     end:false,
     start:true,
     a1:0,
     a2:0,
     a3:0,
     a4:0,
     a5:0,
     a6:0,
     a7:0,
     i1:0,
     i2:0,
     i3:0,
     i4:0,
     i5:0,
     i6:0,
     i7:0,
    }
  },
methods:{

  addProgress(){
  var bar=this.$refs.progreso;
  bar.style.width=this.progressBar+'%';
  bar.setAttribute('aria-valuenow',this.progressBar);
  //bar.css('width', this.progressBar+'%').attr('aria-valuenow', this.progressBar); 
  },

  modGenProgress(category){
  
  var bar=this.$refs.[category];

  if(category[0]=="a"){
  bar.style.width=(this.[category]/4*100)+'%';
  bar.setAttribute('aria-valuenow',this.[category]/4*100);
  }else{
  bar.style.width=(this.[category]/10*100)+'%';
  bar.setAttribute('aria-valuenow',this.[category]/10*100);
  }
  },

  editAnswer(category,operation){
    if(operation=="add"){
      this.[category]++;
    }else{
      this.[category]--;
    }

  },

  backQuestion(){
    this.a--;
    this.b--;
    this.progressBar--;
    this.addProgress();
  },

  nextQuestion(answer){

    if(this.questions.length -1 == this.a){

    //pregunta final

    if(answer==1){
    this.editAnswer(this.questions[this.a].category.toString(),'add');
    this.modGenProgress(this.questions[this.a].category.toString());
    }

      this.start=false;
      this.end=true;

    }else{

  
    if(answer==1){
    //x si volvió y cambió de opinión
    if(this.questions[this.a].choice==0){

    this.questions[this.a].choice=1;
    this.editAnswer(this.questions[this.a].category.toString(),'add');
    this.modGenProgress(this.questions[this.a].category.toString());
    }
    
    }else{

    if(this.questions[this.a].choice==1){

      this.questions[this.a].choice=0;
      //decrementar el progreso!
      this.editAnswer(this.questions[this.a].category.toString(),'dec');
      this.modGenProgress(this.questions[this.a].category.toString());
      }
    }
    
    }

    //progress bar
    this.progressBar++;
    this.addProgress();

          this.a++;
          this.b++;
          this.select=false;
        }
    }//fin methods

}//fin app

</script>

<style>
#app {
  font-family: Roboto, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
