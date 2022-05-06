<template>
    <div>
        <div class="sections__title">{{ this.sectionName }}</div>
        <SectionItem
            @delete-section-item="deleteSectionItem"
            @generate-output-code="this.$emit('generate-output-code', this.sectionName, this.createdFields)"
            v-for="createdFields in this.createdFields" :key="createdFields.id"
            v-bind:createdFields="createdFields"
            v-bind:fields="section.fields"
        />
        <button class="btn-add" v-bind:class="{'no-item': this.createdFields.length === 0}"
                @click="addSectionItem(section.fields)">Добавить
        </button>
    </div>
</template>

<script>
import SectionItem from "@/components/SectionItem";

export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Section",
    props: ["section", "sectionName", "createdFieldsData"],
    data() {
        return {
            createdFields: this.createdFieldsData
        }
    },
    components: {
        SectionItem
    },
    methods: {
        addSectionItem(fields) {
            const newSectionItem = {
                id: Date.now(),
            }

            fields.forEach((item) => {
                newSectionItem[item.name] = {
                    type: item.type,
                    value: ""
                }
            });

            this.createdFields.push(newSectionItem)
            this.$emit('generate-output-code', this.sectionName, this.createdFields)
        },
        deleteSectionItem(sectionItemId) {
            this.createdFields = this.createdFields.filter(item => item.id !== sectionItemId)
            this.$emit('generate-output-code', this.sectionName, this.createdFields)
        }
    }
}
</script>

<style scoped>

.sections__title {
    font-size: 24px;
    font-weight: bold;
    text-align: center;
    margin-bottom: 30px;
}

.btn-add.no-item {
    margin-top: 0;
}
</style>