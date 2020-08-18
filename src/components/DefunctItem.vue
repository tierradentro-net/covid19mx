<template>
	<v-container>
		<v-row dense>
			<v-col cols="12">
				<v-card class="mx-auto mb-15" dark max-width="800">
					<v-img class="white--text align-end" :src="Avatar">
						<v-card-title>{{ defunct.ID_REGISTRO }}</v-card-title>
					</v-img>
					<v-card-subtitle class="lighten-5--text pb-1 subtile-2">{{ Fecha }}</v-card-subtitle>
					<v-card-text class="lighten-4--text">
						<div class="white--text subtitle-1">{{ Sexo }} de {{ defunct.EDAD }} años</div>
						<div>{{ Municipio }}, {{ Estado }}</div>
						<div v-bind:class="{'esconder':Embarazada}">Embarazada</div>
						<div v-bind:class="{'esconder':Hablante}">Hablante de lengua indígena</div>
						<div v-bind:class="{'esconder':Migrante}">Migrante</div>
						<div> 
							<v-btn class="ma-2" dark v-bind:class="{'esconder':Diabetes}"> Diabetes</v-btn>
							<v-btn class="ma-2" dark v-bind:class="{'esconder':Obesidad}"> Obesidad</v-btn>
							<v-btn class="ma-2" dark v-bind:class="{'esconder':Tabaquismo}"> Tabaquismo</v-btn>
							<v-btn class="ma-2" dark v-bind:class="{'esconder':Hipertension}"> Hipertensión</v-btn>
							<v-btn class="ma-2" dark v-bind:class="{'esconder':EPOC}"> Enfermedad pulmonar obstructiva crónica</v-btn>
							<v-btn class="ma-2" dark v-bind:class="{'esconder':Cardiovascular}"> Cardiopatía</v-btn>
							<v-btn class="ma-2" dark v-bind:class="{'esconder':Inmunosupresion}"> Inmunosupresión</v-btn>
							<v-btn class="ma-2" dark v-bind:class="{'esconder':Otras}"> Otras comorbilidades</v-btn>
						</div>
						<!--<div v-bind:class="{'esconder':Resultado}">Positivo SARS-CoV-2</div>-->
					</v-card-text>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
import Entidades from '../assets/data/entidades.json';
import Municipios from '../assets/data/municipios.json';

	export default {
		name: "DefunctItem",
		props: ["defunct"],
		data() {
			return {
				Fecha: '',
				Avatar: '',
				Sexo: '',
				Estado: '',
				Municipio: '',
				Embarazada: false,
				Hablante: false,
				Migrante: false,
				Diabetes: false,
				Obesidad: false,
				Tabaquismo: false,
				Hipertension: false,
				EPOC: false,
				Cardiovascular: false,
				Inmunosupresion: false,
				Otras: false,
				Resultado: false
			}
		},
		methods: {
			setData() {
				//FECHA DEFUNCION
				var FechaTemp = new Date(this.defunct.FECHA_DEF);
				this.Fecha = FechaTemp.toLocaleDateString("es-ES", { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })
				this.Fecha = this.Fecha.replace(/(^\w{1})/g, match => match.toUpperCase());
				//SEXO
				switch (this.defunct.SEXO) {
					case 1:
						this.Sexo = "Mujer";
						this.Avatar = "assets/img/m.png";
						break;
					case 2:
						this.Sexo = "Hombre";
						this.Avatar = "assets/img/h.png";
						break;
					default:
						this.Sexo = "No especificado";
						this.Avatar = "assets/img/n.png";
						break;
				}
				//ESTADO
				var Entidad = Entidades.filter(entidad => entidad.CLAVE_ENTIDAD == this.defunct.ENTIDAD_NAC);
				this.Estado = Entidad[0].ENTIDAD_FEDERATIVA;
				//MUNICIPIO
				var Municipio = Municipios.filter(municipio => municipio.CLAVE_MUNICIPIO == this.defunct.MUNICIPIO_RES && municipio.CLAVE_ENTIDAD == this.defunct.ENTIDAD_NAC);
				this.Municipio = Municipio[0].MUNICIPIO;
				console.log(Municipio[0].MUNICIPIO)
				/*switch (this.defunct.ENTIDAD_NAC) {
					case 1:
						this.Estado = "Aguascalientes";
						break;
					case 2:
						this.Estado = "Baja California";
						break;
					case 15:
						this.Estado = "Estado de México";
						break;
					default:
						this.Estado = "No especificado";
						break;
				}*/
				//EMBARAZADA: 1=SI => false=no esconder, 2=NO => true=esconder
				this.Embarazada = this.defunct.EMBARAZO == 1 ? false : true;
				//HABLANTE
				this.Hablante = this.defunct.HABLA_LENGUA_INDIG == 1 ? false : true;
				//MIGRANTE
				this.Migrante = this.defunct.MIGRANTE == 1 ? false : true;
				//DIABETES
				this.Diabetes = this.defunct.DIABETES == 1 ? false : true;
				//OBESIDAD
				this.Obesidad = this.defunct.OBESIDAD == 1 ? false : true;
				//TABAQUISMO
				this.Tabaquismo = this.defunct.TABAQUISMO == 1 ? false : true;
				//HIPERTENSION
				this.Hipertension = this.defunct.HIPERTENSION == 1 ? false : true;
				//EPOC
				this.EPOC = this.defunct.EPOC == 1 ? false : true;
				//CARDIOVASCULAR
				this.Cardiovascular = this.defunct.CARDIOVASCULAR == 1 ? false : true;
				//INMUSUPR
				this.Inmunosupresion = this.defunct.INMUSUPR == 1 ? false : true;
				//OTRAS_COM
				this.Otras = this.defunct.OTRAS_COM == 1 ? false : true;
				//RESULTADO
				this.Resultado = this.defunct.RESULTADO == 1 ? false : true;
			}
		},
		mounted() {
			this.setData()
		}
	}
</script>

<style scoped>
	.esconder{
		display: none;
	}
</style>