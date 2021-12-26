<template>
    <v-container fill-height fluid>
        <v-col align="center">
            <CoursesCursos :cursos="cursos" :titulo="'Mis cursos  ' +  semestre.semester+ '-' +semestre.year.toString()" />
        </v-col>
    </v-container>
</template>
<script>
    import Courses from "../../components/Courses/Cursos.vue";
    export default {
    components: { Courses },
    layout: "logged",
    props: ['cursos','semestre'],
    };
</script>