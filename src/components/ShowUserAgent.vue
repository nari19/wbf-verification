<template>
  <div class="ShowUserAgent">
    <h3>ユーザエージェントの取得</h3>
    <table v-for="(tableItem, key) in tableItems" :key="key">

      <thead>
        <tr><th>{{ tableItem[0] }}</th></tr>
      </thead>

      <tbody>
        <span v-for="(tableDom, key) in tableItem.filter((v, i) => i!=0)" :key="key">
          <!-- left -->
          <tr align="left">
            <td>{{ tableDom[0] }}</td>
          </tr>
          <!-- right -->
          <tr class="get_status" align="right">
            <td><ul>
              <li v-for="(getItem, key) in tableDom[1]" :key="key">{{ getItem }}</li>
            </ul></td>
          </tr>
        </span>
      </tbody>

    </table>
    <p>
      指標の参考 :
      <a href="http://www.saitolab.org/fp_site/">Web Browser Fingerprint解説ページ</a>
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
  webStorage = [
    "SessionS: " + !window.sessionStorage,
    "LocalS: " + !window.localStorage
  ];
  devicePixcel = [window.screen.height + " * " + window.screen.width];
  deviceAvailPixcel = [window.screen.availHeight + " * " + window.screen.availWidth];
  naUserAgent = navigator.userAgent.split("").map((v,i) => (i%35==34) ? v+"," : v).join("").split(",");
  naMimeType = Object.keys(navigator.mimeTypes).map( v =>
    ["type", "suffixes"].map( x => navigator.mimeTypes[v][x]).join(" | ")
  );
  wiScreenPixielDepth = [window.screen.pixielDepth ? window.screen.pixielDepth : "not supported"];

  tableItems = [
    [
      "ソフトウェア特徴点",
      ["x0: インストール済みプラグイン", this.navigatorPlugins],
      ["x1: ブラウザ名", [navigator.appName]],
      ["x2: ブラウザのバージョン番号", [parseInt(navigator.appVersion)]],
      ["x3: ユーザエージェント", [navigator.userAgent]],
      ["x4: mimeTypeオブジェクト", this.naMimeType],
      ["x5: ユーザの使用言語", [navigator.language]],
      ["x6: ユーザのOS", [navigator.platform]],
      ["x7: appCodeName", [navigator.appCodeName]],
      ["HTTPクッキーの利用不可", [navigator.cookieEnabled]],
      ["Web Storageの利用不可", this.webStorage],
    ],
    [
      "ハードウェア・色深度特徴点",
      ["x8 デバイスピクセル比", this.devicePixcel],
      ["x9 screen.availHeight", this.deviceAvailPixcel],
      ["x10 screen.colorDepth", [window.screen.colorDepth]],
      ["x11 screen.pixielDepth", this.wiScreenPixielDepth],
      ["リフレッシュノート", []],
      ["ハードディスク空き容量", []],
      ["CPUコア数", []],
      ["SSE2", []],
      ["タッチ機能", []],
      ["画面の向き", []],
      ["カメラ・マイクの個数", []]
    ],
    [
      "その他",
      ["x12 getTimezoneOffset", [(new Date).getTimezoneOffset()]],
      ["プライベートIPアドレス", []],
      ["LAN内に属するホストのIPアドレス", []],
      ["Acceptヘッダ", []],
      ["Accept-Charset", []],
      ["Accept-Encoding", []],
      ["Accept-Language", []],
      ["CONNECTION", []],
      ["Referer", []]
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
    padding: 0 1rem;
    width: 100%;
    max-width: 380px;
    display: inline-block;
    vertical-align: top;
    border-collapse: collapse;
    thead {
      border-bottom: 2px solid #2c3e50;
    }
    tr {
      display: block;
      th {
        width: 380px;
      }
      ul {
        list-style-type: none;
        padding: 0;
        margin: 4px 0;
        width: 90%;
      }
    }
    .get_status {
        border-bottom: 1px solid #999;
        color: #42b983;
    }
}
</style>
