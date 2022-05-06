<template>
    <div>
        <div class="section-item" v-for="field in fields" :key="field.name">
            <input type="text"
                   @keyup="this.$emit('generate-output-code')"
                   v-model="fieldValue[field.name].value"
                   v-bind:placeholder="field.name"
            >
        </div>

        <button class="btn-delete" @click="this.$emit('delete-section-item', createdFields.id)">Удалить</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            fieldValue: this.createdFields
        }
    },
    props: ["fields", "createdFields"],
    name: "SectionItem",
    emits: ["delete-section-item", "generate-output-code"],
}
</script>

<style scoped>
.section-item input {
    border-radius: 5px;
    width: 100%;
    margin-bottom: 10px;
    background-color: var(--light-grey);
    padding: 15px;
    box-sizing: border-box;
    border: 0;
    font-size: 14px;
}

.section-item input::placeholder {
    color: var(--dark-grey);
}

.section-item input:focus {
    outline: none;
}
</style>