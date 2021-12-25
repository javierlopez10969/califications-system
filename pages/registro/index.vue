<template>
    <v-container fill-height fluid>
        <v-col align="center">
            <CoursesCursos :cursos="registro" />
        </v-col>
    </v-container>
</template>
<script>
    export default {
    layout: "logged",
    props: ['registro'],
    };
</script>