<template>
    <div class="ShowUserAgent">
        <h3>ユーザエージェントの表示</h3>
        <table v-for="(tableItem, key) in tableItems" :key="key">
            <thead>
                <tr>
                    <th>{{ tableItem[0] }}</th>
                </tr>
            </thead>
            <tbody>
                <span
                    v-for="(tableDom, key) in tableItem.filter(
                        (v, i) => i != 0
                    )"
                    :key="key"
                >
                    <tr align="left">
                        <td>{{ tableDom[0] }}</td>
                    </tr>
                    <tr class="get_status" align="right">
                        <td>
                            <ul>
                                <li
                                    v-for="(getItem, key) in tableDom[1]"
                                    :key="key"
                                >
                                    {{ getItem }}
                                </li>
                            </ul>
                        </td>
                    </tr>
                </span>
            </tbody>
        </table>
        <p>
            指標の参考 :
            <a href="http://www.saitolab.org/fp_site/"
                >Web Browser Fingerprint解説ページ</a
            >
        </p>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class ShowUserAgent extends Vue {
    navigatorPlugins = [...Array(navigator.plugins.length)].map(
        (_, i) => navigator.plugins[i].name
    );
    navigatorCookieEnabled = [navigator.cookieEnabled];
    webStorage = [
        "SessionS: " + !window.sessionStorage,
        "SessionS: " + !window.localStorage
    ];
    browserName = [navigator.appName];
    browserVersion = [parseInt(navigator.appVersion)];

    tableItems = [
        [
            "ソフトウェア特徴点",
            ["インストール済みプラグイン", this.navigatorPlugins],
            ["HTTPクッキーの利用不可", this.navigatorCookieEnabled],
            ["Web Storageの利用不可", this.webStorage],
            ["Canvas Fingerprinting", []],
            ["タイムゾーン", []],
            ["ブラウザ名", this.browserName],
            ["ブラウザのバージョン番号", this.browserVersion]
        ],
        [
            "ネットワーク特徴点",
            ["グローバルIPアドレス", []],
            ["プライベートIPアドレス", []],
            ["LAN内に属するホストのIPアドレス", []],
            ["Acceptヘッダ", []],
            ["Accept-Charset", []],
            ["Accept-Encoding", []],
            ["Accept-Language", []],
            ["CONNECTION", []],
            ["Referer", []]
        ],
        [
            "ハードウェア・色深度特徴点",
            ["リフレッシュノート", []],
            ["ハードディスク空き容量", []],
            ["CPUコア数", []],
            ["SSE2", []],
            ["タッチ機能", []],
            ["画面の向き", []],
            ["デバイスピクセル比", []],
            ["カメラ・マイクの個数", []]
        ]
    ];
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
    margin: 40px 0 0;
}
a {
    color: #42b983;
}
table {
    margin: 2rem auto;
    width: 100%;
    max-width: 380px;
    display: inline-block;
    border-collapse: collapse;
    position: relative;
    left: 5rem;
    thead {
        border-bottom: 2px solid #2c3e50;
    }
    tr {
        display: block;
        ul {
            list-style-type: none;
            padding: 0;
            margin: 4px 0;
        }
    }
    .get_status {
        border-bottom: 1px solid #999;
        color: #42b983;
    }
}
</style>
