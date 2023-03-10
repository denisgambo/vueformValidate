<template></template>

<script>
export default {
    name: 'TechnoList',

    data() {
        return {
            technolist: ["Java", "JavaScript", "Angular", "Django"],
        }
    },

    methods: {
        emitTechnoList() {
            this.$emit("technos", this.technolist)
        },

    },


    mounted() {
        this.emitTechnoList()
    }
}
</script>