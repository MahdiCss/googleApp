<template>
<q-layout view="lHh Lpr lFf">
    <q-toolbar class="text-primary">
        <q-toolbar-title>
        </q-toolbar-title>
        <a href="" class="footElment">Gmail </a>
        <q-btn flat round dense icon="apps" class="appIcon" />
        <a class="myAccount">M</a>
    </q-toolbar>
    <q-page-container>
        <router-view />
    </q-page-container>
    <div class="q-pa-md footer">
        <div class="row">
            <div class="col">
                <p class="footElment">France</p>
            </div>
        </div>

        <div class="row">
            <div class="col-sm-6">
                <span>
                    <a href="https://www.google.com/intl/fr_tn/ads/?subid=ww-ww-et-g-awa-a-g_hpafoot1_1!o2&utm_source=google.com&utm_medium=referral&utm_campaign=google_hpafooter&fg=1" class="footElment">Publicité</a>
                    <a href="https://www.google.com/services/?subid=ww-ww-et-g-awa-a-g_hpbfoot1_1!o2&utm_source=google.com&utm_medium=referral&utm_campaign=google_hpbfooter&fg=1" class="footElment">Entreprise</a>
                    <a href="https://about.google/?utm_source=google-TN&utm_medium=referral&utm_campaign=hp-footer&fg=1" class="footElment">À propos</a>
                </span>
            </div>
            <div class="col-sm-6" style="float:right">
                <span style="float:right">
                    <a href="https://policies.google.com/privacy?hl=fr-TN&fg=1" class="footElment">Confidentialité </a>
                    <a href="https://policies.google.com/terms?hl=fr-TN&fg=1" class="footElment">Conditions </a>
                    <a href="" class="https://www.google.com/preferences?hl=en">Paramètres </a>
                </span>
            </div>
        </div>

    </div>
</q-layout>
</template>

<script>
/* eslint-disable */
export default {
    name: 'MainLayout',
    data() {
        return {
            leftDrawerOpen: false
        }
    }
}
</script>

<style>
.footer {
    background: #f8f9fa;
}

.footElment {
    padding: 10px;
    text-decoration: none;
    color: black
}

.myAccount {
    background: #ff6023;
    width: 33px;
    padding-left: 8.2px;
    padding-top: 4px;
    height: 33px;
    border-radius: 100%;
    color: white;
    font-size: 19px;
    cursor: pointer
}

.myAccount:hover {
    background: #ffb123;
}

.appIcon {
    padding-right: 14px;
    padding-top: 2px;
    color: gray;
}

button.q-btn.q-btn-item.non-selectable.no-outline.appIcon.q-btn--flat.q-btn--round.q-btn--actionable.q-focusable.q-hoverable.q-btn--wrap.q-btn--dense:hover {
    background: none !important;
    color: black;
}
</style>
