<template>
<q-page class="flex flex-center">

    <div class="search-div " v-bind:class="{ onfocus: isfocused }">
        <img alt="Quasar logo" src="~assets/images/google.png">
        <q-input rounded v-model="inputSearch" @focus="activate()" @keydown="autocomplete()">
            <template v-slot:prepend>
                <q-icon name="search" />
            </template>
            <template v-slot:append>
                <q-avatar>
                    <img class="google-cls" src="~assets/images/Google_mic.svg">
                </q-avatar>
            </template>
        </q-input>
        <div class="btn-div">
            <q-btn class="My-btn" text-color="black" label="Recherche Google" @click="searchIt()" />
            <q-btn class="My-btn " text-color="black" label="J'ai de la chance" @click="searchIt()" />
            <ul v-if="isfocused">
                <q-inner-loading :showing="visible">
                    <q-spinner-gears size="50px" color="primary" />
                </q-inner-loading>
                <template>
                    <li v-for="s in resualts" :key="s.id">
                        <a :href="s.link">{{s.title}}</a>
                    </li>
                    <q-btn class="My-btn" text-color="black" label="Recherche Google" @click="searchIt()" />
                    <q-btn class="My-btn" text-color="black" label="J'ai de la chance" @click="searchIt()" />
                </template>
            </ul>
            <p>Google disponible en : <a href="https://www.google.com/setprefs?sig=0_qZ_04SrrcTuiGxyywlo4lPtbaeU%3D&hl=en&source=homepage&sa=X&ved=0ahUKEwjRoMi99MDuAhWuzYUKHWu4CI0Q2ZgBCA8">English</a> </p>
        </div>
    </div>

</q-page>
</template>

<script>
/* eslint-disable */
import axios from 'axios'
const api_key = 'AIzaSyCV7_J3uzuM8bbmUIKxAeR4vGnerUHJw2o'
export default {
    name: 'PageIndex',
    data() {
        return {
            data: '',
            inputSearch: '',
            resualts: [],
            isfocused: false,
            visible: false
        }
    },
    created() {},
    methods: {
        getSeatchRes() {
            this.visible = true
            axios.get('https://www.googleapis.com/customsearch/v1?key=' + api_key + '&cx=017576662512468239146:omuauf_lfve&q=' + this.inputSearch)
                .then((response) => {
                    let res = response.data,
                        i = 0;
                    if (typeof res.items != undefined) {
                        if (res.items.length > 0) {
                            let list = res.items.map(it => {
                                return {
                                    "id": i++,
                                    "title": it.title,
                                    "link": it.link
                                }
                            })
                            if (list.length > 6) {
                                this.resualts = list.splice(0, 6)
                            }
                        }
                    }
                    this.visible = false
                })
        },
        activate() {
            if (this.inputSearch.length == 0)
                this.isfocused = false
            else
                this.isfocused = true
        },
        desactivate() {
            this.isfocused = false
        },
        autocomplete() {
            this.isfocused = true
            if (this.inputSearch.length == 0)
                this.isfocused = false
            if (this.inputSearch.length > 0) {
                this.getSeatchRes()
            }

        },
        searchIt() {
            location.href = 'https://www.google.com/search?source=hp&ei=YN4TYJPfOcqdjLsPxpuTmAc&q=' + this.inputSearch + '&oq=' + this.inputSearch + '&gs_lcp=CgZwc3ktYWIQAzIKCAAQxwEQrwEQEzIICAAQDRAeEBMyCAgAEA0QHhATMggIABANEB4QEzIGCAAQHhATMggIABANEB4QEzIICAAQDRAeEBMyCAgAEA0QHhATMggIABANEB4QEzIICAAQDRAeEBM6CAgAELEDEIMBOgsIABCxAxDHARCjAjoFCAAQsQM6CwgAELEDEMcBEK8BOgIIADoICAAQxwEQrwE6DggAELEDEIMBEMcBEK8BOgUILhCxAzoCCC46CAgAEMcBEKMCOgUILhCTAjoECAAQHjoECAAQDToGCAAQDRAKUI8MWIwjYLwkaANwAHgAgAGaAYgBgAqSAQQwLjEwmAEAoAEBqgEHZ3dzLXdperABAA&sclient=psy-ab&ved=0ahUKEwiTj-vf8sDuAhXKDmMBHcbNBHMQ4dUDCAc&uact=5'
        },
    },

}
</script>

<style>
.search-div {
    width: 40%;
    text-align: center;
    min-width: 400px;
}

.q-field__marginal {
    height: 42px;
    color: rgba(0, 0, 0, 0.54);
    font-size: 24px;
    padding-left: 10px;
}

.q-field__control.relative-position.row.no-wrap {
    height: 42px;
}

.q-avatar__content.row.flex-center.overflow-hidden {
    padding-right: 15px;
    padding-top: 2px;
}

.google-cls {
    transform: scale(0.7);
    margin-left: 12px;
}

.btn-div {
    margin-top: 3%;
}

.q-field--standard .q-field__control:before {
    background: #fff;
    display: flex;
    border: 1px solid #dfe1e5;
    box-shadow: none;
    border-radius: 24px;
    height: 44px;
    margin: 0 auto;
}

.My-btn {
    background: #f8f9fa;
    box-shadow: none;
    margin: 10px;
}

ul {
    width: 100%;
    position: relative;
    top: -86px;
    background: #ffffff;
    box-shadow: 0 4px 6px rgb(32 33 36 / 28%);
    list-style: none;
    text-align: center;
    padding: 0;
    border-bottom-right-radius: 20px;
    border-bottom-left-radius: 20px;
}

li {
    padding: 7px 0;
    background: white;
    text-align: left;
    padding-left: 47px;
}

li>a {
    text-decoration: none;
    color: gray;
}

.onfocus .q-field--standard .q-field__control:before {
    border: 1px solid rgba(0, 0, 0, 0.24);
    transition: border-color 0.36s cubic-bezier(0.4, 0, 0.2, 1);
    border-bottom-left-radius: 0;
    border-bottom-right-radius: 0;
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;
    border-color: rgba(223, 225, 229, 0);
    box-shadow: 0 1px 6px rgb(32 33 36 / 28%);
}
</style>
