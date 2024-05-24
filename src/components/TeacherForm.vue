<template>
    <div class="container">
    <h3>Añadir profesor</h3>
    
    <div> <label>Nombre:</label><input type="text" v-model="teacher.teacherName"/> </div>
    <div> <label>Apellido:</label><input type="text" v-model="teacher.surname"/> </div>
    <div> <label>DNI:</label><input type="text" v-model="teacher.dni" /> </div>
    <div> <label>Materias:</label><input type="text" v-model="subject" /> <button @click="handleSubject">Agregar</button> </div>
    <div>
        <ul>
            <li v-for="(elm,index) in teacher.subjects" :key="index">{{elm}}</li>
        </ul>
    </div>
    <input type="checkbox" v-model="teacher.doc" />Documentacion entregada
    <button @click="addProfesor">Agregar</button>
    
    <section>
        <h3>Tabla de profesores</h3>
        <table>
            <tr>
                <th>Nombre</th>
                <th>Apellido</th>
                <th>DNI</th>
                <th>Materias</th>
                <th>Documentacion entregada</th>
            </tr>
            <tr v-for="elm in teachers" :key="elm.dni">
                <th> {{ elm.teacherName }}</th>
                <th> {{ elm.surname }}</th>
                <th> {{ elm.dni }}</th>
                <th> 
                <ul>
                    <li v-for="(item,index) in elm.subjects" :key="index">{{item}}</li>
                </ul> 
                </th>
                <th v-if="elm.doc"> Entregada </th>
                <th v-else> No entregada </th>
            </tr>
        </table>
    </section>
</div>
</template>


<script lang="ts" setup>
import { ref,Ref } from 'vue'

interface ITeacher{
    teacherName:string,
    surname:string,
    dni:string,
    subjects: Array<string>,
    doc: boolean
}

let teacher:Ref<ITeacher> = ref({
    teacherName:'',
    surname:'',
    dni:'',
    subjects:[],
    doc: false
})

let teachers:Ref<Array<ITeacher>> = ref([])
let subject:Ref<string> = ref('')  

const handleSubject = () => {
    teacher.value.subjects.push(subject.value)
    subject.value = ''
}
const addProfesor = () => {
    teachers.value.push({
        teacherName:teacher.value.teacherName ,
        surname:teacher.value.surname ,
        dni:teacher.value.dni ,
        subjects:teacher.value.subjects ,
        doc:teacher.value.doc
    })
    teacher.value.teacherName = ''
    teacher.value.surname = ''
    teacher.value.dni = ''
    teacher.value.subjects = []
    teacher.value.doc = false


}
</script>


<style scoped>
.container {
    margin: 0 auto;
    width: 20%;
    padding: 20px;
    background-color: #f7f7f7;
    border: 1px solid #ddd;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    overflow-x: auto;
}

.container h3 {
color: #333;
}

.container input[type="text"],
.container button {
    padding: 8px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 3px;
    width: calc(100% - 10px);
}

.container input[type="checkbox"] {
    margin-right: 5px;
}


.container button {
    width: 150px; /* Ajusta el valor según tus necesidades */
}
.container table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 20px;
    max-width: 100%; 
    
}

.container th, .container td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
}

.container th {
    background-color: #f2f2f2;
}

.container tr:nth-child(even) {
    background-color: #f9f9f9;
}

.container tr:hover {
    background-color: #f2f2f2;
}

</style>