<template>
    <div class="white-block">
        <div id="html-code">
            <div v-for="(section, sectionName) in sections" :key="section.id">
                <h1><span style="color: rgb(0, 166, 80);">{{ sectionName }}</span></h1>

                <div v-for="createdField in section.createdFields" :key="createdField.id">
                    <div v-for="field in section.fields" :key="field.name">
                        <h2 v-if="createdField[field.name].type === 'h2'">
                            {{ createdField[field.name].value }}
                        </h2>
                        <p v-else-if="createdField[field.name].type === 'text'">
                            {{ createdField[field.name].value }}
                        </p>
                        <p v-else-if="createdField[field.name].type === 'link'">
                        <span style="color: rgb(0, 0, 238);">
                            <a v-bind:href="createdField[field.name].value"
                               target="_blank">{{ createdField[field.name].value }}</a>
                        </span>
                        </p>
                    </div>
                </div>
                <hr>
            </div>
        </div>

        <div class="copy-btns">
            <div class="copy-btn" @click="copyHtml">
                Копировать код
            </div>
            <div class="copy-btn" @click="copyJson">
                Копировать JSON
            </div>
        </div>
    </div>
</template>


<script>
export default {
    name: "OutputCode",
    props: ["sections"],
    methods: {
        copyHtml() {
            let htmlCode = document.getElementById("html-code").outerHTML;

            // eslint-disable-next-line no-useless-catch
            try {
                navigator.clipboard.writeText(htmlCode)
            } catch (e) {
                throw e;
            }
        },
        copyJson(){
            // eslint-disable-next-line no-useless-catch
            try {
                navigator.clipboard.writeText(JSON.stringify(this.sections))
            } catch (e) {
                throw e;
            }
        }
    }
}
</script>

<style scoped>
.copy-btns {
    display: flex;
    position: absolute;
    top: 20px;
    right: 20px;
    gap: 20px;
}

.copy-btn {
    background-color: var(--green-color);
    border-radius: 5px;
    padding: 5px 10px;
    color: #ffffff;
    transition: .3s;
}

.copy-btn:hover {
    transition: .3s;
    filter: var(--light-shadow);
    cursor: pointer;
}
</style>