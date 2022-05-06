<template>
    <Header/>
    <div class="container">
        <section>
            <div class="sections">
                <Section
                    v-for="(section, sectionName) in sections" :key="section.id"
                    v-bind:sectionName="sectionName"
                    v-bind:section="section"
                    v-bind:createdFieldsData="section.createdFields"
                    @generate-output-code="generateOutputCode"
                />
            </div>
        </section>
        <section>
            <OutputCode
                v-if="Object.keys(filteredSections).length !== 0"
                v-bind:sections="filteredSections"
            />
        </section>
    </div>
</template>

<script>
import Section from "@/components/Section";
import Header from "@/components/Header";
import OutputCode from "@/components/OutputCode";

export default {
    name: 'App',
    data() {
        let localData = localStorage.getItem("sections") !== null ? JSON.parse(localStorage.getItem("sections")) : {};
        let sectionsData = {
            "Правила работы": {
                id: 1,
                fields: [
                    {
                        name: "Заголовок",
                        type: "h2"
                    },
                    {
                        name: "Описание",
                        type: "text"
                    }
                ],
                createdFields: [],
            },
            "Сервера": {
                id: 2,
                fields: [
                    {
                        name: "Название",
                        type: "h2"
                    },
                    {
                        name: "Ссылка",
                        type: "link"
                    }
                ],
                createdFields: [],
            },
            "Доступы в админку": {
                id: 3,
                fields: [
                    {
                        name: "Сайт",
                        type: "link"
                    },
                    {
                        name: "Название пользователя",
                        type: "h2"
                    },
                    {
                        name: "Логин",
                        type: "text"
                    },
                    {
                        name: "Пароль",
                        type: "text"
                    }
                ],
                createdFields: [],
            },
            "FTP/SFTP": {
                id: 4,
                fields: [
                    {
                        name: "FTP/SFTP",
                        type: "text"
                    },
                    {
                        name: "Название сайта",
                        type: "text"
                    },
                    {
                        name: "IP сервера",
                        type: "link"
                    },
                    {
                        name: "Логин",
                        type: "text"
                    },
                    {
                        name: "Пароль",
                        type: "text"
                    }
                ],
                createdFields: [],
            },
            "Хостинг": {
                id: 5,
                fields: [
                    {
                        name: "Ссылка на хостинг",
                        type: "link"
                    },
                    {
                        name: "Логин",
                        type: "text"
                    },
                    {
                        name: "Пароль",
                        type: "text"
                    }
                ],
                createdFields: [],
            },
            "Git": {
                id: 6,
                fields: [
                    {
                        name: "Ссылка на git",
                        type: "link"
                    },
                    {
                        name: "Логин",
                        type: "text"
                    },
                    {
                        name: "Пароль",
                        type: "text"
                    }
                ],
                createdFields: [],
            },
        };

        for (let key in localData) {
            sectionsData[key].createdFields = localData[key].createdFields
        }

        return {
            sections: sectionsData,
            filteredSections: localData
        }
    },
    components: {
        Section,
        Header,
        OutputCode
    },
    methods: {
        generateOutputCode(sectionName, createdFields) {
            this.filteredSections = {}
            this.sections[sectionName].createdFields = createdFields

            for (let key in this.sections) {
                if (this.sections[key].createdFields.length > 0) {
                    this.filteredSections[key] = this.sections[key]
                }
            }

            localStorage.setItem('sections', JSON.stringify(this.filteredSections))
        }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

:root {
    --dark-blue-color: #F01825;
    --main-shadow: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    --light-shadow: drop-shadow(0px 0px 2px rgba(0, 0, 0, 0.25));
    --light-grey: #ECEFF3;
    --dark-grey: #B0BCCC;
    --green-color: #42b983;
}

body {
    margin: 0 0 500px 0;
    padding: 0;

}

* {
    font-family: "Roboto", sans-serif;
}

.container {
    width: 1700px;
    margin: 0 auto;
}

.sections {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-gap: 40px;
}

section{
    margin-top: 40px;
}

.btn-delete {
    width: 100%;
    background-color: #fff;
    padding: 15px;
    border-radius: 5px;
    transition: .3s;
    margin-bottom: 10px;
    filter: var(--light-shadow);
    border: 2px solid #fff;
    font-size: 14px;
}

.sections .btn-add {
    width: 100%;
    background-color: #fff;
    border: 2px dashed #b7b7b7;
    padding: 15px;
    border-radius: 5px;
    margin-top: 30px;
    transition: .6s;
    font-weight: bold;
    font-size: 16px;
}

.sections .btn-add:hover, .btn-delete:hover {
    filter: var(--main-shadow);
    background-color: var(--dark-blue-color);
    border: 2px solid var(--dark-blue-color);
    color: #ffffff;
    cursor: pointer;
    transition: .3s;
}

.sections .btn-add:hover {
    background-color: var(--green-color);
    border: 2px solid var(--green-color);
}

.white-block {
    background-color: #fff;
    filter: var(--light-shadow);
    border-radius: 10px;
    padding: 40px;
}

.grid-2fr {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    margin-top: 40px;
    grid-gap: 40px;
}
</style>
