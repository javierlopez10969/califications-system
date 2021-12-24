<template>
    <v-container fill-height fluid>
        <v-col align="center">
            <CoursesCursos :cursos="cursos" />
        </v-col>
    </v-container>
</template>
<script>
    import Courses from "../../components/Courses/Cursos.vue";
    export default {
    components: { Courses },
    layout: "logged",
    props: ['cursos'],
    };
</script>